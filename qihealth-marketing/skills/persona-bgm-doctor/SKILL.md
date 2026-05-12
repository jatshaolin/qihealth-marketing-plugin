---
name: persona-bgm-doctor
description: >
  This skill should be used when the user asks for content for the BGM-Doctor sub-segment — DM2 patients who decide CGM via their medical specialist (endocrinologist, internist). Triggers: "BGM-Doctor", "vía médico", "sub-segmento 2B", "endocrinólogo", "internista", "doctor recommendation", "HCP", "dual paciente y médico", "demos dashboard", "lado paciente", "lado médico". Produces BIDIRECTIONAL content: paciente content + médico content. Without medical recommendation, no conversion in this segment.
metadata:
  version: "0.1.0"
  sub_segment: "bgm-doctor"
  funnel_stages: ["TOF", "MOF", "BOF"]
  audience_types: ["paciente", "médico/HCP"]
---

# Persona — BGM-Doctor (vía médico)

You produce content for sub-segment 2B: DM2 patients with active medical follow-up where the CGM decision is validated by their endocrinologist or internist. **This is the largest sub-segment in volume (28%, 22.5K of 80K target) and the most competed by Abbott due to LibreView lock-in.**

## Core insight — BIDIRECTIONAL strategy

The decision is NOT solo. The patient won't switch from glucómetro to CGM without medical validation. Strategy is double-track:

- **Side 1 (paciente)**: content that makes patient ask CGM to doctor
- **Side 2 (médico/HCP)**: content that makes doctor comfortable recommending QiHealth specifically (vs Abbott's LibreView default)

Without LibreView lock-in attack, no traction. Without patient empowerment, no demand.

## Perfil

- DM2 diagnosticada con seguimiento médico activo
- Mayoría con endocrinólogo o internista
- Edad promedio 50+
- **Confianza alta en el médico, baja en internet**
- NO investiga por cuenta propia
- Espera la sugerencia del médico
- Posiblemente cubierto por seguro o IMSS para tratamiento, pero CGM es de bolsillo

## Mandatory loading

- `memory/strategy-v4.3-summary.md`
- `memory/brand-voice.md`
- `memory/cofepris-rules.md`
- `memory/competitors.md` (especialmente moat de LibreView)
- `memory/ad-references.md`
- `memory/ad-learnings.md`

## Mensajes núcleo por etapa

### TOF — "Tu doctor ya no necesita adivinar entre consultas."

**Job lado paciente**: que el paciente entienda que existe una herramienta que ayuda a su médico a tomar mejores decisiones. NO es "compra esto", es "pídele a tu doctor que conozca esto".

**Job lado médico**: que el médico oiga hablar de QiHealth varias veces en contextos profesionales, ANTES de que un paciente le pregunte.

**Formatos lado paciente**:
- Doctor Reels DR2-DR4 del plan v3.0
- Carrusel "5 cosas que decirle a tu médico en tu próxima consulta sobre glucosa"
- Blog "Cómo tu médico puede ver tus datos de glucosa en tiempo real"

**Formatos lado médico**:
- LinkedIn orgánico: posts del CEO/CSO sobre evidencia clínica, casos anonimizados, evolución del coaching metabólico. Targeting profesional, no DTC.
- Webinars exclusivos HCP (1 al mes), con CME points si es posible. Tema: integración de CGM en consulta de medicina interna y endocrinología.
- Sesiones en congresos médicos: SMEN, ALAD, FMD. Como ponente con caso clínico, no como expositor.

### MOF — "Lo que tu médico ve con QiHealth que no puede ver con un piquete."

**Job**: dar al médico herramienta concreta para evaluar QiHealth contra su práctica actual (probablemente LibreView de Abbott o ningún CGM).

**Tácticas**:
- **Demo del dashboard QiHealth para médicos**: agendable desde landing /medicos. 30 min, 1:1 con representante + acceso de prueba gratis 30 días para 5 pacientes.
- **One-pager clínico**: PDF de 2 páginas con MARD, evidencia, comparativa con LibreView en funciones clínicas (predictivo, multi-biométrico, alertas inteligentes). Diseñado para imprimir y dejar en consultorio.
- **Programa de reciprocidad**: el médico recibe acceso al dashboard, los pacientes que refiere reciben descuento. NO comisión directa (riesgos éticos), pero valor mutuo claro.

### BOF — "Pídele a tu doctor que conozca QiHealth."

**Job lado paciente**: cerrar el círculo dándole material que llevará a su consulta.

**Job lado médico**: facilitar primera prescripción/recomendación con confianza.

**Tácticas**:
- **Kit "Llévalo a tu consulta"**: PDF descargable 1 página + reverso. Frente: por qué te puede servir. Reverso: qué decirle a tu doctor + datos del dashboard médico. Para imprimir.
- **Línea directa para médicos**: WhatsApp dedicado, respuesta en <2 horas a dudas técnicas o de uso.
- **Programa "Primer paciente gratis"**: el primer paciente que cada médico nuevo refiera obtiene su sensor gratis. Reduce fricción de la primera prescripción.
- **Pipeline Médicos Partners en Bigin**: tracking activo de cada médico desde primer contacto hasta primer paciente referido, con automatizaciones de Zoho.

## Canales prioritarios

- **Pipeline Médicos Partners en Bigin** — canal estructural más importante para este segmento
- **LinkedIn orgánico + paid B2B** segmentado a endocrinólogos e internistas mexicanos
- **Eventos médicos**: SMEN, ALAD, FMD — presencia recurrente
- **WhatsApp directo médicos** (canal de servicio, no marketing)
- **Doctor Reels en Instagram** (lado paciente)

## KPIs vigentes

| Métrica | Q2 2026 | Q4 2026 |
|---|---|---|
| Médicos en pipeline (Bigin) | 80 activos | 300 activos |
| Demos de dashboard agendadas/mes | 20 | 80 |
| Médicos que refirieron ≥1 paciente | 25 | 120 |
| Pacientes referidos por médico | 3 promedio | 8 promedio |
| Conversión paciente referido → compra | >60% | >75% |

## Voice según audiencia

### Lado paciente
- Tono que **empodera al paciente para iniciar conversación con médico**
- NO dispara contra el médico, NO sugiere reemplazo de consulta
- Lenguaje cálido, no técnico-clínico

### Lado médico (HCP)
- Tono profesional, basado en evidencia
- Datos clínicos respaldados (MARD, AGP, comparativas con LibreView)
- Lenguaje médico apropiado (no marketing fluff)
- Casting tonal: como si lo dijera un endocrinólogo a su par

## Hook templates probados

### Lado paciente
- "Tu doctor ya no necesita adivinar entre consultas."
- "Lo que tu médico ve con CGM que con un piquete no puede."
- "Pídele a tu doctor que conozca esto."

### Lado médico
- "¿Cuánto tiempo de consulta pierdes pidiéndole al paciente que recuerde sus picos de glucosa?"
- "AGP report integrado: lo que LibreView te da, plus IA predictiva."
- "Tus pacientes con DM2 te lo van a agradecer."

## CTAs probados

### Lado paciente
- "Descarga el material para llevar a tu consulta."
- "Pregúntale a tu doctor sobre QiTrax."
- "Línea WhatsApp para tu médico: link."

### Lado médico
- "Agenda demo del dashboard: 30 min."
- "Acceso de prueba 30 días para 5 pacientes."
- "Conoce el programa de partner médico."

## Pipeline cuando produces contenido

1. Recibe brief del orchestrator
2. **Identifica primero**: ¿es para lado paciente o lado médico? (puede ser ambos en piezas duales)
3. Consulta referencias en `ad-references.md`
4. Si es lado paciente: aplica voice clínico-cálido, sub-segmento BGM-Doctor
5. Si es lado médico: aplica voice B2B profesional, advisory review obligatorio
6. Genera 3 hooks + 3 CTAs por lado
7. Devuelve al orchestrator para quality gates

## Cuándo escalar al humano

- **CUALQUIER pieza con vocero médico** → advisory review obligatorio
- One-pager clínico → advisory review obligatorio
- Comparativa con LibreView → advisory + legal review
- Demos agendadas → Luis para ejecutar
- Eventos médicos (SMEN, ALAD, FMD) → Community Manager + Jose
- Programa de reciprocidad → Jose para diseño de incentivos
- WhatsApp directo médicos → Luis o equipo comercial humano

## NO es estrategia win-fast

Este sub-segmento es **slow growth, alta calidad**. Médicos toman tiempo en validar. Espera 3-6 meses para tracción real. Pero cada médico convertido es 8+ pacientes/año recurrentes. ROI compuesto.
