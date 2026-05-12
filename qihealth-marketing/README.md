# QiHealth Marketing — Sistema Agéntico

Plugin interno de QiHealth para Claude Cowork. Reemplaza la operación de agencia tradicional con un orquestador + 6 personas especializadas alineadas con la Estrategia de Contenido v4.3 (5 sub-segmentos × 3 etapas funnel = 15 celdas operativas).

## Qué hace

Este plugin opera como un equipo de marketing completo:

- Produce contenido orgánico para TikTok, Instagram, Facebook, LinkedIn y blog SEO
- Genera variantes de paid media para Meta Ads, TikTok Ads y Google Ads
- Mantiene un loop de iteración de anuncios con feedback humano en lenguaje natural
- Vigila competencia continuamente: Abbott (FreeStyle Libre) y Sibionics México
- Construye listas de médicos endocrinólogos/internistas y los contacta, pasando leads calientes al equipo comercial
- Ejecuta SEO completo (keyword research, pillar pages, satélites, backlinks)
- Aplica quality gates obligatorios: COFEPRIS compliance, brand voice QiHealth, factual review

## Componentes principales

### Personas (6)

Una por sub-segmento de la estrategia v4.3, más una transversal de SEO:

- `persona-cgm-switchers` — usuarios actuales de Abbott
- `persona-bgm-self` — glucómetro DIY
- `persona-bgm-doctor` — vía médico
- `persona-no-measurers` — sin medir
- `persona-legacy` — hijos de diabéticos
- `persona-seo` — transversal, autoridad clínica E-E-A-T

### Quality Gates (3)

- `cofepris-check` — gate obligatorio antes de publicación
- `brand-voice-qihealth` — tono clínico-cálido
- `factual-review` — verifica cifras, citas, fuentes

### Producción de contenido

Reels (TikTok + IG), carruseles, scripts de Doctor Reels, landing pages, anuncios paid (Meta + TikTok), pillar pages SEO, artículos satélite, email sequences, WhatsApp flows, quizzes interactivos, one-pagers clínicos.

### Iteración de anuncios

Loop completo: monitor de performance → clasificación winner/loser/fatiga → feedback en lenguaje natural → variantes nuevas en menos de 24 horas.

### Operaciones

Morning brief automático (Lun-Vie 7:00 AM), competitor watch cada 6h, lead routing en Bigin, hand-off comercial a Luis con cita en Calendar.

## Cómo empezar

### Instalación vía Cowork Marketplace (recomendado)

1. Push de este repo a GitHub privado de QiHealth (ver `GITHUB-SETUP.md` para guía paso a paso)
2. En Cowork Desktop → **Settings → Plugins → Add Marketplace**
3. URL del repo: `https://github.com/qihealth/qihealth-marketing-plugin`
4. Install el plugin
5. Conectar MCPs del usuario: Slack, Notion, Google Drive, Gmail, Calendar, ClickUp, Bigin (Zoho), Zoho Desk, Apify, Apollo, Canva, Ahrefs, Supermetrics
6. Cargar credenciales de Meta Ads y TikTok Ads (cuando estén disponibles)
7. Invocar el orquestador desde cualquier conversación de Cowork: `/qihealth-marketing [tu pedido]`

### Updates futuros

Cuando se agreguen skills o se actualicen archivos de memoria:
- Editar archivo
- `git add . && git commit -m "..." && git push`
- Cowork detecta auto la nueva versión y ofrece update

Ver `GITHUB-SETUP.md` para detalles completos.

## Personas

El orquestador detecta automáticamente el sub-segmento del pedido y carga la persona correspondiente. También puedes invocar una persona directamente.

## Memoria del plugin

El plugin opera con memoria persistente cargada al inicio:

- `memory/strategy-v4.3.md` — Estrategia de Contenido completa
- `memory/brand-voice.md` — Tono y lenguaje QiHealth
- `memory/cofepris-rules.md` — Claims permitidos y prohibidos
- `memory/competitors.md` — Perfil de Abbott + Sibionics México
- `memory/kpis-by-segment.md` — Targets Q2 y Q4 2026 por sub-segmento
- `memory/product-catalog.md` — SKUs y mensajes por producto
- `memory/ad-references.md` — Biblioteca de anuncios ganadores (input del usuario)
- `memory/cofepris-claim-library.md` — Claims aprobados con fuentes verificadas

## Compliance

QiTrax es producto registrado COFEPRIS (Reg. 2370E2025 SSA). El gate `cofepris-check` es obligatorio en todo el pipeline de producción de contenido. Ningún output del plugin se considera "ready to publish" sin haber pasado por las 3 capas de quality gates.

## Governance de paid media

Por default, el plugin opera en **Nivel 1 de governance**: read + recommend. Lee Meta Ads y TikTok Ads APIs, analiza performance, propone cambios. La ejecución de pause/scale/launch siempre la hace un humano (Performance Manager). Niveles 2 y 3 (autonomía progresiva) se habilitan después de 4-8 semanas de validación.

## Hand-off comercial

Cuando el sistema identifica un lead caliente (médico que responde a outreach, micro-paciente que pide reunión), genera contexto, propone slots del Calendar de Luis, agenda la cita, crea task en ClickUp y notifica a Luis vía Slack. La cierra siempre el equipo comercial humano.

## Version

**0.2.0 — Mayo 2026 — MVP + Fase 1 completo.**

51 skills construidas, 9 archivos de memoria, 5 scheduled tasks. Cubre todos los sub-segmentos × etapas de la estrategia v4.3 + iteración de ads + SEO completo + LLM SEO + outreach médico + hand-offs + reportes ejecutivos.

Documento de arquitectura completo: `qihealth-sistema-agentico-marketing-v1.md` y `HANDOFF-cowork-macmini.md` (no incluidos en el plugin, viven separados en el bundle).

### Skills agregadas en v0.2.0 (vs v0.1.0)

**Personas adicionales** (4): persona-bgm-self, persona-bgm-doctor, persona-cgm-switchers, persona-seo

**Producción** (5): doctor-reel-brief, pillar-page-drafter, seo-satellite-article, landing-page-copy, one-pager-clinical, lead-magnet-builder, quiz-builder, email-sequence-builder, whatsapp-flow-builder

**SEO + LLM SEO** (4): seo-keyword-research, seo-internal-linking, seo-monthly-report, llm-seo-optimizer, llm-citation-tracker

**Outreach** (4): medical-list-builder, kol-outreach, commercial-handoff-luis, influencer-hunter

**Operaciones** (5): weekly-performance-report, monthly-performance-report, lead-routing-bigin, paid-roas-analysis, ab-test-designer

**Análisis + utilidades** (3): nps-mining, consent-tracker, notion-knowledge-mgmt

### Scheduled tasks v0.2.0 (5 totales)
- morning-brief (Lun-Vie 7AM)
- competitor-watch-6h (cada 6h)
- weekly-prep-friday (Vie 2PM)
- monthly-perf-report (día 1 6AM)
- seo-rank-tracking (Lun 8AM)
