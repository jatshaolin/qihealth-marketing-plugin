---
name: email-sequence-builder
description: >
  This skill should be used to build multi-email sequences for QiHealth nurturing and lifecycle. Triggers: "email sequence", "secuencia de emails", "drip campaign", "email nurture", "post-purchase emails", "welcome series", "email para [sub-segmento]", "follow-up emails". Produces complete sequences with timing, branching logic, subject lines, body copy, CTAs, and exit conditions. Output ready for Zoho Campaigns or similar.
metadata:
  version: "0.1.0"
  type: "production"
  format: "Email sequence"
---

# Email Sequence Builder

Build complete email nurturing and lifecycle sequences for QiHealth. Output to Zoho Campaigns or similar email platform.

## Mandatory loading

- `memory/strategy-v4.3-summary.md`
- `memory/brand-voice.md`
- `memory/cofepris-rules.md`
- `memory/product-catalog.md`
- The persona skill of target sub-segment

## Tipos de secuencias

### A. Welcome series (post-signup)
5 emails en primeros 14 días post-email-capture. Onboarding emocional, no clínico.

### B. Post-purchase Insight 15 (No-Measurers)
5 emails durante los 15 días del producto. Cierre con upgrade a membresía.

### C. Post-purchase Plan Legacy (Legacy)
5 emails primer mes. Anclados en familia.

### D. Pre-webinar (todos sub-segmentos)
3 emails antes del webinar (T-7, T-3, T-0).

### E. Post-webinar (todos sub-segmentos)
3 emails post-webinar (replay + nurture + offer).

### F. Re-engagement (lead frío >30 días)
3 emails con contenido nuevo + soft offer.

### G. Cancelación / churn save
2 emails (intent de cancelar → propuesta de ajuste).

### H. Hand-off comercial (a Luis)
Notification a médico/lead con info de demo + recordatorio T-1 día.

## Estructura por email

```yaml
email:
  sequence_name: "Welcome — No-Measurers"
  trigger: "Email capture vía quiz '¿Estás en riesgo?'"
  position: 1 of 5
  send_timing: "Inmediato post-signup"
  
  subject_line:
    primary: "Bienvenido a entenderte (no a alarmarte)"
    variant_a: "Tu reporte de riesgo está listo"
    variant_b: "Lo que viene en los próximos 14 días"
  
  preheader: "Tu primer paso para conocer tu metabolismo"
  
  body:
    intro: |
      Hola [Nombre],
      
      Te suscribiste al quiz "¿Estás en riesgo?" hace un momento. Tu reporte personalizado lo encuentras al final de este email.
    
    section_1:
      content: |
        Antes que nada: este reporte NO es diagnóstico. Es información que vale la pena conocer para conversar mejor con tu médico (o decidir si vale la pena ir).
      
    section_2:
      content: |
        En los próximos 14 días te voy a compartir [N] piezas de info que te van a ayudar a entender tu metabolismo. Sin alarmismo, sin marketing fluff, sin promesas vacías.
    
    cta:
      text: "Lee tu reporte completo"
      link: "[link al PDF del reporte]"
      style: "primary button"
  
  footer:
    signature: "Equipo QiHealth"
    disclaimer: "Este contenido es educativo. No sustituye consulta médica."
    unsubscribe: "[link estándar]"
  
  exit_conditions:
    - "User unsubscribes"
    - "User converts to Insight 15"
```

## Secuencias específicas por sub-segmento

### Welcome No-Measurers (5 emails)

| Email | Día | Subject | Tema central |
|---|---|---|---|
| 1 | T+0 | "Bienvenido a entenderte" | Reporte del quiz + intro emocional |
| 2 | T+2 | "5 cosas que vas a descubrir" | Educación sobre CGM |
| 3 | T+4 | "Lo que me sorprendió en mis 15 días" | Story de descubrimiento (testimonial) |
| 4 | T+7 | "Tu primer CGM con coach" | Oferta Insight 15 con timing |
| 5 | T+10 | "Última info antes de decidir" | Recap + objection handling + CTA fuerte |

### Welcome Legacy (5 emails)

| Email | Día | Subject | Tema central |
|---|---|---|---|
| 1 | T+0 | "Lo que viste en tu papá no es tu destino" | Bienvenida emocional |
| 2 | T+2 | "Lo que la ciencia dice sobre genética" | Educación: 50/50 explicado |
| 3 | T+4 | "Lo que mi papá no pudo medir" | Story de prevención |
| 4 | T+7 | "Plan Legacy + bundle familiar" | Oferta Plan Legacy con upsell padre |
| 5 | T+10 | "Cuídate como tu papá no pudo" | Emotional close + CTA |

### Post-purchase Insight 15

| Email | Día | Subject | Tema |
|---|---|---|---|
| 1 | T+0 | "Tu sensor llega [fecha]" | Onboarding lo que viene |
| 2 | T+1 | "Aplicación del sensor (video)" | Tutorial visual |
| 3 | T+7 | "Mid-point: qué patrones estás viendo" | Check-in + tips |
| 4 | T+13 | "Tu reporte final está casi listo" | Anticipo del reporte |
| 5 | T+15 | "Tu reporte + el siguiente paso" | Upgrade to membresía |

### Pre-webinar (3 emails)

| Email | Día | Subject |
|---|---|---|
| 1 | T-7 | "Confirma tu lugar: webinar [tema]" |
| 2 | T-3 | "Lo que vas a aprender en el webinar" |
| 3 | T-0 (1h antes) | "Tu link de Zoom para hoy" |

## Reglas COFEPRIS en emails

Mismas que cualquier contenido — cofepris-check obligatorio antes de envío. Especial atención a:
- NO claims de cura en emails post-purchase
- NO comparaciones cuantitativas con Abbott sin fuente
- NO promesas de pérdida de peso o "transformación"
- Disclaimers obligatorios en pie de cada email

## Specs técnicos

- **Width**: 600px max (mobile responsive)
- **Plain text + HTML versions**
- **Pre-header**: 50-100 caracteres (visible en preview)
- **Subject**: 30-50 caracteres óptimo
- **CTAs**: máximo 1 primary por email + 1-2 secondary
- **Imágenes**: alt-text obligatorio
- **Links**: UTM tags para attribution

## Output format

```markdown
# EMAIL SEQUENCE — [Tipo] — [Sub-segmento]

**Trigger**: [...]
**Total emails**: 5
**Timing**: [...]

## Email 1 — T+0
**Subject**: "[subject]"
**Preheader**: "[preheader]"
**Body**:
[texto completo]

**CTA**: "[texto]" → [link]

[Variantes A/B del subject]

## Email 2 — T+2
[...]

## Branching logic
- If user clicks CTA email 4 → skip email 5, send "thank you for considering"
- If user opens email 3 but doesn't click → resend variant subject

## Exit conditions
- Unsubscribe
- Convert to product
- 30 días sin opens (mover a re-engagement)
```

## Quality gates

- cofepris-check (cada email)
- brand-voice-qihealth
- factual-review (si hay datos)
- Spam score test (Mail-Tester o similar)
- Mobile preview test

## Cuándo escalar al humano

- Email a HCP (B2B) → advisory + legal review
- Email post-cancel con offer de retención → Jose
- Email con testimonial de paciente real → consent-tracker
- Mass unsubscribe spike → investigate causa
