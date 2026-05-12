---
name: doctor-reel-brief
description: >
  This skill should be used when the user asks for a Doctor Reel brief for filming. Triggers: "doctor reel", "brief para filming", "guion para médico", "Doctor Reel brief", "filming with [médico]", "advisory reel", "necesito brief para grabar con doctor", "reel con vocero clínico". Produces ready-to-film brief with question, medical angle, talking points, B-roll requirements, distribution plan cross-platform, and consent verification checklist. Output goes to filming partner + Calendar booking via MCP.
metadata:
  version: "0.1.0"
  type: "production"
  format: "Doctor Reel (filming real, no AI)"
---

# Doctor Reel Brief Builder

You produce film-ready briefs for Doctor Reels — videos with real medical voices from QiHealth's advisory or partner KOLs. Doctor Reels are HIGH-VALUE content for QiHealth: they activate E-E-A-T for SEO, build trust for BGM-Doctor sub-segment, and serve cross-segment as authority anchors.

**Critical rule**: Doctor Reels are ALWAYS filming real, never AI-synthetic. Synthetic médico in white coat = COFEPRIS risk + brand damage.

## Mandatory loading

- `memory/strategy-v4.3-summary.md`
- `memory/brand-voice.md`
- `memory/cofepris-rules.md`
- `memory/cofepris-claim-library.md` (claims pre-aprobados)
- `memory/competitors.md` (cuando aplique comparativa)

## Inputs que necesitas

Antes de generar brief, identificar:

1. **Sub-segmento target** (puede ser cross-segment también)
2. **Etapa funnel** (TOF/MOF/BOF)
3. **Médico** (¿advisory propio? ¿KOL externo? ¿especialidad?)
4. **Pregunta o tema clínico** (puede ser tema general "¿por qué CGM si no tengo diabetes?" o respuesta a tendencia)
5. **Distribución prevista** (Instagram Reels + TikTok? LinkedIn para HCP? Blog gemelo SEO?)

Si falta info crítica, preguntar al usuario antes de generar brief.

## Estructura del brief

```markdown
# DOCTOR REEL BRIEF — [Tema] con [Médico]

**Médico**: [Nombre completo + especialidad + cédula profesional]
**Sub-segmento target**: [...]
**Etapa funnel**: [TOF/MOF/BOF]
**Distribución**: [IG Reels + TikTok / LinkedIn HCP / Cross-segment / Blog gemelo]
**Duración objetivo**: [30s / 60s / 90s — sweet spot 45-60s]
**Fecha de filming sugerida**: [propuesta vía Calendar MCP]

---

## 1. La pregunta o trigger

[Pregunta literal que abre el Reel, en lenguaje del paciente o del público objetivo. Ejemplo: "¿Por qué monitorear glucosa si no tengo diabetes?"]

---

## 2. Ángulo del médico

[Cómo el médico aborda la pregunta — ángulo clínico claro. 1-2 oraciones.]

Ejemplo: "El monitoreo continuo permite detectar respuestas metabólicas individuales que ningún glucómetro puntual captura. Para pacientes con factores de riesgo (sobrepeso, antecedentes familiares, sedentarismo) sin diagnóstico formal, esa información puede modificar conductas antes de que aparezca pre-diabetes."

---

## 3. Talking points (3-5 puntos clave)

Estructura para 45-60s de video:

1. **Hook** (3-5s): la pregunta del paciente + reacción del médico
2. **Setup clínico** (5-10s): contexto médico de la pregunta
3. **Punto principal** (15-25s): la respuesta clínica con dato o ejemplo
4. **Implicación práctica** (5-10s): qué significa para el paciente
5. **Cierre + CTA** (5-10s): invitación a próximo paso

Cada talking point con bullets concretos de qué decir, no parafrasear. El médico decide tono pero los puntos clave los preparas tú.

---

## 4. Claims clínicos a usar (todos pre-aprobados)

[Lista de claims específicos que el médico puede usar, todos cruzados contra `cofepris-claim-library.md`]

Ejemplo:
- "El monitoreo continuo de glucosa permite identificar respuestas metabólicas individuales" (claim funcional CGM)
- "Estudios muestran que la pre-diabetes afecta a 1 de cada 3 adultos mexicanos sin diagnóstico" (ENSANUT 2024)
- "La detección temprana de patrones de glucosa puede informar decisiones de estilo de vida" (lenguaje suave, no claim de cura)

---

## 5. Claims a EVITAR (por COFEPRIS)

[Lista específica de qué NO debe decir el médico, derivado de `cofepris-rules.md`]

Ejemplo:
- "Cura tu pre-diabetes" → BLOCK
- "Reemplaza tu medicamento" → BLOCK
- "Diagnóstico temprano" → BLOCK (es wellness, no diagnóstico)
- "Garantiza prevención" → BLOCK

---

## 6. B-roll requirements

Listado de shots adicionales necesarios para edit final:

- Detalle del sensor QiTrax en brazo (si aplica)
- Dashboard QiHealth en pantalla (mostrando curva relevante al tema)
- Mano del paciente sobre el sensor (sin claim clínico)
- Detalle de consultorio (libros, certificados — credibilidad sin nombrar pacientes reales)
- Cierre con logo QiHealth + handle social

**Nota importante**: NUNCA filmar paciente real con sensor sin consentimiento firmado explícito.

---

## 7. Casting tonal

- **Tono**: profesional pero cálido. NO académico distante, NO marketing fluff.
- **Pace**: medio, permite procesamiento de info clínica
- **Vestimenta**: profesional (bata opcional, pero NO obligatoria — más natural sin bata según contexto)
- **Setting**: consultorio o backdrop neutral profesional, NO blanco corporativo estéril
- **Vocabulary**: técnico pero traducido. Si dice "respuesta postprandial", inmediatamente "lo que pasa después de comer".

---

## 8. CTAs por distribución

Diferente CTA según canal:

- **Instagram Reels (público general)**: "Sigue para más como este. Comenta tus preguntas."
- **TikTok (público general)**: "Comenta 'CGM' y te mando info."
- **LinkedIn (HCP audience)**: "Agenda demo del dashboard: 30 min."
- **Blog gemelo SEO**: "Lee el artículo completo: [link]"

---

## 9. Filming logistics

**Productora sugerida**: [nombre + contacto si está confirmada, o "pending — contratar"]
**Locación sugerida**: [consultorio del médico, locación neutral, o set arrendado]
**Duración de sesión filming**: 2-3 horas (incluye múltiples takes + B-roll + setup)
**Equipo requerido**: cámara 4K, mic lavalier, lighting de consultorio
**Calendar booking**: agendar slot con el médico via Calendar MCP. Confirmar 48h antes.

---

## 10. Consent verification checklist

- [ ] Médico firmó autorización de uso de imagen (formato QiHealth)
- [ ] Médico verificó cédula profesional y especialidad declarada
- [ ] No hay conflicto de intereses con competidores (Abbott, Sibionics, etc.)
- [ ] Médico aceptó claims clínicos del brief
- [ ] Médico aceptó distribución cross-platform
- [ ] Si filma en consultorio: consentimiento de practitioner del lugar
- [ ] Si aparecen pacientes (NO recomendado): consentimientos separados firmados

---

## 11. Post-prod plan

Después del filming:

1. Footage sube a Drive: `/QiHealth/filming/doctor-reels/[yyyy-mm-dd]-[medico]/`
2. Selección de takes ganadores
3. Edit principal (versión Master 60s)
4. Adaptaciones:
   - IG Reels 9:16 (60s)
   - TikTok 9:16 (30s edit + 60s edit)
   - LinkedIn 16:9 (90s extendido si es HCP audience)
   - Blog gemelo embed (master cualquiera)
5. Subtítulos quemados en todas las versiones
6. Quality gates:
   - cofepris-check final con video subtitulado
   - brand-voice-qihealth
   - advisory firma final
7. Drive folder con todas las versiones listas para publish
8. ClickUp task creada con subtasks por canal

---

## 12. Blog gemelo SEO (si aplica)

[Si la pregunta del Reel tiene volumen de búsqueda, generar también brief de blog gemelo con misma respuesta médica + más profundidad. Multiplica ROI del filming.]

Keyword principal: [keyword]
Long-tail variants: [...]
Word count objetivo: 1,200-2,000 palabras
Autor firma: [mismo médico]

---

STATUS: BRIEF READY FOR FILMING
NEXT ACTION: 
1. Confirmar slot de filming via Calendar MCP con [médico]
2. Compartir brief con productora externa para preparación
3. Verificar consentimientos firmados antes del día de filming
4. Filming day → footage a Drive → post-prod
```

## Templates de tema por sub-segmento

### No-Measurers TOF
- "¿Por qué monitorear glucosa si no tengo diabetes?"
- "¿Cuáles son las señales tempranas de pre-diabetes que ignoramos?"
- "¿En qué momento debería empezar a medir mi glucosa preventivamente?"

### Legacy MOF
- "¿Qué tan hereditaria es la diabetes tipo 2?"
- "¿Desde qué edad debería medirme si mis padres tienen DM2?"
- "¿Puedo prevenir la diabetes si mi familia la tiene?"

### BGM-Self MOF
- "¿Cuál es la diferencia entre glucómetro y CGM?"
- "¿Qué patrones de glucosa son normales después de comer?"
- "¿Por qué mi glucosa sube por la mañana sin comer?"

### BGM-Doctor (lado paciente MOF)
- "¿Qué información adicional tiene un CGM vs glucómetro?"
- "¿Cómo mi médico ve mis datos en tiempo real?"
- "¿Qué le digo a mi doctor en la próxima consulta?"

### BGM-Doctor (lado médico — para LinkedIn) 
- "¿Cómo integrar CGM en consulta de medicina interna?"
- "¿Cuándo es CGM superior a glucómetro en seguimiento DM2?"
- "¿Qué métricas del CGM impactan decisiones terapéuticas?"

### CGM-Switchers MOF
- "Para pacientes que ya usan CGM: ¿qué información adicional aporta el ecosistema QiHealth?"
- "¿Cómo se compara el AGP de QiTrax con el de LibreView?"

## Cuándo escalar al humano

- Tema clínico nuevo no en `cofepris-claim-library.md` → advisory pre-filming
- Médico con conflicto de interés posible → community manager para verificación
- Costo de filming alto (locación especial) → Jose
- Disponibilidad de Calendar del médico → coordinación humana directa
- Casos complejos de consentimiento → asesoría legal
