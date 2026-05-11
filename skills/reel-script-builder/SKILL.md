---
name: reel-script-builder
description: >
  This skill should be used when the user asks for a script of a TikTok Reel or Instagram Reel for QiHealth. Triggers: "guion de reel", "script reel", "reel para TikTok", "reel para IG", "video corto", "necesito un reel", "make a Reel for [sub-segmento]", "video de 30 segundos", "video de 60 segundos", "reel pilar", "reel de comparación". Produces full script with timestamps, hooks, B-roll suggestions, on-screen text, captions, and 3 hook variants for A/B testing.
metadata:
  version: "0.1.0"
  type: "production"
  formats: ["TikTok", "Instagram Reels"]
---

# Reel Script Builder — TikTok + Instagram

You produce ready-to-shoot scripts for short-form vertical video (9:16) optimized for TikTok and Instagram Reels. Each script includes timestamps, dialogue or VO, B-roll suggestions, on-screen text, music suggestions, and 3 hook variants for testing.

## Mandatory loading

Before producing, read:
- `memory/strategy-v4.3-summary.md` — sub-segment messaging
- `memory/brand-voice.md` — voice rules + hook templates
- `memory/cofepris-rules.md` — claims to avoid
- `memory/ad-references.md` — proven references for similar pieces
- `memory/ad-learnings.md` — what has worked before
- The persona skill of the target sub-segment

## Input expected

- Sub-segmento (CGM-Switchers / BGM-Self / BGM-Doctor / No-Measurers / Legacy)
- Etapa funnel (TOF / MOF / BOF)
- Duración objetivo (30s default, options 15s / 60s)
- Plataforma primaria (TikTok / IG / both)
- Mensaje núcleo o tema (puede ser explícito o derivado de la matriz)
- Casting disponible (voiceover anónimo / médico / paciente real / generated B-roll only)
- CTA específico (si existe; si no, derivarlo del sub-segmento)

## Script structure (30-60 second Reel)

### Section 1 — Hook (0-3 seconds)

**Critical**. The 3 first seconds determine retention. Algorithms (TikTok especially) decide reach in the first second.

Generate **3 hook variants** for A/B testing:

- Variant A: **Pregunta directa** (e.g., "¿Sabes que 1 de cada 3 mexicanos tiene pre-diabetes y no lo sabe?")
- Variant B: **Estadística punzante** (e.g., "14 millones de mexicanos. ¿Y tú?")
- Variant C: **Anclaje personal o emocional** (e.g., "Mi papá vivió la diabetes. Yo no voy a vivirla.")

For each variant:
- Specify on-screen text (large, high-contrast)
- Specify VO or speaker pace (energético / introspectivo / clínico)
- Verify against `cofepris-rules.md` (especially BLOCK list)

### Section 2 — Setup del problema (3-10 seconds)

Establecer el problema o contexto. Por sub-segmento:

- **No-Measurers**: revelar el dato/situación que crea la duda
- **Legacy**: anclar la memoria familiar o la urgencia generacional
- **BGM-Self**: mostrar la limitación del glucómetro/piquete
- **CGM-Switchers**: mostrar el gap entre "tu CGM actual" y "lo que falta"
- **BGM-Doctor (paciente)**: mostrar la frustración del médico con datos parciales

Output: 1-2 oraciones de setup con visual support.

### Section 3 — Revelación / Explicación (10-30 seconds)

El core del Reel. Aquí es donde la pieza entrega valor real:

- Mostrar el contraste (glucómetro vs CGM, sensor solo vs ecosistema, etc.)
- Mostrar dato concreto (curva de glucosa, dashboard, captura de app)
- Si aplica, voz médica del advisory ("esto es lo que veo cuando un paciente usa CGM con IA...")

Visual: B-roll de uso del producto, capturas de pantalla del dashboard, grabación de doctor (si aplica), animaciones explicativas.

### Section 4 — Producto / CTA (30-50 seconds)

CTA explícito o implícito según etapa funnel:

- **TOF**: CTA suave ("sigue para más", "comenta para info")
- **MOF**: CTA medio ("inscríbete al webinar", "lee el blog completo")
- **BOF**: CTA directo ("empieza con 15 días", "agenda demo", "Plan Legacy aquí")

Texto en pantalla del CTA. Si la plataforma es Reels IG, considerar swipe-up o link en bio.

### Section 5 — Call to comments / saves (50-60 seconds o último segundo)

Cierre que invita a engagement:

- "Comenta '15' y te mando info"
- "Guarda este video para enseñárselo a tu papá"
- "Etiqueta a alguien que necesite ver esto"
- "Sigue para más como este"

Esto sube engagement signal del algoritmo y mejora reach orgánico.

## Specs técnicos por plataforma

### TikTok

- Aspect ratio: 9:16
- Duration: 15s, 30s, 60s, hasta 3 min (sweet spot 30-45s para healthtech educativo)
- Audio: usar trending sounds del momento si aplica al tono (verificar trends antes de elegir)
- Captions: TikTok auto-captions OK, pero validar tipografía y contraste
- Hashtags: #diabetes #salud #cgm #prevención + 2-3 nicho (#hijosdediabéticos #prediabetes #monitoreoglucosa)
- Avoid: emojis excesivos, watermarks de otras plataformas, tono "fitness influencer"

### Instagram Reels

- Aspect ratio: 9:16
- Duration: 15s-90s (sweet spot 30-60s para QiHealth)
- Audio: música original del Reel (carga propia) o trending audio de IG (separado de TikTok)
- Captions: Reels permite captions más densas en descripción (1-3 párrafos OK)
- Hashtags: 5-10 mezclados (3 de marca, 3 de categoría, 4 de nicho)
- Cross-post a Stories y feed cuando convenga

### Adaptaciones cuando se usa para ambos

- Producir master en 9:16 con texto seguro fuera de safe zones de ambas plataformas
- Subtítulos quemados (no solo auto-captions) para que se vea en feed con audio off
- Versión TikTok puede ser 5-10s más corta que IG (TikTok tolera mejor brevity)
- Hashtags y caption diferentes por plataforma (no copy-paste)

## Output format

```markdown
# REEL SCRIPT — [Sub-segmento] [Etapa] — [Tema corto]

**Brief**: [link Notion o resumen 1 línea]
**Sub-segmento**: [...]
**Etapa funnel**: [...]
**Duración objetivo**: [...]
**Plataforma primaria**: [...]

---

## Hook variants (3 — para A/B test)

### Variant A — [tipo: pregunta directa / estadística / personal]
**On-screen text**: "[texto]"
**VO/speaker**: "[texto]"
**Pace**: [energético / introspectivo / clínico]

### Variant B — [tipo]
...

### Variant C — [tipo]
...

---

## Script completo (asumiendo Hook A — para variantes alternar primer segmento)

### 0:00-0:03 — Hook
**On-screen**: "[texto]"
**VO**: "[texto]"
**B-roll**: [descripción del visual]

### 0:03-0:10 — Setup
**On-screen**: "[texto si aplica]"
**VO/dialogue**: "[texto]"
**B-roll**: [descripción]

### 0:10-0:30 — Revelación
**On-screen**: "[texto si aplica]"
**VO/dialogue**: "[texto]"
**B-roll**: [descripción incluyendo capturas de dashboard, gráficas, etc.]

### 0:30-0:50 — Producto + CTA
**On-screen**: "[texto del CTA]"
**VO/dialogue**: "[texto]"
**B-roll**: [descripción]

### 0:50-0:60 — Call to comments
**On-screen**: "[texto]"
**VO/dialogue**: "[texto]"

---

## Variantes de CTA (3 — para A/B test)

1. "[CTA opción A]"
2. "[CTA opción B]"
3. "[CTA opción C]"

---

## Caption sugerida

### Para TikTok
[Caption con hashtags]

### Para Instagram Reels
[Caption + hashtags]

---

## B-roll requirements

- [lista de shots necesarios para producción]
- [si aplica filming real con médico/paciente: agendar via Calendar MCP]
- [si aplica B-roll generado: prompt para Higgsfield/Canva]

---

## Music / sound

- TikTok: [trending audio sugerido + link, si aplica]
- IG: [original audio o IG audio sugerido]
- Mood: [energético / contemplativo / urgente / esperanzador]

---

## Quality gates pendientes
- [ ] cofepris-check
- [ ] brand-voice-qihealth
- [ ] factual-review
- [ ] (si aplica) advisory medical review

---

STATUS: SCRIPT-DRAFT — pasa a quality gates antes de filming
NEXT ACTION: Run cofepris-check on this draft
```

## Hook templates por sub-segmento (referencia rápida)

### No-Measurers
- "[Estadística punzante en México]. ¿Y tú?"
- "Antes de [acción reactiva], [acción preventiva]."
- "5 señales silenciosas que [solemos ignorar]."

### Legacy
- "[Padre/Madre] lo vivió. [Tú no tienes / No vas a tener] que vivirlo."
- "Mi [padre/madre] [acción específica]. Yo decidí [acción preventiva]."
- "El [50%] es genética. El otro [50%] lo decides tú."

### BGM-Self
- "Tu glucómetro te miente. No por mala fe — por física."
- "Si te midieras solo aquí, dirías que estás bien."
- "Esto pasó después de comer tortillas. Y mi médico no lo había visto."

### CGM-Switchers
- "Tu sensor te dice qué pasó. ¿Y por qué?"
- "Mismo precio, más datos. Te muestro la diferencia."
- "Si tu CGM no te dice esto, le falta una capa."

### BGM-Doctor (paciente)
- "Tu doctor ya no necesita adivinar entre consultas."
- "Lo que tu médico ve con CGM que con un piquete no puede."
- "Pídele a tu doctor que conozca esto."

## Cuando hacer Doctor Reel (filming real)

Si el sub-segmento + etapa requieren voz de autoridad clínica, recomendar Doctor Reel en lugar de Reel genérico:

- BGM-Doctor TOF/MOF (lado paciente y lado médico)
- Legacy MOF (anti-fatalismo)
- No-Measurers MOF (¿por qué monitorear si no tengo diabetes?)
- CGM-Switchers MOF (validación clínica del switch)

En esos casos, output del builder es un Doctor Reel brief (no un script completo), y la pieza pasa al skill `doctor-reel-brief`.

## Iteración con feedback

Si el usuario pide variante de un Reel existente con feedback ("este me late pero falta más emocional", "el hook no engancha"):

1. Cargar el Reel original + feedback
2. Identificar el eje que cambia (hook / casting / voice / CTA / pace)
3. Producir nueva versión solo cambiando ese eje (no regenerar todo)
4. Agregar al final del output una línea: "Eje modificado: [...]" para trazabilidad
5. Guardar iteración en `memory/ad-learnings.md` para acumulación
