---
name: morning-brief-generator
description: >
  This skill should be used to generate the daily morning brief for QiHealth marketing. Triggers: "morning brief", "qué pasó ayer", "estado del día", "/qihealth-morning-brief", or fires automatically Lun-Vie 7:00 AM via scheduled task. Aggregates state of all 6 personas, ad performance, lead pipeline, content production queue, competitor alerts, and produces a scannable Slack message + email summary with daily decisions Jose needs to make.
metadata:
  version: "0.1.0"
  type: "operations"
  cadence: "daily 7:00 AM Lun-Vie + on-demand"
---

# Morning Brief Generator

Tu rol es producir el morning brief diario de QiHealth marketing — un resumen scannable que Jose (y opcionalmente el equipo) lee al arrancar el día. Llega a Slack `#qihealth-marketing-daily` y al email de Jose a las 7:00 AM Lun-Vie.

## Mandatory loading

Antes de generar el brief:
- `memory/strategy-v4.3-summary.md`
- `memory/kpis-by-segment.md` (para comparar contra targets)
- `memory/competitors.md` (para contexto de alertas)

Tools requeridas (cuando estén conectadas):
- Bigin MCP (estado de pipelines)
- GA4 / Search Console / Supermetrics MCP (tráfico)
- Meta Ads / TikTok Ads APIs (performance ads)
- ClickUp MCP (queue de producción de contenido)
- Slack MCP (notificación)

En MVP fase 1, si APIs no están conectadas, opera con datos manuales o "pending data — pídele a Performance Manager".

## Estructura del brief

### Encabezado

```
QIHEALTH MORNING BRIEF — [día de la semana, fecha]

📅 Día N de la semana de [foco semanal según calendario v4.3]
```

### Sección 1 — Estado de las 6 personas (1 línea cada una)

```
🎯 ESTADO POR PERSONA

CGM-Switchers: [N piezas en producción] / [M en queue] / [estado vs target del mes]
BGM-Self: ...
BGM-Doctor: ...
No-Measurers: ...
Legacy: ...
SEO transversal: [N pillars activos] / [M satélites] / [keywords top-10]
```

Si una persona está bloqueada (advisory pending, COFEPRIS flag), destacar con 🚨.

### Sección 2 — Performance último 24h y 7d

```
📊 PERFORMANCE

Últimas 24h:
- Tráfico orgánico: X visitas (vs ayer +Y%)
- Conversiones: N (vs ayer +M%)
- Spend total paid: $X MXN
- ROAS promedio paid: Xx
- Leads nuevos en Bigin: N (etiquetados por sub-seg: [tabla mini])

Últimos 7 días vs benchmark:
- [métrica 1]: estado [verde/amarillo/rojo]
- [métrica 2]: estado
```

### Sección 3 — Ads activos clasificados (de `ad-winner-loser-classifier`)

```
💰 ADS — clasificación

🟢 WINNERS (escalar): N
- [Ad name] — ROAS Xx — recomiendo +Y% budget
- ...

🟡 MAYBE (iterar): N
- [Ad name] — performance variable — iterar hook

🔴 LOSERS (kill): N
- [Ad name] — CTR X% por debajo benchmark — pausar

⚠️ FATIGA (refresh): N
- [Ad name] — frecuencia X — refresh con 4 variantes nuevas
```

### Sección 4 — Pipeline médicos y leads calientes

```
👨‍⚕️ MÉDICOS PIPELINE (Bigin)

- Total activos: N
- Demos agendadas hoy: N (con [nombres])
- Médicos esperando seguimiento >7 días: N (lista)
- Médicos que respondieron y necesitan hand-off a Luis: N
```

### Sección 5 — Alertas competidores

```
🔍 COMPETIDORES (últimas 24h)

Abbott: [cambios o "sin novedades"]
Sibionics: [cambios o "sin novedades"]

🚨 Si hay cambio relevante: descripción + recomendación específica
```

### Sección 6 — Decisiones que necesita Jose hoy

```
✅ DECISIONES DEL DÍA

1. [Decisión 1 con link a contexto]
2. [Decisión 2]
3. [Decisión 3]

(máximo 5 decisiones — más es ruido)
```

### Sección 7 — Calendario del día

```
📅 AGENDA DE HOY

- 10 AM: Filming Doctor Reel "[tema]" con [médico]
- 12 PM: Demo dashboard con Dr. [nombre] — confirmar Luis disponible
- 4 PM: ...
```

### Sección 8 — Próximos 7 días (look-ahead)

```
🔮 SEMANA EN VISTA

- Producir: N piezas para [sub-seg foco semanal]
- Lanzar: [campaign si aplica]
- Webinar: [día / sub-seg]
- Filming: [día / pieza]
```

### Footer

```
---
Brief generado por sistema agéntico QiHealth — [versión plugin]
¿Algo que ajustar o profundizar? Responde en este thread o ejecuta /qihealth-morning-brief con argumentos.

STATUS: REPORT-DELIVERED
NEXT: [si hay decisiones pendientes, listar primer paso. Si no, "operación normal"]
```

## Reglas de tono

- **Conciso**. Cada sección máximo 5-7 líneas. Si necesita más, link a doc detallado en Notion/Drive.
- **Action-oriented**. Cada hallazgo trae recomendación o decisión.
- **Numérico**. Datos concretos, no descripciones genéricas.
- **Honesto sobre falta de data**. Si una métrica no está disponible, declarar "pending data" no inventar.

## Cuándo el brief se vuelve menos útil (signal para iterar)

- Si Jose lo deja de abrir 3 días seguidos → ajustar (probable demasiado largo o no relevante)
- Si las "decisiones del día" no se ejecutan → revisar si las está priorizando correctamente
- Si las alertas competidor no resultan en acciones → calibrar severidad

Cada mes, sampling de 5 briefs random + feedback de Jose sobre utilidad real.

## Versión email vs Slack

### Slack
- Versión completa con emojis y secciones
- Threadable para respuestas y discusión
- Embedded enlaces y mentions cuando aplique

### Email
- Versión slightly más larga
- Embedded gráficas si aplica (charts de tráfico, ROAS, etc.)
- Para Jose si quiere review más detallado

## Cadencia y excepciones

- **Lunes-Viernes 7:00 AM**: brief automático
- **Sábado-Domingo**: NO se envía brief (descanso, salvo que Jose pida via comando)
- **Festivos**: skip default (Jose puede override)
- **Ciclo semanal especial — Lunes**: brief incluye plan de producción de la semana entera (extra section)
- **Ciclo mensual especial — primer lunes del mes**: brief incluye reporte mensual condensado (Sec adicional)

## On-demand vía /qihealth-morning-brief

Argumentos opcionales:
- `--detailed` — brief expandido con más data
- `--sub-segmento [nombre]` — focus en un sub-seg
- `--skip-section [sección]` — omitir una sección si Jose ya la conoce

## Cuándo escalar al humano

- Si el brief detecta crisis (ROAS cae 50% en 24h, Abbott cambia precio drástico, error de cofepris-check publicado) → notificación directa a Jose adicional al brief regular
- Si data MCP es inconsistente → flagear "data integrity issue" y NO publicar el brief hasta resolver
