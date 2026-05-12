---
name: commercial-handoff-luis
description: >
  This skill should be used to hand off hot leads (médicos who responded, qualified prospects) to Luis from the commercial team. Triggers: "hand off to Luis", "agendar cita con prospecto", "médico respondió positivo", "agendar demo Luis", "commercial handoff", "lead caliente para Luis", "agenda demo con [médico]". Manages the flow: lead responds → propose 3 Calendar slots from Luis → médico confirms → create Calendar event + ClickUp task + Bigin update + Slack notification.
metadata:
  version: "0.1.0"
  type: "operations"
  channel: "commercial-handoff"
  human_owner: "luis@qihealth.ai"
---

# Commercial Handoff — Luis (luis@qihealth.ai)

Tu rol es gestionar el handoff de leads calientes al equipo comercial humano (Luis). El flujo es: prospecto califica → calendar matching → confirmación → tarea creada con todo el contexto. Luis ejecuta el cierre humano.

## Mandatory loading

- `memory/strategy-v4.3-summary.md`
- `memory/product-catalog.md` (Plan Switch, Plan Legacy, Bundle Primer mes, demo del dashboard médico)
- Acceso a Calendar MCP (compartido con Luis o con visibilidad de su disponibilidad)
- Acceso a Bigin MCP (pipeline Médicos Partners + DTC Consumidor)
- Acceso a ClickUp MCP (lista Médicos Pipeline + Adhoc)
- Slack MCP (`#qihealth-commercial-handoffs`)

## Cuándo se activa esta skill

3 escenarios principales:

### Escenario 1 — Médico responde positivamente a outreach

`kol-outreach` envió mensaje, médico respondió pidiendo demo o info.

### Escenario 2 — Lead inbound caliente

Alguien (paciente o médico) llenó form de demo / contacto / interés en dashboard partner.

### Escenario 3 — Lead orgánico calificado

Sistema detectó pattern (ej: alguien comentó 3 veces "cuánto cuesta" en piezas de un sub-segmento) → propone hand-off.

## Flujo de hand-off (paso a paso)

### Paso 1 — Validar que el lead es realmente hot

Antes de hand-off, validar:

- ¿El lead expresó interés explícito? (NO inferir interés de un like)
- ¿La info de contacto está verificada en Bigin?
- ¿No es un duplicado de lead ya en proceso con Luis?
- ¿El sub-segmento + producto correspondiente está claro?

Si dudoso, devolver a nurturing en vez de hand-off prematuro (saturaría a Luis).

### Paso 2 — Generar context briefing para Luis

Cuando es hot, prepara briefing completo:

```yaml
hand_off:
  lead_id: "[bigin_lead_id]"
  type: "médico" / "paciente"
  name: "Dr. Jorge Pérez García"
  contact:
    email: "..."
    phone: "..."
    linkedin: "..."
  
  context:
    sub_segment: "BGM-Doctor"
    funnel_stage: "MOF"
    journey_summary: |
      - Outreach inicial sent: 5 mayo via LinkedIn
      - Respuesta recibida: 9 mayo 7:42 AM
      - Mensaje literal del médico: "Me interesa conocer la plataforma. ¿Pueden mostrar el dashboard?"
    
    qihealth_fit_score: 9.0  # de medical-list-builder
    relevance_signals:
      - Endocrinólogo CDMX 12 años experiencia
      - Audiencia genuina 4.2K en LinkedIn
      - Habla de pre-diabetes recientemente
      - NO está afiliado a Abbott
    
    product_match: "Demo del dashboard médico + programa partner clínico"
    
    suggested_talk_track: |
      1. Agradecer la respuesta + breve presentación
      2. Demo dashboard (énfasis en IA predictiva, alertas, multi-biométrico)
      3. Programa de prueba: 30 días gratis para 5 pacientes
      4. Programa de reciprocidad (no comisión, valor mutuo)
      5. Si interés, agendar follow-up en 7 días post-demo

  bigin_pipeline:
    current_stage: "Demo Scheduled"
    tags: ["endocrinólogo", "cdmx", "alta-prioridad"]
    owner_change: "AI → Luis"
```

### Paso 3 — Calendar matching

Consultar Calendar MCP con disponibilidad de Luis. Proponer 3 slots dentro de 48-72h:

- Mañana 10:00 AM
- Pasado mañana 3:00 PM
- Viernes 11:00 AM

Cada slot debe:
- Tener bloque de 30 minutos disponible en Calendar de Luis
- No coincidir con eventos críticos de Jose (también verificar)
- Ser horario hábil México (9 AM - 6 PM)

### Paso 4 — Outreach al médico para confirmar slot

Generar mensaje de respuesta al médico via mismo canal donde respondió:

```
Dr. Pérez, gracias por su interés. Para mostrarle el dashboard tengo 3 horarios disponibles esta semana:

- Mañana viernes 10:00 AM
- Lunes 3:00 PM
- Martes 11:00 AM

¿Cuál le funciona mejor? Le envío link de Zoom/Meet una vez confirme. La demo es de 30 minutos.

Saludos,
Luis Equipo Comercial QiHealth
```

**Output va al usuario (Jose o Luis) para aprobación antes de envío**. NO auto-send.

### Paso 5 — Cuando médico confirma slot

Al recibir confirmación:

1. **Crear evento en Calendar**:
   - Título: "Demo QiHealth — Dr. Jorge Pérez (Endocrinólogo)"
   - Atendees: Luis + médico + Zoom/Meet link
   - Descripción: brief contextual con info clave del médico

2. **Crear task en ClickUp**:
   - List: Médicos Pipeline
   - Title: "Demo: Dr. Jorge Pérez García — [fecha]"
   - Subtasks:
     - [ ] Preparar demo personalizada (Luis review brief 24h antes)
     - [ ] Realizar demo
     - [ ] Capture nota de demo + interés expresado
     - [ ] Follow-up 7 días post-demo
     - [ ] Decide outcome: Close / Nurture / No fit
   - Owner: Luis
   - Due date: día de demo + 1 día (para capture nota)
   - Priority: High

3. **Update Bigin**:
   - Pipeline Médicos Partners
   - Stage: "Demo Scheduled"
   - Notes: append context briefing completo
   - Tags: ["demo-scheduled", "endocrinólogo", "cdmx"]
   - Owner: Luis

4. **Notificar a Slack**:
   - Channel: `#qihealth-commercial-handoffs`
   - Format: action required (sec slack-notifier)
   - Mention: @luis
   - Content: context briefing condensado + link a ClickUp task + link a Bigin lead

5. **Confirmar al médico** (vía mismo canal):
   - Envío del link de Zoom/Meet
   - Confirmación de hora + agenda corta de los 30 min

## Estructura del Slack message

```
✅ ACCIÓN REQUERIDA — Médico respondió a outreach: Dr. Jorge Pérez (endocrinólogo CDMX)

📅 Demo agendada: Viernes 11 mayo, 11:00 AM (30 min)

📋 Context:
- Sub-segmento: BGM-Doctor
- Score QiHealth fit: 9.0
- Outreach inicial: 5 mayo via LinkedIn
- Respondió: hoy 7:42 AM
- Mensaje literal: "Me interesa conocer la plataforma. ¿Pueden mostrar el dashboard?"

🎯 Talk track sugerido:
1. Dashboard demo (énfasis IA predictiva)
2. Programa 30 días gratis para 5 pacientes
3. Programa partner clínico

@luis — task creada en ClickUp con full brief: [link]
Calendar event: [link]
Bigin lead: [link]

Cualquier ajuste, responde aquí o ejecuta /qihealth-marketing.
```

## Casos especiales

### Médico pide demo PERO no cabe en Calendar de Luis en 72h

- Proponer slots de la siguiente semana
- Si Luis está en evento (congreso, vacaciones): proponer alternativa (Jose ejecuta demo o agenda con backup)

### Médico pide demo presencial (no Zoom)

- Verificar que está en CDMX (geográfico viable)
- Coordinar con Luis para locación
- Update task ClickUp con flag "presencial"

### Médico responde con duda clínica NO con interés en demo

- NO hand-off prematuro
- Forward la duda al advisory médico vía `#qihealth-medical-review`
- Sistema redacta respuesta clínica (post advisory approval)
- Cuando se resuelve la duda, re-evaluar interés en demo

### Lead inbound de paciente (no médico)

- Sub-segmento determina pipeline:
  - DTC Consumidor (BGM-Self, No-Measurers, Legacy, CGM-Switchers)
  - Mismo flow general pero owner puede ser equipo comercial DTC, no Luis específico
- Si Plan Switch alto valor → Luis también puede manejar
- Si Insight 15 entry-level → flow más automatizado, no necesita hand-off humano (sistema cierra)

## Métricas a watch

- **Time from response to first demo**: target <72h
- **Demo show-up rate**: target >80%
- **Demo to deal close rate**: target >40% (Luis tracking)
- **Average time from first touch to first patient referred** (médicos): target <30 días
- **Backlog de hand-offs sin attendido**: alert si >3 leads sin Luis respondiendo en 24h

## Cuándo escalar al humano (más allá de Luis)

- Si Luis está fuera (vacaciones, evento) → Jose como backup
- Si el lead es estratégicamente high-value (top médico de SMEN/FMD/AMD) → Jose directo, no via Luis
- Si lead pide algo fuera de scope normal (partnership institucional, etc.) → Jose
- Si conflict con un lead ya manejado por agencia previa → Jose para limpiar

## Cuándo NO hacer hand-off

- Lead frío (sin response explícito)
- Lead duplicado (ya en proceso)
- Lead de competidor o vocero pagado de Abbott
- Lead que no calza con producto QiHealth (ej: pediatra que quiere CGM para niños — NO aprobado)
- Volume excesivo (>3 hand-offs/día a Luis sin que cerrara los anteriores)
