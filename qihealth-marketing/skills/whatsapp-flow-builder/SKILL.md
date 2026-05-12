---
name: whatsapp-flow-builder
description: >
  This skill should be used to build WhatsApp messaging flows for QiHealth via Zoho or similar. Triggers: "whatsapp flow", "WhatsApp para [médico/paciente]", "WA messaging", "automated WhatsApp", "WhatsApp Business sequence". Produces conversational flows with branching, pre-approved templates (COFEPRIS-safe), opt-in compliance, and routing to human handoff when needed.
metadata:
  version: "0.1.0"
  type: "production"
  channel: "whatsapp"
---

# WhatsApp Flow Builder

Build WhatsApp Business flows for QiHealth. WhatsApp es canal de servicio + nurture + reactivación, no mass marketing.

## Mandatory loading

- `memory/strategy-v4.3-summary.md`
- `memory/brand-voice.md`
- `memory/cofepris-rules.md`

## Reglas críticas WhatsApp Business

### Opt-in obligatorio
- Solo enviar a usuarios que opt-in explícito (form, checkout, etc.)
- Mensaje de bienvenida con disclaimer + unsubscribe option

### Templates pre-aprobados (Meta WhatsApp Business)
- Mensajes outbound (que abren conversación) requieren template aprobado por Meta
- Tipos permitidos: utility, marketing (opt-in), authentication
- Templates deben ser approved antes de usarse — proceso 24-48h

### Anti-spam
- Máximo 1-2 mensajes outbound por día por contacto
- Frequency cap a nivel cuenta (Meta lo enforced)
- Unsubscribe respetado inmediatamente

## Flows típicos

### Flow 1 — Post-purchase Insight 15 (paciente)

```
[Trigger: Compra Insight 15]

Día 0: Bienvenida + tracking del envío
↓
Día 2: "¿Llegó tu sensor?" → branch:
   Sí → "Aquí está el video de aplicación: [link]"
   No → "Permíteme verificar el envío" → handoff a humano
↓
Día 4: "¿Qué patrones estás viendo?" + tip educativo
↓
Día 8: Mid-point check-in + invitación a feedback
↓
Día 14: "Tu reporte estará listo mañana. ¿Pregunta antes?"
↓
Día 15: Reporte completo + CTA upgrade a membresía
```

### Flow 2 — Pre-demo médico (con Luis)

```
[Trigger: Demo agendada vía commercial-handoff-luis]

T-24h: Recordatorio + link Zoom
↓
T-1h: "Tu demo con Luis es en 1 hora. Link: [zoom]"
↓
T+30min (post-demo): "¿Cómo te fue con la demo? Si tienes preguntas, responde aquí."
   → Respuestas se enrutan a Luis
↓
T+7 días: Follow-up de Luis (humano, no automatizado)
```

### Flow 3 — Quiz follow-up (No-Measurers)

```
[Trigger: Completó quiz + opt-in WhatsApp]

T+0: "Hola [Nombre], aquí tu reporte completo: [link PDF]"
↓
T+2 días: "¿Pudiste leer el reporte? ¿Alguna pregunta?"
   → Branch:
     Pregunta sobre Insight 15 → flow comercial
     Pregunta clínica → handoff humano + advisory
     Sin respuesta → seguir flow
↓
T+5 días: "Te comparto un video corto sobre lo que pasa después de comer tortillas: [link]"
↓
T+10 días: Última invitación a Insight 15 antes de cerrar nurture
```

### Flow 4 — Médico interesado (post-outreach LinkedIn)

```
[Trigger: Médico aceptó pasar a WhatsApp, post-outreach]

T+0: Confirmación de conexión + brief de QiHealth
↓
T+1: "¿Tienes preguntas antes de la demo?"
   → Branch:
     Pregunta clínica → handoff advisory
     Pregunta comercial → handoff Luis
     Sin respuesta → propuesta de slots Calendar
↓
[Demo se agenda — sale del flow automatizado, queda con Luis humano]
```

## Estructura de mensaje WhatsApp

```yaml
message:
  template_name: "qihealth_welcome_insight15"  # registrado en Meta Business
  template_category: "utility"  # o "marketing"
  
  content:
    body: |
      Hola [{{name}}], 👋
      
      Tu sensor QiTrax está en camino. Llegará en [{{delivery_date}}].
      
      Mientras tanto, aquí está la guía rápida de aplicación: [{{video_link}}]
      
      ¿Pregunta? Responde aquí — tenemos a un coach humano del otro lado.
    
    buttons:
      - text: "Ver tutorial"
        type: "url"
        url: "[link]"
      - text: "Hablar con coach"
        type: "quick_reply"
        payload: "talk_to_coach"
  
  fallback: "Mensaje en texto plano para devices que no soportan rich"
  
  exit_conditions:
    - User responds with "STOP", "BAJA", "PARAR" → unsubscribe
    - User clicks "Hablar con coach" → handoff a humano
```

## Compliance check específico

- ✅ Template aprobado por Meta
- ✅ Opt-in registrado y verifiable
- ✅ Unsubscribe option visible
- ✅ Mensaje promocional respeta opt-in marketing (no utility)
- ✅ COFEPRIS check sobre claims (igual que email)

## Quality gates

- cofepris-check (todo claim clínico)
- brand-voice
- Meta template approval (24-48h proceso)

## Cuándo escalar al humano

- Cualquier pregunta clínica del paciente → advisory
- Pregunta sobre pricing personalizado → Luis o equipo comercial
- Crisis emocional o queja seria → Jose + community manager
- Spike de unsubscribes → investigate causa

## Integración con Zoho CRM

Cada mensaje WhatsApp se loggea en Bigin como interacción del lead. Status del flow visible en pipeline.
