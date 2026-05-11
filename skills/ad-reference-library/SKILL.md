---
name: ad-reference-library
description: >
  This skill should be used when Jose or the team submits an ad as reference for the system to learn from — winning ads, competitor ads, inspiration ads. Triggers: "agrega esta referencia", "guarda este anuncio como referencia", "este anuncio funcionó porque", "captura esta referencia", "input de anuncio ganador", "referencia de inspiración". Extracts structured patterns from the submitted ad (hook, structure, angle, casting, voice, CTA), tags by sub-segment + format + funnel stage, and appends to memory/ad-references.md.
metadata:
  version: "0.1.0"
  type: "memory-management"
---

# Ad Reference Library — Ingesta y procesamiento

Tu rol es procesar referencias de anuncios que el equipo de QiHealth (Jose y otros) considera como benchmarks. Extraes patrones estructurados, los catalogas, y los guardas en `memory/ad-references.md` para que el sistema los consulte cada vez que produce contenido nuevo.

## Mandatory loading

Antes de procesar cualquier referencia:
- `memory/ad-references.md` (estado actual)
- `memory/strategy-v4.3-summary.md` (para identificar sub-segmento)
- `memory/brand-voice.md` (para clasificar tono)

## Input que recibes

Cuatro formatos posibles:

### Formato 1 — Screenshot pegado en chat
Imagen del anuncio + comentario corto del usuario.

Acción:
1. Lee la imagen visualmente
2. Extrae: copy visible, headline, hook, CTA, casting (si hay persona), brand visible
3. Pregunta al usuario si falta info crítica (sub-segmento target, por qué le late)

### Formato 2 — Link directo
URL a Reel/TikTok/Meta Ad Library/IG.

Acción:
1. Si tienes WebFetch disponible, abre el link
2. Si no, pídele al usuario que pegue screenshot o describa
3. Procesa igual que screenshot

### Formato 3 — Copy/descripción textual
Usuario describe el anuncio en palabras.

Acción:
1. Lee la descripción
2. Si crítica info falta (sub-segmento, formato, etc.), pregunta
3. Procesa con la info disponible

### Formato 4 — Lista batch (varios anuncios)
Usuario pasa varios links/screenshots en una sola request.

Acción:
1. Procesa uno por uno
2. Mantén orden y numeración
3. Genera output consolidado

## Extracción estructurada

Para cada anuncio, extraer:

| Campo | Ejemplo | Cómo se infiere |
|---|---|---|
| Source | Link/screenshot | Provisto por usuario |
| Marca / advertiser | Abbott / Sibionics / Otro | Visible en el anuncio o usuario lo dice |
| Sub-segmento target inferido | CGM-Switchers / BGM-Self / etc. | Basado en mensaje + audiencia |
| Formato | Reel / Carrusel / Static / Video largo | Visible en el medium |
| Etapa funnel | TOF / MOF / BOF | Basado en CTA + mensaje |
| Hook (primeros 3s) | Texto literal o descripción | Directo del anuncio |
| Estructura | Problema-revelación-CTA / Comparativa / Testimonial / Educativo | Análisis de arco |
| Ángulo | Emocional / Racional / Urgencia / Curiosidad | Análisis tonal |
| Casting | Médico / Paciente / Animación / Texto on-screen / VO | Visible |
| Voice | Clínico / Cálido / Aspiracional / Casual | Análisis tonal |
| CTA | Texto literal del CTA | Directo del anuncio |
| Por qué funciona (hipótesis) | Explicación estructurada | Tu análisis + comentario del usuario |
| Tipo de referencia | Replicar formato / Inspiración / Anti-patrón | Pregunta al usuario o infiere de su comentario |

## Output al agregar referencia

```markdown
=== REFERENCE PROCESSED ===
ID: REF-{auto-incremental-yyyymmdd}-{N}
Source: {link/screenshot description}
Marca: {advertiser}
Sub-segmento target: {sub-seg}
Etapa funnel: {TOF/MOF/BOF}
Formato: {format}

Hook: "{texto literal}"
Estructura: {tipo}
Ángulo: {emocional/racional/etc}
Casting: {tipo}
Voice: {tono}
CTA: "{texto literal}"

Hipótesis de por qué funciona:
- {bullet 1}
- {bullet 2}
- {bullet 3}

Tipo de referencia: [✓] Replicar / [ ] Inspiración / [ ] Anti-patrón

Notas adicionales: {si aplica}

==================
APPENDED to: memory/ad-references.md
NEXT: Si tienes más referencias, mándalas. Si no, esta queda disponible para que las personas las consulten al producir contenido.
```

## Cuándo pedir clarificación

Si la información es insuficiente para clasificar correctamente:

- **Sub-segmento ambiguo**: pregunta "¿Para qué sub-segmento ves este anuncio? CGM-Switchers, BGM-Self, BGM-Doctor, No-Measurers, o Legacy?"
- **Tipo de referencia ambiguo**: pregunta "¿Es para REPLICAR formato (mismo sub-seg, copia directa), INSPIRACIÓN (otro sub-seg, captar feel), o ANTI-PATRÓN (NO replicar)?"
- **Por qué funciona** ambiguo: pregunta "¿Qué específicamente te late? Hook, casting, voice, ángulo emocional, CTA?"

Si el usuario no quiere ampliar info, procesa con lo disponible y marca el campo como "Inferido — sin confirmación".

## Reglas de procesamiento

### Anti-patrones siempre se procesan también
Si el usuario marca un anuncio como "esto NO me late" o "esto es lo que NO queremos", se guarda como anti-patrón. Es valioso saber qué evitar.

### Referencias cross-industry son OK
Anuncios que NO son healthtech pero tienen formato/voice que sirve para inspirar también se guardan. Etiquetar como "Inspiración cross-industry — [industria de origen]".

### Privacy y propiedad intelectual
- NO descargar ni guardar imagen completa del anuncio (solo descripción)
- Solo metadata + descripción + análisis estructurado
- Source link siempre conservado

### Si el usuario sube su propio anuncio que ganó
Procesarlo como referencia. Tag adicional: "QiHealth-historical-winner". Estos son los más valiosos para entrenamiento del sistema.

## Cómo se usa después

Cada vez que una persona (orchestrator + sub-segmento) produce un anuncio:

1. Busca en `memory/ad-references.md` referencias para mismo sub-seg + etapa + formato
2. Selecciona top 3 referencias relevantes
3. Identifica el patrón ganador (hook + estructura + ángulo)
4. Adapta el patrón a la pieza nueva
5. En el output, especifica: "Inspirado por: REF-{ID-1}, REF-{ID-2}" para trazabilidad

Esto crea aprendizaje compuesto: cuanto más alimente Jose la biblioteca, mejor produce el sistema.

## Categorías prioritarias para arrancar

Para tener el sistema bien calibrado en MVP, idealmente capturar:

- 3-5 referencias por sub-segmento × etapa funnel = 45-75 referencias en total como objetivo
- **Distribución sugerida**:
  - 40% Abbott (competidor #1, audiencia que queremos converter de CGM-Switchers)
  - 20% Sibionics (competidor de precio agresivo)
  - 20% Otra healthtech LATAM o global (Dexcom internacional, otros CGMs)
  - 20% Cross-industry (ej: anuncios de prevención del cáncer, prevención cardiovascular, otros healthtech con foco emocional)

## Comando de uso (para Jose)

Para agregar una referencia, Jose puede simplemente:

```
/qihealth-marketing agrega esta referencia: [link o screenshot]
```

O en modo conversacional:

```
"Mira este anuncio de [marca], me late porque [razón]. Es para [sub-segmento]."
```

El orchestrator detecta intent y dispara este skill automáticamente.

## Cuándo escalar al humano

- Si una referencia es ambigua y el usuario no responde clarificaciones → archivar como "pending classification"
- Si una referencia tiene claim COFEPRIS riesgoso (es importante NO replicar) → marcar como anti-patrón + alerta a Jose
- Si una referencia es de un competidor con observación regulatoria conocida → contexto adicional

## Mantenimiento

- **Mensual**: revisar referencias de hace >90 días (¿siguen siendo relevantes?)
- **Cuando una referencia inspire un anuncio que gana**: agregar nota "→ ganó como [QiHealth-creative-id]" para crear cadena de procedencia
- **Si una referencia inspira anuncios que pierden consistentemente**: marcar como "Reference-questionable — review"
