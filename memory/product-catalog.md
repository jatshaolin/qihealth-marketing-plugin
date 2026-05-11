# Catálogo de productos QiHealth

Mapeo de SKUs y mensajes por producto. El plugin consulta este archivo cuando una pieza necesita CTA específico, comparativa de precio, o referencia de bundle.

## Productos centrales

### QiTrax CGM (sensor)

- **Registro COFEPRIS**: Reg. 2370E2025 SSA (categoría wellness, no diagnóstico)
- **Duración**: 14 días por sensor
- **Lectura**: continua, sin escaneo manual
- **Resistencia al agua**: hasta 1m, máximo 1 hora
- **App móvil**: QiHealth (iOS + Android)
- **Compatibilidad**: con dashboard QiHealth + integración con bandas, anillos y básculas QiHealth (multi-biométrico)

### NutriCoach (coaching de IA)

- Capa de inteligencia que interpreta los datos del sensor
- Integrado en la app QiHealth
- Disponible 24/7
- Personaliza recomendaciones según perfil del usuario y datos en tiempo real
- Diferenciador frente a Abbott (que solo muestra datos)

### Longevity Engine (5 scores propietarios)

- Qi Score (general)
- Metabolic Score
- Sleep Score
- Activity Score
- Body Composition Score

Cada score se calcula con datos multi-biométricos y predicciones de IA. Diferenciador estructural frente a CGMs single-input.

### Dashboard Médico

- Plataforma para HCP (endocrinólogos, internistas, médicos del deporte)
- IA predictiva sobre patrones del paciente
- Alertas inteligentes (no solo umbrales)
- AGP report compatible
- Integración con multi-biométrico
- Diferenciador frente a LibreView (que solo muestra glucosa con dashboard básico)

---

## SKUs y bundles vigentes

### Insight 15 (entry-level — sub-segmento No-Measurers)

- 1 sensor QiTrax (15 días)
- Reporte automatizado al final
- Acceso a NutriCoach por 15 días
- **Posicionamiento**: descubrimiento personal, no compromiso largo
- **CTA típico**: "Conoce tu metabolismo en 15 días"
- **Precio**: [pendiente confirmar — Jose define]

### Bundle "Primer mes" (sub-segmento BGM-Self)

- 2 sensores QiTrax (30 días total)
- Onboarding 1:1 con coach
- Reporte interpretado al final
- Garantía: si no entiendes los datos al final, reembolso
- **Posicionamiento**: tu primer CGM con guía
- **CTA típico**: "Tu primer CGM con soporte humano"
- **Precio**: [pendiente confirmar]

### Plan Switch (sub-segmento CGM-Switchers)

- Membresía QiHealth con sensor QiTrax + dashboard + NutriCoach + scores
- Importación de historial LibreView (programa "Trae tu historial")
- Garantía 30 días — si no percibe valor adicional vs CGM anterior, reembolso completo
- **Posicionamiento**: upgrade desde CGM básico, no alternativa equivalente
- **CTA típico**: "Migra sin perder tu historial. Prueba 30 días."
- **Precio**: [pendiente confirmar]

### Plan Legacy (sub-segmento Legacy)

- Membresía con CGM (15 días iniciales)
- Onboarding 1:1 con coach
- Reporte personalizado de riesgo genético
- **Posicionamiento**: prevención por historia familiar
- **CTA típico**: "Tu plan de prevención porque conoces la historia familiar"
- **Precio**: [pendiente confirmar]

### Plan Legacy + 1 (upsell para sub-segmento Legacy)

- Plan Legacy del hijo + sensor adicional para padre/madre con diabetes diagnosticada
- Pricing combinado con descuento
- Especialmente fuerte para Día del Padre, Día de la Madre, Navidad, cumpleaños
- **CTA típico**: "Cuídate tú. Y regálale claridad a quien te la dio."

### Membresía QiHealth (estándar)

- Acceso continuo: sensores recurrentes + NutriCoach + scores + dashboard médico
- Modelo de suscripción (mensual/anual)
- Diferencia frente a programa 4+1 de Abbott: no es transaccional, es suscripción de inteligencia metabólica
- **Precio**: [pendiente confirmar]

---

## Diferenciadores estructurales (vs competencia)

Cuando el sistema produce contenido comparativo, debe anclar siempre en estos diferenciadores. NO pelear en "sensor vs sensor" (ahí gana Abbott por escala).

| Eje | QiHealth | Abbott (FreeStyle Libre) | Sibionics |
|---|---|---|---|
| Sensor CGM 14 días | ✓ | ✓ | ✓ |
| Coaching de IA (NutriCoach) | ✓ | ✗ | ✗ |
| 5 scores propietarios | ✓ | ✗ | ✗ |
| Multi-biométrico (sueño + actividad + composición) | ✓ | ✗ (solo glucosa) | ✗ (solo glucosa) |
| Dashboard médico con IA predictiva | ✓ | LibreView (sin IA) | ✗ |
| Posicionamiento prevención (no solo dx) | ✓ | ✗ | ✗ |
| Advisory médico mexicano visible | ✓ | FMD/AMD/SMEN | ✗ |
| Onboarding 1:1 con coach humano | ✓ | MyFreeStyle (digital) | ✗ |

---

## Lo que NO está en el catálogo (NO ofrecer)

- QiTrax NO se vende como dispositivo de diagnóstico
- QiTrax NO sustituye consulta médica
- NO existe (al día de hoy) versión pediátrica con claim médico
- NO existe modelo de financiamiento a meses sin intereses oficial (verificar antes de claim)
- NO existe (al día de hoy) integración con seguros médicos privados (vigilar — oportunidad futura)

---

## Reglas de mención de precio

- Precios siempre en MXN
- Comparativa con Abbott siempre debe usar pricing público verificable (4+1 amortizado)
- Comparativa con Sibionics siempre debe ir acompañada de comparativa de valor compuesto, no precio unitario
- Nunca prometer precio sin confirmar que está vigente (precios de promoción son temporales)
- En anuncios paid, el precio se confirma con el equipo comercial antes de publicación si es claim destacado

---

## Actualización

Este catálogo se actualiza cuando:
- Cambia un precio (Jose o equipo comercial notifica)
- Se lanza un nuevo SKU o bundle
- Cambia un diferenciador (ej: si Abbott lanza coaching de IA, esa columna cambia)
- Cambia el registro COFEPRIS o se adiciona uno nuevo

Cualquier cambio aquí dispara recalibración del `cofepris-claim-library` y revisión de los CTAs en producción.
