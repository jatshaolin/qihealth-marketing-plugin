---
name: seo-keyword-research
description: >
  This skill should be used to research SEO keywords for QiHealth content. Triggers: "keyword research", "buscar keywords", "investigar palabras clave", "SEO opportunity analysis", "long-tail keywords", "search volume", "keyword difficulty". Uses Ahrefs MCP (when connected) + Apify SERP scraping + Google Search Console (vía Supermetrics) to identify keyword opportunities by sub-segment cluster.
metadata:
  version: "0.1.0"
  type: "operations"
  channel: "SEO"
---

# SEO Keyword Research

Research keywords para alimentar la estrategia de pillar pages + satélites. Activa Ahrefs cuando esté conectado (lunes).

## Mandatory loading

- `memory/strategy-v4.3-summary.md`
- `memory/competitors.md` (gaps de Abbott México)

## MCPs requeridos

- **Ahrefs** (primary): volume, KD (Keyword Difficulty), SERP analysis
- **Apify**: SERP scraping cuando Ahrefs no tenga data México específica
- **Supermetrics** (cuando esté): bridge para Google Search Console para impressions reales

## Proceso

### Paso 1 — Definir cluster target

Sub-segmento → cluster keywords. Si user dice "research para pillar BGM-Self" → cluster "glucómetro vs CGM".

### Paso 2 — Seed keywords

Empezar con 5-10 seed keywords del cluster (de strategy v4.3 sec 7.2).

Ejemplo cluster BGM-Self:
- glucómetro vs CGM
- monitor continuo glucosa
- CGM México
- primer CGM
- diferencia glucómetro CGM

### Paso 3 — Expansion via Ahrefs

Para cada seed, Ahrefs Keywords Explorer:
- Related keywords
- Questions ("¿qué es...", "¿cómo...")
- Also rank for
- Newly discovered

Filtrar por: idioma español, ubicación México, KD <40 (alcanzable para domain DR <30).

### Paso 4 — SERP analysis

Para top 10 keywords candidatas, ver SERP en Google México:
- ¿Quién rankea actualmente? (Mayo Clinic, Manual MSD, ENSANUT vs marcas)
- ¿Qué tipo de content? (blog largo, video, listicle)
- ¿Featured snippets disponibles?
- ¿AI Overviews / People Also Ask?

### Paso 5 — Scoring

Cada keyword score:
- **Volume**: peso 30% (target >100 searches/mes mínimo)
- **KD**: peso 25% (target <40 para satélites, <50 para pillars)
- **Intent match**: peso 25% (¿coincide con buyer journey del sub-segmento?)
- **SERP opportunity**: peso 20% (¿hay gap claro vs competidores?)

Total score 0-100. Priorizar score >65.

### Paso 6 — Mapeo a buyer journey de 4 stages (framework expandido)

Cada keyword también se mapea a uno de 4 stages del buyer journey. Este framework expande tu funnel TOF/MOF/BOF original con mayor granularidad:

| Stage | Concepto | Mapping a v4.3 | Ejemplos de keywords |
|---|---|---|---|
| **Stage 1: Problem-unaware** | Persona tiene el problema pero NO sabe cómo se llama o cuál es la categoría | TOF (revelación) | "por qué me siento cansado después de comer", "se me eriza la piel de tanta sed", "despierto cansado todas las mañanas" |
| **Stage 2: Problem-aware** | Conoce el problema, está investigando soluciones | TOF + MOF inicial | "qué es pre-diabetes", "síntomas de azúcar alta", "cómo controlar la glucosa" |
| **Stage 3: Solution-aware** | Compara opciones y proveedores | MOF | "glucómetro vs CGM", "FreeStyle Libre opiniones", "QiTrax vs Abbott", "vale la pena un CGM" |
| **Stage 4: Ready to buy** | Quiere comprar/probar AHORA | BOF | "comprar QiTrax", "CGM México precio", "sensor de glucosa entrega rápida CDMX" |

Por cada keyword del análisis, asignar stage explícito. Esto te da:
- Foco de spend prioritario en Stage 4 (lower volume, higher conversion)
- Plan de contenido educational para Stage 1-2 (mayor volume, lower competition)
- Comparativas y battle cards para Stage 3

### Paso 7 — Categorización en 3 buckets

Adicional al stage, cada keyword se etiqueta en uno de 3 buckets de content type:

| Bucket | Cuándo aplicar | Dónde vive en website |
|---|---|---|
| **Problem-awareness content** | Búsqueda indica problema sin solución conocida (Stage 1-2) | Blog satélites educativos + pillar pages educativas |
| **Solution-comparison content** | Búsqueda evalúa opciones (Stage 3) | Pillar "QiTrax vs FreeStyle Libre", comparativas, /switch landing |
| **Local/Service ready content** | Búsqueda quiere comprar ya (Stage 4) | Service pages, landings de producto, /insight15, /legacy, /switch |

**Prioridad de producción para QiHealth**:
1. **Stage 4 primero** — Service pages que cierran. Lower volume pero converting at 5-10x.
2. **Stage 3 segundo** — Comparativas. Capturar el comprador en consideración.
3. **Stage 2 tercero** — Educational content que alimenta funnel.
4. **Stage 1 cuarto** — Long-tail awareness. Volumen alto pero conversion baja, valioso para SEO compounding.

Importante: la mayoría de marcas SEO **invierten todo en Stage 2 (educational)** que genera tráfico pero NO conversiones. QiHealth debe atacar **Stage 4 + Stage 3 primero**, después educational.

## Output format

```yaml
keyword_research:
  query: "research for BGM-Self pillar"
  cluster: "Glucómetro vs CGM"
  total_keywords_analyzed: 47
  qualified (score >65): 23
  
  top_opportunities:
    - keyword: "diferencia glucómetro y monitor continuo"
      volume_monthly_mx: 880
      kd: 22  # bajo, alcanzable
      intent: "informational"
      stage: 3  # solution-aware (comparativa)
      bucket: "solution-comparison"
      target_funnel: "MOF"
      serp_competitors:
        - "Manual MSD"
        - "Mayo Clinic ES"
        - "Diabetes Forecast"
      gap_opportunity: |
        Ningún competidor mexicano tiene contenido localizado.
        Manual MSD es global, sin contexto México.
      qihealth_fit: "Excellent — primary pillar keyword"
      score: 88
      recommended_page_type: "Pillar page comparativa"
    
    - keyword: "qué es un cgm"
      volume_monthly_mx: 1200
      kd: 28
      intent: "informational"
      serp_competitors:
        - "Abbott México (pero genérico)"
        - "Wikipedia"
      gap_opportunity: |
        Abbott tiene contenido pero no centrado en CGM como categoría
        (centrado en Libre como producto).
      qihealth_fit: "Strong — pillar o primer satélite"
      score: 82
    
    - keyword: "vale la pena CGM"
      volume_monthly_mx: 320
      kd: 18
      intent: "commercial-informational"
      gap_opportunity: |
        Keyword con intent comercial, bajo competidor. Easy win.
      qihealth_fit: "Perfect — satélite con CTA fuerte"
      score: 90
    
    [... más keywords ...]
  
  recommended_action:
    - "Usar 'diferencia glucómetro y monitor continuo' como keyword principal del pillar"
    - "Crear 3-4 satélites alrededor: 'qué es un CGM', 'vale la pena CGM', 'primer CGM México'"
    - "Long-tail bonus: 'CGM sin receta México' (volume bajo pero zero competencia)"
  
  cluster_total_potential:
    monthly_traffic_target_12mo: 8500
    conversions_estimated: 70 leads/mes vía cluster
```

## Reglas de selección

### Priorizar
- Long-tail con KD <30 (gana primero, sube pirámide gradualmente)
- Question-based keywords (alta intent + featured snippet potential)
- Keywords con SERP "Mayo Clinic + Wikipedia" pero NO competidor mexicano (gap claro)
- Keywords con intent transaccional bajo competencia ("vale la pena", "comprar", "costo")

### Evitar
- Head terms ("diabetes", "glucosa") — Mayo Clinic + AMD dominan, gasto perdido
- Keywords con KD >50 sin domain authority madura
- Keywords con SERP dominado por papers académicos (intent NO match con buyer)
- Keywords con AI Overviews que dan respuesta completa (low CTR a sitio)

## LLM SEO consideration

Cuando estés haciendo keyword research, considerar también AEO/GEO:

- ¿Esta keyword genera AI Overview en Google?
- ¿La pregunta es citable por ChatGPT/Perplexity/Claude?
- Para AEO: keywords con format "¿qué es...", "¿cómo funciona...", "¿cuál es la diferencia..."
- LLMs citan más fácilmente contenido con FAQ schema + autor médico

Cross-pollination con skill `llm-seo-optimizer` cuando el contenido va a optimizar para citation en LLMs.

## Output a otras skills

- → `pillar-page-drafter`: keyword principal + estructura sugerida
- → `seo-satellite-article`: 8-12 keywords long-tail para satélites del cluster
- → `seo-internal-linking`: estructura semántica para internal linking
- → `seo-monthly-report`: keywords a trackear en Search Console

## Cuándo escalar al humano

- Decisión de head term vs long-tail strategy → SEO strategist + Jose
- Identificación de "money keyword" con KD alto pero alto valor → Jose
- Hallazgo de gap específico vs competidor → Jose para validar estrategia
- Cambio en SERP landscape (Google update, nuevo competidor) → SEO strategist
