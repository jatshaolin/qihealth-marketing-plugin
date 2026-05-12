---
name: one-pager-clinical
description: >
  This skill should be used to produce one-pager clinical documents (PDFs) for HCPs and medical partners. Triggers: "one-pager clínico", "one pager para médicos", "PDF clínico", "kit llévalo a tu consulta", "material para HCP", "leave-behind médicos". Produces 2-page PDF (front + back) with clinical evidence, MARD, AGP comparison, advisory medical review trigger, ready for printing or digital distribution.
metadata:
  version: "0.1.0"
  type: "production"
  format: "PDF 2 pages"
  audience: "HCP + Paciente"
---

# One-Pager Clinical Builder

Produces clinical one-pagers for two use cases:
1. **For HCPs** — leave-behind para consultorio que el médico revisa rápidamente
2. **For patients** — "Llévalo a tu consulta" — material que el paciente lleva al médico

## Mandatory loading

- `memory/cofepris-claim-library.md`
- `memory/product-catalog.md`
- `memory/competitors.md` (cuando aplique comparativa)

## Estructura — One-pager HCP

### Página 1 — Resumen ejecutivo clínico

**Encabezado**:
- Logo QiHealth
- Título: "QiTrax CGM + Dashboard Clínico"
- Subtítulo: "Información técnica para profesionales de la salud"

**Sección A — Sensor**:
- MARD (verificable con fuente)
- Duración: 14 días
- Calibración: no requerida
- Compatibilidad: app móvil + dashboard clínico

**Sección B — Dashboard clínico (diferenciador)**:
- IA predictiva (alertas tempranas)
- AGP report compatible
- Multi-biométrico (glucosa + sueño + actividad + composición)
- Acceso al médico vía link compartido por paciente

**Sección C — Evidencia y validación**:
- Registro COFEPRIS 2370E2025 SSA
- Advisory clínico (nombres + cédulas)
- Si hay datos clínicos publicados: cita con link

### Página 2 — Comparativa + programa partner

**Sección D — Comparativa con LibreView (Abbott)**:
Tabla honesta:
| Característica | QiHealth | LibreView |
|---|---|---|
| Sensor 14 días | ✓ | ✓ |
| AGP report | ✓ | ✓ |
| IA predictiva | ✓ | ✗ |
| Multi-biométrico | ✓ | ✗ |
| Coaching IA paciente | ✓ | ✗ |

**Sección E — Programa Partner Clínico**:
- Acceso dashboard gratuito
- 30 días de prueba para 5 pacientes
- Demo personalizada 30 min
- WhatsApp directo soporte técnico
- NO comisiones (reciprocidad sin riesgo ético)

**Sección F — Cómo agendar demo**:
- Calendly link (con Calendar de Luis)
- WhatsApp soporte
- Email comercial

**Footer**:
- Disclaimer regulatorio
- Versión + fecha de revisión médica
- Advisory firmante visible

## Estructura — One-pager Paciente ("Llévalo a tu consulta")

### Frente

**Headline**: "5 cosas que decirle a tu doctor sobre QiTrax"

**Body**: 5 bullets cortos que empoderan al paciente sin reemplazar al médico:
1. "Tengo factores de riesgo metabólico"
2. "Estoy considerando monitoreo continuo de glucosa"
3. "Quiero entender mis patrones, no diagnóstico"
4. "Existe QiHealth — sensor + dashboard donde tú ves mis datos"
5. "¿Qué opinas?"

### Reverso

**Para tu doctor**:
- 1 párrafo introductorio para el médico (qué es QiHealth)
- 3-4 bullets de funcionalidad clínica
- Link QR a one-pager HCP completo
- WhatsApp directo médicos
- Calendly demo

## Specs técnicos

- **Tamaño**: Letter (8.5" x 11") o A4 (depende mercado)
- **Páginas**: 2 (frente + reverso)
- **Formato**: PDF imprimible + versión digital (web embed)
- **Tipografía**: profesional (no marketing-y)
- **Colores**: brand QiHealth + alto contraste para lectura clínica

## Quality gates

- **OBLIGATORIO advisory médico review** antes de producir final
- cofepris-check sobre cada claim
- factual-review sobre MARD, comparativas, datos
- Legal review si comparativa frontal con Abbott

## Output format

Markdown estructurado con:
- Texto literal de cada sección
- Brief visual para diseñador (sin generar visual)
- Quality gates status
- Approval workflow

## Variantes específicas

### One-pager especialidades
- Endocrinología (foco DM2 + AGP)
- Internista (foco multi-factor riesgo metabólico)
- Médico del deporte (foco optimization + multi-biométrico)
- Nutriólogo clínico (foco postprandial + tracking)

## Cuándo escalar al humano

- TODO one-pager → advisory médico OBLIGATORIO
- Comparativa con LibreView → legal review
- MARD claim → factual-review con fuente verificable de Abbott
- Programa partner → Jose para términos legales
- Diseño final → diseñador senior on-call
