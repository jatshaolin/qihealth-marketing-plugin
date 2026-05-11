---
name: carousel-builder
description: >
  This skill should be used when the user asks for an Instagram carousel for QiHealth. Triggers: "carrusel", "carousel IG", "post de slides", "5 slides", "8 slides", "10 slides", "necesito un carrusel para [sub-segmento]", "carrusel educativo", "carrusel comparativo". Produces full carousel copy slide by slide with visual direction, headline, body text, and visual hierarchy guidance.
metadata:
  version: "0.1.0"
  type: "production"
  formats: ["Instagram Carousel", "LinkedIn Carousel"]
---

# Carousel Builder — Instagram Carousels

You produce ready-to-design carousel posts for Instagram (and LinkedIn when relevant). Carousels for QiHealth are educational and high-save-rate by design — they prioritize utility per slide over aesthetic flourish.

## Mandatory loading

Before producing, read:
- `memory/strategy-v4.3-summary.md`
- `memory/brand-voice.md` — voice rules + structure rules
- `memory/cofepris-rules.md`
- `memory/ad-references.md` — proven references
- The persona skill of target sub-segment

## Why carousels work for QiHealth

- **High save rate** = algorithm boost. People save educational carousels to reread. Save rate >3% = winner.
- **Slow consumption** = depth permitido que un Reel no permite. Puedes meter 5-7 ideas reales.
- **Shareable** by topic ("voy a compartir esto con mi mamá").
- **Re-purposable**: cada slide puede convertirse en short Reel o pieza standalone.

## Estructura estándar (5-10 slides)

### Slide 1 — Hook visual + headline

- **Headline (3-7 palabras grandes)**: el dato/pregunta/promesa que detiene scroll
- **Visual**: simple, alto contraste, un solo elemento focal
- **Subheadline opcional**: 1 línea de contexto

Ejemplo (Legacy):
- Slide 1 headline: "50% genética. 50% lo decides tú."
- Visual: ilustración minimalista de DNA dividido a la mitad
- Subhead: "Lo que dice la ciencia sobre tu riesgo de diabetes."

### Slides 2-7 — Contenido (1 idea por slide)

Reglas:
- **1 sola idea por slide**. Si no cabe una idea en 1 slide, dividirla.
- **Headline + 2-4 líneas de body** máximo
- **Visual de soporte**: gráfica simple, ilustración, dato grande, captura de dashboard
- **Mantener tipografía consistente** entre slides
- **Numeración o iconos** para guiar el flujo

Tipos de slides intermedios:

**Tipo A — Dato con contexto**:
- Slide 2: "[Dato grande]"
- Body: 2-3 líneas explicando contexto + fuente

**Tipo B — Pregunta-respuesta**:
- Slide 3: "[Pregunta común]"
- Body: respuesta breve

**Tipo C — Mito vs realidad**:
- Slide 4: "Mito: [creencia común]"
- Slide 5: "Realidad: [evidencia]"

**Tipo D — Lista (si es lista)**:
- Slide N: "Causa #1: [...]"
- Slide N+1: "Causa #2: [...]"
- (no toda lista funciona; si son <5 items, mejor un solo slide; si son >7, dividir en posts)

**Tipo E — Comparativa visual**:
- Tabla 2 columnas (ej: "Glucómetro vs CGM con IA")
- 4-5 filas máximo

### Slides 8-9 — Síntesis o cierre

- **Slide de cierre conceptual**: "Lo que esto significa para ti"
- O **slide de "qué hacer ahora"**: paso accionable

### Slide final — CTA + brand

- **CTA explícito**: "Toma el quiz", "Lee el blog", "Empieza con 15 días"
- **Logo QiHealth + handle**
- **Hashtags principales** (también van en caption)

## Specs técnicos

### Instagram Carousel
- **Aspect ratio**: 1:1 (1080x1080) o 4:5 (1080x1350) — 4:5 ocupa más feed real estate
- **Slides**: 2-10 (sweet spot 7-9 para educativo)
- **File**: PNG o JPEG cada slide

### LinkedIn Carousel (cuando aplique para BGM-Doctor)
- **Aspect ratio**: 1:1 o 4:5
- **PDF multi-página** (LinkedIn document upload)
- **Slides**: 5-12

## Output format

```markdown
# CAROUSEL — [Sub-segmento] [Etapa] — [Tema]

**Brief**: [resumen 1 línea]
**Sub-segmento**: [...]
**Etapa funnel**: [...]
**Slides totales**: [N]
**Plataforma**: Instagram (1:1 o 4:5) / LinkedIn

---

## Slide 1 — Hook visual + headline

**Headline (grande)**: "[texto]"
**Subheadline (si aplica)**: "[texto]"
**Visual direction**: [descripción simple]
**Color/mood**: [neutro clínico / cálido / urgente]

---

## Slide 2 — [tipo: dato / pregunta / mito / etc.]

**Headline**: "[texto]"
**Body (2-4 líneas)**: 
"[texto]"
**Visual direction**: [descripción]
**Source citada**: [si aplica]

---

## Slide 3 — [tipo]

[mismo formato]

---

[... slides 4-N ...]

---

## Slide final — CTA + brand

**Headline**: "[CTA específico, ej: "Empieza con 15 días"]"
**Subheadline**: "[contexto del CTA]"
**Visual**: Logo QiHealth + handle @qihealth
**Hashtags principales**: #...

---

## Caption sugerida (para feed)

[caption + hashtags + posibles preguntas para invitar comments]

---

## Variantes de hook (Slide 1) para A/B test

1. "[hook A]"
2. "[hook B]"
3. "[hook C]"

---

## Quality gates pendientes
- [ ] cofepris-check
- [ ] brand-voice-qihealth
- [ ] factual-review

STATUS: CAROUSEL-DRAFT — pasa a quality gates
NEXT ACTION: Run cofepris-check
```

## Templates por sub-segmento

### No-Measurers — "5 señales silenciosas de pre-diabetes"

- Slide 1: Hook "5 señales silenciosas que tu cuerpo te está dando"
- Slides 2-6: 1 señal por slide (energía vespertina baja, sed aumentada, despertares nocturnos, hambre 2h después de comer, antojos repetitivos)
- Slide 7: "1 de cada 3 mexicanos las ignora"
- Slide 8: "Conoce tu metabolismo en 15 días"
- Slide 9: CTA + brand

### Legacy — "Lo que tu papá no pudo medir, tú sí"

- Slide 1: Hook "Lo que tu papá no pudo medir, tú sí."
- Slide 2: "En 1990, su única opción era el piquete."
- Slide 3: "Hoy hay tecnología continua, IA y prevención real."
- Slide 4: "El 50% es genética. El otro 50% lo decides tú."
- Slide 5: Datos clínicos sobre prevención DM2
- Slide 6: Cómo funciona QiTrax
- Slide 7: Plan Legacy + bundle familiar
- Slide 8: CTA + brand

### BGM-Self — "5 cosas que tu glucómetro NO te dice"

- Slide 1: Hook "5 cosas que tu glucómetro NO te dice"
- Slides 2-6: una limitación por slide (picos nocturnos, dawn phenomenon, respuesta postprandial completa, correlación con sueño, tendencias de 14 días)
- Slide 7: "El glucómetro te da una foto. El CGM te da la película."
- Slide 8: "Tu primer CGM con guía: bundle Primer mes"
- Slide 9: CTA + brand

### CGM-Switchers — "QiTrax vs FreeStyle Libre: comparativa honesta"

- Slide 1: Hook "QiTrax vs FreeStyle Libre. Comparativa honesta."
- Slide 2: "En sensor, son 95% iguales."
- Slide 3: Tabla "Sensor: ambos OK"
- Slide 4: "Donde difieren: ecosistema de inteligencia"
- Slide 5: Tabla "Coaching de IA: QiHealth ✓ / Abbott ✗"
- Slide 6: Tabla "Multi-biométrico: QiHealth ✓ / Abbott ✗"
- Slide 7: "Mismo precio. Más contexto."
- Slide 8: "Cambia sin perder tu historial — 30 días de garantía"
- Slide 9: CTA + brand

### BGM-Doctor (lado paciente) — "5 cosas que decirle a tu doctor"

- Slide 1: Hook "5 cosas que decirle a tu doctor en tu próxima consulta sobre glucosa"
- Slides 2-6: 1 cosa por slide (síntomas que has notado, antecedentes familiares, hábitos, querer probar CGM, opciones disponibles)
- Slide 7: "Tu doctor agradece pacientes que llegan con datos"
- Slide 8: "Descarga el material para llevar a tu consulta"
- Slide 9: CTA + brand

## Reglas de density

- **Texto por slide**: máximo 25-35 palabras (incluyendo headline + body)
- **Slides totales**: 5-10 (más de 10 pierde retention; menos de 5 no justifica formato)
- **Líneas por body**: máximo 4
- **Hashtags en caption**: 5-10 (no en slide)

## Iteración con feedback

Si el usuario pide ajuste de un carrusel existente:
- "Hazlo más visual" → reducir texto, aumentar visual direction
- "Está muy denso" → dividir slides con +35 palabras
- "Falta CTA fuerte" → reescribir slide final + agregar CTA contextual mid-carousel
- "Cambia el ángulo" → regenerar slides 2-6 manteniendo slide 1 hook + slide final CTA
