# COFEPRIS Rules — QiHealth

Reglas de compliance regulatorio. Toda pieza producida por el plugin pasa por el quality gate `cofepris-check` antes de avanzar a publicación. Este documento define qué bloquea, qué se reformula y qué se permite.

## Contexto regulatorio

QiTrax es producto registrado COFEPRIS bajo número **Reg. 2370E2025 SSA** en categoría wellness (no diagnóstico). Esto define las fronteras de lo que se puede comunicar:

- QiTrax NO es dispositivo de diagnóstico
- QiTrax NO reemplaza tratamiento médico
- QiTrax NO cura ni previene enfermedades específicas
- QiTrax SÍ permite monitoreo continuo de glucosa intersticial para autoconocimiento metabólico
- QiTrax SÍ se conecta con seguimiento médico vía dashboard

## BLOCK automático (palabras y frases)

Estas activan bloqueo inmediato en `cofepris-check`. La pieza no avanza. Reformular obligatorio.

### Categoría 1 — Claims de cura o prevención específica

- "cura", "curar", "curativo"
- "elimina la diabetes", "revierte la diabetes definitivamente"
- "previene la diabetes" (sin matiz)
- "evita complicaciones" (sin matiz)
- "reemplaza la insulina"

### Categoría 2 — Claims de diagnóstico

- "diagnóstico", "diagnóstica", "diagnosticar"
- "detecta tu diabetes" (claim de detección clínica)
- "confirma si tienes diabetes"
- "te dice si eres diabético"

### Categoría 3 — Claims de tratamiento

- "tratamiento", "trata"
- "reemplaza tu medicamento"
- "no necesitas insulina"
- "sustituye al endocrinólogo"

### Categoría 4 — Claims comparativos engañosos

- "100% mejor que Abbott"
- "la única solución"
- "el único CGM con IA en México" (verificar antes de claim de exclusividad)
- "garantizado", "100% efectivo"

### Categoría 5 — Lenguaje predatorio

- "milagroso", "milagrosa"
- "el secreto que tu médico no te cuenta"
- "lo que las farmacéuticas no quieren que sepas"
- "increíble descubrimiento"
- "transforma tu vida en X días"

### Categoría 6 — Testimoniales con claims clínicos

- Testimonial que diga "se me curó la diabetes con QiTrax"
- Testimonial que diga "dejé de tomar mi medicina gracias a"
- Testimonial que diga "evité la insulina por usar"
- Cualquier testimonial sin nombre completo, edad y diagnóstico real verificable

## FLAG con sugerencia de rephrase

Estos no bloquean pero el sistema sugiere reformulación. Si el humano valida el contexto, puede pasar.

| Original | Sugerencia |
|---|---|
| "Previene" | "Ayuda a detectar señales tempranas de" |
| "Trata" | "Complementa el seguimiento de" |
| "Garantizado" | "Respaldado por" |
| "Mejor que el glucómetro" | "Diferente al glucómetro porque..." |
| "Cura tus picos" | "Te ayuda a entender tus picos" |
| "Reduce tu glucosa" | "Te da datos para conversar con tu médico sobre tu glucosa" |
| "Combate la diabetes" | "Acompaña el manejo de tu diabetes" |
| "Alarga tu vida" | "Aporta información para decisiones más informadas" |

## PERMITIDO (sin restricción adicional)

### Claims funcionales del producto

- "Muestra tu glucosa cada 5 minutos"
- "Se conecta con tu médico vía dashboard"
- "Monitoreo continuo durante 14 días"
- "Sin pinchazos"
- "Compatible con tu app móvil"
- "Resistente al agua hasta 1m"

### Datos respaldados con cita

- "ENSANUT 2024 reporta que..." (con link)
- "Según la ADA, la pre-diabetes afecta a..." (con cita)
- "Estudios indexados muestran que..." (con DOI o link)
- "Registro COFEPRIS 2370E2025 SSA"

### Lenguaje de descubrimiento personal

- "Entiende tu metabolismo"
- "Conoce tus patrones"
- "Descubre cómo reacciona tu cuerpo"
- "Toma decisiones informadas"
- "Conversa mejor con tu médico"

### Comparaciones honestas verificables

- Comparativa de funciones técnicas con sources públicas
- "Abbott no incluye coaching de IA. QiHealth sí." (verificable)
- "Abbott mide solo glucosa. QiHealth integra glucosa + sueño + actividad + composición corporal." (verificable)

## Triggers de revisión humana (advisory médico)

Estos casos NO se bloquean automáticamente, pero disparan notificación al advisory en Slack y la pieza queda en status `pending-medical-review` hasta que un médico del advisory firme aprobación. SLA: 24 horas en weekdays.

- Pieza que menciona condición clínica específica (DM1, DM2, pre-diabetes, complicaciones diabéticas, hipoglucemia, hiperglucemia)
- Pillar page o artículo SEO largo (>1500 palabras)
- Doctor Reel o pieza con vocero médico
- Comparación frontal con competidor (Abbott o Sibionics) — riesgo legal por publicidad comparativa
- Cualquier pieza para sub-segmento Legacy con claim sobre genética hereditaria
- Pieza que cite estudios clínicos o datos epidemiológicos
- Email automatizado a HCPs con afirmación clínica
- One-pager clínico para entregar en consultorio

## Tabla de claims por sub-segmento (referencia rápida)

### CGM-Switchers (sub-seg 1)

| SÍ se puede claim | NO se puede claim |
|---|---|
| "Más datos que tu sensor actual" | "Mejor que Abbott" |
| "Mismo precio, más contexto" | "Abbott miente" / "Abbott engaña" |
| "Migra sin perder tu historial" | "Reemplaza Abbott" |
| "Tu médico sigue viendo todo" | "Abbott es obsoleto" |

### BGM-Self (sub-seg 2A)

| SÍ se puede claim | NO se puede claim |
|---|---|
| "Ve la película completa" | "Curarás tu pre-diabetes" |
| "Sin piquetes" | "Detectarás si eres diabético" |
| "Datos continuos vs puntuales" | "Reemplaza al médico" |
| "Conoce tus patrones" | "Garantizamos resultados" |

### BGM-Doctor (sub-seg 2B)

| SÍ se puede claim | NO se puede claim |
|---|---|
| "Tu médico ve más" | "Reemplaza la consulta médica" |
| "Decisiones con datos continuos" | "El médico ya no es necesario" |
| "Pídele a tu doctor que conozca QiHealth" | "Diagnóstico remoto" |
| "Acompaña el seguimiento clínico" | "Cura supervisada por médico" |

### No-Measurers (sub-seg 3)

| SÍ se puede claim | NO se puede claim |
|---|---|
| "Conoce tu metabolismo" | "Detecta tu diabetes" |
| "Antes de medicarte, mide" | "Diagnóstico temprano" |
| "Antes de la enfermedad, la información" | "Confirma si tienes pre-diabetes" |
| "Empieza con 15 días, sin compromiso" | "Resultados garantizados en 15 días" |

### Legacy (sub-seg 4)

| SÍ se puede claim | NO se puede claim |
|---|---|
| "El 50% lo decides tú" | "No tendrás diabetes" |
| "Información previene" | "Garantizamos prevención" |
| "Conoce tu riesgo, decide tu camino" | "Anula tu predisposición genética" |
| "Cuídate como tu papá no pudo" | "Cura el destino familiar" |

## Reglas absolutas de programa de influencers

Aplica a todo KOL y micro-paciente:

1. Nunca claim de cura, prevención específica de complicaciones, o reemplazo de tratamiento médico.
2. Toda mención del producto debe identificarse como contenido patrocinado o relación con la marca (#publicidad, #colaboración con QiHealth).
3. Cualquier dato clínico mencionado debe ir respaldado por fuente oficial (registro COFEPRIS, paper publicado, resultado clínico propio del influencer con su CGM).
4. KOLs médicos deben siempre identificar su especialidad y cédula profesional.
5. Micro-pacientes nunca pueden hablar como médicos.

## Cuando hay duda

Si el sistema duda entre PASS y FLAG, el default es FLAG. Si duda entre FLAG y BLOCK, el default es BLOCK. Mejor frenar una pieza buena que sacar una observable. Una observación COFEPRIS cuesta más que cualquier campaña.

## Actualización

Esta lista evoluciona. Cada vez que el advisory médico aprueba un claim nuevo, se agrega a `memory/cofepris-claim-library.md` con su fuente. Cada vez que el advisory rechaza un claim que el sistema permitió pasar, se agrega aquí como BLOCK adicional.
