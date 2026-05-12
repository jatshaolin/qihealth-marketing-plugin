---
name: seo-internal-linking
description: >
  This skill should be used to audit and suggest internal linking strategy for QiHealth SEO content. Triggers: "internal linking", "audit de enlaces internos", "link building interno", "estructura de links", "pillar to satellite linking". Maps current linking graph, identifies orphans, suggests new links for topic cluster strength.
metadata:
  version: "0.1.0"
  type: "operations"
  channel: "SEO"
---

# SEO Internal Linking Auditor

Audita la estructura de enlaces internos del blog QiHealth y sugiere mejoras. Internal linking es señal de topic cluster fuerza para Google y mejora session depth.

## Mandatory loading

- `memory/strategy-v4.3-summary.md` (5 clusters de keywords)

## Proceso

### Paso 1 — Crawl del sitio
Vía Apify (Screaming Frog API alternative) o manual. Output: lista de URLs + outbound internal links de cada una.

### Paso 2 — Mapeo de cluster

Por cada cluster (BGM-Self, No-Measurers, Legacy, BGM-Doctor, CGM-Switchers):
- Identificar pillar page
- Identificar satélites
- Verificar que pillar linkea a TODOS sus satélites
- Verificar que CADA satélite linkea de vuelta al pillar
- Identificar links cross-cluster (cuando hay overlap natural)

### Paso 3 — Detectar problemas

- **Orphan pages**: páginas sin links entrantes (perdidas)
- **Over-linked**: pillar con >40 links salientes (dispersa autoridad)
- **Anchor text issues**: anchors genéricos ("click aquí") vs descriptivos
- **Broken internal links** (404)
- **Pages con potencial PR no aprovechado** (high traffic pero no linkea a producto/conversion)

### Paso 4 — Sugerencias específicas

Por cada problema, generar acción concreta:

```
- ORPHAN: /articulo-X no tiene links entrantes
  → Agregar link desde pillar /pre-diabetes-mexico en sección "Síntomas tempranos"
  → Anchor: "5 síntomas silenciosos"

- OVER-LINKED: pillar /pre-diabetes-mexico tiene 52 links salientes
  → Reducir a 25-30 links más relevantes
  → Quitar links a categorías no-cluster

- WEAK ANCHOR: link de /pillar a /satélite-X usa anchor "click aquí"
  → Cambiar a "factores de riesgo metabólico" (descriptivo + keyword)
```

## Output format

```markdown
=== INTERNAL LINKING AUDIT ===

**Period**: [fecha]
**Total pages analyzed**: [N]
**Total internal links**: [N]

### Cluster status

| Cluster | Pillar links a satélites | Satélites linkean back | Status |
|---|---|---|---|
| BGM-Self | 10/12 | 8/12 | ⚠️ Improve |
| No-Measurers | 12/12 | 12/12 | ✅ Strong |
| Legacy | 8/10 | 9/10 | ⚠️ Add 2 |
| BGM-Doctor | 6/8 | 5/8 | 🔴 Needs work |
| CGM-Switchers | 4/4 | 4/4 | ✅ Strong |

### Issues detected

1. **Orphan pages**: 3
   - /articulo-X — sugerir link desde [pillar Y]
   - ...

2. **Over-linked pillars**: 1
   - /pre-diabetes-mexico (52 links) → reduce to 30

3. **Weak anchors**: 12 instances
   - [lista con sugerencias específicas]

4. **Broken links**: 0

### Cross-cluster opportunities

- /diabetes-hereditaria (Legacy) podría linkear a /sintomas-prediabetes (No-Measurers) en sección "Factores ambientales"
- /comparativa-libre-qitrax (Switchers) podría linkear a /dashboard-medicos (BGM-Doctor) en sección "Para tu médico"

### Recommended actions

1. [Acción 1 con paso a paso]
2. [Acción 2]
3. [...]

NEXT ACTION: Implementar cambios en CMS. Re-audit en 30 días.
```

## Cadencia

- **Mensual** vía scheduled task seo-rank-tracking
- **Bajo demanda** cuando hay publish nuevo (verificar internal links nuevos al instante)

## Cuándo escalar al humano

- Cambios estructurales mayores (mover satélite a otro cluster) → SEO strategist
- Detección de duplicate content o cannibalization → Jose
- Cambios en CMS structure (URL slugs, categorías) → Jose
