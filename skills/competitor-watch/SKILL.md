---
name: competitor-watch
description: >
  This skill should be used to monitor and report competitor activity for QiHealth. Triggers: "qué hizo Abbott", "competitor snapshot", "Sibionics nuevo", "watch competition", "competitor analysis", "qué cambió Abbott", "novedades del mercado CGM", "Abbott Meta Ad Library", "Sibionics precio". Reads memory/competitors.md, runs Apify scrapes when available (Meta Ad Library, competitor sites, marketplaces), reports changes by category (new ads, price changes, new partnerships, brand sentiment) with severity and recommendations.
metadata:
  version: "0.1.0"
  type: "operations"
  cadence: "every 6h (scheduled) + on-demand"
---

# Competitor Watch — Abbott + Sibionics + others

Tu rol es monitorear continuamente los movimientos de la competencia en el mercado mexicano de CGMs y reportar cambios accionables. La estrategia v4.3 explícitamente pide vigilar Abbott (FreeStyle Libre) como competidor #1 y Sibionics como competidor de precio agresivo.

## Mandatory loading

Antes de cualquier scan o reporte:
- `memory/competitors.md` — perfiles completos
- `memory/strategy-v4.3-summary.md` — contexto estratégico
- `memory/ad-references.md` (para detectar si un ad scraped ya está en biblioteca)

## Cobertura

### Tier 1 — Vigilancia continua (cada 6h via scheduled task)

**Abbott (FreeStyle Libre México)**
- Meta Ad Library México con `advertiser:Abbott Diabetes Care` (vía Apify)
- Sitio freestylelibre.mx (cambios de precio, promociones)
- Programa 4+1 ("Abracemos la Libertad") — términos y condiciones
- Posts orgánicos en redes Abbott México

**Sibionics (México)**
- Sitio sibionics.com.mx (precios, productos)
- Meta Ad Library México con `advertiser:Sibionics`
- Mercado Libre + Amazon MX (precios y disponibilidad)
- Distribuidor Kabla Store

### Tier 2 — Vigilancia semanal (lunes via scheduled task)

- KOLs médicos firmantes/promotores de competidores (¿cambio de bandera?)
- Reviews y comentarios en blogs y FB groups de diabetes (sentimiento)
- Cambios en posicionamiento web/SEO (nuevos artículos, nuevos keywords)

### Tier 3 — Vigilancia mensual

- Dexcom (¿lanzamiento oficial México?)
- Medtronic Guardian Connect (¿producto sin bomba?)
- Glucómetros tradicionales (¿lanzan CGM?)

## Categorías de cambio detectado

Cada hallazgo se clasifica:

### A. Nuevos ads en Meta Ad Library
- ¿Cuántos? ¿Cuándo lanzaron? ¿Cuál es el creative?
- Inferir audiencia target (demografía, intereses)
- Inferir sub-segmento atacado (¿van por DM2 dx? ¿por pre-diabéticos? ¿por Legacy?)
- Cuándo dispara recomendación a QiHealth: si es claim sensible o si ataca un sub-segmento donde tenemos campaña activa

### B. Cambios de precio o promoción
- Precio unitario de sensor
- Programa 4+1 (Abbott) o promociones equivalentes
- Bundles o membresías

Cuándo dispara: cualquier cambio de precio se reporta inmediatamente. Puede requerir respuesta (ej: ajustar landing /switch).

### C. Nuevas alianzas o endorsements
- Abbott con nueva organización (FMD/AMD/SMEN ya están — vigilar nuevas)
- Sibionics con farmacias o cadenas
- Cualquier KOL médico relevante firmando con competidor

Cuándo dispara: alta atención. Estos son moats de largo plazo.

### D. Nuevos productos o funcionalidades
- Lanzamiento de Libre 3 en México
- Sibionics GS3 con cambios técnicos
- Nuevas integraciones o accesorios

Cuándo dispara: alta atención. Puede cambiar la comparativa de producto.

### E. Cambios en SEO / contenido propio
- Nuevos artículos en blog del competidor
- Nuevos keywords ranqueando
- Nuevas pillar pages

Cuándo dispara: media atención. Útil para defender territorio SEO.

### F. Sentimiento en redes y reviews
- Quejas recurrentes de usuarios (oportunidad para QiHealth)
- Casos virales positivos del competidor (a igualar o contrarestar)
- Crisis o controversias (oportunidad de positioning)

Cuándo dispara: depende del volumen y severidad.

## Cadencia de reporte

### Reporte cada 6h (scheduled task `competitor-watch-6h`)

Output a Slack `#qihealth-competitor-alerts`:

```
🔍 COMPETITOR WATCH — [timestamp]

✅ Sin cambios detectados en últimas 6h
[O]
🚨 Cambios detectados:
- Abbott: [cambio resumen + link]
- Sibionics: [cambio resumen + link]

🔥 Severidad: [LOW / MEDIUM / HIGH]
🎯 Recomendación inmediata: [acción concreta o "ninguna" si es info]
```

### Reporte semanal completo (lunes morning brief)

Output más profundo:
- Resumen de cambios de la semana por categoría
- Tendencias detectadas
- Top 3 acciones recomendadas para QiHealth esta semana

### Reporte on-demand (vía /qihealth-competitor-snapshot)

Cuando Jose o Performance Manager preguntan:

```
=== COMPETITOR SNAPSHOT — [timestamp] ===

ABBOTT (FreeStyle Libre)
- Estado de Meta Ads: N anuncios activos, M nuevos esta semana
- Precio actual: $X MXN unitario / Programa 4+1 vigente
- Posts orgánicos últimos 7 días: [resumen]
- KOLs firmados: [estado]
- Cambios desde última check: [diff]

SIBIONICS
- Estado de Meta Ads: ...
- Precio actual: $X MXN GS1 / $Y MXN GS3 (oferta vigente: ...)
- Distribución actual: [...]
- Cambios desde última check: [diff]

OTROS (vigilancia ligera)
- Dexcom: [...]
- Medtronic: [...]

ACCIONES RECOMENDADAS:
1. [...]
2. [...]
3. [...]
```

## Output format estructurado al sistema

Cada hallazgo se guarda también en archivo de tracking (no en chat):

```yaml
- timestamp: 2026-05-09T12:00:00
  competitor: Abbott
  category: new_ad
  severity: medium
  source: https://www.facebook.com/ads/library/...
  description: "Nuevo ad de Abbott México targeting Legacy con mensaje 'Comparte LibreLinkUp con tu familia'"
  detected_change: |
    Abbott aparentemente está empezando a posicionar LibreLinkUp como herramienta de prevención familiar (similar al sub-segmento Legacy de QiHealth).
  recommended_action: |
    Acelerar producción de carrusel "50% genética. 50% lo decides tú" con énfasis en multi-biométrico (lo que LibreLinkUp NO tiene). Posiblemente ajustar landing /legacy con respuesta directa.
  status: pending_review_jose
```

## Apify integration (cuando esté el access)

El scheduled task usa estas Apify actor calls:

### Meta Ad Library scraper
- Input: `advertiser_name`, `country: MX`, `time_range: last_7_days`
- Output: lista de ads con creative + copy + targeting inferido
- Cadencia: cada 6h

### Website change detector
- Input: lista de URLs (sibionics.com.mx, freestylelibre.mx)
- Output: diff de contenido vs scrape anterior
- Cadencia: cada 6h

### Marketplace scraper
- Input: lista de URLs (Mercado Libre Sibionics, Amazon MX Sibionics)
- Output: precios actuales
- Cadencia: cada 24h

Antes del lunes (cuando se conecta Apify), el sistema opera con scraping manual sugerido — proporciona links al humano para que él haga el scrape y pegue el resultado.

## Anti-patrones (lo que NO hace este skill)

- NO reproduce creative de la competencia copiando frases (riesgo legal)
- NO ataca personalmente a marcas o personas (incluye anti-Abbott personal)
- NO genera FUD (fear/uncertainty/doubt) sin evidencia
- NO promueve respuesta competitiva agresiva basada en un solo data point — siempre cross-check

## Cuándo escalar al humano

- Cambio mayor de Abbott (lanzamiento Libre 3 México, cambio de precio drástico, alianza nueva con FMD/AMD/SMEN) → Jose + Performance Manager
- Crisis de competidor (controversia mediática, observación regulatoria) → Jose + advisory legal
- Sibionics empuja precio agresivo (ej: $999 MXN) → Jose + equipo comercial (puede requerir respuesta de pricing)
- Cualquier dato que pueda cambiar la estrategia trimestral → Jose

## Mantenimiento

- Cada mes, revisar Tier 1 / Tier 2 / Tier 3 (¿agregar nuevo competidor?)
- Cada trimestre, validar que los Apify actors siguen funcionando (cambios en Meta Ad Library API o anti-scraping de competidores)
- Cada año, revisión del competitive landscape completo (¿quién entró? ¿quién salió? ¿quién es el nuevo competidor real?)
