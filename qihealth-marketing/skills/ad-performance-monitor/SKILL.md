---
name: ad-performance-monitor
description: >
  This skill should be used to pull current ad performance data from Meta Ads and TikTok Ads APIs. Triggers: "performance ads", "cómo van los anuncios", "Meta Ads stats", "TikTok Ads performance", "ad metrics now", "pull ad data". Reads Meta Ads API and TikTok Ads API and returns standardized performance data per ad, ad set, and campaign. Used by ad-winner-loser-classifier and morning-brief-generator. Activates when API credentials are connected (target Lunes post-MVP).
metadata:
  version: "0.1.0"
  type: "operations"
  channel: "paid"
  status: "stub-pending-api-connection"
---

# Ad Performance Monitor

Tu rol es pulling de performance data desde las APIs de Meta Ads y TikTok Ads y devolver data estandarizada para que otras skills (ad-winner-loser-classifier, morning-brief-generator) la consuman.

## Estado actual: STUB (pending API connection)

Esta skill está construida en draft pero requiere conexión a:
- Meta Ads API (vía MCP cuando esté disponible)
- TikTok Ads API (cuando QiHealth abra la cuenta de TikTok Ads, target lunes)

Mientras no haya conexión, esta skill responde con: "Pending API connection. Activate after Meta Ads + TikTok Ads MCP credentials are configured."

## Cuando esté activa

### Mandatory loading

- `memory/kpis-by-segment.md`
- `memory/strategy-v4.3-summary.md`

### MCPs requeridos

- Meta Ads API (vía Meta Business MCP cuando esté disponible)
- TikTok Ads API (vía TikTok for Business MCP)
- Supermetrics (alternativa o complemento si está disponible)

### Output estandarizado

Para cada ad activo, devuelve:

```yaml
ad_id: "12345"
ad_name: "Reel Legacy V1 - Mi papá lo vivió"
sub_segmento: "legacy"
funnel_stage: "TOF"
platform: "Meta"
campaign_id: "67890"
adset_id: "11111"

period: "last_7_days"

metrics:
  impressions: 145000
  reach: 89000
  clicks: 2350
  ctr: 1.62%
  cpm_mxn: 178
  cpc_mxn: 7.50
  cpl_mxn: 145
  conversions: 32
  conversion_rate: 1.36%
  spend_mxn: 17600
  roas: 3.2
  frequency: 1.63
  saves: 145 (org si aplica)
  comments: 87
  shares: 23

trends:
  ctr_vs_prev_period: "-12%"
  cpm_vs_prev_period: "+8%"
  frequency_vs_prev_period: "+0.3"
```

### Cadencia

- **Real-time pull**: cuando ad-winner-loser-classifier o morning-brief-generator lo invoca
- **Background pull cada 4h**: cache de data fresca para reducir API calls
- **Diario consolidado**: resumen de todos los ads activos para morning brief

### Reglas de uso

- Cache de 4h para reducir API calls
- No bloquear consumo de otras skills si API call lento (default a cache)
- Si data es vieja >12h, declarar "stale" en el output
- Si API call falla, declarar "API unavailable" y NO inventar data

### Cuándo escalar al humano

- Si APIs devuelven data inconsistente con Bigin (conversiones que no aparecen en CRM) → flag a Performance Manager para investigar tracking
- Si una métrica clave (ROAS, conversion) está en 0 después de spend significativo → tracking probablemente roto
- Si un campaign nuevo no aparece en pull → MCP probablemente desfasado o credentials caducadas

## Activación

Cuando los MCPs de Meta Ads y TikTok Ads estén conectados:

1. Update este SKILL.md cambiando `status: "active"`
2. Test pull con un campaign de prueba
3. Verificar que ad-winner-loser-classifier consume la data correctamente
4. Activar scheduled task de background pull

Hasta entonces, output es: `"STATUS: STUB-PENDING-API-CONNECTION. Esta skill se activa cuando Meta Ads API y TikTok Ads API estén configuradas (target Lunes post-MVP)."`
