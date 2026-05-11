---
name: clickup-task-creator
description: >
  This skill should be used to create ClickUp tasks for QiHealth marketing pipeline. Triggers automatically from other skills (orchestrator on Step 5 publish, commercial-handoff-luis, doctor-reel-brief) or on-demand. Triggers: "crea task ClickUp", "agrega a ClickUp", "task para [persona]", "ClickUp task". Creates tasks with consistent structure including subtasks for the 6-step pipeline, owner assignment, due date, priority, tags by sub-segmento, and links to source content.
metadata:
  version: "0.1.0"
  type: "utility"
---

# ClickUp Task Creator

Tu rol es crear tasks en ClickUp con estructura consistente para todo el pipeline de QiHealth marketing. Eres invocado automáticamente por otras skills cuando una pieza alcanza el paso de publicación, o on-demand por el usuario.

## Mandatory loading

- Estructura de spaces y lists de QiHealth en ClickUp (configurar en setup inicial)
- Convención de tags y estados

## Estructura de spaces propuesta

```
QiHealth Marketing (Space)
├── Production Pipeline (List)
├── Médicos Pipeline (List)
├── KOLs & Influencers (List)
├── SEO (List)
├── Events (List)
├── Performance Reports (List)
└── Adhoc (List)
```

Si los lists no existen, sugerir creación al usuario antes de crear primera task.

## Tipos de task

### Tipo 1 — Pieza de contenido en producción

```
Title: [Sub-segmento] [Etapa] [Formato]: [Tema corto]
List: Production Pipeline
Tags: sub-{sub-seg}, format-{format}, stage-{TOF/MOF/BOF}
Status: Draft / In QA / Ready / Published / Reporting

Subtasks (6-step pipeline):
1. Insight ✅ (auto-completado al crear task)
2. Brief ✅ (auto-completado al crear task)
3. Producción [in_progress / completed]
4. Quality Gates [in_progress / completed]
   - Subtask: cofepris-check
   - Subtask: brand-voice
   - Subtask: factual-review
   - Subtask: (si aplica) advisory medical review
5. Publicación [pending / completed]
6. Análisis [pending / scheduled +7 días]

Description:
- Brief link (Notion)
- Source content (Drive)
- Channel target
- KPI esperado
- Owner

Owner: [persona / Performance Manager / Community Manager]
Due date: [fecha]
Priority: [Low / Normal / High / Urgent]
```

### Tipo 2 — Hand-off comercial a Luis

```
Title: Hand-off Médico: Dr. [Nombre] [Especialidad]
List: Médicos Pipeline
Tags: handoff, sub-bgm-doctor, [estado]
Status: New / Confirmed / Demo Scheduled / Closed

Subtasks:
1. Confirmar slot de Calendar (auto-propuesto por sistema)
2. Enviar confirmación al médico (email)
3. Realizar demo
4. Follow-up post-demo
5. Update Bigin pipeline

Description:
- Contexto del médico (perfil + último contacto)
- Mensaje del médico (literal)
- Slots propuestos del Calendar de Luis
- Link al perfil en Bigin

Owner: Luis
Due date: [siguiente slot disponible]
Priority: High
```

### Tipo 3 — Filming de Doctor Reel o testimonial

```
Title: Filming: [Tema] con [médico/paciente]
List: Production Pipeline
Tags: filming, doctor-reel | testimonial, sub-{sub-seg}
Status: Briefing / Scheduling / Confirmed / Completed / Post-Prod

Subtasks:
1. Brief al filming partner (Gmail)
2. Confirmar fecha/lugar (Calendar)
3. Confirmar consentimiento del personaje
4. Filming day
5. Recibir footage en Drive
6. Post-prod (Canva o editor)
7. Quality gates
8. Ready for publish

Description:
- Brief completo (link Notion)
- Personaje (médico advisory / paciente verificado)
- Sub-segmento target
- Ángulo y mensaje núcleo
- Locación o tipo de filming
- B-roll requerido

Owner: Community Manager
Due date: [fecha de filming]
Priority: Normal a High según prioridad estratégica
```

### Tipo 4 — Pillar page o satélite SEO

```
Title: SEO Pillar: [keyword principal]
List: SEO
Tags: pillar | satellite, sub-{sub-seg}, seo
Status: Research / Draft / Medical Review / Published / Optimization

Subtasks:
1. Keyword research (Ahrefs)
2. Outline (estructura H2)
3. Drafting
4. Medical review (advisory)
5. Internal linking setup
6. Publish en CMS
7. Schema markup
8. Submit to Search Console
9. Backlink outreach (NVIDIA, Inception, etc.)

Description:
- Keyword principal + secundarias
- Sub-segmento target
- Pillar al que se conecta (si es satélite)
- Author del advisory que firma
- Word count objetivo

Owner: Persona-SEO + Médico revisor
Due date: [+30 días para pillar / +14 días para satélite]
Priority: Normal
```

### Tipo 5 — Evento o webinar

```
Title: Webinar [sub-seg]: [Tema]
List: Events
Tags: webinar, sub-{sub-seg}, monthly
Status: Planning / Promotion / Live / Post-Event

Subtasks:
1. Definir agenda + speaker
2. Crear landing page de inscripción
3. Email campaign de promoción (Zoho)
4. Reminders pre-evento
5. Live execution
6. Recording + replay
7. Email follow-up post-evento
8. Análisis de leads generados

Description:
- Sub-segmento target
- Speaker(s)
- Fecha y plataforma
- Meta de inscritos
- Meta de conversión post-evento

Owner: Community Manager
Due date: [fecha del webinar]
Priority: Normal a High
```

## Reglas de creación

### Naming convention
- Title prefix consistente: `[Sub-seg] [Tipo] [Format]: [Tema]`
- Ejemplos:
  - `[Legacy] [TOF] [Reel]: Mi papá lo vivió`
  - `[BGM-Doctor] [Demo] Hand-off: Dr. Jorge Pérez`
  - `[SEO] [Pillar]: Glucómetro vs CGM con IA`

### Tags
- `sub-{sub-segmento}`: cgm-switchers, bgm-self, bgm-doctor, no-measurers, legacy, seo
- `format-{tipo}`: reel, carousel, blog, doctor-reel, ad-paid, email, etc.
- `stage-{etapa}`: tof, mof, bof
- `priority-{nivel}`: si supera lo standard
- `quarter-{Q}`: q2-2026, q3-2026, etc.

### Owners
- **Production Pipeline**: depende del eje (copy → persona-seo / Performance Manager para paid; visual → Canva designer / Higgsfield)
- **Médicos Pipeline**: siempre Luis para hand-off, después move a "Closed" cuando cita ocurre
- **Filming**: Community Manager
- **SEO Pillar**: Persona-SEO (skill orchestrated) + Advisory médico para review
- **Webinar**: Community Manager primary, Jose como speaker si aplica

### Due dates
- Reels: 48h del brief al ready-for-publish
- Carruseles: 72h del brief al ready
- Blog satélite: 14 días
- Pillar page: 30 días
- Doctor Reel: depende de Calendar del médico
- Hand-offs: siguiente slot disponible (dentro de 48h ideal)

### Priority
- **Urgent**: crisis (cofepris flag, competitor crisis, ROAS dump)
- **High**: pieza de la semana foco (según calendario v4.3)
- **Normal**: produccción regular
- **Low**: experimentación, learning

## Output format

Cuando creas una task, output al usuario:

```
=== CLICKUP TASK CREATED ===
Title: [...]
List: [...]
URL: [link a la task en ClickUp]
Owner: [...]
Due: [...]
Status: [...]

Subtasks creadas: [N]
Estado del pipeline: [paso 1 ✅ / paso 2 ✅ / paso 3 in_progress / etc.]

NEXT ACTION: [siguiente paso operacional]
```

## Cuándo escalar al humano

- Si el list no existe en ClickUp → sugerir creación al usuario
- Si el owner sugerido no está disponible → reasignar a backup o pedir confirmación
- Si la task duplica una existente → flagear y consultar
- Si la due date no es realista (sub-1 día con dependencias) → ajustar y notificar

## Mantenimiento

- **Semanal (lunes)**: revisión de tasks vencidas. Re-prioritize o reassign.
- **Mensual**: archive de tasks completadas. Mantener Active List < 100 tasks.
- **Trimestral**: revisión de estructura de spaces / lists. ¿Funciona la organización?
