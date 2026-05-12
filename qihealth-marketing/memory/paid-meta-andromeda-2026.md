# Meta Andromeda 2026 — Reglas operativas para QiHealth

**Fuente**: análisis basado en Meta engineering disclosures + observaciones de practitioners 2025-2026 (incluyendo @adsacademyof, @humoenargentina, y community Meta Ads LATAM).

Andromeda es el nuevo retrieval engine personalizado de Meta para Advantage+ que cambió las reglas del juego en 2025-2026. Este documento define cómo QiHealth opera paid Meta bajo Andromeda — todas las skills de paid (`ad-creative-variants`, `ad-feedback-iterator`, `creative-fatigue-detector`, `ad-winner-loser-classifier`) deben respetar estas reglas.

---

## 1. Qué es Andromeda

Andromeda es el motor que Meta usa internamente para:
- **Seleccionar a quién mostrar un ad** (retrieval personalizado, no solo audience match)
- **Rankear ads competidores** en cada subasta
- **Decidir dónde colocar el ad** (FB feed vs IG Reels vs Stories vs Marketplace)
- **Estimar predicted action** (CTR + conversion likelihood) por usuario individual

A diferencia del modelo pre-2024 (que dependía fuerte de detailed targeting + lookalikes manuales), Andromeda usa ML para inferir audience-creative fit individualmente.

---

## 2. Qué cambió vs pre-Andromeda

### Cambio 1 — Detailed targeting pierde peso

**Antes**: definías audiencia con interests, behaviors, demographics, lookalikes específicos. Meta servía a esa audiencia.

**Ahora**: Andromeda ignora bastante el detailed targeting si encuentra usuarios más probables de convertir afuera de él. Tu "audiencia objetivo" se vuelve sugerencia, no instrucción.

**Implicación**: Detailed targeting solo funciona como **señal inicial** para que Andromeda aprenda. Después se expande automáticamente.

### Cambio 2 — Advantage+ Audiences es el default

**Antes**: Advantage+ era opcional / experimental.

**Ahora**: Advantage+ es donde Meta pone el budget de optimización ML. Las campañas que NO usan Advantage+ tienen menor reach y mayor CPM en general.

**Implicación**: Usa Advantage+ Audiences por default. Detailed targeting solo cuando hay justificación clara (ej: B2B muy específico, restricciones legales).

### Cambio 3 — Diversidad creativa pesa más

**Antes**: 3 variantes pulidas y bien optimizadas funcionaban.

**Ahora**: Andromeda explora y mata rápido. Necesita **8-12 variantes** por concepto para tener señales suficientes y decantar winners.

**Implicación**: La regla del plugin es **8-12 variantes por concepto, no 3**. Producir bulk, no pulir uno solo.

### Cambio 4 — Decantación acelerada

**Antes**: 7-14 días para evaluar un ad.

**Ahora**: Andromeda decide winners en **48-72 horas**.

**Implicación**: NO esperes 7 días para juzgar. Si en 72h no rinde, está muerto. Y si rinde, escalar inmediato.

### Cambio 5 — Signals fuertes premiados

Andromeda penaliza creatives ambiguos. Premia:

- **Mensaje núcleo cristalino** (no ambiguo)
- **CTA explícito** (no implícito)
- **Hook sin warm-up** (problema desde frame 1)
- **Producto/marca visible** (sin ser intrusivo)
- **Brand familiarity signals** (consistencia entre creatives del mismo advertiser)

### Cambio 6 — Creative fatigue es brutal

**Antes**: un creative duraba semanas o meses.

**Ahora**: cuando Andromeda satura la audiencia óptima, fatigue aparece en **5-10 días** (vs 21-30 antes). Frecuencia >3.5 = matar inmediato.

---

## 3. Reglas operativas QiHealth bajo Andromeda

### Regla 1 — Asume Advantage+ Audiences por default

Solo usa detailed targeting cuando:
- Audiencia muy específica B2B (ej: endocrinólogos LinkedIn — pero ese es LinkedIn, no Meta)
- Requirement legal específico (raro en healthtech wellness)
- Saturación de Advantage+ confirmada (que es muy improbable los primeros meses)

### Regla 2 — Producir 8-12 variantes mínimo por concepto

Tu skill `ad-creative-variants` debe generar mínimo 8 variantes diversificando 3+ ejes simultáneamente:
- Hook angle (5 tipos: pregunta directa, estadística, anclaje personal, pattern interrupt, comparativa)
- Casting (VO fem, VO masc, médico, paciente, animación)
- Format (15s, 30s, 60s, static, carrusel)
- Tono (clínico, cálido, urgente, curioso)
- CTA strength

### Regla 3 — Cadencia de evaluación de 48-72h

`ad-winner-loser-classifier` debe correr cada 24-48h sobre cada ad nuevo. No esperar 7 días.

Decisión criteria:
- **Winner** (escalar inmediato): 3 de 4 KPIs en winner zone a 48h
- **Maybe** (iterar): performance variable a 48h
- **Loser** (matar): 3+ KPIs en loser zone a 72h
- **Fatiga** (refresh): frecuencia >3.5 + CTR drop >25%

### Regla 4 — Iteration target <24h

Cuando un creative gana o pierde, `ad-feedback-iterator` debe entregar variantes nuevas en **<24h del feedback**. Andromeda no espera.

### Regla 5 — Mensaje núcleo cristalino

Quality gate del plugin (`brand-voice-qihealth`) ya valida esto. Adicional para Andromeda: el mensaje principal debe estar visible en los primeros 3 segundos del Reel, no construirse poco a poco.

### Regla 6 — Brand consistency entre variantes

Andromeda detecta cuando un advertiser tiene creatives consistentes y los favorece. Eso significa:
- Todos los Reels QiHealth deben tener mismo logo placement
- Mismas fuentes
- Mismo color grading
- Misma estructura general (aunque hooks varíen)

La skill `visual-prompt-builder` debe respetar estos brand consistency rules cuando genere prompts Higgsfield.

### Regla 7 — Lookalikes basados en datos propios (cuando los haya)

Una vez QiHealth tenga 100+ conversiones, crear Lookalike 1% basado en compradores. Andromeda usa lookalikes propios para refinar discovery muy rápido.

Mientras tanto: Lookalikes basados en visitantes a web (Custom Audience desde Pixel) + Lookalikes de followers IG.

### Regla 8 — Tracking via CAPI obligatorio

Meta Conversions API (CAPI) es CRÍTICO para Andromeda. Sin CAPI bien implementado, Andromeda no tiene señales de conversión y optimiza mal.

**Antes de lanzar paid**: confirmar que Pixel + CAPI están configurados con events:
- ViewContent
- AddToCart
- Purchase
- Lead
- Schedule (para agendar demos médico)

---

## 4. Benchmarks bajo Andromeda (LATAM healthtech)

Estos benchmarks vienen de practitioners 2026 — el plugin `ad-winner-loser-classifier` los usa para clasificar:

### Meta Ads (FB + IG) bajo Andromeda

| Métrica | Winner | Maybe | Loser |
|---|---|---|---|
| CTR (orgánico-style hook) | >2.5% | 1.5-2.5% | <1.5% |
| CTR (direct-response hook) | >3.5% | 2-3.5% | <2% |
| CPM | <$200 MXN | $200-350 MXN | >$350 MXN |
| Frecuencia (a 7 días) | <2.5 | 2.5-3.5 | >3.5 (fatiga) |
| Conversion rate | >2% | 1-2% | <1% |
| ROAS | >3.0x | 1.5-3.0x | <1.5x |

### Cambios vs benchmarks pre-Andromeda

- **CPM ha subido ~20%** en general (Andromeda es más caro)
- **CTR ha subido ~15%** (creatives mejores ganan más)
- **ROAS estable** si el creative + landing convierten
- **Frecuencia fatiga aparece más rápido** (3.5 vs 5.0 antes)

---

## 5. Errores comunes a evitar

### Error 1 — Pulir 3 variantes en vez de producir 12

Resultado: Andromeda no tiene suficientes señales, decanta mal, performance mediocre.

**Fix**: producir bulk, dejar Andromeda decantar, escalar al winner.

### Error 2 — Usar detailed targeting muy restrictivo

Resultado: Andromeda no puede expandir, CPM sube, reach baja.

**Fix**: Advantage+ Audiences como base. Detailed solo si es estratégico.

### Error 3 — Esperar 7 días para juzgar

Resultado: gastaste budget en losers que Andromeda ya identificó como malos en 48h.

**Fix**: Check daily a 48-72h. Kill rápido, escalar rápido.

### Error 4 — Refresh tardío

Resultado: continuaste corriendo creative en frecuencia 4-5, CTR cayendo, gastando sin convertir.

**Fix**: `creative-fatigue-detector` corre diario. Refresh al detectar fatiga (frec 3.5).

### Error 5 — No CAPI / Pixel mal implementado

Resultado: Andromeda no sabe quién convierte, optimiza por proxy débil.

**Fix**: CAPI bien implementado ANTES de lanzar paid serio.

### Error 6 — Brand inconsistency entre creatives

Resultado: Andromeda no construye brand familiarity, cada creative arranca desde cero.

**Fix**: brand consistency obligatoria. Logo, fuentes, color grading consistentes.

---

## 6. Específico para healthtech YMYL bajo Andromeda

### COFEPRIS interactúa con Andromeda así

- Cuando Andromeda evalúa "brand safety", penaliza creatives con red flags clínicos
- Claims como "cura", "diagnóstico", "garantizado" → no solo COFEPRIS bloquea, también Meta penaliza
- Compliance limpio = Andromeda confía + mejor delivery

### Audiences healthtech bajo Andromeda

- Advantage+ tiende a expandir bastante en healthtech
- Detailed signals iniciales útiles: "interest: diabetes", "interest: salud", "behavior: caregivers"
- Custom Audience desde Pixel de visitantes a /pre-diabetes blog
- Lookalike de compradores Insight 15 (cuando haya 100+)

### Restrictions específicas de Meta en healthtech

- NO "before/after" imagery
- NO claims de pérdida de peso
- NO imagery de personas tristes/enfermas (Meta lo penaliza como "negative")
- NO sensores aplicados visibles si parecen invasivos
- SÍ lifestyle imagery con personas activas y healthy

### Sub-segmentos QiHealth bajo Andromeda

**No-Measurers TOF**: Andromeda expande mucho aquí (audience amplia). Necesitas 12+ variantes para que decante.

**Legacy TOF/MOF**: Andromeda decanta más rápido (audience más específica por emocional). 8 variantes alcanza.

**CGM-Switchers**: Custom Audience desde Pixel + Lookalike de visitantes /comparativa. Detailed targeting puede ayudar inicialmente.

**BGM-Self MOF**: Advantage+ funciona bien. Long-form content (Reel 60s) suele decantar bien.

**BGM-Doctor**: NO se hace paid Meta para lado HCP (mejor LinkedIn). Para lado paciente, Advantage+ similar a BGM-Self.

---

## 7. Workflow integrado con plugin QiHealth

### Producción

1. Orchestrator + persona del sub-segmento → brief
2. `ad-creative-variants` → produce 8-12 variantes (no 3)
3. `visual-prompt-builder` → genera assets vía Higgsfield manteniendo brand consistency
4. Quality gates (`cofepris-check`, `brand-voice`, `factual-review`)
5. Output: variants ready, Performance Manager humano sube a Meta Ads Manager

### Lanzamiento

1. Performance Manager configura Advantage+ campaign
2. Setea minimum budget per variant ($150 MXN/día como floor)
3. CAPI verificado activo

### Monitoreo (cada 24-48h)

1. `ad-performance-monitor` pull data Meta API
2. `ad-winner-loser-classifier` clasifica
3. `creative-fatigue-detector` detecta refresh needs
4. Output: morning brief con recomendaciones

### Iteración (<24h del feedback)

1. Jose o Performance Manager da feedback
2. `ad-feedback-iterator` produce variantes ajustadas
3. Quality gates re-ejecutan
4. Performance Manager lanza variantes nuevas

### Aprendizaje acumulado

Cada iteración se anota en `memory/ad-learnings.md`. A los 60-90 días, el sistema sabe específicamente qué funciona para QiHealth en cada sub-segmento bajo Andromeda.

---

## 8. Fuentes y validación

Este documento se basa en:
- Meta Engineering Blog (December 2024): "Meta Andromeda: Supercharging Advantage+ automation"
- Observaciones de practitioners 2026: @adsacademyof, @humoenargentina
- Best practices community Meta Ads LATAM
- Validation con benchmarks de QiHealth (cuando existan datos propios)

**Actualizar este documento**:
- Cada vez que Meta publique cambio mayor en Andromeda
- Cada vez que un practitioner respetado reporte nueva táctica probada
- Cada trimestre con learnings propios de QiHealth

---

## Historial de cambios

- **2026-05-12**: documento inicial creado a partir de análisis de TikTok @adsacademyof + Meta engineering docs + observaciones LATAM healthtech
