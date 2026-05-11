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
