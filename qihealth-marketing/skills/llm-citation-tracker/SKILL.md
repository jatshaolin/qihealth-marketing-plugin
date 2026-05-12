---
name: llm-citation-tracker
description: >
  This skill should be used to track citation of QiHealth in LLMs (ChatGPT, Perplexity, Claude, Gemini, AI Overviews). Triggers: "track LLM citations", "¿QiHealth aparece en ChatGPT?", "Perplexity mentions", "AI search visibility". Manually queries LLMs (or via API when available) with brand + cluster queries to detect mentions, links, and competitive positioning.
metadata:
  version: "0.1.0"
  type: "operations"
  channel: "SEO + AEO/GEO"
  cadence: "weekly + monthly"
  status: "manual-MVP-pending-LLM-APIs"
---

# LLM Citation Tracker

Trackea menciones de QiHealth en respuestas de LLMs y AI search. **Manual en MVP** (semanal + mensual); automatizable cuando se construya MCPs para LLM APIs.

## Mandatory loading

- `memory/strategy-v4.3-summary.md`
- `memory/competitors.md`

## Queries estándar a testear

### Por sub-segmento

**No-Measurers**:
- "¿Debo medirme la glucosa si no tengo diabetes?"
- "¿Cuáles son síntomas de pre-diabetes en México?"
- "¿Qué es un CGM y para qué sirve?"

**Legacy**:
- "¿Es hereditaria la diabetes tipo 2?"
- "¿Cómo prevenir diabetes si mis padres la tienen?"
- "¿Desde qué edad debería medirme si hay diabetes en mi familia?"

**BGM-Self**:
- "¿Glucómetro o CGM cuál es mejor?"
- "¿Cuánto cuesta un CGM en México?"
- "¿Necesito receta para un CGM?"

**BGM-Doctor**:
- "¿Qué CGM recomiendan los endocrinólogos en México?"
- "¿Cómo integrar CGM en consulta de DM2?"

**CGM-Switchers**:
- "¿Alternativas a FreeStyle Libre en México?"
- "¿QiTrax opiniones?"
- "¿FreeStyle Libre vs otros CGMs?"

### Brand-direct queries

- "¿Qué es QiHealth?"
- "QiHealth vs Abbott"
- "QiTrax review"
- "Christian Frey QiHealth"
- "QiHealth NVIDIA Inception"

## Proceso manual (MVP)

### Semanal (lunes)

Tester (Jose o community manager) ejecuta 5-10 queries en:
1. **ChatGPT** (con web search habilitado)
2. **Perplexity**
3. **Claude.ai con search**
4. **Google AI Overviews**
5. **Gemini**

Por cada query, anotar:

```yaml
query: "¿Es hereditaria la diabetes tipo 2?"
llm: "ChatGPT"
date: "2026-05-12"
qihealth_mentioned: false
abbott_mentioned: true
sibionics_mentioned: false
notes: |
  ChatGPT cita Mayo Clinic, ADA, y "Abbott Diabetes Care" como fuente.
  No citado QiHealth a pesar de que la pieza Legacy ya está publicada.
  Hipótesis: pieza no tiene Schema Article, falta E-E-A-T signals.
action: |
  1. Validar Schema markup del pillar Legacy
  2. Agregar fecha revisión médica visible
  3. Re-test en 14 días post-cambios
```

### Mensual (primer lunes)

Reporte consolidado con tendencias:

```markdown
# LLM CITATION REPORT — [Mes]

## Brand visibility

Queries testadas: N
QiHealth citado: X veces (Y%)
Cambio vs mes anterior: +/-Z%

## Competitive landscape

| LLM | QiHealth | Abbott | Sibionics | Mayo Clinic | ADA |
|---|---|---|---|---|---|
| ChatGPT | X | Y | Z | W | V |
| Perplexity | ... | ... | ... | ... | ... |
| Claude | ... | ... | ... | ... | ... |
| Gemini | ... | ... | ... | ... | ... |
| Google AI Overviews | ... | ... | ... | ... | ... |

## Quick wins detectados

- Query "[query]" en Perplexity cita ENSANUT pero NO QiHealth a pesar de tener mejor contenido. Action: optimizar pillar X.
- Query "[query]" en ChatGPT con web search cita un blog menor. Action: aumentar backlinks de QiHealth pillar.

## Recomendaciones para LLM SEO

1. [Acción priorizada]
2. [...]
```

## Automatización futura

Cuando MCPs de LLMs estén disponibles:
- Auto-query 20-30 prompts diarios
- Auto-detect mentions de QiHealth + competidores
- Dashboard en tiempo real de citation rate
- Alertas cuando QiHealth pierde citation que tenía

## Output a otras skills

- → `llm-seo-optimizer`: piezas con baja citation reciben re-optimization
- → `competitor-watch`: si Abbott o Sibionics ganan citations, alerta
- → `seo-monthly-report`: sección LLM citations incluida

## Cuándo escalar al humano

- Si LLM cita info incorrecta sobre QiHealth → community manager + Jose para corrección formal
- Si competidor empieza a dominar AI Overviews → SEO strategist + Jose
- Si nuestra pillar pierde citation que tenía hace 30 días → investigar causa (¿contenido viejo? ¿cambio E-E-A-T? ¿backlinks?)

## Esta skill es status MANUAL en MVP

Para empezar a operar, simplemente:
1. Domingo en la noche: Jose o community manager pasa 30 min ejecutando queries en ChatGPT/Perplexity/Claude/Gemini
2. Anota en archivo en Drive `/QiHealth/llm-citation-tracking/[fecha].md`
3. Lunes el sistema (vía morning brief) sintetiza
4. Acciones se planean en review viernes

Eventualmente automatizar.
