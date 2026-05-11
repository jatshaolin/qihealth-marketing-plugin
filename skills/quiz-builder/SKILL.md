---
name: quiz-builder
description: >
  This skill should be used to build interactive quizzes as lead magnets for QiHealth. Triggers: "quiz", "quiz de riesgo", "¿Estás en riesgo?", "interactive quiz", "quiz para No-Measurers", "scoring quiz", "lead magnet quiz". Produces full quiz structure: questions, answer options, scoring logic, result categories, personalized report, and email follow-up sequence. Output ready for implementation in quiz platform (Typeform, Outgrow, custom).
metadata:
  version: "0.1.0"
  type: "production"
  format: "Interactive quiz"
---

# Quiz Builder

Build interactive quizzes that serve as high-converting lead magnets. Primary use case: quiz "¿Estás en riesgo?" for No-Measurers (target sub-segment 3, sec 4.4 strategy v4.3).

## Mandatory loading

- `memory/strategy-v4.3-summary.md`
- `memory/cofepris-rules.md` (importantísimo — quiz no puede dar diagnóstico)
- `memory/brand-voice.md`

## Estructura estándar

### Component 1 — Hook + intro (landing del quiz)
- Headline: "¿Estás en riesgo metabólico? 5 preguntas, 2 minutos."
- Subheadline: contexto + tiempo estimado + qué obtienes al final
- CTA: "Empieza el quiz" (botón grande)

### Component 2 — Preguntas (5-7 max)
Cada pregunta:
- Pregunta clara en lenguaje cotidiano
- 3-5 opciones de respuesta
- Cada opción con valor de scoring (oculto al usuario)
- Una pregunta por slide (no abrumar)

### Component 3 — Email capture (después de pregunta N-1)
- "Tu reporte personalizado está listo. ¿A dónde te lo enviamos?"
- Email + nombre (mínimo)
- Opcional: WhatsApp para follow-up

### Component 4 — Scoring logic
- Sumar puntos de respuestas
- Categorizar resultado: Bajo / Medio / Alto riesgo (o tiers más granulares)
- **NUNCA decir "tienes diabetes" o "tienes pre-diabetes"** (eso es diagnóstico → COFEPRIS BLOCK)
- SÍ decir "factores de riesgo elevados" o "señales que vale la pena monitorear"

### Component 5 — Reporte personalizado (resultado)
- Tu categoría: [riesgo bajo/medio/alto]
- Qué significa específicamente
- Qué factores te llevaron ahí
- Recomendaciones concretas (NO médicas — lifestyle)
- CTA principal: Insight 15 (entry product) o Plan Legacy según sub-segmento
- CTA secundario: webinar o blog correspondiente

### Component 6 — Email follow-up sequence (5 emails)
- Email 1 (inmediato): reporte completo en PDF
- Email 2 (día 2): "5 cosas que descubrirás con un CGM"
- Email 3 (día 4): testimonial de alguien con resultado similar
- Email 4 (día 7): oferta Insight 15 con timing claro
- Email 5 (día 10): último email antes de mover a nurturing

## Quiz "¿Estás en riesgo?" template (No-Measurers)

### Pregunta 1
"¿Cuál es tu edad?"
- 18-29 (1 punto)
- 30-44 (2 puntos)
- 45-59 (3 puntos)
- 60+ (4 puntos)

### Pregunta 2
"¿Tienes familiar directo con diabetes (padre/madre/hermano)?"
- No (0 puntos)
- Sí, uno (2 puntos)
- Sí, dos o más (4 puntos)

### Pregunta 3
"¿Cuál describe mejor tu peso?"
- Saludable (0)
- Sobrepeso ligero (2)
- Sobrepeso o obesidad (4)

### Pregunta 4
"¿Te has sentido cansado/a sin razón clara, tienes sed inusual, o despiertas más cansado/a últimamente?"
- Nunca (0)
- A veces (2)
- Frecuentemente (4)

### Pregunta 5
"¿Te mides la glucosa actualmente?"
- Sí, con CGM (skip — no aplica, redirect a otro quiz)
- Sí, con glucómetro (1)
- No, nunca (3)

[Email capture aquí]

### Resultados
- 0-6 puntos: Riesgo bajo → "Tu perfil sugiere buenas bases. CGM puede darte info preventiva extra."
- 7-13 puntos: Riesgo medio → "Tienes señales que vale la pena monitorear. Considera CGM 15 días."
- 14+ puntos: Riesgo alto → "Tu perfil sugiere factores de riesgo metabólico elevados. CGM puede revelar patrones importantes. Habla con tu médico."

**NUNCA**: "Tienes pre-diabetes" / "Tienes diabetes" / "Necesitas medicamento"

## Quiz variants por sub-segmento

- **No-Measurers**: "¿Estás en riesgo?" (descrito arriba)
- **Legacy**: "¿Cuál es tu riesgo hereditario de diabetes?"
- **BGM-Self**: "¿Qué tan completa es tu medición de glucosa?"
- **BGM-Doctor (paciente)**: "¿Qué decirle a tu doctor en tu próxima consulta?"

## Output format

Genera:
1. Estructura completa del quiz (questions + options + scoring)
2. Copy de cada resultado (3-5 tiers)
3. Email sequence 5 emails post-quiz
4. CTAs específicos por tier de resultado
5. FAQ del quiz si aplica

## Quality gates

- cofepris-check: NUNCA dar diagnóstico, siempre "factores de riesgo" / "señales"
- brand-voice: tono educativo, no alarmista
- factual-review: scoring respaldado por criterios clínicos conocidos (no inventado)

## Cuándo escalar al humano

- Scoring logic con implicación clínica → advisory médico
- Resultado "alto riesgo" puede ser detonante regulatorio si parece diagnóstico → cofepris-check
- Email sequence con claims clínicos → factual-review + advisory
- Decisión de pricing del CTA en resultado → Jose
