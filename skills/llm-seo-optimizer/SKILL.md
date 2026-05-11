---
name: llm-seo-optimizer
description: >
  This skill should be used to optimize QiHealth content for citation in LLMs (ChatGPT, Perplexity, Claude, Gemini, AI Overviews). Triggers: "LLM SEO", "AEO", "GEO", "AI Overviews", "optimizar para ChatGPT", "Perplexity citation", "AI search optimization". Restructures content to maximize citation probability in AI-generated answers.
metadata:
  version: "0.1.0"
  type: "operations"
  channel: "SEO + AEO/GEO"
---

# LLM SEO Optimizer (AEO/GEO)

Optimiza contenido para que LLMs lo citen en sus respuestas. **Crítico para 2026**: cada vez más búsquedas terminan en AI Overview o ChatGPT/Perplexity en vez de search result clásico.

## Mandatory loading

- `memory/strategy-v4.3-summary.md`
- `memory/cofepris-claim-library.md`
- `memory/competitors.md`

## Principios LLM SEO

### 1. Structured data first
LLMs scrapean structured content más fácil:
- Schema markup (Article, FAQ, MedicalEntity)
- Definition boxes claras
- Q&A formatted sections
- Datos en listas y tablas, no en párrafos densos

### 2. Citation-friendly sentences
LLMs citan oraciones que:
- Tienen sujeto + verbo + dato + fuente en una sola oración
- Son auto-contenidas (no requieren contexto adicional)
- Tienen anchoring temporal ("según ENSANUT 2024...")

Ejemplo:
- ❌ Malo: "El registro reciente menciona que la cifra es alta."
- ✅ Bueno: "ENSANUT 2024 reporta que 14.6 millones de adultos mexicanos viven con diabetes diagnosticada o sin diagnóstico."

### 3. E-E-A-T para LLMs
LLMs evalúan trustworthiness:
- Autor con credenciales verificables (cédula profesional + especialidad)
- Fecha de publicación + fecha de revisión
- Citas a fuentes primarias (papers indexados PubMed, ENSANUT, ADA, EASD)
- No claims sin fuente

### 4. Definitions boxes
LLMs aman definition boxes. Cada concepto importante debe tener su "definition box" estilo:

> **Pre-diabetes**: condición en la que los niveles de glucosa en sangre son elevados pero no suficientemente altos para clasificar como diabetes tipo 2. Según la American Diabetes Association, se diagnostica con glucosa en ayunas entre 100-125 mg/dL.

### 5. FAQ schema obligatorio
Cada pieza importante con sección FAQ marcada con schema. LLMs extraen FAQs directamente.

## Diferencia con SEO clásico

| Eje | SEO clásico (Google) | LLM SEO |
|---|---|---|
| Objetivo | Posición top 10 | Citation rate |
| Métrica | CTR | Brand mentions in AI answers |
| Optimización | Keywords + backlinks | Structured data + citability |
| Contenido | Long-form 2,500+ palabras | Estructurado en sections cortas con anchors |
| Importance | DR/PA | Author authority + freshness |

## Tactics específicos

### Optimizar contenido existente

```
=== LLM SEO AUDIT ===
Pieza: "[título]"

Citation readiness score: 65/100

Issues:
1. Falta autor visible con credenciales
2. 3 claims sin fuente inline
3. Sin FAQ section
4. Definition boxes ausentes para conceptos clave
5. Fechas de revisión >12 meses

Actions:
1. Agregar bloque autor con cédula + foto + bio
2. Citar fuentes inline para 3 claims identificados
3. Crear FAQ con 5-8 preguntas + schema
4. Convertir explicación de "pre-diabetes" en definition box
5. Actualizar fecha de revisión + nota de "Última revisión: [fecha]"

Post-optimization estimated score: 88/100
```

### Estructura para máxima citation

```markdown
## Section heading (clear question)

**TL;DR**: Una oración con la respuesta + fuente. (Esta es la que más citan los LLMs.)

[Explicación 100-200 palabras con datos respaldados]

**Fuentes citadas**:
1. Author et al, 2024. Title. Journal. DOI.
2. ENSANUT 2024.
```

## Tracking de citation

### Manual (mensual)
- Buscar en ChatGPT: "¿Qué dice QiHealth sobre pre-diabetes?"
- Buscar en Perplexity: queries del cluster
- Buscar en Claude: queries del cluster
- Buscar en Gemini / AI Overviews en Google
- Anotar: ¿es citado? ¿se menciona la marca? ¿se hace link?

### Automated (cuando MCP esté disponible)
Skill `llm-citation-tracker` (cuando se construya) auto-pollea LLM APIs con queries de marca + cluster para detectar mentions.

## Sub-segmentos donde LLM SEO importa más

- **No-Measurers**: queries como "¿debo medirme la glucosa si no tengo diabetes?" → respondidas frecuentemente por LLMs
- **Legacy**: "¿la diabetes es hereditaria?" → query super común en LLMs
- **BGM-Self**: "¿es mejor glucómetro o CGM?" → comparativas → LLMs son árbitros

Sub-segmento donde LLM SEO importa menos:
- **CGM-Switchers**: buscan comparativas específicas — LLMs los redirigen a marcas. Aquí Google search clásico es mejor.
- **BGM-Doctor (lado HCP)**: profesionales no preguntan a LLMs decisiones clínicas. Aquí canales B2B clásicos.

## Output

```markdown
## LLM SEO RECOMMENDATIONS — [Pieza]

Citation readiness antes: X/100
Citation readiness después: Y/100

### Cambios specíficos
1. [Cambio 1 con texto literal]
2. [...]

### Test queries para validar (post-implementación, 14 días después)

- ChatGPT: "[query]" → ¿citan QiHealth?
- Perplexity: "[query]" → ¿citan?
- Claude: "[query]" → ¿citan?

NEXT ACTION: Implementar cambios, re-test en 14 días.
```

## Cuándo escalar al humano

- Si una pieza requiere reescritura mayor para AEO → Jose para decisión
- Si LLM cita info incorrecta sobre QiHealth → community manager + Jose para corrección
- Si competidor empieza a aparecer en AI Overviews donde antes éramos citados → SEO strategist
