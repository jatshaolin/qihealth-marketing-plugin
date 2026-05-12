---
name: creative-fatigue-detector
description: >
  This skill should be used to detect creative fatigue in active QiHealth ads. Triggers: "creative fatigue", "está fatigando", "frecuencia alta", "necesita refresh", "anuncio cansado", "fatigue check", or runs automatically as part of ad-winner-loser-classifier. Detects when an ad shows fatigue signals (frequency >3.5, CTR drop >25%, CPM rise >30%) and recommends refresh action. Requires Meta Ads + TikTok Ads APIs (activates Lunes post-MVP).
metadata:
  version: "0.1.0"
  type: "operations"
  channel: "paid"
  status: "stub-pending-api-connection"
---

# Creative Fatigue Detector

Tu rol es detectar cuando un anuncio en producción ha alcanzado fatiga creativa — el momento en que la audiencia ya vio el creative tantas veces que la performance cae a pesar de que el concepto sigue siendo bueno. Detección temprana evita gastar presupuesto en creative agotado.

## Estado actual: STUB (pending API connection)

Esta skill requiere `ad-performance-monitor` activo (que a su vez requiere Meta Ads + TikTok Ads APIs). Activación target: lunes post-MVP.

## Cuando esté activa

### Mandatory loading

- `memory/kpis-by-segment.md`
- `memory/ad-learnings.md`
- Output reciente de `ad-performance-monitor`

### Señales de fatiga

Un ad se clasifica como "FATIGA" cuando se cumplen al menos 2 de estas 3:

**Señal 1 — Frecuencia alta**
- Frecuencia >3.5 a 7 días
- Frecuencia >5.0 a 14 días
- (frecuencia = impressions / reach: cuántas veces el mismo usuario ve el anuncio)

**Señal 2 — CTR cayendo**
- CTR cae >25% vs primer 7 días del lifecycle del ad
- CTR cae >40% vs peak histórico del ad

**Señal 3 — CPM subiendo**
- CPM sube >30% vs primer 7 días del ad
- (Meta y TikTok suben CPM cuando el creative pierde score de relevancia)

### Diferencia entre fatiga y loser

- **Fatiga**: el creative funcionó al inicio. Performance buena luego cayó. Concept viable, presentation agotada.
- **Loser**: el creative nunca funcionó. Performance baja desde día 1. Concept o execution mal calibrado.

Si dudas, default a FATIGA (más optimista) y recomendar refresh. Si refresh tampoco funciona, reclasificar a LOSER.

### Acción recomendada al detectar fatiga

```
=== FATIGA DETECTED ===
Ad: [nombre]
Sub-segmento: [...]
Plataforma: [...]
Lifecycle del ad: [N días en producción]

Señales detectadas:
- Frecuencia: X (umbral: 3.5)
- CTR drop: X% vs primer 7 días
- CPM rise: X% vs primer 7 días

Performance histórica:
- Pico: [día X — CTR Y%]
- Actual: [CTR Z%]
- Spend acumulado: $X MXN
- Conversiones acumuladas: N

Recomendación:
1. PAUSE el ad inmediatamente (no seguir gastando en fatiga)
2. Generar 4-6 variantes de refresh:
   - Mantener mensaje núcleo y audiencia
   - Cambiar hook + casting + B-roll + music
   - NO cambiar CTA ni concept
3. Re-launch con audiencia idéntica (no agrandar audience al cambiar creative)
4. Seguimiento: si refresh tampoco rinde >benchmark Loser en 48h → kill concept

Tags para learning:
- "fatigue-{sub-seg}-{format}-{lifecycle}"
- Lifecycle promedio antes de fatiga este sub-seg: [si hay histórico]

GOVERNANCE: Recomendación. Performance Manager ejecuta pause + variantes refresh.
NEXT ACTION: Confirmar pause + autorizar producción de variantes refresh
```

### Cadencia de scan

- **Diaria** (parte del morning brief): scan de todos los ads activos con frecuencia >2.5
- **Tiempo real**: cuando Performance Manager pregunta sobre un ad específico
- **Alerta automática**: si un ad cruza umbral de FATIGA en cualquier scan, notificación inmediata a Slack `#qihealth-paid-performance`

### Aprendizaje acumulado de fatiga

Cada caso de fatiga se anota en `memory/ad-learnings.md`:

```
[Fecha] | [Sub-seg] | [Format] | Fatigue at lifecycle día N | Frecuencia X
- Concept: ...
- Pico de performance: día X — CTR Y%
- Refresh strategy: cambió eje [...]
- Resultado del refresh: [...]
```

A los 90 días, este aprendizaje permite predecir cuánto dura un creative para QiHealth en cada sub-segmento — moat operacional.

### Cuándo escalar al humano

- Si TODOS los ads de un sub-segmento muestran fatiga simultánea → posible problema de audiencia, no creative
- Si fatiga aparece muy temprano (lifecycle <5 días) → posible problema de targeting o creative quality
- Si después de 2-3 refreshes el concept sigue sin recuperar → kill concept y volver a brief
- Cualquier patrón anómalo (CPM normal pero CTR cae sin frecuencia alta) → Performance Manager para investigar

## Activación

Cuando ad-performance-monitor esté activo:

1. Update status de esta skill a "active"
2. Test con un ad histórico que se sepa fatigado (validation)
3. Activar scan diario en morning brief
4. Configurar alertas Slack en `#qihealth-paid-performance`

Hasta entonces, output: `"STATUS: STUB-PENDING-API-CONNECTION. Esta skill se activa cuando ad-performance-monitor esté operacional con Meta + TikTok APIs."`
