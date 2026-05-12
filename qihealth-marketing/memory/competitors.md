# Competitors — Perfiles de monitoreo

**Última actualización: Mayo 12, 2026**

Vivos: **Abbott (FreeStyle Libre)**, **Sibionics México**. Otros en fase 2: Dexcom, Medtronic Guardian. Esta memoria alimenta `competitor-watch` y el scheduled task `competitor-watch-6h`.

---

## 1. Abbott — FreeStyle Libre / Libre 2 Plus

### Datos de marca

- **Productos en México**:
  - FreeStyle Libre (original) — Reg. 1090E2017 SSA
  - FreeStyle Libre 2 Plus (con alarmas opcionales) — **Reg. 0995E2025 SSA** (nuevo, 2025)
  - Lector FreeStyle Libre 2 — Reg. 0997E2025 SSA
- **Tagline mexicano**: "Queremos que vivas tu vida libremente... sin barreras"
- **Sitio oficial**: freestyle.abbott/es-mx
- **Tienda oficial**: freestylelibretienda.com.mx
- **Programa de retención**: 4+1 ("Abracemos la Libertad") — 1 sensor gratis por cada 4 comprados

### Precios actuales (mayo 2026)

| Producto | Precio MXN | Status |
|---|---|---|
| **FreeStyle Libre 2 Plus** (current, con alarmas) | **desde $1,629.00** | ✅ **Producto vigente** |
| Lector FreeStyle Libre 2 | $1,504.36 | Reader actual |
| Kit Inicial FL2 (1 reader + 2 sensors) | $3,505.95 | Bundle entry |
| FreeStyle Libre **1 original** (legacy) | $1,299.00 | ⚠️ **Liquidación de inventario viejo** — sin alarmas, requiere calibración, casi descontinuado |

**Nota importante (corregido)**: El precio bajo de $1,299 MXN es del **FreeStyle Libre 1 (versión original)** — producto legacy en liquidación, NO competencia real. El producto vigente de Abbott es **FreeStyle Libre 2 Plus a $1,629+**. Abbott NO bajó precio competitivamente — está vaciando stock viejo.

**Implicación competitiva real**:
- **Sibionics GS1 ($1,299) vs FreeStyle Libre 2 Plus ($1,629+)** = Sibionics 20% más barato que el producto current
- El FL1 a $1,299 no es alternativa real para usuarios bien informados (sin alarmas, calibración manual, app limitada)
- La pelea real de precio es entre Sibionics y QiHealth, NO entre Abbott y Sibionics en producto current

### Distribución en México (9 cadenas + online)

Disponible en:
- Tienda oficial Abbott (freestylelibretienda.com.mx)
- Farmacia San Pablo
- Farmacias Guadalajara
- Farmacias del Ahorro
- Farmacias Benavides
- Farmacias Especializadas
- Sanborns
- Amazon MX
- Walmart MX
- City Fresko (La Comer)

Distribución masiva — mayor footprint que cualquier competidor.

### Mensaje y pilares

Abbott no vende tecnología, vende **libertad**. Cuatro pilares:

1. **Sin pinchazos** — el 40% de pacientes no se medía con la frecuencia recomendada por el dolor
2. **Datos continuos = decisiones informadas** — pasar de fotografías a la película
3. **Compartir con quien importa** — LibreView (médico) y LibreLinkUp (familia)
4. **Más asequible de lo que piensas** — accesibilidad económica vía 4+1

### Moat (lo que hay que vencer)

| Capa | Cómo opera | Cómo ataca QiHealth |
|---|---|---|
| LibreView (lock-in del médico) | Plataforma gratuita donde el médico ve a TODOS sus pacientes Libre en un solo dashboard | Dashboard QiHealth con IA predictiva, alertas inteligentes, multi-biométrico |
| Programa 4+1 | 1 sensor gratis por cada 4 comprados — crea hábito de recompra | Membresía QiHealth no transaccional (sensor + coaching IA + scores + dashboard médico) |
| Alianzas FMD/AMD/SMEN | Endorsement institucional con las 3 organizaciones de diabetes más relevantes de México | Construir advisory propio + advisory board con KOLs respetados |
| Programa MyFreeStyle (onboarding) | Educación progresiva — 89% de usuarios más seguros tras participar | Onboarding QiHealth con NutriCoach + agentes IA — interpretación + acción |
| Distribución masiva 9+ cadenas | En todas las farmacias y supermercados grandes de México | Aún no replicable — QiHealth es DTC online |
| Sistema de "Agenda tu cita" oficial | Demos médicos vía web freestylelibretienda.com.mx/date/new-date | QiHealth con commercial-handoff-luis + advisory en Slack |

### Grietas (donde QiHealth gana)

1. **Sin coaching de IA** — Abbott muestra datos, QiHealth los interpreta y guía la acción
2. **Solo glucosa** — Abbott mide una variable, QiHealth integra glucosa + sueño + actividad + composición + 5 scores propietarios
3. **Solo diabetes diagnosticada** — Abbott no captura al pre-diabético sin diagnóstico, QiHealth sí
4. **Mensaje global no adaptado** — Abbott México usa creativos casi idénticos a otros mercados, sin localizar para insight mexicano específico
5. **SEO en español-mexicano débil** — Abbott no domina keywords largas de prevención y herencia diabetes

### Presencia social Abbott México

- Facebook: `FreeStyleDiabetesLatAm` (cuenta regional LatAm, no México-exclusivo)
- Instagram: `@freestylediabetes`
- YouTube: `@FreeStyleLatinoamerica`

NO tienen TikTok México dedicado — gap claro para QiHealth.

### Regla de oro

Nunca competir en "sensor vs sensor". Esa es la cancha de Abbott (escala global, 40M+ usuarios, FMD/AMD detrás, 9 cadenas de distribución). Competir siempre en "sensor + ecosistema de inteligencia" vs "sensor solo".

### Lo que vigilar continuamente

- Nuevos ads en Meta Ad Library México (cuenta Abbott Diabetes Care)
- Cambios en programa 4+1 (precio, condiciones, expansión)
- Nuevos endorsements con asociaciones médicas
- Lanzamiento FreeStyle Libre 3 en México (cuando ocurra)
- Cambios de pricing en cualquier retailer (especialmente Amazon MX, Walmart)
- Posicionamiento en redes (TikTok México, IG, YouTube)
- Activaciones con KOLs médicos mexicanos
- Cualquier mención negativa o queja de usuarios (oportunidad de switch)

### Vector primario de monitoreo

Apify scraping cada 6h de:
- Meta Ad Library con filtro `country:MX` y `advertiser:Abbott Diabetes Care`
- freestylelibretienda.com.mx (cambios de precio)
- Programa 4+1 página
- Mercado Libre / Amazon MX (precios y disponibilidad de FL2 Plus)

---

## 2. Sibionics — México (Distribuido por Kabla)

### Datos de marca

- **Productos disponibles en México**: Sibionics GS1 (CGM 14 días)
- **Origen**: fabricante chino con presencia global (2.6M+ usuarios en 96 países claim)
- **Distribuidor exclusivo en México**: **Kabla Comercial S.A. de C.V.** — la mayor empresa de IVD (In Vitro Diagnostics) en México
- **Sitio en México**: sibionics.com.mx
- **Registro COFEPRIS**: 0097W2026 SSA
- **Empresa marketing**: Kabla DX (división de Kabla)

### Precios actuales (mayo 2026)

| Cantidad | Precio MXN |
|---|---|
| 1 sensor GS1 | **$1,299.00 MXN** |
| 2 sensores | (consulta web) |
| 4 sensores | (consulta web) |

**Cambio importante**: Precio bajó de $1,399 MXN (precio que teníamos en memoria) a **$1,299 MXN** sin marcar como "oferta" — parece precio definitivo. Bajó ~$700 MXN del precio regular original ($1,949).

### Modelo comercial — NUEVO

**Suscripción recurrente activada**: en la página de producto ahora ofrecen "compra recurrente o diferida" con cargo automático.

> *"Este artículo es una compra recurrente o diferida. Al continuar, acepto la política de cancelación y autorizo a realizar cargos en mi forma de pago según los precios, la frecuencia y las fechas indicadas en esta página hasta que se prepare mi pedido o yo lo cancele"*

Cantidades disponibles: 1, 2 o 4 sensores con cargo recurrente. **Copiaron el playbook de Abbott 4+1 sin diseñar programa custom — es subscription puro**. Esto reduce su churn drásticamente.

### Ads paid Meta — CONFIRMADO ACTIVOS

UTM tags en URL canónico de su página de producto confirman campaign activo:

```
utm_source=facebook
utm_medium=paid
utm_campaign=120246105728850343
utm_id=120246105728850343
utm_content=120246105728840343
utm_term=120246105728860343
```

**Sibionics MX está corriendo ads paid en Facebook/Meta con presupuesto asignado para México**.

### Posicionamiento

Sibionics se posiciona como **alternativa de precio agresivo + ciencia respaldada**. Mismo formato (CGM 14 días sin escaneo) a fracción del costo de FreeStyle Libre 2 Plus. Recientemente añadieron mensaje de "ciencia" para subir percepción.

### Claims que usan (audit COFEPRIS-style)

| Claim | Lectura | Status |
|---|---|---|
| "Líder Mundial en CGM" | Aspiracional, no verificable vs Abbott | ⚠️ Discutible pero permitido |
| "2.6M+ usuarios en 96 países" | Verificable, dato global | ✅ OK |
| "Certificado CE MDR UE desde 2023" | Verificable, true | ✅ OK |
| "3,900+ instituciones médicas colaboran" | Verificable global, no MX | ✅ OK |
| "Sin dolor / sin calibración / sin escaneo" | Claims funcionales | ✅ OK |
| "Impermeable IP28" | Spec técnica verificable | ✅ OK |
| "Confianza respaldada por la ciencia" | Genérico aspiracional | ✅ OK |
| "Innovación / Desarrollo tecnológico propio" | OK no específico | ✅ OK |

NO usan claims regulatoriamente sospechosos (cura, diagnóstico, prevención específica) — están dentro de COFEPRIS-safe.

### Riesgo competitivo (revisado)

Sibionics es **el competidor más agresivo en precio** + ahora con **subscription model**. Captura:

1. **Price-sensitive en BGM-Self**: usuarios primerizos que buscan probar CGM sin invertir mucho
2. **Switchers de Abbott por costo**: usuarios cansados del modelo 4+1, ahora con sub directa de Sibionics
3. **No-Measurers entry-level**: pueden probar Sibionics primero antes de QiHealth Insight 15

**Cambio vs antes**: con $1,299 + subscription, Sibionics ya es VIABLE como entry-level recurrente. Antes era solo "prueba unitaria barata".

### Grietas de Sibionics (oportunidades)

1. **Sin ecosistema clínico**: no tiene equivalente a LibreView ni dashboard QiHealth para médicos
2. **Sin coaching de IA**: solo muestra datos crudos
3. **Sin marca clínica fuerte en México**: distribuido por Kabla pero no tiene endorsements de FMD/AMD/SMEN
4. **Sin advisory médico mexicano visible**
5. **Sin integraciones multi-biométrico** (sleep + actividad + composición)
6. **Soporte por WhatsApp limitado** (no es 24/7, depende de horario Kabla)
7. **Sin posicionamiento de prevención** para no-medidores
8. **Brand fragmentada**: a veces "Sibionics", a veces "Sibionics by Kabla" — confusión

### Estrategia de defensa QiHealth vs Sibionics

QiHealth NO compite con Sibionics en precio unitario por sensor. Compite en:

- **Membresía con valor compuesto**: sensor + coaching + scores + dashboard médico
- **Autoridad clínica**: advisory médico mexicano firmando contenido
- **Soporte humano**: NutriCoach + soporte por chat real
- **Onboarding diferenciado**: el primer mes incluye 1:1 con coach
- **Plan Insight 15 entry-level**: para competir en entry-level con descubrimiento + reporte personalizado

Mensaje núcleo defensa: **"Un sensor barato sin coaching es solo un dato más. La diferencia está en lo que haces con esos datos."**

### Presencia social Sibionics MX

- Facebook: `facebook.com/sibionics.mx`
- Instagram: `@sibionics.mx`
- TikTok: `@sibionicsmx`
- YouTube: `@SibionicsMx`
- WhatsApp soporte: +52 81 4444 1003 (operado por Kabla)
- Sección HCP: proview.sisensing.com (armando relación con médicos)

### Programa global a vigilar

Sibionics globalmente corre campaña "From 0 to 1" — primer CGM a precio muy bajo (€9.90 vs €62.99 regular) para nuevos usuarios. **Si lo lanzan en México, sería disruptor mayor**. Vigilar email marketing y newsletters.

### Lo que vigilar continuamente

- Cambios de precio en sibionics.com.mx (escenarios sub-$1,299)
- Lanzamiento de Sibionics GS3 en México (versión más nueva, ya en otros mercados)
- Distribución en nuevas farmacias o marketplaces
- Posicionamiento en redes (especialmente TikTok México y FB groups de diabetes)
- Reviews y comentarios en redes
- Activaciones con KOLs médicos
- Estrategia de Meta Ads (qué creatives están corriendo)
- Lanzamiento del programa "From 0 to 1" en México (alta probabilidad)

### Vector primario de monitoreo

- Apify scraping cada 6h de sibionics.com.mx (precios, productos, subscription)
- Apify scraping de Meta Ad Library México con `advertiser:Kabla` o `advertiser:Sibionics`
- Apify scraping de Mercado Libre y Amazon MX para precio en marketplaces
- Búsqueda manual mensual en blogs y FB groups de diabetes para sentiment

---

## Otros competidores (vigilancia más liviana)

### Dexcom (G7)

- No tiene presencia comercial fuerte en México (importación gris)
- Líder en USA y Europa
- Vigilar si lanza México oficialmente (sería disruptor mayor)
- Diferenciador: aprobado para uso pediátrico (QiHealth no)

### Medtronic Guardian Connect

- Presencia en México pero foco en pacientes con bomba de insulina (DM1)
- No compite directo con QiHealth en sub-segmentos prioritarios
- Vigilar si lanza producto sin bomba

### Glucómetros tradicionales (Accu-Chek, OneTouch, Contour)

- NO son competidor directo del CGM (categoría diferente)
- Sí son el **status quo** del que QiHealth quiere mover a BGM-Self y BGM-Doctor
- No requieren monitoreo continuo, pero sí tracking de movimientos en categoría (ej: si Accu-Chek lanza CGM, eso cambia el juego)

---

## Comparativa precio CGM México (mayo 2026)

### Productos vigentes (la pelea real)

| Producto | Precio unitario MXN | Subscription | Distribución |
|---|---|---|---|
| **FreeStyle Libre 2 Plus** (Abbott current) | **$1,629+** | Programa 4+1 | 9 cadenas + online |
| **Sibionics GS1** | **$1,299** | ✓ Recurring automático | Solo Kabla + online |
| **QiTrax (Insight 15, 15 días)** | [pendiente confirmar Jose] | Membresía QiHealth | DTC online |

### Producto legacy (NO competencia real para usuarios informados)

| Producto | Precio unitario MXN | Por qué no compite |
|---|---|---|
| FreeStyle Libre 1 original | $1,299 | Sin alarmas, calibración manual, app limitada — Abbott liquidando inventario |

**Conclusión revisada**:

- Sibionics GS1 ($1,299) es el sensor más barato vigente del mercado mexicano (20% menos que FL2 Plus)
- Abbott NO bajó precio de FL2 Plus — sigue defendiéndolo a $1,629+ con LibreView lock-in
- La pelea real de precio entry-level es **Sibionics vs QiTrax Insight 15**, no Abbott
- QiTrax compite con Sibionics en valor compuesto (sensor + IA + scores + soporte), no en precio unitario
- QiTrax compite con FL2 Plus en upgrade de ecosistema (IA + multi-biométrico + advisory mexicano), no en precio unitario

---

## Cómo se usa este documento

El plugin lee este archivo cada vez que se invoca `competitor-watch` o cuando el orquestador detecta un pedido relacionado con comparativas, switches, o posicionamiento.

Cada hallazgo del scheduled task `competitor-watch-6h` se reporta a Slack #qihealth-competitor-alerts con:

- Tipo de cambio detectado (nuevo ad, cambio de precio, nuevo producto, mención en redes)
- Source (URL, screenshot)
- Severidad (info / atención / acción inmediata)
- Recomendación específica (ej: "Abbott bajó 4+1 a 5+1 — considerar respuesta en /switch landing")

Las recomendaciones siempre las firma humano (Jose o Performance Manager) antes de ejecutar.

---

## Historial de cambios

- **2026-04-XX**: documento inicial con perfiles Abbott + Sibionics base
- **2026-05-12**: actualización con — Sibionics precio bajó a $1,299, activó subscription recurrente, confirmados ads paid Meta. Abbott lanzó FreeStyle Libre 2 Plus en MX (Reg. 0995E2025) a $1,629+, distribución expandida a 9 cadenas. Tabla comparativa de precios agregada.
- **2026-05-12 corrección**: clarificado que el precio $1,299 de Abbott es del FreeStyle Libre 1 original (legacy en liquidación), NO del producto current. El producto vigente es FL2 Plus a $1,629+. Implicación: pelea real de precio entry-level es Sibionics vs QiTrax, no Abbott.
