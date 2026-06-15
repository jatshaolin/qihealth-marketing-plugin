# Log de Actualizaciones de KPIs de Ventas

Registro de cada ejecución del skill `kpi-ventas-updater`.

## Historial

| Fecha ejecución | Semana cubierta | Pedidos | Ventas Netas (MXN) | Estado |
|---|---|---|---|---|
| 2026-06-15 | 2026-06-08 al 2026-06-14 | 36 | $86,106.96 | ✅ OK |

## Notas

- El skill corre automáticamente cada lunes a las 8:00 AM (America/Mexico_City).
- Fuente de datos: Shopify MCP (`mcp__Shopify__run-analytics-query`).
- Destino: Google Sheet `QiHealth_KPIs_Ventas_2026_v2` en Drive folder `1Xwi1lr92w_Zx-Lbv2aGV1R4_5Ti9l9SC`.
- En caso de falla, el skill reporta error y NO escribe datos inventados.
