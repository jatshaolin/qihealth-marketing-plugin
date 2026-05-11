---
name: influencer-hunter
description: >
  This skill should be used to identify potential KOLs and micro-influencers for QiHealth. Triggers: "influencer hunter", "buscar influencers", "find micro-influencers", "KOLs candidates", "lista de creadores de contenido". For KOLs médicos use medical-list-builder. For non-medical creators (lifestyle, pacient micro-influencers, content creators de salud), this skill uses Apify + Apollo + Instagram/TikTok scraping to find candidates matching QiHealth's strict influencer rules (see brand-voice).
metadata:
  version: "0.1.0"
  type: "operations"
  channel: "outreach"
---

# Influencer Hunter (Non-Medical)

Identifica micro-influencers de pacientes y creadores que pueden colaborar con QiHealth. NO macros de wellness/fitness/lifestyle (regla brand-voice).

## Mandatory loading

- `memory/strategy-v4.3-summary.md` (sec 8 influencers)
- `memory/cofepris-rules.md`
- `memory/brand-voice.md` (la regla central)

## Tipologías target

### A. Micro-influencers de pacientes (PRIMARY target)
- Personas reales con diabetes, pre-diabetes, hijos de diabéticos
- Audiencia 1K-50K
- Engagement >5% (alto vs macros)
- Documentan su vida sin que marca sea eje
- Diversidad: edad, género, geo México, tipo diabetes, ocupación

### B. Creadores de contenido de salud (SECONDARY)
- Comunicadores de salud (no médicos pero educados)
- Editoriales de prevención de diabetes
- NO fitness/wellness/biohacking (excluded por brand-voice)
- Audiencia 5K-100K

### C. Voceros institucionales (raros, alto valor)
- Asociaciones de pacientes con presencia digital (FMD, AMD divisiones de pacientes)
- Embajadores de ONGs de salud metabólica

## Criterios de filtro

### MUST have
- Diagnóstico real verificable (en caso de pacientes)
- Mexicanos o foco México (>70% audiencia)
- Engagement rate >5%
- Línea editorial compatible
- Sin patrocinios médicos previos de competidores (Abbott, Dexcom, Medtronic)

### Deal-breakers
- Vocero pagado actual de Abbott/Dexcom/Medtronic/Sibionics
- Audiencia inflada con bots (>40%)
- Historial de promoción de productos no éticos (suplementos sin sustento, etc.)
- Estigmatización de diabetes en su contenido
- Claims médicos sin respaldo

## Proceso de hunting

### Paso 1 — Búsqueda inicial
Apify scrape:
- Instagram: hashtags #diabetestipo2 #prediabetes #vivirconDM2 #hijosdediabéticos (audiencia México)
- TikTok: mismos hashtags + Spanish-language filter
- YouTube: canales de educación diabetes pequeños

### Paso 2 — Filtrado
Apollo enrich con engagement rate + audiencia demográficos. Filtrar por criterios above.

### Paso 3 — Manual screening
Revisar últimos 20 posts de cada candidato:
- ¿Habla genuinamente de la condición?
- ¿Calidad del contenido?
- ¿No tiene anti-patrón de wellness influencer?
- ¿Audiencia auténtica (comentarios reales)?

### Paso 4 — Output

```yaml
candidate_id: "INFL-001"
name: "@dianalavida_dm2"
platform: "Instagram"
real_name: "Diana Martínez"
location: "GDL, México"
audience: 12,400
engagement_rate: 8.2%

profile_summary: |
  Mujer 38 años con DM2 dx hace 6 años. Documenta su día a día,
  alimentación, control glucémico (con glucómetro). Tono honesto,
  educativo. Sin promociones médicas. Audiencia mayoría México 75%.

content_signals:
  - Posts de pre-diabetes/DM2: 80% del contenido
  - No menciona Abbott, Dexcom ni competidores
  - Comentarios reales con preguntas de pacientes (no spam)
  - Recientemente preguntó "¿alguien usa CGM aquí?" → señal de interés

qihealth_fit: "Excellent"
fit_score: 9.0

recommended_approach: |
  Acceso anticipado a producto QiTrax sin obligación de publicar.
  Si decide compartir, código de descuento para su audiencia (SEEDS).
  NO pago por post.

contact:
  email: "[Apollo enriched]"
  instagram_dm: "[for first touch]"
  
next_action: "DM personalizado con propuesta producto comp + invitación a comunidad micro-pacientes"
```

### Paso 5 — Output a kol-outreach
Lista enriquecida → `kol-outreach` redacta primer mensaje personalizado.

## Volumen target

Para arrancar el programa SEEDS:
- Mes 1: 10 micro-influencers identificados y contactados
- Mes 3: 15-20 activos
- Mes 12: 25-30 activos (target strategy v4.3)

## Cuándo escalar al humano

- Influencer con criterio dudoso (gray area de fit) → community manager
- Influencer con alta audiencia (>100K) → Jose (caso especial, evaluar costo/beneficio)
- Cualquier influencer con dudas regulatorias → asesoría legal antes de outreach
- Detección de influencer con conflicto previo no obvio → Jose
