---
name: lead-magnet-builder
description: >
  This skill should be used to design and produce lead magnets (ebooks, checklists, calculadoras, guides) for QiHealth. Triggers: "lead magnet", "ebook para captar leads", "checklist", "calculadora", "guide gratuita", "downloadable content". Produces lead magnet content + landing copy + email follow-up triggered.
metadata:
  version: "0.1.0"
  type: "production"
---

# Lead Magnet Builder

Produce lead magnets de alta conversión para QiHealth. Cada magnet enlazado a un sub-segmento + email sequence post-download.

## Tipos de lead magnets

### Por sub-segmento

**No-Measurers**:
- Quiz "¿Estás en riesgo metabólico?" (ya cubierto por quiz-builder)
- Ebook "Pre-diabetes en México: lo que tienes que saber"
- Calculadora "¿Cuándo deberías empezar a medirte?"

**Legacy**:
- Ebook "Hijo de diabético: tu mapa de prevención"
- Checklist "5 conversaciones que tener con tu papá sobre su diabetes"
- Quiz "Tu plan de prevención familiar"

**BGM-Self**:
- Ebook "Glucómetro vs CGM: la guía honesta 2026"
- Checklist "Lo que tu glucómetro NO te dice"
- Calculadora "Costo total de medir glucosa: glucómetro vs CGM"

**BGM-Doctor (lado paciente)**:
- Checklist "5 preguntas para hacerle a tu doctor en tu próxima consulta"
- Ebook "Cómo entender tu AGP report"

**CGM-Switchers**:
- Ebook "Migrar de Libre a otro CGM: guía paso a paso"
- Calculadora "Tu costo real con programa 4+1 de Abbott"

### Cross-segment
- Glossary "Términos de salud metabólica que importan"
- Ebook "Una vida con diabetes en México: realidades, datos, opciones"

## Estructura estándar

### Ebook (10-25 páginas PDF)

1. **Portada**: título + autor + QiHealth branding
2. **Tabla de contenidos**
3. **Intro** (1-2 páginas): por qué este ebook + qué vas a aprender
4. **Capítulos** (5-8): contenido por chapters
5. **Conclusión + CTA**: producto / servicio / siguiente paso
6. **Sobre el autor + advisory**: credenciales
7. **Disclaimer regulatorio**: "Este contenido es educativo..."
8. **Referencias**: fuentes citadas

### Checklist (1-3 páginas)

- Hook claro arriba
- Lista accionable (5-12 items)
- Tips contextuales
- CTA al final

### Calculadora (web interactiva o spreadsheet)

- Inputs claros
- Lógica de cálculo (transparente, sin claims engañosos)
- Output personalizado
- Email capture al final para "guardar resultado"
- CTA producto basado en resultado

## Reglas COFEPRIS

- Ningún lead magnet puede dar diagnóstico
- Calculadora de "riesgo" NUNCA debe decir "tienes diabetes"
- Disclaimer obligatorio en todo magnet
- Si claim clínico → advisory review

## Output

```markdown
# LEAD MAGNET — [Título] — [Sub-segmento]

**Tipo**: Ebook / Checklist / Calculadora / Quiz / Glossary
**Páginas**: N
**Sub-segmento**: [...]
**Email sequence post-download**: [reference a email-sequence-builder]

## Contenido completo
[texto literal de cada sección]

## Diseño brief
[para diseñador — paleta, tipografía, layout sugerido]

## Landing del lead magnet
[copy de la landing donde se descarga + form email capture]

## Email follow-up (5 emails)
[invocar email-sequence-builder para generar]

## CTA principal post-download
[producto correspondiente al sub-segmento]
```

## Quality gates

- cofepris-check
- brand-voice
- factual-review
- Advisory review (obligatorio para ebooks con claims clínicos)

## Cuándo escalar al humano

- Calculadora con lógica clínica → advisory para validar fórmula
- Ebook con autor médico firmante → coordinar con advisory
- Magnet con datos cuantitativos → factual-review obligatorio
