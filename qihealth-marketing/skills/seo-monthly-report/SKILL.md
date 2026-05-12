---
name: seo-monthly-report
description: >
  This skill should be used to generate monthly SEO performance reports for QiHealth. Triggers: "reporte SEO mensual", "monthly SEO report", "SEO performance", "ranking trends". Aggregates Search Console + GA4 + Ahrefs data, compares to targets, identifies winners/losers, recommends actions.
metadata:
  version: "0.1.0"
  type: "operations"
  channel: "SEO"
  cadence: "monthly (día 1)"
---

# SEO Monthly Report

Genera reporte mensual de performance SEO. Combina Search Console + GA4 + Ahrefs data via Supermetrics MCP.

## Mandatory loading

- `memory/kpis-by-segment.md` (targets SEO)
- `memory/strategy-v4.3-summary.md` (5 clusters)

## MCPs requeridos

- Supermetrics (bridge a Search Console + GA4)
- Ahrefs (DR, backlinks, ranking history)

## Estructura del reporte

```markdown
# SEO MONTHLY REPORT — [Mes Año]

## Resumen ejecutivo

- Tráfico orgánico total: X visitas (vs mes anterior +Y%)
- Conversiones desde orgánico: N (vs target M)
- Domain Rating: X (vs hace 30 días Y)
- Keywords en top 10: N (cambio +/- desde mes anterior)

## Performance por cluster

| Cluster | Tráfico/mes | Top 10 keywords | Conversiones | vs Target Q |
|---|---|---|---|---|
| BGM-Self | 2,400 | 8 | 18 | 65% del Q target |
| No-Measurers | 3,100 | 12 | 22 | 80% |
| Legacy | 1,200 | 5 | 14 | 55% |
| BGM-Doctor | 800 | 3 | 4 | 40% |
| CGM-Switchers | 1,600 | 6 | 9 | 70% |

## Top 5 keywords ganadoras

1. "pre-diabetes en México" — posición 4 (subió de 12)
2. "diferencia glucómetro CGM" — posición 7 (subió de 18)
3. ...

## Top 5 keywords problema

1. "QiTrax México opiniones" — posición 28 (cayó de 15)
2. ...

## 🏆 Page 2 Goldmine (sección crítica — fastest wins)

Este es el corazón del reporte. Identifica keywords donde QiHealth rankea entre posiciones 11-20 con **al menos 100 impressions/mes**. Estos son los quick wins más altos del SEO — una optimización pequeña puede mover esos keywords a top 10 y multiplicar tráfico.

**Filtros aplicados**:
- Posición actual: 11-20 (página 2 de Google)
- Impressions mensuales: >100 (validar demanda real)
- Idealmente con click-through también pero impressions es el filtro mínimo

### Page 2 Goldmine este mes

| Keyword | Posición actual | Impressions/mes | Página que rankea | Acción específica para subir a top 10 |
|---|---|---|---|---|
| "qué es CGM México" | 14 | 480 | /blog/que-es-cgm | Optimizar title tag (agregar "México" al inicio), H1, primeros 100 palabras |
| "FreeStyle Libre alternativas" | 18 | 320 | /switch | Expandir content sobre alternativas, agregar tabla comparativa schema FAQPage |
| "diabetes hereditaria síntomas" | 12 | 280 | /pillar/diabetes-hereditaria | Agregar internal linking desde Legacy satélites + actualizar autor con cédula |
| ... | ... | ... | ... | ... |

### Per keyword detallado (para top 10 del goldmine)

Por cada keyword en page 2 goldmine, el reporte incluye:

- **Title tag actual**: "[texto]"
- **¿Contiene keyword?**: Sí/No
- **Posición de keyword en title**: 1er, 2do, etc.
- **H1 actual**: "[texto]"
- **¿Contiene keyword en H1?**: Sí/No
- **¿Está en primeros 100 palabras del body?**: Sí/No
- **Word count de la página**: N palabras
- **Internal links hacia la página**: N (de qué páginas)
- **Meta description actual**: "[texto]"
- **CTR actual**: X%
- **Diagnóstico**: razón principal por la que NO está en top 10

### Sprint de optimización Page 2 — propuesta 30 días

| Semana | Acción | Output esperado |
|---|---|---|
| Sem 1 | Title tag + H1 fixes para top 10 keywords del goldmine | 3-5 keywords suben a top 10 en 14-21 días |
| Sem 2 | Content additions para pages <500 palabras | Aumenta authority signal de pages |
| Sem 3 | Internal linking fixes — qué pages deben linkear a qué | Distribución de authority a goldmine pages |
| Sem 4 | Meta description rewrites para pages con high impressions/low CTR | Sube CTR sin tocar position |

**Importante**: para cada fix, el reporte NO solo dice qué hacer — incluye **el copy literal** que el editor/developer debe pegar (no instrucciones genéricas, copy exacto).

## Pages performance

- **Top pages by traffic**: ...
- **Top pages by conversion**: ...
- **Underperformers** (bounce >75%): ...
- **Featured snippets ganados/perdidos**: ...

## Backlinks

- Nuevos backlinks de calidad (DR 50+): N
- Backlinks perdidos: M
- Backlink ratio QiHealth vs Abbott vs Sibionics: [comparativa]

## Recomendaciones para mes siguiente

1. [Acción 1 priorizada]
2. [Acción 2]
3. [Acción 3]

## Health check técnico

- Core Web Vitals: [status]
- Crawl errors: N
- Index coverage: X%
- Mobile usability: status
```

## Output a Slack

```
📊 SEO MONTHLY REPORT — [Mes Año]

Tráfico orgánico: X visitas (+Y%)
Conversiones: N (vs target M)
Keywords top-10: K

🏆 Ganadoras:
- [keyword] → posición [N]
- [keyword] → posición [N]

⚠️ Atención:
- [keyword] cayó a posición [N]

🎯 Acciones priorizadas (3):
1. ...
2. ...
3. ...

Full report: [link Notion/Drive]
```

## Cuándo escalar al humano

- Penalty manual de Google detectado → Jose + SEO strategist URGENTE
- Caída de tráfico >30% mes a mes → investigar Google update
- Pérdida de featured snippet importante → SEO strategist
- Bajada masiva de keywords → Jose
