---
name: monthly-performance-report
description: >
  This skill should be used to generate monthly executive performance report for QiHealth marketing. Triggers: "monthly report", "reporte mensual", "executive report", "month review", "/qihealth-monthly". Aggregates 30 days of all channels + sub-segments, identifies macro trends, recommends budget reallocation between sub-segments, prepares strategic decisions for Jose.
metadata:
  version: "0.1.0"
  type: "operations"
  cadence: "Día 1 6:00 AM cada mes (scheduled task)"
---

# Monthly Performance Report

Reporte ejecutivo mensual. Diferente del weekly: mira tendencias macro, evalúa allocation de presupuesto entre sub-segmentos, e identifica decisiones estratégicas.

## Mandatory loading

- `memory/kpis-by-segment.md`
- `memory/strategy-v4.3-summary.md`
- Reports semanales del mes anterior

## Estructura

```markdown
# QIHEALTH MARKETING — MONTHLY REPORT [Mes Año]

## Resumen ejecutivo (1 página max)

### Métricas clave del mes

| Métrica | Mes actual | Mes anterior | YTD | vs Target Q |
|---|---|---|---|---|
| Conversiones totales | X | Y | Z | A% |
| Spend total marketing | $X | $Y | $Z | A% |
| CAC promedio | $X | $Y | $Z | vs target $W |
| ROAS promedio paid | X | Y | Z | vs target W |
| Tráfico orgánico | X | Y | Z | vs target |
| Leads nuevos Bigin | X | Y | Z | vs target |

### 3 wins del mes
1. ...
2. ...
3. ...

### 3 losses del mes
1. ...
2. ...
3. ...

### Decisión estratégica recomendada
[1 párrafo con la decisión que Jose debe tomar este mes]

---

## Performance por sub-segmento (deep dive)

### CGM-Switchers
- Performance vs target Q: X%
- ROAS: Xx
- Conversiones: N (vs M target/mes)
- Análisis: [tendencia, qué funcionó, qué no]
- Recomendación: [escalar / mantener / pivotar]

[Mismo para BGM-Self, BGM-Doctor, No-Measurers, Legacy]

### SEO transversal
- DR actual: X (vs hace 30 días)
- Keywords en top 10: N (cambio)
- Pillar pages publicadas en el mes: M
- Tráfico orgánico total: X (vs prev mes Y, +/- Z%)

---

## Reasignación de presupuesto sugerida

Comparar allocation actual vs performance real:

| Sub-segmento | % spend actual | % conversiones | ROAS | Recomendación |
|---|---|---|---|---|
| CGM-Switchers | 15% | 12% | 3.5x | Mantener |
| BGM-Self | 25% | 30% | 4.2x | +5% del Legacy |
| BGM-Doctor | 15% | 8% | 2.1x | Mantener (cycle largo) |
| No-Measurers | 25% | 35% | 3.8x | Mantener |
| Legacy | 20% | 15% | 2.5x | -5% a BGM-Self |

**Recomendación**: Reasignar 5% de Legacy a BGM-Self para mes siguiente. Re-evaluar Legacy creative (puede ser fatigue, no problema de sub-segmento).

---

## Equipo & operaciones

- Médicos activos en pipeline Bigin: N (vs target Q)
- Demos realizadas el mes: M
- Médicos que refirieron ≥1 paciente: K (vs target Q)
- KOLs activos: N
- Micro-pacientes activos: M
- Doctor Reels publicados: K

---

## Compliance & riesgos

- COFEPRIS observaciones: 0 ✅ (target)
- Cofepris-check blocks que requirieron rephrase: N
- Advisory reviews completados: M (de N solicitados)
- SLA de advisory cumplido: X%

---

## Calendario mes siguiente

- Sub-segmento foco principal: [sub-seg]
- Pillar page nueva: [título]
- Webinars planificados: N
- Filming days: N
- Lanzamientos paid: ...

---

## Próximas decisiones estratégicas (3-6 meses)

1. ¿Activar Nivel 2 de governance paid? (criterio: ROAS estable + Performance Manager acepta >80% recomendaciones)
2. ¿Considerar nuevo sub-segmento corporativo (Empresas B2B)?
3. ¿Activar canal LinkedIn paid para BGM-Doctor B2B?

---

## Anexos

- Top 10 piezas ganadoras del mes (link a cada una)
- Top 10 piezas underperformers (link)
- Competitive intelligence digest (Abbott + Sibionics)
- Ad learnings consolidados (link a `memory/ad-learnings.md`)
```

## Output a Slack + email a Jose

```
📊 MONTHLY REPORT — [Mes Año]

Conversiones: X (vs Y mes ant, +/- Z%)
ROAS: Xx | CAC: $X
Spend: $X total

🏆 Top 3 wins:
- ...

🎯 3 decisiones para Jose:
1. ...
2. ...
3. ...

Full report: [link Notion]
PDF descargable: [link]
```

## Cuándo escalar al humano

- Si CAC sube >50% mes a mes → análisis de raíz urgente
- Si ROAS cae bajo 1.5x consistentemente en un sub-seg → reconsiderar allocation
- Si un sub-segmento NO está cumpliendo >50% del target Q al final del mes 2 → strategy review
- Cualquier observación COFEPRIS → escalación inmediata Jose + asesoría legal
