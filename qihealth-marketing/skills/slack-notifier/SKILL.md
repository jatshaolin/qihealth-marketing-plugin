---
name: slack-notifier
description: >
  This skill should be used to send formatted notifications to QiHealth Slack channels. Triggers automatically from other skills (orchestrator, cofepris-check, competitor-watch, morning-brief-generator) or on-demand. Triggers: "notifica en Slack", "post to Slack", "send Slack", "alerta Slack", "Slack message". Sends to specific QiHealth channels with consistent formatting, severity icons, and thread structure for follow-ups.
metadata:
  version: "0.1.0"
  type: "utility"
---

# Slack Notifier — QiHealth channels

Tu rol es enviar mensajes formateados a los canales de Slack de QiHealth con consistencia. Eres invocado por otras skills (orchestrator, cofepris-check, competitor-watch, morning-brief-generator) o directamente por el usuario.

## Channels QiHealth (estándar)

| Channel | Propósito | Audiencia |
|---|---|---|
| `#qihealth-marketing-daily` | Morning brief + updates diarios | Jose + equipo marketing |
| `#qihealth-marketing-pipeline` | Updates de piezas en producción | Equipo producción + Jose |
| `#qihealth-medical-review` | Triggers de advisory médico | Advisory + Jose |
| `#qihealth-cofepris-flags` | BLOCK / FLAG de cofepris-check | Jose + advisory |
| `#qihealth-competitor-alerts` | Alertas Abbott + Sibionics | Jose + Performance Manager |
| `#qihealth-paid-performance` | Updates ad performance | Performance Manager + Jose |
| `#qihealth-commercial-handoffs` | Hand-offs a Luis | Luis + Jose + equipo comercial |
| `#qihealth-seo-updates` | Movimientos SEO | Jose |
| `#qihealth-leads-hot` | Leads calientes que requieren acción | Equipo comercial |

Si un canal no existe, sugerir crearlo antes de enviar.

## Mandatory loading

- Lista de channels arriba
- Estructura de mensaje según severidad

## Tipos de mensaje

### 1. Info (sin urgencia)

```
ℹ️ INFO — [tema corto]

[contenido principal — 2-5 líneas]

[link al recurso o al thread de detalle]
```

### 2. Action required (necesita decisión humana)

```
✅ ACCIÓN REQUERIDA — [tema corto]

[descripción del contexto — 2-3 líneas]

Decisión necesaria:
- [opción 1]
- [opción 2]

@[mención al humano responsable]
SLA: [tiempo si aplica]
```

### 3. Alert (severidad alta — atención inmediata)

```
🚨 ALERTA — [tema corto]

[descripción — 2-4 líneas]

Por qué importa:
- [consecuencia 1]
- [consecuencia 2]

Acción inmediata recomendada:
- [paso 1]

@[mention] — confirma antes de [tiempo].
```

### 4. Flag (advertencia, no urgente pero requiere review)

```
⚠️ FLAG — [tema corto]

[descripción — 2-3 líneas]

Recomendación:
- [acción]

@[mention si aplica]
```

### 5. Success (logro o milestone)

```
✅ SUCCESS — [tema corto]

[descripción — 1-2 líneas]

[métrica concreta o dato]

[link a detalle si aplica]
```

### 6. Pending (en espera)

```
⏳ PENDING — [tema corto]

[descripción del estado actual]

Bloqueado por: [persona / sistema / data]
Esperando: [qué se espera]
SLA: [tiempo]

@[mention si aplica]
```

## Reglas de formato

### Headers
- Mensajes empiezan con icono + tipo en mayúsculas + tema corto
- Tema corto: máximo 8 palabras, identificable

### Body
- 2-5 líneas para body principal
- Bullets cuando hay más de 2 puntos
- Numeración cuando hay secuencia

### Mentions
- @user específico cuando hay acción required de esa persona
- @channel solo para alerts críticos (rara vez)
- @here para presencia inmediata necesaria
- Sin mention si es info general

### Links
- Siempre incluir link al recurso completo (Notion doc, ClickUp task, Drive folder)
- Format: `<URL|texto descriptivo>` para previews

### Threading
- Si la notificación dispara discusión esperada, declarar "Responde en este thread"
- Si es info que no necesita respuesta, no abrir thread innecesario

## Output format

```
[CHANNEL: #qihealth-...]
[ICON + TYPE]: [TEMA]

[body completo del mensaje formateado según tipo]
```

## Anti-patrones (lo que NO hacer)

- **Spam**: NO enviar más de 5-7 mensajes/día por channel salvo emergencia
- **Mention masivo**: NO @here para info que puede esperar al morning brief
- **Mensajes ambiguos**: cada mensaje debe tener acción clara o ser puramente informativo (declarar cuál)
- **Cross-posting**: NO copiar el mismo mensaje a múltiples channels (route a UNO específico)
- **Emojis excesivos**: 1-2 emojis en header + body limpio. NO usar emojis decorativos.

## Ejemplos

### Ejemplo 1 — Cofepris flag a `#qihealth-cofepris-flags`

```
⚠️ FLAG — Reel Legacy TOF detectó claim genético no verificado

Pieza en producción: "El 50% es genética"
Quality gate: cofepris-check sugiere FLAG
Sugerencia de rephrase: "El riesgo familiar es relevante pero modificable"

@christianfrey — ¿lo aprobamos como está o ajustamos?
SLA: 24h en weekday

Pieza queda en hold hasta tu respuesta.
[link al draft en Drive]
```

### Ejemplo 2 — Competitor alert a `#qihealth-competitor-alerts`

```
🚨 ALERTA — Abbott bajó precio del programa 4+1

Cambio detectado: ahora 5 sensores por el precio de 4+1 anterior, $1,200 MXN unitario amortizado (antes $1,303 MXN).

Por qué importa:
- Reduce ventaja de QiHealth en sub-segmento CGM-Switchers
- Puede afectar MOF de switchers que estaban en consideración

Acción inmediata recomendada:
- Revisar landing /switch — ajustar comparativa de precio
- Considerar respuesta competitiva en email a CGM-Switchers en pipeline Bigin

@josetorres @performance-manager — discusión esta tarde?
SLA: respuesta en <4h
[link al post de Abbott México]
```

### Ejemplo 3 — Hand-off a `#qihealth-commercial-handoffs`

```
✅ ACCIÓN REQUERIDA — Médico respondió a outreach: Dr. Jorge Pérez (endocrinólogo CDMX)

Contexto:
- Outreach enviado: 5 mayo
- Respondió: hoy 7:42 AM
- Mensaje: "Me interesa conocer la plataforma. ¿Pueden mostrar el dashboard?"

Sistema propone 3 slots de Calendar de Luis:
- Hoy 3 PM
- Mañana 10 AM
- Mañana 2 PM

@luis — ¿confirmas algún slot? Sistema agenda + envía confirmación + crea task ClickUp.
[link al perfil del médico en Bigin]
```

## Cuándo escalar (al sistema mismo)

- Si el envío a Slack falla (MCP error, rate limit) → notificar al usuario directamente en chat + email backup
- Si un channel no existe → sugerir creación antes de enviar
- Si un mention apunta a usuario que no está en el channel → ajustar mention o invitar al usuario primero

## Volumen y throttling

- Cada channel tiene threshold de volumen máximo:
  - `#qihealth-marketing-daily`: 1 mensaje principal/día (morning brief) + máximo 3 follow-ups
  - `#qihealth-medical-review`: bajo volumen — solo reviews (1-3/día)
  - `#qihealth-cofepris-flags`: bajo volumen — solo blocks/flags reales (1-3/día)
  - `#qihealth-competitor-alerts`: 4 alertas/día máximo (1 por scheduled task) salvo cambio mayor

Si el sistema detecta excedencia, hold y batch para siguiente check.
