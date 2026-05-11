---
name: ad-creative-variants
description: >
  This skill should be used to generate paid ad creative variants for QiHealth across Meta Ads (Facebook + Instagram), TikTok Ads, and Google Ads. Triggers: "variantes de anuncio", "ad creative", "8 variantes para Legacy", "ad copy variations", "anuncios paid", "creatives para Meta", "creatives para TikTok", "anuncio para A/B test", "iterar ad creative". Generates N variants per platform with specs, copy variations, hook variations, and creative direction. Designed for Meta Andromeda 2026 (high creative diversity, fast iteration).
metadata:
  version: "0.1.0"
  type: "production"
  channel: "paid"
  platforms: ["Meta", "TikTok", "Google"]
---

# Ad Creative Variants — Paid Production

You generate paid ad creative variants for QiHealth optimized for **Meta Andromeda 2026**. Andromeda rewards high creative diversity + fast iteration + clear signals + Advantage+ Audiences. Your job is to produce 8-12 variants per concept (not 3) so the algorithm has enough to test fast.

## Mandatory loading

Before producing variants, read:
- `memory/strategy-v4.3-summary.md`
- `memory/brand-voice.md`
- `memory/cofepris-rules.md`
- `memory/ad-references.md` — winning references (input from Jose)
- `memory/ad-learnings.md` — accumulated learnings
- `memory/kpis-by-segment.md` (paid benchmarks por canal)
- The persona skill of target sub-segmento

## Filosofía Andromeda 2026

Meta Andromeda es el retrieval engine personalizado de Meta para Advantage+ que cambió las reglas del juego en 2025-2026. Implicaciones para producción de creative:

### 1. Diversidad creativa > optimización por slot
**Antes (pre-Andromeda)**: 3 variantes pulidas y optimizadas
**Ahora**: 8-12 variantes con diversidad real (hook, ángulo, casting, voice, format) — Andromeda explora rápido y mata rápido.

### 2. Decantación rápida
Andromeda decide winners en 48-72h. NO esperes 7 días para juzgar. El sistema produce variantes en bulk para que el algoritmo decante rápido.

### 3. Signals fuertes
Cada creative debe tener:
- **Mensaje núcleo cristalino** (no ambiguo)
- **CTA explícito** (no implícito)
- **Hook sin warm-up** (problema desde frame 1)
- **Producto/marca visible** (sin ser intrusivo)

### 4. Advantage+ Audiences default
Detailed targeting tradicional pierde peso. Asume Advantage+ por default; usa detailed solo cuando hay justificación clara (ej: targeting B2B de endocrinólogos en LinkedIn, no en Meta).

## Variantes por concepto (sweet spot 8-12)

Para cada pieza, generar variantes diversificadas en estos ejes:

### Eje 1 — Hook angle
- Variant 1: Pregunta directa
- Variant 2: Estadística punzante
- Variant 3: Anclaje personal/emocional
- Variant 4: Pattern interrupt (visual o auditivo)
- Variant 5: Comparativa directa

### Eje 2 — Casting / voice
- Voiceover anónimo (femenino)
- Voiceover anónimo (masculino)
- Médico del advisory (Doctor Reel)
- Paciente real (testimonial)
- Animación + texto on screen

### Eje 3 — Format
- Reel 15s (super corto)
- Reel 30s (estándar)
- Reel 60s (long-form)
- Static image + texto
- Carrusel paid (5 slides)
- Video sin audio (caption-driven)

### Eje 4 — Tono
- Clínico
- Cálido / introspectivo
- Urgente
- Curioso
- Educativo puro

### Eje 5 — CTA
- Suave: "Sigue para más"
- Medio: "Toma el quiz / Lee el blog"
- Directo: "Empieza con 15 días"
- Urgente: "Esta semana, descuento"

Generar 8-12 combinaciones que diversifiquen al menos 3 ejes simultáneamente. NO duplicar (variant 1 y variant 2 deben ser distintas en por lo menos 3 ejes).

## Specs por plataforma

### Meta (Facebook + Instagram Ads)

#### Aspect ratios
- **9:16** (1080x1920) — Stories, Reels (PRIMARIO en 2026)
- **4:5** (1080x1350) — feed
- **1:1** (1080x1080) — backup, cuando no hay 4:5
- **1.91:1** (1200x628) — link ads, feed clásico (deprecated mostly)

#### Copy length
- **Primary text**: hasta 125 chars en preview, hasta 2200 chars total. Sweet spot 80-150 chars.
- **Headline**: hasta 27 chars (mostrar truncado)
- **Description**: 27 chars
- **CTA button**: pre-set ("Más información", "Comprar ahora", "Registrarse", etc.)

#### Variants por ad set
- Mínimo 4 creative variants por ad set
- Ideal 6-8 creative variants por ad set para Andromeda
- Si presupuesto bajo: 4 ad sets x 4 variants = 16 creatives totales

### TikTok Ads (cuando exista cuenta de QiHealth)

#### Aspect ratios
- **9:16** (1080x1920) — único ratio recomendado

#### Format types
- **In-Feed**: aparece en For You feed
- **TopView**: aparición prominente al abrir app (premium)
- **Spark Ads**: boost de orgánico (mejor performance — usa creative orgánico ganador)

#### Copy length
- **Caption**: hasta 100 chars (sweet spot 60-80)
- **CTA**: pre-set similar a Meta

#### Specs creativos
- Hook 0-3s super agresivo
- Texto on-screen quemado (audio-off ready)
- Trending audio cuando aplique tonalmente

### Google Ads (Search + Display)

QiHealth en Search tiene oportunidad limitada — keywords de "diabetes" son caros. Mejor usar Display y YouTube Ads para retargeting de visitantes a blog SEO + landing pages.

#### YouTube Ads
- **Skippable in-stream**: 15-180s, hook obligatorio en primeros 5s
- **Non-skippable**: 15s
- **Bumper**: 6s, ultra concentrado

#### Display
- **Responsive Display Ads**: subir múltiples assets, Google los combina
- **Banner sizes**: 300x250, 728x90, 320x50, 300x600 (priorizar Responsive)

## Output format

```markdown
# AD CREATIVE VARIANTS — [Sub-segmento] [Etapa] — [Tema]

**Brief**: [referencia o resumen]
**Sub-segmento**: [...]
**Etapa funnel**: [...]
**Plataforma(s)**: [Meta / TikTok / Both / + Google]
**Variantes totales**: [N, sweet spot 8-12]

---

## Variante 1 — [hook angle: "pregunta directa"] / [casting: VO femenino] / [format: Reel 30s]

### Para Meta (FB+IG)

**Primary text**: 
"[texto, max 125 chars en preview]"

**Headline**: 
"[texto, max 27 chars]"

**CTA button**: [Ver más / Comprar ahora / Inscribirse / etc.]

**Visual direction**: 
[descripción del visual: hook + body + CTA card]

**Audio direction**: 
[VO con tono específico]

### Para TikTok (si aplica)

**Caption**: 
"[texto, max 100 chars]"

**Spec creativos**: 
[diferencias vs Meta — más agresivo, audio trending, etc.]

---

## Variante 2 — [eje cambia: "estadística punzante"] / [casting: VO masculino] / [format: Reel 15s]

[mismo formato]

---

[... variantes 3-12 ...]

---

## Audiencias sugeridas

### Meta (Andromeda + Advantage+)
- Audiencia 1 (Advantage+): Lookalike de compradores de glucómetros + intereses diabetes/salud
- Audiencia 2 (Detailed): Personas con familiar directo con diabetes (Legacy específico)
- ...

### TikTok
- Audiencia 1: Custom audience de visitantes a /pre-diabetes blog
- Audiencia 2: Lookalike de inscritos al quiz "¿Estás en riesgo?"
- ...

---

## Hipótesis de variant winner (predicción)

[1-2 líneas anticipando cuál variante esperas que gane y por qué — sirve para comparar con resultado real y mejorar el sistema]

---

## Quality gates pendientes

- [ ] cofepris-check (cada variante)
- [ ] brand-voice-qihealth (cada variante)
- [ ] factual-review (cada variante)
- [ ] (si aplica) advisory medical review

STATUS: VARIANTS-DRAFT
NEXT ACTION: Run cofepris-check on all variants in parallel
GOVERNANCE: Estas variantes son drafts. Performance Manager humano aprueba lanzamiento en Meta/TikTok Ads Manager (Nivel 1 governance).
```

## Reglas de iteración con feedback

Cuando un creative gana en producción real:

1. Identificar el eje ganador (hook? casting? voice?)
2. Generar 4-6 variantes nuevas que **mantengan ese eje** y varíen los otros
3. Continuar exploración hasta encontrar combinaciones aún más fuertes
4. Append a `memory/ad-learnings.md` con tag específico del eje ganador

Cuando un creative pierde:

1. NO descartar el concepto inmediatamente
2. Hipotetizar qué eje falló (hook? casting? CTA? timing?)
3. Generar 2-3 variantes con ese eje cambiado y los demás iguales
4. Si todas las variantes pierden → kill el concepto, append learning como "anti-patrón Sub-X"

## Reglas de creative fatigue (cuando aplica)

Si una variante alcanza:
- Frecuencia >3.5 (a 7 días)
- CTR cae >25% vs primer día
- CPM sube >30% vs primer día

→ trigger refresh. Generar 4-6 variantes nuevas que iteren sobre el ganador (mismo concepto, hook nuevo, casting nuevo, etc.). Mantener el concepto vivo, refrescar la presentación.

## Cuándo escalar al humano

- Decisión de lanzamiento de campaña → Performance Manager + Jose (Nivel 1)
- Decisión de presupuesto > $X (define Jose) → Jose
- Variante que toca claim sensible → cofepris-check + advisory si dudas
- Variante con casting de paciente real → community manager + verificación de consentimiento
