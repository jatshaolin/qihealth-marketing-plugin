# Biblioteca de claims aprobados — QiHealth

Lista vivente de afirmaciones que el advisory médico ha aprobado, con su fuente verificable. El sistema usa esta biblioteca cada vez que produce contenido para minimizar idas y vueltas con el médico revisor.

## Cómo se usa

Cuando una pieza necesita hacer un claim cuantitativo o clínico, primero busca en este archivo. Si la afirmación ya está aprobada con fuente, se usa directamente. Si no, se marca como "pending-medical-review" y se manda al advisory.

## Estado al inicio del MVP

Esta biblioteca se llena durante operación. Al arrancar, contiene los claims base extraídos de la estrategia v4.3 y de fuentes públicas verificables. Conforme el advisory aprueba o rechaza claims nuevos, esta lista crece.

---

## Claims aprobados

### Categoría: Epidemiología en México

| Claim | Fuente | Aprobado por | Fecha |
|---|---|---|---|
| "La diabetes en México afecta a más de 14 millones de personas" | ENSANUT 2024 | Advisory pendiente | — |
| "Se estima que 1 de cada 3 mexicanos tiene pre-diabetes sin saberlo" | ENSANUT 2024 + IMSS 2023 | Advisory pendiente | — |
| "El 50% del riesgo de DM2 es genético; el otro 50% es estilo de vida" | ADA Position Statement 2023 | Advisory pendiente | — |

### Categoría: Funcionalidad QiTrax

| Claim | Fuente | Aprobado por | Fecha |
|---|---|---|---|
| "QiTrax mide tu glucosa cada 5 minutos" | Especificación técnica del producto | Confirmado | Pre-MVP |
| "QiTrax tiene autonomía de 14 días" | Especificación técnica del producto | Confirmado | Pre-MVP |
| "QiTrax es resistente al agua hasta 1 metro por máximo 1 hora" | Especificación técnica del producto | Confirmado | Pre-MVP |
| "QiTrax no requiere calibración con piquete" | Especificación técnica del producto | Confirmado | Pre-MVP |
| "Registro COFEPRIS 2370E2025 SSA" | Documento oficial COFEPRIS | Confirmado | Pre-MVP |

### Categoría: Diferenciadores QiHealth

| Claim | Fuente | Aprobado por | Fecha |
|---|---|---|---|
| "QiHealth integra glucosa + sueño + actividad + composición corporal" | Documentación de producto (multi-biométrico) | Confirmado | Pre-MVP |
| "QiHealth incluye coaching de IA (NutriCoach), Abbott no" | Comparación pública verificable | Advisory pendiente | — |
| "El dashboard QiHealth tiene IA predictiva, LibreView no" | Comparación pública verificable | Advisory pendiente | — |

### Categoría: Genética y diabetes hereditaria (sub-segmento Legacy)

| Claim | Fuente | Aprobado por | Fecha |
|---|---|---|---|
| "Tener un padre con DM2 aumenta tu riesgo entre 40-50% según literatura clínica" | American Diabetes Association | Advisory pendiente | — |
| "Estilo de vida importa más que la genética en pre-diabetes (modificación posible)" | DPP Trial 2002 | Advisory pendiente | — |
| "Hijos de diabéticos pueden retrasar o evitar DM2 con cambios tempranos" | DPP Outcomes Study 2015 | Advisory pendiente | — |

### Categoría: CGM en general

| Claim | Fuente | Aprobado por | Fecha |
|---|---|---|---|
| "Los datos continuos permiten ver patrones que el glucómetro puntual no captura" | ADA Standards of Care 2024 | Advisory pendiente | — |
| "El uso de CGM se asocia con mejor control glucémico en DM2" | Beck et al. 2017, Diabetes Care | Advisory pendiente | — |

---

## Claims rechazados (NO usar)

Esta sección se llena cuando el advisory rechaza una propuesta. Cada rechazo se anota con razón para evitar repetirlo.

| Claim propuesto | Razón de rechazo | Alternativa permitida |
|---|---|---|
| "Previene diabetes" | Claim regulatorio prohibido por COFEPRIS | "Ayuda a detectar señales tempranas de" |
| "Reemplaza al endocrinólogo" | Claim de sustitución de tratamiento | "Acompaña tu seguimiento médico" |
| "Cura la pre-diabetes" | Claim de cura prohibido | "Te da herramientas para entender tu pre-diabetes" |
| "Garantiza pérdida de peso" | Claim no verificable + COFEPRIS | "Aporta información sobre tu metabolismo" |

---

## Workflow de aprobación de claim nuevo

Cuando una pieza propone un claim que no está en esta biblioteca:

1. La skill `factual-review` detecta que es claim nuevo
2. Genera mensaje al advisory en Slack `#qihealth-medical-review` con:
   - El claim propuesto
   - El contexto (qué pieza, qué sub-segmento)
   - Fuente sugerida (si existe)
   - Una pregunta clara: ¿APROBADO / RECHAZADO / NECESITA REFORMULACIÓN?
3. Pieza queda en status `pending-medical-review` (no se publica)
4. SLA del advisory: 24 horas en weekdays
5. Cuando el advisory responde:
   - Si APROBADO: se agrega a esta biblioteca con fuente y firma del médico
   - Si REFORMULACIÓN: el médico propone alternativa, se agrega como variante
   - Si RECHAZADO: se agrega a la sección "Claims rechazados" con razón
6. La pieza se reformula automáticamente con la versión aprobada y se desbloquea

## Mantenimiento

- **Mensual**: revisar claims que no se han usado en mucho tiempo (¿siguen siendo relevantes?)
- **Trimestral**: validar que las fuentes siguen vigentes (publicaciones nuevas pueden actualizar evidencia)
- **Cuando cambie la regulación COFEPRIS**: revisión completa
- **Cuando entre nuevo médico al advisory**: orientación sobre la biblioteca + sus claims aprobados
