---
name: ab-test-designer
description: >
  This skill should be used to design A/B tests for QiHealth marketing experiments. Triggers: "A/B test", "experiment", "split test", "diseñar prueba", "hipótesis test". Designs experiments with clear hypothesis, variant definitions, primary/secondary metrics, sample size, duration, decision criteria. NEVER auto-executes — output goes to Performance Manager.
metadata:
  version: "0.1.0"
  type: "operations"
  channel: "experimentation"
---

# A/B Test Designer

Diseña experimentos rigurosos con hipótesis clara, samples adecuados y criterios de decisión.

## Mandatory loading

- `memory/kpis-by-segment.md`
- `memory/ad-learnings.md`

## Estructura del test

```yaml
test_id: "TEST-{YYYY-MM-DD}-{N}"
name: "Hook variant: Pregunta vs Estadística — Legacy Reel TOF"

hypothesis: |
  Reels Legacy con hook "Estadística punzante" (Variant B) tendrán
  CTR >20% superior a Reels con hook "Pregunta directa" (Variant A)
  en audiencias paid Meta Lookalike-Legacy.

variants:
  A (control): "Hook pregunta directa"
  B (test): "Hook estadística punzante"

audiences:
  shared:
    - Lookalike-Legacy 1%
    - Detailed: parents of diabetic adults (age 30-50)
  
test_design:
  split: 50/50
  duration: 14 días (mínimo para confidence)
  min_spend_per_variant: $1,500 MXN
  
primary_metric: CTR
secondary_metrics:
  - CPL (cost per lead)
  - Save rate (organic equivalent)
  - Conversión a landing /legacy

sample_size:
  estimated_impressions_per_variant: 40,000
  confidence_level: 90%
  minimum_detectable_effect: 15% lift
  
decision_criteria:
  winner: |
    Si CTR variant B > variant A en >15% relative lift
    Y p-value <0.10
    Y CPL no degradado >20%
  loser: |
    Si A iguala B (sin lift significativo) → mantener A (default)
  inconclusive: |
    Si sample size <target → extender 7 días más o aumentar spend

next_action_if_winner_B: |
  1. Pausar variant A
  2. Escalar variant B con +50% budget
  3. Generar 4-6 variantes nuevas que mantienen "estadística punzante"
  4. Append learning a memory/ad-learnings.md
```

## Reglas

### NO hacer

- A/B test sin hipótesis clara
- Variants que difieren en >1 variable (no es A/B real)
- Stop antes del minimum sample
- "Peeking" (mirar resultados mid-test y decidir prematuro)
- Tests con confidence <85%

### SÍ hacer

- 1 variable cambiada por test (hook, casting, voice, CTA, audience)
- Sample size calculado upfront
- Decision criteria definida ANTES de correr
- Documentar resultado (ganador o no) en `memory/ad-learnings.md`

## Tests prioritarios para QiHealth

1. **Hook angle (Legacy)**: pregunta vs estadística vs anclaje personal
2. **Casting (No-Measurers)**: VO femenino vs masculino vs Doctor Reel
3. **CTA strength (CGM-Switchers)**: "Cambia hoy" vs "Conoce más" vs "30 días gratis"
4. **Format (BGM-Self)**: Reel 30s vs Carrusel 5-slides
5. **Audiencia (Legacy)**: Lookalike vs Detailed targeting

## Output

Test design listo para que Performance Manager ejecute en Meta/TikTok Ads Manager.

## Cuándo escalar al humano

- Decisión de spend total del test → Performance Manager
- Test que sale resultado contraintuitivo → Jose para discusión
- Test que viola brand voice o COFEPRIS → cofepris-check + advisory
