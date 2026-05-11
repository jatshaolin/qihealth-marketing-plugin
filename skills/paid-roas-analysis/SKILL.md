---
name: paid-roas-analysis
description: >
  This skill should be used to analyze ROAS performance of QiHealth paid campaigns across Meta and TikTok. Triggers: "ROAS analysis", "análisis ROAS", "performance por sub-segmento", "spend efficiency", "paid efficiency". Pulls ad spend + revenue by sub-segment, calculates ROAS, identifies sub-segment efficiency, recommends budget reallocation.
metadata:
  version: "0.1.0"
  type: "operations"
  channel: "paid"
---

# Paid ROAS Analysis

Análisis de eficiencia de paid media por sub-segmento.

## Mandatory loading

- `memory/kpis-by-segment.md`
- `memory/strategy-v4.3-summary.md`

## MCPs requeridos
- Meta Ads API (vía Meta Business)
- TikTok Ads API
- Supermetrics (bridge)
- Bigin (attribution revenue)

## Análisis estándar

### Por sub-segmento
- Spend total mes
- Conversiones atribuibles
- Revenue generado
- ROAS = revenue / spend
- CAC = spend / conversiones
- Comparación vs target Q

### Reasignación recomendada
- Si sub-seg A ROAS >4x y allocation actual 15% → recomendar +5%
- Si sub-seg B ROAS <1.5x consistente → reducir allocation o pausar
- Cambios sugeridos van a Performance Manager humano para ejecutar

### Trend detection
- ROAS subiendo: scale opportunity
- ROAS plano alto: optimizar bid strategy
- ROAS cayendo: investigar (creative fatigue? audiencia saturada? Andromeda update?)

## Output

```
=== ROAS ANALYSIS — [Período] ===

| Sub-seg | Spend | Conv | Revenue | ROAS | CAC | Target | Status |
|---|---|---|---|---|---|---|---|
| CGM-Switch | $X | N | $Y | Zx | $W | 3.5x | ✅ |
| ...

🎯 Recomendaciones:
1. Reallocar $X de [sub-seg A] a [sub-seg B] (ROAS justifica)
2. Pausar campaign [ID] en [sub-seg C] (ROAS <1.5x por 14 días)
3. ...

NEXT: Performance Manager humano ejecuta cambios.
```

## Cuándo escalar al humano

- Cambio de allocation >10% en un mes → Jose
- ROAS de sub-seg <1.0x → urgente investigación
- Sospecha de fraud / click farms → Performance Manager + Meta/TikTok support
