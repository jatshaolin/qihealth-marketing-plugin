---
name: notion-knowledge-mgmt
description: >
  This skill should be used to sync briefs, learnings, insights, and decisions to Notion for team visibility. Triggers: "sync to Notion", "guardar en Notion", "actualizar Notion", "Notion knowledge", "agregar a wiki". Maintains team-wide Notion workspace with consistent structure: Briefs, Learnings, Decisions, Calendars, KPIs.
metadata:
  version: "0.1.0"
  type: "utility"
---

# Notion Knowledge Management

Mantiene la wiki de QiHealth marketing en Notion sincronizada con el output del sistema agéntico.

## MCPs requeridos
- Notion (read + write)

## Estructura Notion sugerida

```
QiHealth Marketing (workspace)
├── 📋 Briefs (database)
│   ├── Por sub-segmento (tag)
│   ├── Por formato (tag)
│   └── Status (tag)
├── 📚 Learnings (database)
│   ├── Wins
│   ├── Losses
│   ├── Insights
│   └── Anti-patrones
├── 🎯 Decisiones (database)
│   ├── Fecha
│   ├── Decisión tomada
│   ├── Owner
│   └── Status
├── 📅 Calendar editorial (página)
├── 📊 KPIs dashboard (página)
├── 👥 Equipo y roles (página)
└── 🔍 Competitive intel (página)
```

## Tipos de sync

### A. Brief de pieza
Cuando se produce una pieza nueva, crear entry en Briefs database con:
- Title, sub-segmento, etapa funnel, formato
- Link a Drive con la pieza
- Link a ClickUp task
- Status del pipeline (Step 1-6)

### B. Learning post-iteración
Cuando un ad gana/pierde, append a Learnings con:
- Pattern descubierto
- Sub-segmento + format
- Evidencia (link a la pieza + performance data)
- Aplicabilidad a otras piezas

### C. Decisión estratégica
Cuando Jose toma decisión importante (cambio de allocation, pause de canal, etc.):
- Fecha
- Decisión
- Rationale
- Acciones derivadas
- Review date (cuándo re-evaluar)

### D. Calendar updates
Sync calendario editorial:
- Filming scheduled
- Webinars
- Lanzamientos paid
- Pillar pages publish dates

## Cadencia de sync

- **Real-time**: cuando se crea brief / task / decisión importante
- **Diaria**: morning brief incluye link a Notion calendar
- **Semanal**: viernes 5 PM (post-review) sync de learnings de la semana
- **Mensual**: dashboard KPIs actualizado

## Reglas

- Nunca eliminar entries (archivar, no borrar)
- Tags consistentes (definidos arriba)
- Links cross-database (Brief → Learning relacionado → Decisión)
- Read access para todo el equipo, write controlado

## Cuándo escalar al humano

- Conflict de versiones (alguien editó manualmente algo que el sistema iba a sobrescribir)
- Estructura Notion necesita reorganización → Jose
