---
name: nps-mining
description: >
  This skill should be used to mine NPS responses, support tickets, and customer reviews for insights about QiHealth product, brand, and content. Triggers: "NPS mining", "voice of customer", "VOC", "review analysis", "customer insights", "analizar tickets de soporte", "mineral comentarios". Aggregates qualitative feedback, identifies themes, extracts language patterns for content/copy, surfaces objections for handling.
metadata:
  version: "0.1.0"
  type: "operations"
  channel: "research"
---

# NPS & VOC Mining

Mines qualitative customer feedback para alimentar al sistema: lenguaje real del cliente, objeciones a manejar, insights de producto.

## Sources

- NPS surveys (Zoho Campaigns + Survey)
- Tickets Zoho Desk (categorías + texto)
- Reviews G2 / Trustpilot / Mercado Libre (cuando QiHealth aparezca)
- Comentarios en posts orgánicos (Instagram + TikTok + LinkedIn)
- DMs de Instagram (con keyword search)
- Chats de soporte (Zoho)

## MCPs requeridos

- Zoho Desk (tickets)
- Zoho Campaigns (NPS responses)
- Apify (scraping reviews públicas + comentarios sociales)

## Análisis estándar

### Themes extraction

Por cada batch de feedback (mensual), extraer:

```yaml
themes_detected:
  - theme: "Confusión sobre cómo aplicar el sensor"
    frequency: 23 mentions
    sentiment: neutral
    sub_segment_affected: ["BGM-Self primerizos", "No-Measurers"]
    quotes_examples:
      - "No sé si lo apliqué bien"
      - "El video del tutorial es corto"
      - "¿Lo aplico en cualquier brazo?"
    recommended_action:
      - Mejorar onboarding video (más largo + demos)
      - FAQ específica de aplicación
      - WhatsApp soporte primer día post-compra
  
  - theme: "Comparación con Abbott — duda de cambio"
    frequency: 18
    sentiment: question
    sub_segment_affected: ["CGM-Switchers"]
    quotes_examples:
      - "¿Realmente vale la pena cambiar?"
      - "Pero ya tengo mi rutina con Libre"
    recommended_action:
      - Reforzar mensaje "Trae tu historial" en /switch
      - Doctor Reel específico con switcher real
      - Email automatizado a quien visite /switch sin comprar
```

### Language patterns

Identificar el VOCABULARIO REAL del cliente:

- ¿Qué palabras usa para describir la enfermedad? ("diabetes", "azúcar alta", "azucarado")
- ¿Qué expresan emocionalmente? ("miedo", "frustración", "esperanza")
- ¿Qué buscan? ("control", "tranquilidad", "respuestas")

Estos patterns alimentan a brand-voice + copy de personas (los hooks que funcionan son los que usan vocabulario del cliente).

### Objeciones

Cada objeción identificada se anota con frequency + sub-segmento + recomendación de handling:

```yaml
objeciones:
  - objection: "Es caro vs glucómetro"
    sub_segment: "BGM-Self"
    frequency: 34
    handling_recommendation: |
      Posicionar valor compuesto (no precio unitario):
      sensor + coaching IA + scores + dashboard.
      Argumento: $2.50 MXN/día.
  
  - objection: "Necesito receta médica"
    sub_segment: "todos"
    frequency: 19
    handling_recommendation: |
      Comunicar claramente: COFEPRIS wellness, no requiere receta.
      Pero recomendamos consulta con médico para integración.
```

## Output mensual

```markdown
# NPS & VOC MINING — [Mes]

## Resumen

- Total feedback analizado: N
- NPS score: X (vs prev mes Y)
- Top 3 themes: ...
- Top 3 objeciones: ...
- Language patterns nuevos: ...

## Recomendaciones para sistema

### Brand voice updates
- Agregar a memory/brand-voice.md: palabras del cliente identificadas como ganadoras
- Quitar: palabras prohibidas que el cliente NO usa

### Cofepris claim library
- Claim X mencionado en 12 reviews como bien recibido → considerar agregar a library
- Claim Y mencionado como confuso → revisar

### Producto / experiencia
- Issue X reportado 23 veces → escalar a producto (no marketing)
- Issue Y reportado 8 veces → mejorar onboarding

### Próximas piezas a producir
- Carrusel "Cómo aplicar el sensor paso a paso" — alta demanda
- Reel "Vale la pena el cambio?" — para CGM-Switchers con quotes reales
```

## Cuándo escalar al humano

- Issue de producto (no marketing) → producto team
- Reviewer hostil con escalación pública → Jose + community manager URGENTE
- Patrones que sugieren problema regulatorio (cliente confunde producto con diagnóstico) → asesoría legal
- Decline en NPS >10 puntos en un mes → investigation profunda
