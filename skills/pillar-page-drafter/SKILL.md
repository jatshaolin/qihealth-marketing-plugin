---
name: pillar-page-drafter
description: >
  This skill should be used to draft pillar pages (long-form SEO content 2,500-4,000 palabras) for QiHealth. Triggers: "pillar page", "pillar SEO", "artículo largo para SEO", "draft pillar para [sub-segmento]", "long-form content", "comprehensive guide". Produces YMYL-grade content with E-E-A-T signals, medical advisory review trigger, FAQ schema, internal linking structure, and CTA placements. Output ready for medical review → publish flow.
metadata:
  version: "0.1.0"
  type: "production"
  channel: "SEO"
  format: "Pillar page 2,500-4,000 words"
---

# Pillar Page Drafter

Tu rol es draftear pillar pages — el contenido largo, denso y de alta autoridad clínica que es el motor SEO de QiHealth. Una pillar page bien hecha genera leads recurrentes durante 18+ meses con CAC tendiendo a cero.

## Mandatory loading

- `memory/strategy-v4.3-summary.md` (sec 7 SEO + cluster keywords)
- `memory/brand-voice.md`
- `memory/cofepris-rules.md`
- `memory/cofepris-claim-library.md` (claims aprobados con fuentes)
- `memory/competitors.md`
- `memory/product-catalog.md`

## Las 5 pillar pages de QiHealth (calendario)

| Mes | Pillar | Sub-segmento | Keyword principal |
|---|---|---|---|
| 1 | "Glucómetro vs monitor continuo: cuál necesitas según tu caso" | BGM-Self | glucómetro vs CGM |
| 2 | "Pre-diabetes en México: guía completa de detección y prevención" | No-Measurers | pre-diabetes México |
| 3 | "Mi papá tiene diabetes: ¿yo también? Lo que dice la ciencia" | Legacy | diabetes hereditaria |
| 4 | "CGM en consulta: cómo tu médico ve tus datos en tiempo real" | BGM-Doctor | CGM consulta médica |
| 5 | "QiTrax vs FreeStyle Libre: comparativa completa México 2026" | CGM-Switchers | FreeStyle Libre alternativas |

## Specs técnicas

- **Longitud**: 2,500-4,000 palabras (las cortas no posicionan en YMYL)
- **Estructura**: intro + TOC + 6-10 H2 + FAQ + autor + fecha revisión + citas
- **Conversión**: CTA contextual cada 800-1000 palabras (NO esperar al final)
- **Multimedia**: 1 infografía propia + 1-2 Doctor Reels embebidos + 3-5 imágenes
- **Internal linking**: linkea a 8-12 satélites del mismo cluster
- **Schema markup**: FAQ schema + Article schema + Medical entity schema

## Estructura estándar (template)

### Sección 1 — Intro con dato impactante (200-300 palabras)

- Hook con dato impactante respaldado con fuente
- Reconocer la pregunta del lector como válida
- Promesa de qué va a aprender
- Anchor a autor médico con credenciales visible

Ejemplo (BGM-Self pillar):
> "Si tienes pre-diabetes o diabetes tipo 2 y estás usando glucómetro 1-3 veces por semana, este artículo te interesa. Vamos a hablar de algo que la mayoría no sabe: lo que tu glucómetro NO te dice — y por qué eso importa para tu salud metabólica a 5, 10, 20 años. Este contenido fue revisado por el Dr. Christian Frey, endocrinólogo, advisory clínico de QiHealth."

### Sección 2 — Tabla de contenidos navegable (anchors)

```html
<ul class="toc">
  <li><a href="#que-es-glucometro">1. Qué es un glucómetro</a></li>
  <li><a href="#que-es-cgm">2. Qué es un monitor continuo (CGM)</a></li>
  ...
</ul>
```

### Sección 3 — Definiciones (H2)

Establecer vocabulary que el lector necesita. Importante para Featured Snippets de Google.

Cada concepto en formato "definition box":
> "Un **glucómetro** es un dispositivo médico que mide la glucosa en sangre en un punto específico del tiempo a través de una muestra obtenida por punción capilar (piquete en el dedo)."

### Sección 4 — Comparación o explicación profunda (H2 × 3-5)

Aquí va el grueso del contenido. Cada H2 con:
- Pregunta clara como heading
- Respuesta directa (50-100 palabras)
- Datos respaldados con fuente
- Subsecciones H3 si necesarios

### Sección 5 — Casos clínicos o ejemplos (H2)

Mostrar la teoría aplicada. 2-3 ejemplos concretos. NO testimoniales sin verificación (riesgo COFEPRIS). SÍ casos genéricos clínicos:

> "Caso 1: Paciente con DM2 controlada con glucómetro 2x/día. Lectura de 110 mg/dL post-cena consistente. Al usar CGM: glucosa subió a 240 mg/dL a las 2:00 AM por 3 horas. Información que un glucómetro no captura porque la medición se hace cuando el paciente está despierto."

### Sección 6 — Implicación práctica para el lector (H2)

Qué significa todo esto **para él/ella**. No abstracto.

### Sección 7 — Cuándo considerar CGM (H2)

Lista o tabla con criterios accesibles. NO claim "deberías usar CGM si X" — sí "personas con factores Y suelen considerar CGM".

### Sección 8 — FAQ con schema markup (H2)

8-12 preguntas frecuentes con respuestas concisas. Optimizado para Featured Snippets + AI Overviews.

```html
<div itemscope itemtype="https://schema.org/FAQPage">
  <div itemscope itemprop="mainEntity" itemtype="https://schema.org/Question">
    <h3 itemprop="name">¿Necesito receta médica para usar QiTrax?</h3>
    <div itemscope itemprop="acceptedAnswer" itemtype="https://schema.org/Answer">
      <p itemprop="text">No. QiTrax es producto registrado COFEPRIS en categoría wellness (Reg. 2370E2025 SSA), por lo que no requiere receta médica para su adquisición. Sin embargo, recomendamos consultar con tu médico antes de usarlo si tienes condiciones diabéticas para integrarlo a tu plan de seguimiento.</p>
    </div>
  </div>
  ...
</div>
```

### Sección 9 — Conclusión + CTA principal (H2)

Cierre que sintetiza + invitación al producto/servicio relevante al sub-segmento.

### Sección 10 — Autor + fecha revisión + citas

- Autor con credenciales: foto + nombre + cédula + especialidad + bio corta
- Fecha de publicación + fecha de última revisión médica
- Citas a fuentes (lista bibliográfica al final)

## CTAs contextuales (cada 800-1000 palabras)

Importante: NO esperar al final para el CTA. Posicionarlos durante el flow:

- **~Palabra 800**: CTA suave — newsletter / lead magnet relevante
- **~Palabra 1,800**: CTA medio — quiz "¿Estás en riesgo?" o webinar
- **~Palabra 3,000**: CTA fuerte — producto (Plan correspondiente al sub-segmento)

## Internal linking

Cada pillar linkea a sus 8-12 satélites del mismo cluster. Los satélites linkean de vuelta al pillar.

```
[GLUCÓMETRO VS CGM (PILLAR)]
    ├── satélite 1: "Cómo monitorear glucosa sin piquetes"
    ├── satélite 2: "Qué es un CGM"
    ├── satélite 3: "Vale la pena un CGM"
    ├── satélite 4: "Primer CGM México"
    ├── satélite 5: "CGM sin receta México"
    ├── satélite 6: "Costo CGM México"
    └── ... 8-12 total
```

## Output format

```markdown
# [TÍTULO H1 — keyword principal + accent]

**Autor**: [Dr. Nombre], [especialidad], [cédula]
**Publicado**: [fecha]
**Revisión médica**: [fecha + nombre revisor advisory]
**Palabras**: ~3,000

---

[Intro 200-300 palabras]

## Tabla de contenidos

1. [Sección 1](#anchor1)
2. [Sección 2](#anchor2)
...

---

## Sección 1 — [Pregunta o concepto]
[contenido]

## Sección 2 — [...]
[contenido]

[... 6-10 H2 secciones ...]

---

## Preguntas frecuentes

### ¿[Pregunta 1]?
[Respuesta]

### ¿[Pregunta 2]?
[Respuesta]

[... 8-12 preguntas con FAQ schema ...]

---

## Conclusión

[Síntesis + CTA principal]

---

## Sobre el autor
[Bio del autor médico con credenciales]

## Fuentes
1. [Fuente 1 con link]
2. [Fuente 2 con link]
[...]

---

## Quality gates pendientes

- [ ] cofepris-check (todas las afirmaciones clínicas)
- [ ] brand-voice-qihealth
- [ ] factual-review (todas las cifras y citas)
- [ ] **Advisory médico review obligatorio (>1500 palabras + claims clínicos)**
- [ ] Schema markup validation (Google Rich Results Test)
- [ ] Internal linking audit
- [ ] Image alt-text + WebP optimization

STATUS: PILLAR-DRAFT — Advisory review obligatorio antes de publish
NEXT ACTION: 
1. Enviar a #qihealth-medical-review para advisory
2. SLA 24h en weekdays
3. Iterar según feedback del advisory
4. Post-aprobación: setup en CMS con schema markup
5. Backlink outreach (NVIDIA Inception, Singularity, prensa)
```

## Reglas YMYL críticas

Google trata salud como YMYL — penaliza fuertemente contenido sin E-E-A-T. Reglas:

1. **TODOS los claims clínicos** deben tener fuente verificable inline
2. **Fecha de revisión médica visible** y reciente (max 12 meses)
3. **Autor con credenciales reales** (no anónimo, no "Equipo QiHealth")
4. **Citas a fuentes primarias** (papers indexados, ENSANUT, ADA, EASD, IMSS) — NO citas a blogs personales
5. **Schema markup obligatorio** (Article + FAQ + Medical entity)
6. **Disclaimer al final**: "Este artículo es educativo, no sustituye consulta médica."

## Reglas de prompting interno

Para generar el draft, usar template estructurado:

```
Tema: [keyword + sub-segmento]
Sección X — [pregunta]:
- Datos respaldados con fuente
- Lenguaje accesible (NO médico-académico)
- Conexión con producto QiHealth (sutil, no hard sell)
- 300-500 palabras por sección H2
```

## Cuándo escalar al humano

- **OBLIGATORIO advisory review** antes de publish (no negociable)
- Si claim cuantitativo no tiene fuente clara → factual-review NEEDS-SOURCE → advisory
- Si compite por keyword muy competitiva (head term) → SEO strategist
- Si el pillar es para CGM-Switchers comparativo → advisory + legal review obligatorios
- Si autor médico declinó firma → buscar otro del advisory o postponer

## Iteración post-publish

A 30 días post-publish:
- Pull Search Console: ¿impressions? ¿clicks? ¿posición?
- Pull GA4: ¿tiempo en página? ¿bounce rate? ¿conversión a lead?
- Optimizar contenido si bounce >75% o posición no llegó a top 30
- Agregar internal links nuevos conforme se publican satélites

A 90 días:
- Re-evaluar si entró a top 10 (target Q4)
- Si sí: empezar refresh trimestral
- Si no: análisis de gap + replan keyword strategy
