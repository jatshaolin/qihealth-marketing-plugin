---
name: kpi-ventas-updater
description: >
  Actualiza el Google Sheet de KPIs de ventas semanales con datos frescos de Shopify.
  Triggers: "actualizar KPIs", "update KPIs ventas", "refresh KPIs Drive", "KPIs semana".
  Se invoca automáticamente cada lunes por monday-kpi-update scheduled task.
  Consulta Shopify MCP para el período lunes–domingo de la semana anterior y
  escribe los valores en la fila correspondiente del Google Sheet en Drive.
metadata:
  version: "1.0.0"
  type: "operations"
  channel: "analytics"
  status: "active"
---

# KPI Ventas Updater

Tu rol es consultar Shopify MCP, extraer las métricas de ventas de la semana anterior (lunes a domingo), y actualizar el Google Sheet de KPIs en Drive con esos datos.

## Google Sheet objetivo

- **File ID canónico (xlsx en Drive)**: `1An1vu1uim7SMT3ceE-ZWN6tK3f7c8Jnc`
- **Nombre**: `KPIS_DIGITAL`
- **Pestañas**: Resumen, Enero–Diciembre, Sensores, Bandas, Anillos
- **Estructura**: 13 pestañas — Resumen + Enero a Diciembre. Cada pestaña mensual tiene columnas `1 al 7 / 8 al 14 / 15 al 21 / 22 al 28 / 29 al 30(31)` y filas SHOPIFY, MERCADO LIBRE, AMAZON, TOTAL 3 CANALES con Ventas (MXN), Pedidos, Ticket prom.
- Leer con `mcp__Google_Drive__read_file_content`, identificar la pestaña del mes y columna de semana correcta, actualizar solo las celdas azules de SHOPIFY (Ventas y Pedidos — el Ticket se calcula solo con fórmulas), y guardar.

## Mandatory loading

- `memory/kpis-by-segment.md` — para validar que métricas coinciden con targets
- `memory/strategy-v4.3-summary.md` — contexto general

## Pasos de ejecución (cada lunes)

### 1. Calcular fechas de la semana anterior

- Hoy es lunes. La semana a reportar es lunes pasado → domingo de ayer.
- Ejemplo: si hoy es 2026-06-15 (lunes), el período es 2026-06-08 al 2026-06-14.
- Formato para Shopify: `SINCE YYYY-MM-DD UNTIL YYYY-MM-DD`

### 2. Consultar Shopify MCP — Métricas de ventas

Ejecutar las siguientes queries con `mcp__Shopify__run-analytics-query`:

**Query 1 — Resumen de ventas de la semana:**
```
FROM sales SHOW orders, gross_sales, discounts, returns, net_sales, total_sales SINCE [fecha_lunes] UNTIL [fecha_domingo]
```

**Query 2 — AOV y clientes:**
```
FROM sales SHOW average_order_value, customers, returning_customers, returning_customer_rate SINCE [fecha_lunes] UNTIL [fecha_domingo]
```

**Query 3 — Top productos:**
```
FROM sales SHOW gross_sales, orders GROUP BY product_title ORDER BY gross_sales DESC LIMIT 10 SINCE [fecha_lunes] UNTIL [fecha_domingo]
```

**Query 4 — Sesiones y conversión:**
```
FROM sessions SHOW sessions, online_store_visitors, sessions_that_completed_checkout, conversion_rate SINCE [fecha_lunes] UNTIL [fecha_domingo]
```

### 3. Leer el Google Sheet actual

Usar `mcp__Google_Drive__read_file_content` con el file ID del sheet para entender la estructura actual (columnas, filas existentes, semana donde insertar).

### 4. Mapeo de métricas Shopify → estructura del Sheet

**Estructura del sheet:**
- Columnas de semana: `1 al 7`, `8 al 14`, `15 al 21`, `22 al 28`, `29 al 31`
- Cada semana del lunes anterior mapea a la columna según los días del mes que cubre.
  - Ejemplo: semana 8–14 jun → columna `8 al 14` en sección `JUNIO 2026`

**Filas a actualizar (solo SHOPIFY):**
| Métrica Shopify | Fila en sheet |
|---|---|
| net_sales | SHOPIFY > Ventas (MXN) |
| orders | SHOPIFY > Pedidos |
| average_order_value | SHOPIFY > Ticket prom. |

- El TOTAL MES y PROM. SEMANA se recalculan sumando las columnas de semanas.
- NO tocar filas de MERCADO LIBRE ni AMAZON (esas las captura el equipo manualmente).

### 5. Actualizar el Google Sheet

Usar `mcp__Google_Drive__create_file` para actualizar el contenido:
- Buscar la fila correspondiente a la semana (por fecha o número de semana)
- Si la fila no existe, añadirla al final de los datos
- NO sobrescribir datos existentes de semanas anteriores
- Formato de fecha de semana: `YYYY-MM-DD` (lunes de la semana)

### 6. Comparar vs targets y generar alerta si hay desviación

Al terminar la actualización, comparar las métricas clave vs `memory/kpis-by-segment.md`:
- Si ventas netas < 70% del target semanal → flag "⚠️ BAJO TARGET"
- Si pedidos < 70% del target → flag
- Incluir estas flags en el output final

### 7. Output del skill

Devolver resumen en texto con:
```
✅ KPIs actualizados — Semana [fecha_lunes] al [fecha_domingo]

📊 Métricas clave:
- Pedidos: X
- Ventas brutas: $X MXN
- Ventas netas: $X MXN
- AOV: $X MXN
- Tasa conversión: X%
- Clientes únicos: X

[flags de alerta si aplica]

🔗 Ver sheet: [URL del Google Sheet]
```

## Reglas

- **NO inventar datos**: si Shopify MCP falla, reportar error y NO escribir en el sheet.
- **Idempotencia**: si la semana ya tiene datos en el sheet, verificar con el usuario antes de sobreescribir.
- **Timezone**: todas las fechas en America/Mexico_City (UTC-6).
- **Moneda**: MXN. Si Shopify devuelve en otra moneda, convertir con tasa del día.

## Manejo de errores

- Si Shopify MCP no responde → "❌ Shopify MCP unavailable. KPIs NO actualizados. Reintentar manualmente."
- Si Google Drive no responde → "❌ Google Drive unavailable. Data lista pero NO guardada: [datos en texto]"
- Si el sheet tiene estructura inesperada → "⚠️ Estructura de sheet cambió. Revisión manual necesaria."

## Historial de ejecuciones

El skill debe escribir cada ejecución exitosa en `memory/kpi-update-log.md`:
```
- [fecha]: Semana [inicio]–[fin] actualizada. Pedidos: X. Net Sales: $X MXN.
```
