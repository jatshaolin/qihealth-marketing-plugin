# Competitors — Perfiles de monitoreo

Vivos al inicio del MVP: **Abbott (FreeStyle Libre)** y **Sibionics México**. Otros competidores a vigilar en fase 2: Dexcom, Medtronic Guardian. Esta memoria alimenta a la skill `competitor-watch` y al scheduled task `competitor-watch-6h`.

---

## 1. Abbott — FreeStyle Libre

### Datos de marca

- **Producto principal en México**: FreeStyle Libre 2 (CGM 14 días sin escaneo manual)
- **Tagline mexicano**: "Queremos que vivas tu vida libremente... sin barreras"
- **Posicionamiento**: libertad emocional, eliminación del dolor del piquete
- **Sitio**: freestylelibre.mx
- **Programa de retención**: 4+1 ("Abracemos la Libertad") — 1 sensor gratis por cada 4 comprados

### Mensaje y pilares

Abbott no vende tecnología, vende libertad. Cuatro pilares:

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

### Grietas (donde QiHealth gana)

1. **Sin coaching de IA** — Abbott muestra datos, QiHealth los interpreta y guía la acción
2. **Solo glucosa** — Abbott mide una variable, QiHealth integra glucosa + sueño + actividad + composición + 5 scores propietarios
3. **Solo diabetes diagnosticada** — Abbott no captura al pre-diabético sin diagnóstico, QiHealth sí

### Regla de oro

Nunca competir en "sensor vs sensor". Esa es la cancha de Abbott (escala global, 7M+ usuarios, FMD/AMD detrás). Competir siempre en "sensor + ecosistema de inteligencia" vs "sensor solo".

### Lo que vigilar continuamente

- Nuevos ads en Meta Ad Library México
- Cambios en programa 4+1 (precio, condiciones, expansión)
- Nuevos endorsements con asociaciones médicas
- Lanzamiento de funciones nuevas (Libre 3, integraciones, accesorios)
- Cambios de pricing de sensor unitario
- Posicionamiento en redes (TikTok, IG)
- Activaciones con KOLs médicos
- Cualquier mención negativa o queja de usuarios (oportunidad de switch)

### Vector primario de monitoreo

Apify scraping de Meta Ad Library con filtro `country:MX` y `advertiser:Abbott Diabetes Care`. Cadencia: cada 6 horas vía scheduled task.

---

## 2. Sibionics — México

### Datos de marca

- **Productos disponibles en México**: Sibionics GS1 (CGM 14 días), Sibionics GS3
- **Origen**: fabricante chino con presencia internacional
- **Sitio en México**: sibionics.com.mx
- **Distribución**: directo + Kabla Store (y posiblemente otros)
- **Pricing México (referencia)**: GS1 a $1,399 MXN oferta / $1,949 MXN regular

### Posicionamiento

Sibionics se posiciona como **alternativa de precio agresivo** a Abbott. Mismo formato (CGM 14 días sin escaneo) a fracción del costo.

Características que destaca:

- 14 días de uso continuo
- Sin escaneo manual (continuous reading)
- Resistente al agua
- App móvil propia
- Sin calibración

### Riesgo competitivo

Sibionics es **el competidor más agresivo en precio**. Al ser ~50-60% más barato que un Abbott unitario, captura a usuarios:

1. **Price-sensitive en BGM-Self**: usuarios primerizos que buscan probar CGM sin invertir mucho
2. **Switchers de Abbott por costo**: usuarios cansados del modelo 4+1
3. **No-Measurers** que dudan invertir en QiHealth: pueden probar Sibionics primero como entry-level

### Grietas de Sibionics (oportunidades)

1. **Sin ecosistema clínico**: no tiene equivalente a LibreView ni dashboard QiHealth para médicos
2. **Sin coaching de IA**: solo muestra datos crudos
3. **Sin marca clínica fuerte en México**: no tiene endorsements de FMD/AMD/SMEN
4. **Sin advisory médico mexicano visible**
5. **Sin integraciones multi-biométrico** (sleep + actividad + composición)
6. **Soporte y servicio al cliente** — punto débil reportado en reviews
7. **Sin posicionamiento de prevención** para no-medidores

### Estrategia de defensa QiHealth vs Sibionics

QiHealth NO compite con Sibionics en precio unitario por sensor. Compite en:

- **Membresía con valor compuesto**: sensor + coaching + scores + dashboard médico
- **Autoridad clínica**: advisory médico mexicano firmando contenido
- **Soporte humano**: NutriCoach + soporte por chat real
- **Onboarding diferenciado**: el primer mes incluye 1:1 con coach
- **Plan Insight 15 entry-level**: para competir en entry-level con descubrimiento + reporte personalizado

Para CGM-Switchers, Sibionics NO es competencia (un usuario Abbott no se mueve a Sibionics, se mueve dentro del ecosistema Abbott o a un upgrade real).

Para BGM-Self y No-Measurers, Sibionics SÍ es competencia. Mensaje de defensa: "Un sensor barato sin coaching es solo un dato más. La diferencia está en lo que haces con esos datos."

### Lo que vigilar continuamente

- Cambios de precio en sibionics.com.mx (especialmente promociones)
- Lanzamiento de nuevos productos (GS3, accesorios, app updates)
- Distribución en farmacias o marketplaces nuevos (Mercado Libre, Amazon MX)
- Posicionamiento en redes (especialmente TikTok México y FB groups de diabetes)
- Reviews y comentarios en redes (G2 México, Trustpilot, blogs)
- Activaciones con KOLs (¿están firmando médicos?)
- Estrategia de Meta Ads (¿paid o solo orgánico?)

### Vector primario de monitoreo

- Apify scraping de sibionics.com.mx (precios, productos)
- Apify scraping de Meta Ad Library México con `advertiser:Sibionics` (verificar exact name)
- Apify scraping de Mercado Libre y Amazon MX para precio en marketplaces
- Búsqueda manual mensual en blogs y FB groups de diabetes para sentiment

---

## Otros competidores (vigilancia más liviana)

### Dexcom (G7)

- No tiene presencia comercial fuerte en México (importación gris)
- Líder en USA y Europa
- Vigilar si lanza México oficialmente (sería disruptor mayor)

### Medtronic Guardian Connect

- Presencia en México pero foco en pacientes con bomba de insulina (DM1)
- No compite directo con QiHealth en sub-segmentos prioritarios
- Vigilar si lanza producto sin bomba

### Glucómetros tradicionales (Accu-Chek, OneTouch, Contour)

- NO son competidor directo del CGM (categoría diferente)
- Sí son el **status quo** del que QiHealth quiere mover a BGM-Self y BGM-Doctor
- No requieren monitoreo, pero sí tracking de movimientos en categoría (ej: si Accu-Chek lanza CGM, eso cambia el juego)

---

## Cómo se usa este documento

El plugin lee este archivo cada vez que se invoca `competitor-watch` o cuando el orquestador detecta un pedido relacionado con comparativas, switches, o posicionamiento.

Cada hallazgo del scheduled task `competitor-watch-6h` se reporta a Slack #qihealth-competitor-alerts con:

- Tipo de cambio detectado (nuevo ad, cambio de precio, nuevo producto, mención en redes)
- Source (URL, screenshot)
- Severidad (info / atención / acción inmediata)
- Recomendación específica (ej: "Abbott bajó 4+1 a 5+1 — considerar respuesta en /switch landing")

Las recomendaciones siempre las firma humano (Jose o Performance Manager) antes de ejecutar.
