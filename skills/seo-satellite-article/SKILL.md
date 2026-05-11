---
name: seo-satellite-article
description: >
  This skill should be used to draft SEO satellite articles (800-1,500 words, long-tail keywords). Triggers: "satellite article", "artículo satélite", "blog post SEO", "long-tail content", "draft satélite para [pillar]". Produces medium-form SEO content linked to a pillar page, with E-E-A-T signals, FAQ schema, and conversion CTAs.
metadata:
  version: "0.1.0"
  type: "production"
  channel: "SEO"
  format: "Satellite article 800-1,500 words"
---

# SEO Satellite Article Builder

Drafts the supporting articles around each pillar page. ~50 satellites total across 5 clusters = 10/cluster.

## Mandatory loading

- `memory/strategy-v4.3-summary.md` (sec 7 SEO clusters)
- `memory/brand-voice.md`
- `memory/cofepris-rules.md`
- `memory/cofepris-claim-library.md`

## Specs

- **Word count**: 800-1,500 (sweet spot 1,200)
- **Structure**: intro + H2 sections + FAQ + CTA
- **Target**: 1 long-tail keyword + 2-3 related
- **Internal link**: 1 back-link al pillar parent (obligatorio)
- **Image**: 1-2 mínimo (con alt-text)
- **Schema**: Article + FAQ

## Estructura estándar

1. **Intro** (100-150 palabras): dato impactante + qué va a aprender
2. **Sección 1** (200-300 palabras): respuesta directa al search intent
3. **Sección 2-3** (300-500 palabras): profundización
4. **Sección práctica** (200-300 palabras): qué hacer con esta info
5. **FAQ** (3-5 preguntas con schema)
6. **CTA + link al pillar**

## Templates por cluster

### BGM-Self cluster (linked a pillar "Glucómetro vs CGM")
- "Cómo monitorear glucosa sin piquetes"
- "Qué es un CGM y cómo funciona"
- "Vale la pena un CGM para diabetes tipo 2"
- "Primer CGM en México: guía 2026"
- "CGM sin receta médica en México"
- "Costo de un CGM en México vs glucómetro"
- "Cuántas veces al día medir glucosa"
- "Glucómetro app móvil: la diferencia con CGM"

### No-Measurers cluster (linked a pillar "Pre-diabetes en México")
- "5 síntomas silenciosos de pre-diabetes"
- "Glucosa alta sin diabetes diagnosticada"
- "Qué pasa si no me mido la glucosa"
- "Factores de riesgo diabetes en mexicanos"
- "Antes de medicarte mide: cómo monitorear preventivamente"
- "Antecedentes familiares y riesgo metabólico"
- "Sedentarismo y glucosa: la relación"
- "Sobrepeso y resistencia a la insulina"

### Legacy cluster (linked a pillar "Diabetes hereditaria")
- "Diabetes hereditaria México: lo que sabemos"
- "Riesgo genético diabetes en hijos"
- "Prevenir diabetes si mi papá la tiene"
- "Cuándo empezar a medirme si padres tienen DM"
- "Edad recomendada para chequeo glucosa con antecedentes familiares"
- "Diabetes en familia: cómo proteger a tus hijos"
- "50% genética 50% estilo de vida: la ciencia"
- "Plan de prevención metabólica familiar"

### BGM-Doctor cluster (linked a pillar "CGM en consulta")
- "Cómo pedirle a tu doctor un CGM"
- "Dashboard glucosa médicos: qué ven los doctores"
- "AGP report explicado para pacientes"
- "Integrar CGM con tu endocrinólogo"
- "Reporte AGP: qué significa cada métrica"
- "Cuándo tu médico necesita más que glucómetro"

### CGM-Switchers cluster (linked a pillar "QiTrax vs FreeStyle Libre")
- "Migrar de Libre a otro CGM en México"
- "Exportar datos LibreView paso a paso"
- "MARD de los CGMs: qué significa"
- "Alternativas FreeStyle México 2026"
- "Opiniones reales de usuarios QiTrax"
- "Costo amortizado Abbott 4+1 vs membresía CGM"

## Output format

```markdown
# [TÍTULO con keyword principal]

**Autor**: [Dr. Nombre si requiere firma médica, o "Equipo QiHealth"]
**Publicado**: [fecha]
**Revisión**: [fecha + advisory si aplica]
**Categoría**: [Sub-segmento cluster]
**Pillar parent**: "[Pillar title]" → link

---

## Intro
[100-150 palabras con hook + promesa]

## [H2 Sección 1]
[200-300 palabras respondiendo intent]

## [H2 Sección 2]
[200-300 palabras profundización]

## [H2 Sección 3]
[200-300 palabras práctico]

## Preguntas frecuentes

### ¿[Pregunta 1]?
[Respuesta concisa]

### ¿[Pregunta 2]?
[Respuesta concisa]

[3-5 preguntas total con FAQ schema]

---

## ¿Quieres saber más?
[CTA + link al pillar parent]

[Producto correspondiente: Plan Insight 15 / Plan Legacy / Bundle Primer mes / etc.]

---

**Fuentes**:
1. [Fuente con link]
2. [...]

**Disclaimer**: Este contenido es educativo. No sustituye consulta médica.
```

## Quality gates

- cofepris-check
- brand-voice
- factual-review
- Advisory review SI hay claim clínico nuevo o cifra cuantitativa
- Schema markup validation
- Internal link verification

## Iteración semanal

Cada lunes vía scheduled task seo-rank-tracking, comparar performance de satélites. Optimize los flojos (>30 días, bounce >75%, posición >30).

## Cuándo escalar al humano

- Claim clínico nuevo → advisory
- Comparativa con competidor → legal review
- Si el satélite empieza a outranking al pillar → revisar internal linking + canonical
