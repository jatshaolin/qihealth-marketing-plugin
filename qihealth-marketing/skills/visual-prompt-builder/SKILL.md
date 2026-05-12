---
name: visual-prompt-builder
description: >
  This skill should be used to generate visual generation prompts for QiHealth content, optimized for Higgsfield (generation + character consistency) and Nano Banana / Gemini 2.5 Flash Image (editing + adaptation). Triggers: "prompt para Higgsfield", "prompt para Nano Banana", "imagen para [sub-segmento]", "B-roll prompt", "visual prompt", "genera prompt visual", "necesito imagery para [pieza]". Produces ready-to-paste prompts with sub-segment-specific mood, COFEPRIS-safe guardrails, and structured Drive folder for the generated output.
metadata:
  version: "0.1.0"
  type: "production"
  tools: ["Higgsfield", "Nano Banana / Gemini Image", "Manual"]
---

# Visual Prompt Builder — Higgsfield + Nano Banana

Tu rol es generar prompts de generación visual para que el equipo de QiHealth (o el diseñador) los ejecute manualmente en Higgsfield o Nano Banana, con specs claras por sub-segmento y guardrails COFEPRIS automáticos.

## Mandatory loading

- `memory/brand-voice.md` (mood y vocabulario visual)
- `memory/cofepris-rules.md` (lo que NUNCA se puede mostrar visualmente)
- `memory/strategy-v4.3-summary.md`
- La persona del sub-segmento target

## Cuándo usar Higgsfield vs Nano Banana

| Necesidad | Herramienta recomendada |
|---|---|
| Generar desde cero (no hay imagen base) | **Higgsfield** |
| Character consistency en serie | **Higgsfield** |
| Variantes batch del mismo concepto | **Higgsfield** |
| B-roll lifestyle (manos, escenas, comidas) | **Higgsfield** |
| Generación de video corto | **Higgsfield** |
| Editar imagen existente (cambiar fondo, ajustar elemento) | **Nano Banana** |
| Adaptar mismo creative a 1:1 / 9:16 / 4:5 | **Nano Banana** |
| Retoques de fotos reales del sensor en contextos distintos | **Nano Banana** |
| Limpieza y enhance de imagery existente | **Nano Banana** |

Si dudas, default a Higgsfield para generación pura, Nano Banana para edición sobre asset existente.

## COFEPRIS guardrails — NUNCA generar

Antes de generar cualquier prompt, validar contra `memory/cofepris-rules.md`:

### Prohibido absoluto en imagery
- Persona que parezca tener condición médica visible (inyección de insulina, glucómetro siendo usado por persona con expresión de dolor, etc.)
- Persona que sostenga sensor con texto on-screen que sugiera diagnóstico ("YA TENGO DIABETES")
- Imagery de complicaciones diabéticas (úlceras, amputaciones, retinopatía visible)
- Persona "antes/después" sugiriendo cura o transformación
- Médicos sintéticos con bata blanca que parezcan reales (riesgo de presentación falsa)
- Niños con sensor (QiTrax no está aprobado para uso pediátrico al día de hoy)
- Embarazadas con sensor (regulatorio específico, requiere médico)

### Permitido siempre
- Persona genérica con sensor adherido al brazo SIN texto que sugiera diagnóstico
- Mano sosteniendo el sensor (detalle producto)
- Pantalla del dashboard QiHealth (UI/UX shots)
- Comida y escenas lifestyle (cocina, ejercicio, oficina)
- Imagery emocional anclada (foto warm de familia, retrato introspectivo)
- Datos abstractos (curvas, gráficas, scores en pantalla)

## Estructura del output

```markdown
=== VISUAL PROMPT — [Sub-segmento] [Pieza] ===

**Herramienta recomendada**: [Higgsfield / Nano Banana / Cualquiera]
**Asset destino**: [Reel hook frame / B-roll secuencia X / Carrusel slide N / Static ad / etc.]
**Aspect ratio destino**: [9:16 / 1:1 / 4:5 / 16:9]
**Cantidad de variantes a generar**: [N]

---

## Prompt principal (para pegar directo)

[Prompt en inglés, optimizado para la herramienta — incluyendo subject, style, mood, lighting, framing, negative prompts]

---

## Variaciones del prompt (para batch generation)

### Variant 1 — [eje cambia: lighting]
[Prompt v1]

### Variant 2 — [eje cambia: framing]
[Prompt v2]

### Variant 3 — [eje cambia: subject pose]
[Prompt v3]

[hasta N variants]

---

## Specs adicionales

- **Mood**: [introspectivo / cálido / clínico / educativo]
- **Color palette**: [paleta hex o descriptiva]
- **Casting**: [si aplica — edad, género, expresión sin ser específico]
- **Setting**: [hogar / oficina / clínica / abstracto]
- **Brand presence**: [logo visible / sensor visible / dashboard visible / nada]

---

## COFEPRIS check del prompt

- [ ] Sin persona que sugiera diagnóstico
- [ ] Sin claim médico en imagery
- [ ] Sin imagery de complicaciones
- [ ] Sin médico sintético en bata
- [ ] Sin niños
- [ ] Sin embarazada
- [✓] Validado contra cofepris-rules.md

---

## Output: dónde subir el resultado

Drive folder: `/QiHealth/visuals/[sub-segmento]/[yyyy-mm-dd]/[pieza-nombre]/`

Naming convention: `[pieza-nombre]_[variant-N]_[ratio].png` (ej: `reel-legacy-papa_v01_9x16.png`)

Una vez subido, ejecutar `/qihealth-marketing` con referencia al asset para enlazarlo al brief de la pieza correspondiente.

---

NEXT ACTION: Ejecutar el prompt en [Higgsfield / Nano Banana], descargar las N variantes, subir a Drive folder correspondiente, notificar al orchestrator para enlazar al brief.
```

## Prompt patterns probados por sub-segmento

### No-Measurers — TOF
- **Mood**: revelador, datos, no alarmista
- **Casting**: persona genérica 35-55 años mexicana, expresión reflexiva
- **Setting**: hogar warm o entorno cotidiano
- **Elementos**: mano sosteniendo sensor, glucómetro antiguo en mesa, escena de comida típica mexicana
- **Color**: tonos cálidos, no clínicos fríos

### Legacy — TOF
- **Mood**: introspectivo, family legacy, esperanzador
- **Casting**: persona 35-50 años, profesional, con foto enmarcada del padre/madre cerca
- **Setting**: hogar warm, biblioteca, estudio
- **Elementos**: foto del padre (filtrada o blanco y negro), sensor adherido, mirada introspectiva
- **Color**: tonos cálidos sepia o desaturados con acento dorado

### BGM-Self — MOF
- **Mood**: educativo, descubrimiento, accessible
- **Casting**: persona primerizo-friendly, 30-50 años, mirada curiosa
- **Setting**: cocina, oficina, espacio personal
- **Elementos**: app del dashboard QiHealth en mano, comparativa visual sensor vs glucómetro
- **Color**: balanceado, ligeramente clínico pero accessible

### CGM-Switchers — MOF
- **Mood**: técnico maduro, comparativo honesto, sofisticado
- **Casting**: persona técnicamente alfabetizada, 35-60 años
- **Setting**: oficina/estudio, monitor con dashboard
- **Elementos**: dashboard QiHealth en pantalla grande, sensor en brazo
- **Color**: profesional, contraste alto, branded

### BGM-Doctor (lado paciente) — MOF
- **Mood**: empoderador, preparación de consulta
- **Casting**: paciente 40-65 años, profesional, con bloc de notas o tableta
- **Setting**: sala de espera o consultorio
- **Elementos**: app en mano, dashboard de prepare-for-doctor, lista de preguntas
- **Color**: clínico-cálido, profesional

## Reglas de prompting

### Para Higgsfield (generation)

- Inglés es lo óptimo (modelo entrenado mayoritariamente en EN)
- Especificar **subject + setting + style + lighting + composition + mood** en ese orden
- Incluir **negative prompts** explícitos:
  - `--no needles, no insulin, no medical procedures, no children, no pregnant, no medical professionals in uniform, no before/after`
- Para character consistency, usar **seed reference** del personaje (si Higgsfield Pro/Studio plan)
- Aspect ratio explícito al final del prompt

### Para Nano Banana (editing)

- Empezar con la **imagen base** (foto real o asset existente)
- Describir el cambio específico: "Edit this image to [acción específica]"
- Mantener naturalidad: "preserving the original lighting and skin tones"
- Para format adaptation: "Adapt this image to 9:16 vertical, recompose subject to upper half"
- Negative prompts también aplican

## Output format ejemplo (para Higgsfield Legacy TOF)

```
=== VISUAL PROMPT — Legacy TOF — "Mi papá lo vivió" ===

Herramienta: Higgsfield
Asset destino: B-roll del Reel pilar Legacy
Aspect ratio: 9:16
Variantes a generar: 5

---

## Prompt principal

"Cinematic portrait of a Mexican adult, age 35-50, sitting in a warm-lit home study, looking thoughtfully at an old framed photograph of an elderly parent on the desk. Soft golden hour light coming through window. Slight depth of field, photograph slightly in focus. The person's hand rests near the photograph in a contemplative gesture. Subtle modern aesthetic, warm color grading with sepia tones and gold accents. Cinematic 9:16 vertical composition. --no needles, no medical procedures, no children, no medical uniforms, no before/after comparison, photorealistic, emotional, introspective"

---

## Variant 1 — Lighting change
[same prompt + change "warm-lit" to "cool morning light"]

## Variant 2 — Framing change
[same prompt + "extreme close-up of hands holding the photograph"]

## Variant 3 — Subject change
[same prompt + "woman 40-50 years old"]

## Variant 4 — Setting change
[same prompt + "outdoor garden, golden hour"]

## Variant 5 — Pose change
[same prompt + "person walking past the photograph on a hallway wall"]

---

Specs adicionales:
- Mood: introspectivo + esperanzador
- Color: sepia warm + golden accents
- Casting: mexicano/a 35-50 años, expresión reflexiva
- Setting: hogar warm con elementos personales
- Brand presence: nada (B-roll puro, sin sensor visible en esta secuencia)

---

COFEPRIS check: ✅ PASS — sin claims, sin imagery clínica, sin riesgos

---

Drive folder: /QiHealth/visuals/legacy/2026-05-09/reel-papa-lo-vivio/
Naming: reel-papa-lo-vivio_v01_9x16.png ... reel-papa-lo-vivio_v05_9x16.png

NEXT ACTION: Ejecutar las 5 variantes en Higgsfield (Pro plan), descargar, subir a Drive folder, notificar al orchestrator.
```

## Cuándo escalar al humano

- Prompt que requiera casting muy específico (paciente real, médico real) → filming en lugar de generation
- Prompt que cruce COFEPRIS gray zone → consultar con advisory
- Imagery que requiera retoque preciso de marca (logo + dashboard) → diseñador senior on-call
- Prompt que requiera estilo no-replicable con Higgsfield/Nano Banana → considerar Midjourney o Runway

## Mantenimiento

- **Mensual**: revisión de prompts ganadores (¿qué patterns visuales generaron Reels con mejor CTR/save rate?)
- **Trimestral**: actualización de templates por sub-segmento según learnings
- **Cuando aparezca nueva herramienta visual** (Veo 3, Sora, etc.): evaluación de fit + adición a este builder
