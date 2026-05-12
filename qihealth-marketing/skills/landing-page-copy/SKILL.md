---
name: landing-page-copy
description: >
  This skill should be used to draft landing page copy for QiHealth. Triggers: "landing page", "copy para /switch", "landing /legacy", "landing /quiz", "página de conversión", "landing copy", "hero + sections". Produces hero + sections + FAQ + CTAs + A/B variants. Each landing optimized for specific sub-segment + funnel stage with quality gates.
metadata:
  version: "0.1.0"
  type: "production"
  format: "Landing page"
---

# Landing Page Copy Builder

Produces conversion-optimized landing page copy for QiHealth. Each landing serves a specific sub-segment + funnel stage with hero + value props + social proof + FAQ + CTAs.

## Mandatory loading

- `memory/strategy-v4.3-summary.md`
- `memory/brand-voice.md`
- `memory/cofepris-rules.md`
- `memory/product-catalog.md`
- The persona skill of target sub-segment

## Estructura estándar

### Section 1 — Hero (above the fold)
- **Headline** (8-15 palabras): mensaje núcleo de la etapa funnel
- **Subheadline** (1-2 oraciones): contexto + value prop principal
- **CTA primary**: botón con texto literal accionable
- **Hero visual**: descripción para diseñador (NO genera imagen, da brief)
- **Trust signal mini**: logo COFEPRIS / advisory / testimonial corto

### Section 2 — Problem agitation
- 2-3 puntos del problema que el visitante tiene
- Lenguaje "tú" directo

### Section 3 — Solution (value props)
- 3-5 value props con headline + descripción corta
- Cada uno con icon o ilustración (brief para diseñador)

### Section 4 — Social proof
- 2-3 testimoniales (con consentimiento — pasar por consent-tracker)
- Mención advisory médico
- Logos o stats (si aplica)

### Section 5 — Producto / oferta detallada
- Qué incluye (lista)
- Pricing si BOF
- Garantía si aplica (ej: 30 días Plan Switch)

### Section 6 — FAQ
- 5-8 preguntas frecuentes
- FAQ schema markup
- Respuestas concisas

### Section 7 — CTA final
- Repetir oferta
- Botón claro
- Urgencia razonable (no fake)

## Output

Genera markdown con todas las secciones + variantes A/B del hero (3 opciones) + variantes de CTA button text.

Pasa por quality gates obligatorios antes de devolver.

## Landings prioritarias

- `/switch` — CGM-Switchers BOF (comparativa + garantía + import historial)
- `/legacy` — Legacy BOF (Plan Legacy + bundle familiar)
- `/insight15` — No-Measurers BOF (entry product 15 días)
- `/medicos` — BGM-Doctor (demo dashboard)
- `/primer-mes` — BGM-Self BOF (bundle Primer mes)

## Cuándo escalar al humano

- Comparativas frontales con Abbott → legal review
- Pricing nuevo → Jose
- Testimoniales con paciente real → consent-tracker + community manager
- Disclaimers regulatorios → asesoría legal
