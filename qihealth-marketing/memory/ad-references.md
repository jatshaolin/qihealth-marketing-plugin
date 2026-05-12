# Biblioteca de anuncios de referencia — INPUT del usuario

Archivo vivo. Aquí se acumulan los anuncios ganadores que Jose o el equipo identifica como referencias de calibración para el sistema. Cada referencia se procesa con la skill `ad-reference-library` que extrae los patrones (hook, estructura, ángulo, casting, voice, CTA) y los guarda etiquetados por sub-segmento + formato + etapa funnel.

## Estado al inicio del MVP

VACÍO. Pendiente que Jose mande las primeras referencias durante el sábado.

## Cómo se llena este archivo

Tres formatos aceptados:

1. **Screenshot de anuncio** (Meta Ad Library, Instagram, TikTok, Facebook) pegado en chat con comentario corto
2. **Link directo** a Reel/TikTok/IG/Meta Ad Library
3. **Copy o descripción** ("un anuncio de [marca X] que decía Y, funcionó porque Z")

Para cada referencia, el sistema extrae:

| Campo | Ejemplo |
|---|---|
| Source | Link o screenshot |
| Marca / advertiser | Abbott / Sibionics / Otro |
| Sub-segmento target inferido | CGM-Switchers / BGM-Self / etc. |
| Formato | Reel / Carrusel / Static / Video largo |
| Etapa funnel | TOF / MOF / BOF |
| Hook (primeros 3s) | Texto literal o descripción |
| Estructura | Problema → revelación → CTA / Comparativa / Testimonial / Educativo |
| Ángulo | Emocional / Racional / Urgencia / Curiosidad |
| Casting | Médico / Paciente / Animación / Texto on screen / Voiceover |
| Voice | Clínico / Cálido / Aspiracional / Casual |
| CTA | Texto literal del CTA |
| Por qué funciona (hipótesis) | Explicación |
| Tipo de referencia | Replicar formato / Inspiración tonal / Anti-patrón |

## Plantilla por entrada

```markdown
### [ID] — [Marca] — [Sub-segmento] — [Fecha de captura]

**Source**: [link o referencia]
**Formato**: [Reel/Carrusel/Static/etc]
**Etapa funnel**: [TOF/MOF/BOF]

**Hook**: "..."
**Estructura**: ...
**Ángulo**: ...
**Casting**: ...
**Voice**: ...
**CTA**: "..."

**Hipótesis de por qué funciona**:
- ...

**Tipo de referencia**:
- [ ] Replicar formato (mismo sub-segmento, adaptación directa)
- [ ] Inspiración tonal (otro sub-segmento, captar el feel)
- [ ] Anti-patrón (NO replicar, evitar)

**Notas adicionales**: ...
```

## Anti-patrones (referencias de qué NO hacer)

Esta sección se llena conforme el equipo identifica anuncios que NO debemos replicar. Pueden ser:

- Anuncios con tono wellness/biohacking que no encaja con QiHealth
- Anuncios con claims regulatorios riesgosos (estilo "cura tu diabetes")
- Anuncios genéricos sin diferenciación que no convierten
- Anuncios con casting no creíble (médico falso, paciente sin diagnóstico verificable)

---

## Categorías de captura prioritarias

Para arrancar bien calibrado, idealmente capturamos al menos:

- 3-5 referencias por sub-segmento × etapa funnel = 45-75 referencias en total como objetivo
- Mix de QiHealth-relevant (Abbott, Sibionics, otras healthtech) + cross-industry (anuncios de otros nichos cuyo formato/voice nos sirve para inspirar)
- Distribución sugerida: 60% Abbott + Sibionics, 20% otras healthtech LATAM/global, 20% cross-industry inspiración

## Uso de la biblioteca durante producción

Cada vez que el orquestador o una persona produce un anuncio nuevo, el flujo es:

1. Busca en `ad-references.md` referencias para mismo sub-segmento + etapa + formato
2. Identifica patrón ganador relevante
3. Adapta la estructura/hook/voice del patrón a la pieza nueva
4. Pasa por quality gates (cofepris-check + brand-voice + factual-review)
5. Guarda el output con tag de qué referencias inspiró (trazabilidad)

Cuando un anuncio nuevo gana en producción real, su patrón se promueve automáticamente a esta biblioteca como nueva referencia (con datos reales de performance).
