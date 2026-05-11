---
name: ad-winner-loser-classifier
description: >
  This skill should be used to classify the performance status of any QiHealth ad currently running. Triggers: "clasifica este anuncio", "winner or loser", "está fatigando este ad", "cómo va el reel de Legacy", "evaluación de performance", "should I scale or kill this ad". Reads ad performance data (CTR, CPM, CPL, ROAS, frecuencia) and classifies the ad into Winner (scale), Maybe (iterate), Loser (kill), or Fatiga (refresh). Provides specific recommendations for next action.
metadata:
  version: "0.1.0"
  type: "operations"
  channel: "paid"
---

# Ad Winner/Loser Classifier

Tu rol es clasificar la performance de cada anuncio de QiHealth en Meta Ads y TikTok Ads, y devolver una recomendación accionable. Operates in **Nivel 1 governance**: solo recomienda, no ejecuta cambios — el humano (Performance Manager) ejecuta.

## Mandatory loading

- `memory/kpis-by-segment.md` (benchmarks por canal y sub-segmento)
- `memory/ad-learnings.md` (aprendizajes acumulados)
- `memory/strategy-v4.3-summary.md`

## Input que recibes

Performance data de un anuncio específico (manual en MVP, automático cuando APIs estén conectadas el lunes):

- Ad ID / nombre
- Sub-segmento target
- Plataforma (Meta FB+IG / TikTok)
- Período evaluado (ej: últimos 7 días)
- Métricas:
  - Impressions
  - CTR
  - CPM
  - CPC
  - CPL (cost per lead) o CPA (cost per action)
  - Frecuencia
  - Conversion rate
  - ROAS (revenue / spend)
  - Spend total

## Las 4 categorías

### Categoría 1 — WINNER (escalar)

Criterios (deben cumplirse 3 de 4):

| Métrica | Umbral Winner |
|---|---|
| CTR | >2.5% (Meta) / >1.5% (TikTok) |
| CPM | <$200 MXN (Meta) / <$0.30 MXN por video view TikTok |
| Frecuencia | <2.5 (a 7 días) |
| ROAS | >3.0x (Meta) / >2.5x (TikTok) |

**Acción recomendada**:
- Escalar presupuesto 1.5x-2x (no más, riesgo de fatiga acelerada)
- Generar 5 variantes nuevas que mantienen el eje ganador (`ad-creative-variants` skill con flag "scale variants")
- Considerar duplicar a TikTok Ads si solo está en Meta o viceversa
- Append learning a `memory/ad-learnings.md` con tag "winner-{eje-ganador}"

### Categoría 2 — MAYBE (iterar)

Criterios:
- 1-2 KPIs flojos pero el resto OK
- O performance variable día a día (data inconclusa)
- O frecuencia subiendo pero CTR aún OK

**Acción recomendada**:
- Mantener mismo budget
- Generar 3 variantes que iteran 1 eje (hook típicamente)
- Esperar 48-72h adicionales
- Si en 72h sigue maybe → reclasificar (probable a loser)

### Categoría 3 — LOSER (kill)

Criterios (3+ KPIs por debajo del benchmark Loser):

| Métrica | Umbral Loser |
|---|---|
| CTR | <1.5% (Meta) / <0.8% (TikTok) |
| CPM | >$350 MXN (Meta) / >$0.60 MXN TikTok |
| ROAS | <1.5x (Meta) / <1.2x (TikTok) |
| CPL | >2x el target del sub-segmento |

**Acción recomendada**:
- Pausar el anuncio (recomendación al Performance Manager)
- Análisis post-mortem: identificar qué eje falló
- Si toda la audiencia falló → reconsiderar audience, no solo creative
- Si solo creative falló → mantener audience + producir 3 variantes con ejes muy distintos (hooks, casting, voice)
- Append learning como anti-patrón al sub-segmento

### Categoría 4 — FATIGA (refresh)

Criterios:
- Frecuencia >3.5 a 7+ días
- Y/o CTR cae >25% vs semana anterior
- Y/o CPM sube >30% vs semana anterior

**Acción recomendada**:
- NO matar el concepto (sigue resonando, solo se gastó la novedad)
- Pausar la variante específica
- Generar 4-6 variantes nuevas que mantienen mensaje núcleo + cambian presentación (hook, casting, B-roll, music)
- Re-launch con audiencia idéntica pero creative refresh
- Si refresh también fatiga rápido → entonces sí kill el concepto

## Output format

```
=== AD CLASSIFIER ===
Ad: [nombre o ID]
Sub-segmento: [...]
Plataforma: [Meta / TikTok]
Período: [últimos N días]

Performance:
- CTR: X% (vs benchmark Y%)
- CPM: $X MXN (vs benchmark $Y)
- Frecuencia: X (vs umbral Y)
- ROAS: Xx (vs benchmark Yx)
- CPL: $X (vs target $Y)
- Spend total: $X MXN

Veredicto: [WINNER / MAYBE / LOSER / FATIGA]

Análisis:
- [bullet sobre qué está funcionando o no]
- [bullet sobre eje específico]
- [bullet sobre comparación con sub-seg benchmark]

Acción recomendada:
- [acción específica con números si aplica — ej: "Escalar de $300/día a $500/día"]
- [siguiente paso operacional]
- [seguimiento cuándo: "Re-evaluar en 72h"]

Variantes a generar (si aplica):
- [N variantes según veredicto]

GOVERNANCE: Recomendación. Performance Manager ejecuta el cambio.
NEXT ACTION: [acción concreta para humano]
```

## Reglas de honestidad

- Si la data es insuficiente (ad lleva <48h corriendo, spend <$100), declararlo. No clasificar prematuramente.
- Si la métrica de conversión está rota o no trackeada, declararlo. CTR alto sin tracking de conversión NO es winner — es señal incompleta.
- Si el sub-segmento target del anuncio no coincide con la audiencia configurada, alertar (puede ser misalignment de campaign setup).

## Comparación con histórico

Cuando el sistema clasifica un anuncio, compara contra:
- Promedio histórico del sub-segmento (de `ad-learnings.md`)
- Top performer histórico del sub-segmento (benchmark interno)
- Benchmark de industria (de `kpis-by-segment.md`)

Si un anuncio rinde peor que el histórico de QiHealth pero mejor que la industria, eso es matiz importante (probablemente la cuenta tiene buena maduración).

## Cuando hay duda — defaults conservadores

- Entre WINNER y MAYBE → MAYBE (no escalar prematuro)
- Entre MAYBE y LOSER → MAYBE (dar 48h más antes de matar)
- Entre LOSER y FATIGA → distinguir bien:
  - Si frecuencia es alta pero CTR-spend ratio era bueno antes → FATIGA
  - Si nunca rindió bien desde día 1 → LOSER

## Cuándo escalar al humano

- Cualquier recomendación de escalar >2x el presupuesto → Performance Manager + Jose
- Cualquier recomendación de matar campaign con spend acumulado >$X → Performance Manager + Jose (riesgo de matar prematuro)
- Cualquier patrón sistémico (todos los anuncios de un sub-seg perdiendo, o toda una audiencia fatigando) → Jose para estrategia
- Cuando aparezca data anómala (ej: spike de impresiones sin spend correspondiente) → alerta + investigación

## Cadencia de uso

- **Diaria** (vía morning brief): scan de todos los anuncios activos, clasificación rápida, alertas por excepción
- **Semanal** (review viernes): clasificación completa con análisis profundo, recomendaciones para semana siguiente
- **Bajo demanda**: cuando Jose o Performance Manager pregunte sobre un anuncio específico

## Output al morning brief

En el morning brief automático, output condensado:

```
🟢 WINNERS (escalar): 2
- Reel Legacy "Mi papá lo vivió" — ROAS 4.2x — recomiendo +50% budget
- Carrusel BGM-Self "5 cosas glucómetro" — Save rate 5.8% — extender a Meta paid

🟡 MAYBE (iterar): 3
- ...

🔴 LOSERS (kill): 1
- Reel No-Measurers V3 — CTR 0.9% — kill, mantener V1 y V2

⚠️ FATIGA (refresh): 1
- Reel BGM-Self V2 — frecuencia 4.1 — refresh con 4 variantes nuevas
```

Esto da a Jose visibilidad rápida sin tener que abrir Meta Ads Manager.
