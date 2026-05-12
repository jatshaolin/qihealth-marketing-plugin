---
name: medical-list-builder
description: >
  This skill should be used to build lists of medical specialists (endocrinologists, internists, sports medicine, clinical nutritionists) in Mexico for QiHealth outreach. Triggers: "lista de endocrinólogos", "buscar médicos", "medical list", "Apollo lookup médicos", "lista de doctores", "build doctor list", "endocrinólogos CDMX", "internistas DF", "médicos para outreach", "lista para Bigin Médicos Partners". Uses Apollo MCP (when connected) + Apify + LinkedIn scraping to build enriched lists with email, phone, LinkedIn URL, specialty, location, and recent content output. Output ready for kol-outreach skill.
metadata:
  version: "0.1.0"
  type: "operations"
  channel: "outreach"
---

# Medical List Builder

Tu rol es construir listas enriquecidas de médicos especialistas en México para el outreach del sub-segmento BGM-Doctor. El output alimenta directamente la skill `kol-outreach` que redacta los primeros mensajes.

## Mandatory loading

- `memory/strategy-v4.3-summary.md`
- `memory/competitors.md` (para detectar conflictos de interés con Abbott)
- `memory/cofepris-rules.md` (lenguaje permitido en comunicación HCP)

## MCPs requeridos

- **Apollo** (primary): enriquece nombres con email + phone + LinkedIn + título actual
- **Apify** (secondary): scraping LinkedIn Sales Navigator si Apollo no tiene cobertura
- **Bigin** (output): leads se ingresan al pipeline Médicos Partners

Si Apollo no está conectado todavía, esta skill responde: "Pending Apollo MCP connection. Activate after Apollo OAuth is configured."

## Especialidades target

Por prioridad para QiHealth:

1. **Endocrinólogos** (top prioridad — diabetes es su core)
2. **Internistas** (DM2 frecuentemente manejada por internistas en México)
3. **Médicos del deporte / medicina deportiva** (atletas amateur con interés metabólico)
4. **Nutriólogos clínicos** (complementarios, B2C)
5. **Médicos generales con interés en diabetes** (volumen)

NO target en MVP:
- Cirugía bariátrica (especialidad diferente, no recomendación CGM)
- Pediatría endocrinológica (QiTrax no aprobado para uso pediátrico)
- Endocrinología ginecológica (especialización separada)

## Criterios de filtro

### Filtros básicos
- Ubicación: México (con énfasis CDMX, Guadalajara, Monterrey, Querétaro inicial)
- Cédula profesional vigente
- Experiencia mínima: 5 años de práctica
- Práctica activa (no retirados ni jubilados)

### Filtros de calidad
- Audiencia digital genuina (>3% engagement rate si tiene LinkedIn/Instagram activo)
- Línea editorial compatible (habla de diabetes, salud metabólica, prevención, áreas adyacentes)
- Sin conflicto visible (NO es vocero pagado de Abbott, Dexcom, Medtronic, o laboratorios competidores en categorías de diabetes)

### Filtros NEGATIVOS (deal-breakers)
- Vocero pagado actual de Abbott, Dexcom, Medtronic
- Cédula no verificable
- Historial de prácticas no éticas reportadas
- Audiencia inflada con bots (>40% del engagement parece bot)
- Especialidad declarada que NO concuerda con cédula

## Estructura del output

```yaml
medical_list:
  query:
    specialty: ["endocrinology", "internal medicine"]
    location: ["Mexico City", "Guadalajara"]
    experience_min_years: 5
    audience_min_engagement: 3.0%
  
  results:
    - id: 1
      name: "Dr. Jorge Pérez García"
      cédula: "1234567"  # verificada
      specialty: "Endocrinología"
      sub_specialty: "Diabetes en adulto"
      experience_years: 12
      location: "CDMX (Polanco)"
      hospital_afiliation: ["Hospital ABC", "Consultorio privado"]
      
      contact:
        email: "jorge.perez@hospital.com"  # via Apollo
        phone: "+52 55 1234 5678"  # via Apollo
        linkedin_url: "linkedin.com/in/jorgeperezgarcia"
        instagram: "@drjorgeperez"
      
      digital_presence:
        linkedin_followers: 4200
        instagram_followers: 8500
        engagement_rate: 4.2%
        recent_topics: ["DM2", "Pre-diabetes", "Manejo nutricional"]
        recent_post_examples:
          - "https://linkedin.com/post/...123 — 'La importancia del monitoreo continuo en DM2'"
          - "https://linkedin.com/post/...456 — Caso clínico de paciente con pre-diabetes"
      
      qihealth_fit:
        score: 8.5  # de 10
        signals:
          - "Habla de prevención metabólica"
          - "Audiencia mexicana 80%"
          - "No menciona Abbott en posts recientes"
          - "Engagement con preguntas de pacientes (no solo broadcasting)"
        red_flags: []
        notes: "Buen candidato para outreach. Mensaje sugerido: ángulo de evidencia clínica + dashboard demo."
      
      outreach_recommendation:
        priority: "high"
        first_touch_channel: "linkedin"  # más profesional para HCP
        secondary_channel: "email"
        message_tone: "peer-to-peer, evidencia"
        kol_potential: true  # candidato a co-creación de contenido si se cierra
      
      bigin_action:
        pipeline: "Médicos Partners"
        stage: "Lead"
        tag: "outreach-pendiente"
        owner: "Luis (cuando hand-off)"
```

## Proceso

### Paso 1 — Definir search
Identificar especialidad + ubicación + experiencia mínima. Si el usuario dice "endocrinólogos CDMX", clarificar volumen objetivo (10? 50? 200?).

### Paso 2 — Apollo lookup
Llamar Apollo MCP con filtros:
- Specialty (mapear a Apollo specialty codes)
- Location (Mexico City, Guadalajara, etc.)
- Experience (años desde graduación)

Apollo devuelve listas iniciales con email + phone + LinkedIn cuando disponibles.

### Paso 3 — Apify enrichment (si necesario)
Si Apollo no tiene cobertura para algunos casos, scrape LinkedIn manualmente para obtener:
- Posts recientes (último mes)
- Engagement rate aproximado
- Topics que cubre el médico
- Conexiones con competidores

### Paso 4 — Score QiHealth fit
Por cada candidato, calcular score 0-10 basado en:
- Especialidad match (peso 3)
- Audiencia digital (peso 2)
- Topics relevantes a salud metabólica (peso 2)
- Sin red flags (peso 2)
- Engagement con pacientes (peso 1)

### Paso 5 — Output a Bigin
Cada candidato qualified (score >6.5) se crea como lead en pipeline Médicos Partners de Bigin con:
- Tags por sub-especialidad
- Score como custom field
- Notas con contexto
- Owner: Luis (para hand-off cuando se convierta)

### Paso 6 — Output a kol-outreach
Lista enriquecida lista para que `kol-outreach` redacte el primer mensaje personalizado por cada médico.

## Reglas éticas

### NO hacer
- NO comprar listas no verificadas (riesgo email bounce + reputación)
- NO scrapear datos privados sin justificación legítima
- NO contactar médicos en LinkedIn antes de revisar su perfil completo
- NO usar información de cédula para fines diferentes a verificación
- NO mantener data más allá de lo necesario (privacy)

### SÍ hacer
- Verificar cédula profesional contra registro público mexicano cuando dudoso
- Respetar opt-out: si un médico pide no contactarlo, marcar en Bigin permanentemente
- Limitar volumen de outreach a lo razonable (no spam: máximo 20-30 nuevos contactos por mes inicialmente)
- Personalizar cada primer mensaje (NO mass copy-paste)

## Output al usuario

```
=== MEDICAL LIST GENERATED ===
Query: [endocrinólogos CDMX 5+ años]
Total candidates found: [N]
Qualified (score >6.5): [M]
Added to Bigin Médicos Partners: [M]

Top 5 high-priority candidates:
1. Dr. [...] — score 9.0 — [especialidad] — endorsement strong: [...]
2. Dr. [...] — score 8.5 — [...]
3. ...

Recommended outreach order:
- First batch (this week): top 5 above
- Second batch (next week): scores 7.5-8.4
- Third batch (week 3): scores 6.5-7.4

NEXT ACTION: 
1. Lista en Bigin pipeline Médicos Partners
2. Para iniciar outreach, ejecutar: /qihealth-marketing kol-outreach con lista de [N] médicos
3. Sistema redactará primer mensaje personalizado por cada uno
4. Jose o Luis aprueban antes de envío
5. Respuestas positivas → commercial-handoff-luis para agendar demos
```

## Cuándo escalar al humano

- Cuando un médico aparece con conflicto de interés ambiguo → Jose para decisión
- Cuando volumen sobrepasa 50 médicos en una request → Jose para validar (costo Apollo + dispersión de esfuerzo)
- Cuando cédula no se puede verificar → flagear y skip
- Cuando Apollo devuelve data inconsistente → flagear y usar fallback Apify
- Cuando se piden médicos fuera de las especialidades target → Jose para confirmar excepción
