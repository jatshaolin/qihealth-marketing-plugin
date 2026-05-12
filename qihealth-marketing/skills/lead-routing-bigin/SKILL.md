---
name: lead-routing-bigin
description: >
  This skill should be used to route incoming leads in Bigin CRM by sub-segment and intent. Triggers: "lead routing", "etiqueta lead Bigin", "asignar pipeline", "categorize new lead", "lead nuevo". Reads lead data, infers sub-segment from form responses + behavioral signals, assigns to correct Bigin pipeline (DTC Consumidor / Médicos Partners / Empresas B2B / Farmacias B2B / Marketplace), tags with metadata, triggers email/WhatsApp follow-up via Zoho.
metadata:
  version: "0.1.0"
  type: "operations"
  channel: "CRM"
---

# Lead Routing — Bigin

Etiqueta y enruta leads nuevos automáticamente en Bigin. Crítico para que cada lead reciba el flow correcto (email + WhatsApp + commercial handoff).

## Mandatory loading

- `memory/strategy-v4.3-summary.md` (5 pipelines + criterios sub-segmento)
- `memory/product-catalog.md`

## MCPs requeridos

- Bigin (read + write)
- Zoho Campaigns (trigger email sequence)
- Slack (notificación si lead caliente)
- ClickUp (task creation)

## Pipelines Bigin

1. **DTC Consumidor** — pacientes B2C
2. **Médicos Partners** — HCPs (BGM-Doctor lado médico)
3. **Empresas B2B** — corporativos para programa salud metabólica
4. **Farmacias B2B** — distribución
5. **Marketplace** — leads de marketplaces como ML / Amazon

## Inferencia de sub-segmento

Cuando un lead nuevo entra a Bigin (vía form, checkout, webinar signup, quiz), inferir sub-segmento por:

### Form fields explícitos
- "¿Cómo te mides actualmente?":
  - Con CGM (Abbott u otro) → **CGM-Switchers**
  - Con glucómetro → **BGM-Self** (a menos que también marque "vía médico")
  - No me mido → **No-Measurers**

- "¿Tienes familiar directo con diabetes?"
  - Sí (padre/madre) + edad 30-50 + no me mido → **Legacy** (alta probabilidad)
  - Sí + ya me mido → mantener sub-segmento de mido, tag "legacy-influence" como secondary

- "¿Eres profesional de la salud?"
  - Sí + especialidad médica → **Médicos Partners**

### Source de lead (UTM tags)
- UTM_source: quiz → No-Measurers o Legacy según content del quiz
- UTM_source: comparativa-switch → CGM-Switchers
- UTM_source: webinar-legacy → Legacy
- UTM_source: webinar-bgm-self → BGM-Self
- UTM_source: linkedin-hcp → Médicos Partners

### Behavioral signals (post-signup tracking)
- Páginas visitadas recientemente:
  - /switch → CGM-Switchers
  - /legacy → Legacy
  - /medicos → BGM-Doctor (lado médico)
  - /pre-diabetes-mexico → No-Measurers
  - /glucometro-vs-cgm → BGM-Self

### Email domain
- @hospital, @clinica, @medicalcenter → Médicos Partners
- @empresa corporativa → Empresas B2B
- Email personal (gmail/hotmail) → DTC default

## Proceso de routing

### Paso 1 — Lead enters Bigin
Lead source y data se capturan.

### Paso 2 — Inference engine
- Aplicar reglas explícitas (form fields)
- Aplicar reglas behaviorales (UTM + pages visited)
- Score confidence (alta / media / baja)

### Paso 3 — Asignación
- Si confidence ALTA → asignar pipeline + tag sub-segmento
- Si confidence MEDIA → asignar tentativo + flag para review manual
- Si confidence BAJA → assign default (DTC Consumidor) + tag "needs-segmentation-review"

### Paso 4 — Tagging
Tags estándar en Bigin:
- `sub-{cgm-switchers / bgm-self / bgm-doctor / no-measurers / legacy}`
- `source-{quiz / webinar / blog / paid-meta / paid-tiktok / linkedin / referral}`
- `funnel-{tof / mof / bof}`
- `intent-{high / medium / low}` (basado en behavior)
- `temperature-{cold / warm / hot}`

### Paso 5 — Trigger automation
- Lead asignado a Médicos Partners + intent HIGH → notificación a Luis + agendar primer touch
- Lead DTC + intent HIGH → trigger welcome sequence en Zoho
- Lead con behavior de "ready-to-buy" → notificación a #qihealth-leads-hot + manual review
- Lead frío → assign owner (rotation entre equipo comercial), email nurture

### Paso 6 — Notificación
- Slack #qihealth-marketing-pipeline si lead notable (high value, KOL conocido, etc.)
- Email diario summary a Performance Manager con lead count

## Output al routing

```yaml
lead:
  bigin_id: "leads-12345"
  name: "Juan Pérez"
  email: "juan@example.com"
  
  routing:
    pipeline: "DTC Consumidor"
    sub_segment: "Legacy"
    sub_segment_confidence: "high"
    funnel_stage: "MOF"
    intent: "medium"
    temperature: "warm"
  
  tags:
    - "sub-legacy"
    - "source-webinar"
    - "funnel-mof"
    - "intent-medium"
    - "temperature-warm"
  
  triggers_fired:
    - "welcome_sequence_legacy_v1"
    - "email_1_immediate"
    - "next_email_t+2_days"
  
  notifications:
    - channel: "Slack #qihealth-marketing-pipeline"
      message: "Nuevo lead Legacy desde webinar — Juan Pérez"
  
  owner: "AI nurture (DTC team)"
  next_action: "Welcome email enviado. Re-evaluar intent en T+7 días."
```

## Casos especiales

### Lead que es competidor (mystery shopping)
- Detección: dominio de Abbott México, Sibionics, agencia de research
- Action: mover a pipeline "Excluded" + tag "competitor-recon"
- NO disparar follow-up automation

### Lead duplicado
- Detección: misma email/phone ya existe en otro pipeline
- Action: merge con lead existente, mantener historial, no disparar nueva welcome

### Lead que pide unsubscribe en welcome email
- Action: respetar inmediato, mover a "Unsubscribed", no re-engage por 6 meses

### Lead que responde con interés clínico (no comercial)
- Pregunta médica seria → forward a advisory + community manager
- NO mover a sales pipeline aún — primero servicio

## Cuándo escalar al humano

- Lead que NO encaja en ninguna inferencia clara → manual review
- Lead que es KOL o personalidad reconocida → Jose + community manager
- Lead con queja o crisis → community manager
- Lead duplicado con historial complejo → manual merge
- Volume spike anómalo → investigar causa (bot? campaña viral? bug?)
