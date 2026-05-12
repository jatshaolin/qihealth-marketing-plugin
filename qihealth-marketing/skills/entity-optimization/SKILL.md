---
name: entity-optimization
description: >
  This skill should be used to build and strengthen QiHealth's business entity in Google's Knowledge Graph for stronger local rankings and potential Knowledge Panel triggering. Triggers: "entity optimization", "Knowledge Graph", "Wikidata", "schema markup", "Knowledge Panel", "E-E-A-T", "entity audit". Builds the entity signals that compound for years and that almost no competitor (Sibionics, Abbott México) is doing. Critical for healthtech YMYL where E-E-A-T weights heavily.
metadata:
  version: "0.1.0"
  type: "operations"
  channel: "SEO + LLM SEO"
  inspired_by: "Sarvesh Shrivastava 20 SEO prompts (2026) — prompt 18 adapted for healthtech entity"
---

# Entity Optimization

The most advanced SEO lever almost no healthtech in Mexico is using. Builds QiHealth as a verified entity in Google's Knowledge Graph, which unlocks the highest level of local trust signals + protects rankings against algorithm updates.

For YMYL (Your Money or Your Life) topics like health, entity strength is **disproportionately important** for E-E-A-T (Experience, Expertise, Authoritativeness, Trust).

## Mandatory loading

- `memory/strategy-v4.3-summary.md`
- `memory/cofepris-claim-library.md`
- `memory/product-catalog.md` (data oficial QiHealth)
- `memory/competitors.md` (para benchmark)

## Datos de QiHealth (entity base)

Antes de auditar, confirmar:

```yaml
qihealth_entity:
  legal_name: "QiHealth" # confirmar con Jose
  brand_name: "QiHealth"
  founded: # año
  founder_name: "Jose Torres"
  founder_email: jat@qihealth.ai
  industry: "Healthtech / Continuous Glucose Monitoring"
  location: # Mexico (City?)
  website: # qihealth.ai? confirmar
  product_primary: "QiTrax CGM"
  registro_cofepris: "Reg. 2370E2025 SSA"
  advisory_medical:
    - "Christian Frey, MD"
    - "Vicente Alarcón, MD"
    # otros confirmados
  partnerships:
    - "NVIDIA Inception"
    - "Singularity University (alumni 2011)"
```

## Proceso de audit (5 fases)

### Fase 1 — Knowledge Graph status check

Buscar en Google estas queries y reportar qué aparece:
1. `"QiHealth" México`
2. `"QiHealth" Jose Torres`
3. `QiTrax CGM México`
4. `Jose Torres QiHealth founder`

Si aparece **Knowledge Panel** → entity reconocida ✅
Si NO aparece → entity sin reconocer, trabajo pendiente ⚠️

### Fase 2 — Wikidata presence

Ir a `wikidata.org` y buscar:
- "QiHealth"
- "Jose Torres" + "QiHealth"
- "QiTrax"

Reportar:
- ¿Existe entry en Wikidata?
- ¿Está actualizado y vinculado correctamente?
- ¿Hay referencias cruzadas a otras entidades (NVIDIA Inception, advisory members)?

Si NO existe Wikidata entry → es uno de los primeros entity signals a crear.

### Fase 3 — Schema markup audit

Ir a `search.google.com/test/rich-results` con el URL del homepage de QiHealth.

Reportar:
- ¿Qué schema está implementado actualmente?
- ¿Hay LocalBusiness / Organization / MedicalBusiness schema?
- ¿Está Article schema en blog posts?
- ¿Está MedicalEntity schema en pillar pages (para YMYL)?
- ¿Hay errores o warnings en el Structured Data?

### Fase 4 — Brand consistency audit

Búsqueda en Google de `"QiHealth"` (con comillas exactas) y reportar:
- Dónde aparece la marca (sitios, directorios, prensa, social)
- Inconsistencias en nombre, dirección, teléfono, founder
- Menciones positivas (PR earned)
- Menciones a ignorar (squatters, dominios parasitarios)

### Fase 5 — Cross-platform entity signals

Verificar presencia + consistencia en:

| Plataforma | Status QiHealth | Acción |
|---|---|---|
| Wikipedia (si eligible por notoriedad) | — | Generalmente no eligible hasta 5+ años + cobertura prensa |
| Wikidata | Crear si no existe | Alta prioridad |
| LinkedIn Company Page | — | Verificar + optimizar bio + employees |
| Crunchbase | — | Crear/claim listing |
| NVIDIA Inception directory | — | Asegurar listing + caso de éxito |
| Singularity University alumni | — | Validar perfil Jose como alumni + asociación con QiHealth |
| FMD / AMD / SMEN directorios (largo plazo) | — | Cuando QiHealth tenga advisory establecido |
| ANS o ANME | — | Asociaciones empresariales |
| CONACyT (research) | — | Si aplica investigación clínica propia |

## Output: 5 entregables

### Entregable 1 — LocalBusiness / Organization schema (JSON-LD code)

Generar el bloque completo de JSON-LD listo para pegar en `<head>` del homepage QiHealth. Estructura:

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "MedicalOrganization",
  "name": "QiHealth",
  "description": "Plataforma mexicana de inteligencia metabólica con CGM QiTrax + ecosistema de IA para diabetes y prevención metabólica",
  "url": "https://qihealth.ai",
  "logo": "https://qihealth.ai/logo.png",
  "foundingDate": "[año]",
  "founder": {
    "@type": "Person",
    "name": "Jose Torres",
    "jobTitle": "CEO / Founder",
    "sameAs": [
      "https://www.linkedin.com/in/josetorres",
      "https://www.linkedin.com/in/[handle]"
    ]
  },
  "address": {
    "@type": "PostalAddress",
    "addressCountry": "MX",
    "addressRegion": "[Ciudad]"
  },
  "contactPoint": {
    "@type": "ContactPoint",
    "telephone": "[phone]",
    "contactType": "customer service",
    "areaServed": "MX",
    "availableLanguage": "Spanish"
  },
  "sameAs": [
    "https://www.linkedin.com/company/qihealth",
    "https://www.crunchbase.com/organization/qihealth",
    "https://www.instagram.com/qihealth",
    "https://www.facebook.com/qihealth"
  ],
  "knowsAbout": [
    "Diabetes Type 2",
    "Pre-diabetes",
    "Continuous Glucose Monitoring",
    "Metabolic Health"
  ],
  "medicalSpecialty": "Endocrinology",
  "memberOf": [
    {
      "@type": "Organization",
      "name": "NVIDIA Inception"
    }
  ]
}
</script>
```

### Entregable 2 — Wikidata entry draft

Estructura para crear entrada en Wikidata:
- Etiquetas y descripciones (español + inglés)
- Propiedades clave (P31 instance of, P17 country, P571 inception, P488 chairperson, etc.)
- References (URLs autoritativas que validan cada claim)

### Entregable 3 — Anchor text + brand mention plan

Lista de:
- Qué anchor text construir cuando outreach KOLs o prensa
- Qué brand mentions priorizar
- Estrategia para fortalecer brand signals consistentes

### Entregable 4 — Knowledge Panel triggering plan

Instrucciones para que la Knowledge Panel aparezca:
1. Schema markup en homepage ✅ (entregable 1)
2. Consistencia NAP en 20+ sites autoritativos
3. Wikidata entry ✅ (entregable 2)
4. Prensa de calidad (Forbes Salud, Expansión, Reforma Salud, Inc.)
5. LinkedIn Company Page activa con posts regulares
6. Crunchbase listing completo
7. NVIDIA Inception case study publicado
8. Entry en directorios sectoriales (FMD/AMD/SMEN — largo plazo)

### Entregable 5 — Roadmap de 90 días

| Mes | Acciones |
|---|---|
| Mes 1 | Schema markup deployed + Wikidata entry creada + LinkedIn Company Page optimizada |
| Mes 2 | Crunchbase listing + NVIDIA Inception listing + Brand mention monitoring activo |
| Mes 3 | Primera prensa earned (Forbes/Expansión) + entry en 1 asociación gremial |

## Por qué importa específicamente para QiHealth

### YMYL es brutal en healthtech

Google trata salud como Your Money or Your Life. Sin E-E-A-T fuerte, NO posicionas en YMYL aunque tengas el mejor contenido. Entity signals son el #1 factor en E-E-A-T trust.

### AI Overviews y LLM citations

Cuando ChatGPT, Perplexity, Claude o Google AI Overview responden sobre diabetes/CGM en México, citan entidades verificadas. Si QiHealth no es entity reconocida, NO te citan.

Esta skill complementa `llm-seo-optimizer` y `llm-citation-tracker`.

### Resilencia ante algorithm updates

Empresas con entity fuerte sobreviven Google updates (March Core Update, AI integrations). Las que dependen solo de keywords/backlinks pierden 30-60% de tráfico cuando hay update grande.

### Competidores no lo están haciendo

- **Sibionics MX**: NO tiene Wikidata, schema básico, no aparece en Knowledge Panel
- **Abbott México**: Tiene schema corporativo global pero no específico MX, no tiene Knowledge Panel local
- **Dexcom México**: minimal presence

QiHealth tiene ventana competitiva para construir esto antes de que otros se den cuenta.

## Cuándo escalar al humano

- Decisiones sobre claim a hacer en Wikidata (require evidence) → Jose
- Schema markup deployment → developer / Jose
- Outreach a Forbes / Expansión / Reforma Salud → Jose o PR humano
- Validación de membership FMD/AMD/SMEN → Jose
- Wikipedia eligibility (solo si tienen cobertura prensa suficiente) → Jose

## Cadencia

- **Inicial** (semana 1): full audit fases 1-5
- **Mensual**: re-check Knowledge Panel status + Wikidata visibility
- **Trimestral**: progress tracking del roadmap 90 días
- **Cuando hay milestone** (prensa earned, asociación nueva, advisory member nuevo): update Wikidata + schema markup

## Output al sistema

- → `seo-monthly-report`: sección "Entity signals" trimestral
- → `llm-seo-optimizer`: confirma que content tiene entity-level signals
- → `morning-brief`: alerta cuando Knowledge Panel se activa
- → `memory/entity-status.md`: tracking del progreso
