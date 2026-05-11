---
name: weekly-performance-report
description: >
  This skill should be used to generate weekly performance report for QiHealth marketing review (Vie 4 PM). Triggers: "weekly report", "reporte semanal", "review viernes", "performance semanal", "/qihealth-weekly-review", "weekly prep". Aggregates GA4 + Search Console + Meta/TikTok Ads + Bigin + Zoho Desk for last 7 days, identifies winners/losers, prepares discussion material for Jose + Performance Manager + Community Manager meeting.
metadata:
  version: "0.1.0"
  type: "operations"
  cadence: "Vie 2 PM (scheduled task weekly-prep-friday)"
---

# Weekly Performance Report

Genera material para review viernes 4 PM. Output a Notion + Slack.

## Mandatory loading

- `memory/kpis-by-segment.md`
- `memory/strategy-v4.3-summary.md`

## MCPs requeridos

- Supermetrics (GA4 + Search Console + Meta/TikTok Ads bridge)
- Bigin (pipelines)
- Zoho Desk (tickets)

## Estructura del reporte

```markdown
# WEEKLY PERFORMANCE REPORT — Semana [N], [fechas]

## Resumen ejecutivo (3 bullets)

- [Win principal de la semana]
- [Loss principal de la semana]
- [Decisión que necesita la reunión]

---

## Performance por sub-segmento (vs target Q)

### CGM-Switchers
- Tráfico a /switch: X (vs target Q/4)
- Conversiones switch: N (vs target)
- ROAS paid: Xx
- Top winner: [pieza]
- Top loser: [pieza]
- Decisión sugerida: ...

### BGM-Self
[mismo formato]

### BGM-Doctor
- Médicos nuevos en pipeline: N
- Demos agendadas/realizadas: X/Y
- Hand-offs a Luis cerrados: N
- ...

### No-Measurers
[mismo formato]

### Legacy
[mismo formato]

### SEO transversal
- Tráfico orgánico semana: X
- Nuevos keywords top-10: N
- Pillar pages performance: [tabla]

---

## Ads classification (winner/loser/fatiga)

🟢 WINNERS — escalar (N)
- [Ad name] — ROAS Xx — recomiendo +Y% budget

🟡 MAYBE — iterar (N)
- ...

🔴 LOSERS — kill (N)
- ...

⚠️ FATIGA — refresh (N)
- ...

---

## Competidores esta semana

- **Abbott**: [cambios o sin novedades]
- **Sibionics**: [cambios o sin novedades]
- **Acción recomendada**: ...

---

## Calendario próxima semana

- Sub-segmento foco: [...]
- Piezas en producción: N
- Filming agendado: [día] con [médico]
- Webinar: [día] con [N inscritos]
- Lanzamientos paid: [...]

---

## Decisiones para la reunión (max 5)

1. [Decisión 1 con contexto + opciones]
2. [Decisión 2]
3. ...

---

## Acciones de la semana pasada — seguimiento

| Acción | Owner | Status |
|---|---|---|
| [Acción 1] | Jose | ✅ Done |
| [Acción 2] | Performance Manager | ⏳ In progress |
| [Acción 3] | Luis | 🔴 Blocked |

---

## Métricas globales semana

| Métrica | Esta semana | Semana anterior | Cambio |
|---|---|---|---|
| Tráfico orgánico total | X | Y | +/-Z% |
| Conversiones | X | Y | +/-Z% |
| ROAS promedio paid | X | Y | +/-Z |
| Leads nuevos Bigin | X | Y | +/-Z |
| Spend paid total | $X | $Y | +/-Z |
```

## Output a Slack (post-meeting summary)

```
✅ WEEKLY REVIEW DONE — Semana [N]

🏆 Wins: [3 bullets]
⚠️ Issues: [2 bullets]

🎯 Decisiones tomadas:
1. ...
2. ...
3. ...

📅 Próxima semana foco: [sub-segmento + objetivo]

Full report: [link Notion]
```

## Cuándo escalar al humano

- Métrica clave -30% o más → alerta inmediata Jose (no esperar viernes)
- Bloqueo de >1 semana en una decisión → escalar a Jose
- Spend overshoot → Performance Manager + Jose
