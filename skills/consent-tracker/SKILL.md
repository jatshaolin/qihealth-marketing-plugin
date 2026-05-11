---
name: consent-tracker
description: >
  This skill should be used to track and verify consents for testimonials, KOL agreements, and any content featuring real patients or HCPs. Triggers: "consent check", "verifica consentimiento", "consent verification", "testimonial autorizado", "pruebo consentimiento". Maintains registry of signed consents, validates before publishing testimonials, flags missing consents, escalates ambiguous cases.
metadata:
  version: "0.1.0"
  type: "operations"
  channel: "compliance"
---

# Consent Tracker

Sistema de tracking de consentimientos para testimoniales, KOLs, micro-pacientes y cualquier contenido con persona real. Critical para compliance + ética + legal.

## Mandatory loading

- `memory/strategy-v4.3-summary.md` (programa SEEDS + KOLs)

## Tipos de consentimiento

### A. Testimonial paciente
Persona real con diagnóstico verificable acepta:
- Aparecer en contenido (foto, video, voz)
- Uso por X canales (web, social, paid, presentaciones internas)
- Vigencia (típico 2 años, renovable)
- Derecho a retirar consentimiento futuro
- Información que aparecerá (nombre + edad + diagnóstico + ciudad)

### B. KOL médico
Profesional acepta:
- Co-creación de contenido (Doctor Reels, artículos)
- Uso de su nombre + especialidad + cédula
- Distribución cross-platform
- Términos de la relación (12+ meses con co-creación, no pago-por-post)
- Cláusulas de no-conflicto con competidores

### C. Micro-influencer (programa SEEDS)
Acepta:
- Recibir producto gratis 6 meses sin obligación de publicar
- Si publica, código de descuento personal
- Guidelines mínimas (claims médicos respaldados, #publicidad)
- Salida del programa libre en cualquier momento

### D. Empleado / colaborador interno
Acepta uso de imagen para contenido de marca interno y externo.

## Registry structure

```yaml
consents_registry:
  - id: "CONSENT-001"
    type: "testimonial"
    person_name: "María González"
    person_email: "[contact]"
    
    diagnostico_verificable: 
      condition: "DM2"
      doctor_attesting: "Dr. Jorge Pérez"
      verification_method: "Resultado lab fotografía"
    
    consent_scope:
      - web QiHealth (homepage + testimonios)
      - Instagram orgánico
      - Paid Meta (FB+IG)
      - Email marketing
      - Presentaciones internas
    
    NOT_allowed:
      - LinkedIn (no consintió)
      - Imprenta física
      - Reventa de imagen
    
    duration: "2 años desde firma"
    signed_date: "2026-05-10"
    expiry_date: "2028-05-10"
    
    legal_form_link: "[Drive link al PDF firmado]"
    
    revocation:
      can_revoke: true
      revocation_email: "[contact for revocation requests]"
      revoked: false
```

## Verificación antes de uso

Antes de publicar contenido con persona real, ejecutar verification:

### Paso 1 — Lookup en registry
Persona en cuestión: ¿tiene consent activo?

### Paso 2 — Verificar scope
El uso específico que se va a hacer: ¿está en el scope autorizado?
- Si testimonial fue para "web + Instagram" y se quiere usar en LinkedIn → NO, requiere consent adicional

### Paso 3 — Verificar vigencia
¿Está dentro del período de 2 años?
- Si expiró → NO publicar, solicitar renovación

### Paso 4 — Verificar revocación
¿Persona ha solicitado retirar consent en algún momento?
- Si sí → NO publicar, retirar contenido existente

### Paso 5 — Output

```
=== CONSENT CHECK ===
Person: María González
Use case: Reel testimonial para paid Meta

✅ Consent activo
✅ Scope incluye "paid Meta"
✅ Vigencia OK (hasta 2028-05-10)
✅ No revocado

STATUS: APPROVED
NEXT: Pieza puede proceder a quality gates restantes.
```

O en caso de problema:

```
=== CONSENT CHECK ===
Person: Juan Carlos Ruiz
Use case: Foto en blog SEO para LinkedIn

⚠️ ISSUE DETECTED
- Consent existe pero scope NO incluye "LinkedIn"
- Para usar en LinkedIn, requiere consent adicional o ampliación

STATUS: BLOCKED
ACTION REQUIRED:
1. Contactar Juan Carlos para extender scope
2. O usar imagen genérica en lugar de testimonial real
3. NO publicar hasta resolver
```

## Casos especiales

### Doctor Reel con médico advisory
- Asumir consent inicial al unirse al advisory
- Pero validar scope: ¿incluye TikTok? ¿LinkedIn? ¿uso comercial?
- Si dudas, validar con médico antes

### Testimonial de hijo de diabético (Legacy)
- Si menciona al padre: requiere TAMBIÉN consent del padre (privacidad familiar)
- Si padre falleció: validar con sucesión legal o usar foto que no lo identifique directamente

### Imagery sintética que parezca persona real
- NO requiere consent legal (no es persona real) PERO requiere disclaimer
- "Imagen generada por IA, no representa paciente real"
- Si la imagen sintética parece DEMASIADO real y podría confundirse → re-generar con menos realismo

## Storage

Registry en Drive folder seguro: `/QiHealth/legal/consents-registry/`
- Cada consent: PDF firmado + entry en master registry (Notion DB o YAML)
- Backup mensual

## Cuándo escalar al humano

- Cualquier ambigüedad de scope → asesoría legal
- Solicitud de revocación → comunicar a Jose + retirar contenido inmediatamente
- Solicitud de uso fuera de scope → buscar extension o buscar alternativa
- Persona fallecida → asesoría legal + sucesión
- Conflicto con consent previo en agencia anterior → Jose para resolución
