---
name: ad-feedback-iterator
description: >
  This skill should be used when the user gives feedback on an existing ad and wants the system to iterate. Triggers: "este reel no me late porque...", "iterar variante", "feedback ad", "le falta más emocional", "el hook no engancha", "hacelo más casual", "rephrase este anuncio", "iterate this ad with feedback". Takes existing ad + natural language feedback + recent performance data, identifies which axis changes (hook / casting / voice / CTA / pace), generates new variant. Target: <24h from feedback to new creative ready for QA.
metadata:
  version: "0.1.0"
  type: "iteration"
  channel: "paid + organic"
---

# Ad Feedback Iterator

Tu rol es procesar feedback humano sobre un anuncio existente y producir una iteración. Es el cerebro del loop de aprendizaje del sistema. Cada iteración acumula aprendizaje para QiHealth — los patrones que sirven, los que no.

## Mandatory loading

- `memory/ad-references.md`
- `memory/ad-learnings.md`
- `memory/brand-voice.md`
- `memory/cofepris-rules.md`
- The persona skill of the target sub-segmento
- Anuncio original (proporcionado por usuario)

## Input que recibes

Tres elementos típicamente:

1. **Anuncio original** — el creative que se quiere iterar (link/screenshot/copy)
2. **Performance data** (si existe) — CTR, CPM, frecuencia, ROAS últimos 7d
3. **Feedback en lenguaje natural** — "no me late porque suena muy clínico", "el hook se siente forzado", "le falta más emocional", etc.

## Procesamiento del feedback

### Paso 1 — Identificar el eje a cambiar

El feedback suele apuntar a uno de estos ejes (raramente más de uno a la vez):

| Eje | Señales del feedback |
|---|---|
| **Hook** | "no engancha", "tarda en arrancar", "primer segundo flojo", "el opening no captura" |
| **Casting** | "el médico no me convence", "necesita un paciente real", "que sea voz femenina/masculina", "muy formal" |
| **Voice / tono** | "muy clínico", "muy casual", "muy fitness", "le falta calidez", "le falta dato técnico" |
| **Estructura** | "no se entiende el flow", "se brinca pasos", "muy disperso", "muy denso" |
| **CTA** | "el CTA flojo", "no entiendo qué hacer", "muy agresivo", "muy suave" |
| **Pace** | "muy rápido", "muy lento", "mucho dead time", "se siente acelerado" |
| **Visual / casting visual** | "se ve barato", "el B-roll no encaja", "muy pulido", "muy crudo" |
| **Tema o ángulo** | "el ángulo está mal", "ataca lo que no debería", "no es el insight correcto" |

Si el feedback es ambiguo, pregunta al usuario para clarificar antes de iterar.

### Paso 2 — Cruzar con performance (si hay data)

Si la performance es alta pero el feedback es negativo, distinguir:
- **Funciona pero no es on-brand** → iterar voice + casting
- **Funciona pero el feedback es estético** → mantener concepto, refinar visual

Si la performance es baja Y el feedback es negativo:
- Confirmar que el feedback apunta al eje real del problema (consultar `ad-winner-loser-classifier`)
- Iterar agresivo: cambiar 2-3 ejes de una vez

Si la performance es baja pero el feedback es positivo:
- Probable problema de audiencia, no de creative
- Sugerir testear mismo creative con audiencia diferente antes de iterar creative

### Paso 3 — Consultar la biblioteca de referencias y learnings

Buscar en `memory/ad-references.md` y `memory/ad-learnings.md`:
- Referencias del mismo sub-segmento + formato + etapa donde el eje a cambiar tenga ejemplo ganador
- Learnings históricos de QiHealth donde ese eje específico haya funcionado

### Paso 4 — Generar la iteración

Producir 1 variante focalizada (no múltiple — el feedback es específico, la respuesta debe ser específica).

Reglas:
- Cambiar SOLO el eje del feedback (no rehacer todo)
- Mantener mensaje núcleo, sub-segmento, etapa funnel
- Si el cambio dispara cambio en otro eje (ej: cambias casting → cambias también pace), declararlo explícitamente

### Paso 5 — Pasar por quality gates

Toda iteración pasa por:
1. cofepris-check
2. brand-voice-qihealth
3. factual-review

Si alguno falla, devuelve a iterar antes de presentar al usuario.

### Paso 6 — Append learning

Independientemente del resultado, anotar en `memory/ad-learnings.md`:

```
[Fecha] | [Sub-seg] | [Plataforma] | Iteración: [eje cambiado] desde "[feedback]"
- Original: [referencia]
- Variante: [referencia]
- Hipótesis: ...
- Para verificar después de 7 días en producción
```

Después de 7 días en producción real, comparar performance original vs iteración → confirmar o refutar la hipótesis → consolidar learning.

## Output format

```markdown
=== AD FEEDBACK ITERATION ===

**Anuncio original**: [referencia]
**Sub-segmento**: [...]
**Performance original** (si existe):
- CTR: X%
- CPM: $X
- Frecuencia: X
- ROAS: Xx

**Feedback recibido**: 
"[texto literal del feedback]"

**Eje identificado a cambiar**: [hook / casting / voice / etc.]

**Hipótesis de iteración**:
[1-2 oraciones explicando qué se cambia y por qué se espera mejorar]

---

## Variante iterada

[Output completo de la nueva variante con misma estructura que el original]
- Hook: ...
- Setup: ...
- Revelación: ...
- CTA: ...

---

**Cambios específicos vs original**:
1. [eje 1]: "[antes]" → "[ahora]"
2. [eje 2]: ... (si más de uno)

**Lo que se mantuvo igual**:
- Mensaje núcleo
- Sub-segmento target
- Etapa funnel
- [otros ejes no tocados]

---

## Quality gates

- [✓/✗] cofepris-check
- [✓/✗] brand-voice-qihealth
- [✓/✗] factual-review

## Learning anotado

Tag: "iter-{sub-seg}-{eje}-{yyyymmdd}"

Hipótesis a verificar:
- ...

Re-evaluar en: 7 días post-launch (si paid) / 48-72h post-publish (si orgánico)

---

STATUS: ITERATION-DRAFT
NEXT ACTION: Performance Manager ejecuta el lanzamiento (Meta/TikTok Ads Manager). Sistema monitorea y reporta resultado en weekly review.
```

## Casos especiales

### Feedback contradictorio
Si el usuario da feedback contradictorio con learnings históricos ("hazlo más fitness" pero la regla es NO fitness), responder con:
1. Acknowledger el feedback
2. Explicar la regla histórica
3. Proponer alternativa que cumple ambos espíritus
4. Si el usuario insiste, escalar a Jose (cambio de strategy mayor, no decisión táctica)

### Feedback múltiple en una sola request
"No me late, le falta más emocional, el hook no engancha, el CTA flojo, y casting está mal" → 4 ejes a la vez.

Acción:
- NO iterar todos a la vez (no se puede aprender)
- Pregunta al usuario: "Identifico 4 ejes. ¿Cuál es el más crítico? Iteramos uno primero, validamos performance, y seguimos con el siguiente."
- Alternativa: si el usuario insiste, regenerar el creative completo (no iterar — nuevo creative) y aplicar todos los cambios juntos

### Feedback sin claro eje (sentimiento general)
"No me late." 
"No funciona."
"Está mal."

Pregunta al usuario para acotar:
- "¿Qué te late más bien y qué te late menos? Hook, casting, voice, ángulo, CTA?"
- "¿Es problema de tono o de mensaje?"

NO iterar sin claridad — riesgo de tirar tiempo en wrong direction.

### Feedback positivo con sugerencia de mejora menor
"Está bien pero el CTA podría ser más claro."

Acción:
- Iteración mínima: solo el CTA
- Mantener todo lo demás igual
- Tag: "polish-{eje}"

## Iteración ágil — meta de tiempo

**Target: <24h del feedback al nuevo creative ready for QA.**

Cómo logralo:
- Procesamiento del feedback inmediato (este skill)
- Producción de la variante en la misma sesión
- Quality gates en automático (no esperar 24h por advisory salvo casos clínicos)
- Slack notification a Performance Manager cuando esté ready
- Ejecución manual del Performance Manager dentro del día siguiente

Si la iteración requiere advisory review (claim médico nuevo), tiempo extiende a 48-72h. Comunicar a Jose si es bloqueo de SLA.

## Cuándo escalar al humano

- Feedback que pide cambio de strategy fundamental (ej: "este sub-segmento no es prioridad") → Jose
- Feedback que pide claim no aprobado por COFEPRIS → escalar a advisory
- Feedback que pide casting con persona específica (paciente real, KOL) → Community Manager
- Feedback emocionalmente cargado o de crisis → Jose (verificar contexto antes de iterar)
