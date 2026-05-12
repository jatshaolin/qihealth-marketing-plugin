---
name: review-sentiment-analyzer
description: >
  This skill should be used to extract emotional language patterns, fears, outcomes, and exact phrases from competitor reviews (Abbott + Sibionics) and own reviews. Triggers: "analiza reviews", "sentiment analysis", "voice of customer", "qué dicen los clientes", "extrae lenguaje real", "review mining". Reverse-engineers the exact language customers use to recommend competitors, then builds that vocabulary into QiHealth website copy, GBP content, review request scripts, and ad creative.
metadata:
  version: "0.1.0"
  type: "operations"
  channel: "research + content"
  inspired_by: "Sarvesh Shrivastava 20 SEO prompts (2026) — prompt 13 adapted for healthtech DTC"
---

# Review Sentiment Analyzer

Mines competitor reviews and own reviews to extract the **exact emotional language** real customers use. The output feeds brand-voice, ad-references, and copy across all QiHealth touchpoints.

This is the prompt that most local SEO agencies don't know exists — adapted for QiHealth's DTC healthtech context.

## Mandatory loading

- `memory/strategy-v4.3-summary.md` (5 sub-segments)
- `memory/brand-voice.md` (current QiHealth voice)
- `memory/competitors.md` (Abbott + Sibionics URLs)
- `memory/cofepris-rules.md` (filter clinical claims out of mined patterns)

## MCPs requeridos

- **Apify** (scraping reviews from):
  - GBP / Google Reviews para Abbott México, Sibionics MX (Kabla)
  - Mercado Libre listings de Abbott + Sibionics
  - Amazon MX listings
  - Yelp, Trustpilot, BBB si aplica
- **Web fetch** para revisar reviews públicas
- **Zoho Desk** + **Bigin** para reviews y feedback propio cuando exista

## Proceso de análisis

### Paso 1 — Fuentes de reviews target

Por sub-segmento, identificar fuentes donde hay reviews ricas en lenguaje:

| Sub-segmento | Fuentes prioritarias |
|---|---|
| CGM-Switchers | Reviews Abbott en MercadoLibre MX, Amazon MX, Yelp; FB Groups diabetes con menciones Abbott |
| BGM-Self | Reviews Sibionics + glucómetros (Accu-Chek, OneTouch) |
| BGM-Doctor | Reviews HCPs sobre LibreView en blogs gremiales, LinkedIn posts |
| No-Measurers | NPS y comentarios en posts educativos de Abbott, Sibionics en redes |
| Legacy | Reviews de productos preventivos + reviews en comunidades de "hijos de diabéticos" |

### Paso 2 — Extracción por competidor (mínimo 100 reviews por competidor)

Para cada competidor, extraer:

**A. Top 20 palabras emocionales más usadas**
Ejemplos: "relieved", "impressed", "finally", "trustworthy", "frustrated", "worried", "skeptical"

**B. Top 10 outcomes específicos mencionados**
Ejemplos:
- "se aplicó sin dolor"
- "lo recibí en 24 horas"
- "el dashboard es fácil de leer"
- "mi médico lo pudo ver"

**C. Top 5 miedos/frustraciones ANTES de comprar**
Ejemplos:
- "tenía miedo de que doliera"
- "preocupado por el costo"
- "no sabía si era confiable siendo china"
- "no estaba segura si funcionaría para mí"

**D. Frases exactas que usan al recomendar a otros (gold)**
Las "money phrases" — el lenguaje que un cliente usa cuando vende tu producto por ti.

**E. Language patterns que aparecen en 5-star reviews pero NO en 3-star**
Diferencia entre "satisfied" y "advocate".

**F. Top 5 servicios/features mencionados** (validar match con tu product)

**G. Recurring complaints o themes negativos** (oportunidad de diferenciación)

### Paso 3 — Filtro COFEPRIS

Aplicar `cofepris-check` sobre los patterns extraídos. Filtrar:
- Frases que mencionen cura/diagnóstico (no podemos replicarlas legalmente)
- Claims clínicos sin source (no podemos validarlos)
- Lenguaje predatorio o estigmatizante

Solo quedarse con language patterns COFEPRIS-safe.

### Paso 4 — Comparativa vs QiHealth

Cuando QiHealth tenga reviews propias:
- Comparar mi vocabulario actual vs el de competidores
- Identificar emotional gaps (palabras que MIS clientes NO usan pero los de Abbott sí)
- Identificar advantages (palabras que MIS clientes SÍ usan únicamente)

### Paso 5 — Output: vocabulario activable

Generar 4 outputs accionables:

**Output 1 — brand-voice.md update**:
- Agregar palabras de cliente identificadas como "ganadoras" → vocabulario preferido
- Quitar palabras que clientes NO usan que estaban en versión actual

**Output 2 — Ad copy templates**:
- 5 hooks de Reel con lenguaje real cliente
- 3 carrusel headlines con palabras de cliente
- 3 CTA variants en lenguaje cliente

**Output 3 — Review request script**:
- Cuando QiHealth pida review a cliente, script natural que invite a usar palabras específicas
- Mencionar (sin instruir directo): servicio + ciudad/área + outcome
- Ejemplo: *"Si te late, comparte qué descubriste con QiTrax — qué patrón te sorprendió, en qué te ayudó día a día, lo que sea que te haya importado."*
- NO scripting agresivo ("menciona X y Y")

**Output 4 — Social proof statements para website**:
- 3 frases tipo testimonial que reflejan lenguaje real de cliente
- Atribuibles a cuando QiHealth tenga clientes reales que ratifiquen

## Output format

```markdown
=== REVIEW SENTIMENT ANALYSIS ===
Period: [fecha del análisis]
Sources analyzed: [N reviews across X platforms]

### Competitor A — Abbott (FreeStyle Libre)
Reviews analyzed: [N]
Sub-segments mainly addressed: [...]

**Top 20 emotional words**:
1. word — frequency (% of reviews)
2. ...

**Top 10 outcomes mentioned**:
1. "outcome literal"
2. ...

**Top 5 fears before purchase**:
1. "miedo literal"
2. ...

**Money phrases (recommendation language)**:
1. "..."
2. ...

**5-star vs 3-star language gap**:
- Pattern in 5★: "..."
- Pattern in 3★: "..."

### Competitor B — Sibionics
[same structure]

### Cross-competitor patterns
- Universal customer language: [...]
- Sub-segment-specific patterns: [...]

### Recommendations for QiHealth

**1. brand-voice.md updates**:
- ADD: [palabras nuevas a vocabulario preferido]
- REMOVE: [palabras a evitar que NO usan los clientes]

**2. Ad copy seeds (ready to test)**:
- Reel hook #1: "[texto con lenguaje real]"
- ...

**3. Review request script (when QiHealth has clients)**:
"[texto literal del script]"

**4. Social proof templates for /testimonios page**:
- "..."
- ...

NEXT ACTION: Actualizar memory/brand-voice.md + memory/ad-learnings.md con findings. Re-run cuando QiHealth tenga 30+ reviews propias para gap analysis.
```

## Cadencia recomendada

- **Inicial (semana 0)**: análisis full de Abbott + Sibionics — base de partida
- **Mensual** (primer mes): re-scrape para detectar nuevas frases emergentes
- **Trimestral**: comparativa QiHealth (cuando ya hay base) vs competidores
- **Bajo demanda**: cuando se planea piece nuevo de alto valor (pillar page, Doctor Reel, landing page)

## Casos especiales

### Reviews en inglés vs español
QiHealth target es español-mexicano. Solo procesar reviews en español. Reviews globales en inglés sirven solo para validar themes generales (no para vocabulary copy directo).

### Reviews que mencionan competidores específicos
Cuando un cliente Sibionics menciona "antes usaba Abbott" o viceversa, marcar como "switcher language" — extra valor para sub-segmento CGM-Switchers.

### Reviews de productos cross-category
Reviews de glucómetros tradicionales (Accu-Chek, OneTouch) son útiles para BGM-Self entender lenguaje de transición.

## Anti-patrones

- **NO** copiar frases textuales de competidores (issue legal + brand)
- **NO** generar testimoniales falsos basados en patterns extraídos
- **NO** usar claims clínicos extraídos sin advisory review
- **SÍ** usar VOCABULARIO y ESTRUCTURA emocional como inspiración

## Cuándo escalar al humano

- Pattern que sugiere problema regulatorio (cliente confunde wellness con diagnóstico) → asesoría legal
- Hallazgo de queja sistémica que aplica a QiHealth también → producto + Jose
- Frase de cliente que parece testimonial usable → community manager para validar con cliente real
- Decline súbita en NPS competidor → competitive opportunity, reportar a Jose

## Output a otras skills

- → `brand-voice-qihealth`: actualiza vocabulario preferido
- → `ad-creative-variants`: hooks y CTAs en lenguaje cliente
- → `landing-page-copy`: social proof statements
- → `email-sequence-builder`: subject lines en lenguaje cliente
- → `reel-script-builder`: hooks naturales
- → `ad-reference-library`: patterns ganadores etiquetados
- → `memory/ad-learnings.md`: histórico acumulado
