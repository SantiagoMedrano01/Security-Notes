
## 🔄 El ciclo completo

> [!info] Definición **Risk management**: proceso de identificar, analizar, tratar, monitorear y reportar riesgos para que la organización alcance sus objetivos de forma consistente con su **risk appetite**.

### Las 5 etapas del ciclo de gestión de riesgos

1. **Risk identification** — proceso proactivo para armar una lista exhaustiva de riesgos potenciales que podrían impedir alcanzar los objetivos.
2. **Risk analysis** — evaluar **probabilidad + impacto** de cada riesgo identificado. Dos enfoques:
    
    - **Qualitative** — categorías/escalas descriptivas (ej: alto/medio/bajo)
    - **Quantitative** — valores numéricos
    
    Resultado: lista de riesgos **priorizada**.
3. **Risk treatment** — desarrollar estrategias para gestionar el riesgo: **avoidance, reduction/mitigation, sharing/transfer, acceptance**. La elección depende del impacto y la tolerancia al riesgo de la organización.
4. **Risk monitoring** — proceso **continuo**: seguir riesgos identificados, vigilar el **residual risk**, detectar nuevos riesgos, revisar la eficacia del proceso mismo.
5. **Risk reporting** — comunicar info sobre el riesgo y la eficacia del proceso a los stakeholders. Formatos: dashboards, heat maps, informes detallados — adaptados a la audiencia.

### Temas que vienen en la sección (objetivo 5.2)

- **Risk assessment frequency**: ad hoc, recurring, one-time, continuous
- **Risk identification** + **Business Impact Analysis (BIA)**: conceptos como **RTO**, **RPO**, **MTTR**, **MTBF**
- **Qualitative risk analysis** (escalas descriptivas)
- **Quantitative risk analysis** (datos numéricos/estadísticos)
- **Risk management strategies**: transfer, acceptance, avoidance, mitigation
- **Risk monitoring and reporting**

> [!warning] Para el examen Memorizá el ciclo de 5 pasos en orden — **Identify → Analyze → Treat → Monitor → Report** — porque es la estructura base de toda esta sección del temario. Las 4 estrategias de tratamiento (**avoid, transfer, mitigate, accept**) también son clave.

---

## ⏱️ Risk Assessment Frequency

### Tipos de frecuencia de evaluación de riesgos

Hay 4 tipos principales, según cuándo y por qué se hacen:

**Ad hoc**

- Se hacen según necesidad, en respuesta a un evento o situación puntual que puede introducir riesgo nuevo
- Ejemplos: lanzamiento de producto, entrada a mercado nuevo, catástrofe natural, cambio regulatorio importante
- Pueden repetirse si vuelve a darse una circunstancia similar

**Recurring**

- Se hacen a intervalos regulares (anual, trimestral, mensual), parte de los procedimientos operativos estándar
- Ejemplos: institución financiera controlando credit risk / market risk / operational risk; empresa de tech haciendo penetration testing periódico con ethical hackers para encontrar vulnerabilidades nuevas desde la última evaluación

**One-time**

- Se hacen con un fin específico, atadas a un proyecto o iniciativa puntual, y no se repiten
- Ejemplos: implementación de un sistema nuevo, proyecto de construcción grande, cambio organizacional significativo

**Continuous**

- Monitoreo y evaluación constante, en tiempo real, generalmente habilitado por tecnología
- Ejemplo: equipo de ciberseguridad monitoreando amenazas/vulnerabilidades en tiempo real para responder rápido

### Ad hoc vs one-time (par que se confunde)

||Ad hoc|One-time|
|---|---|---|
|**Disparador**|Evento/situación específica|Proyecto/iniciativa específica|
|**Se repite**|Sí, si vuelve a pasar algo similar|No, nunca se repite|
|**Ejemplo**|Catástrofe natural, cambio regulatorio|Implementar sistema nuevo|

> [!warning] Para el examen
> 
> - Es muy probable que te den un escenario y tengas que identificar cuál de los 4 tipos aplica
> - La trampa clásica es **ad hoc vs one-time**: ambos suenan "puntuales", pero ad hoc es reactivo a eventos y puede repetirse; one-time está atado a un proyecto específico y no se repite nunca
> - **Continuous** = tiempo real / tecnología habilitando monitoreo constante — no confundir con "recurring" que tiene intervalos fijos (mensual/trimestral/anual)

---

## 🔎 Risk Identification & BIA

### Risk identification

Primer paso del risk management process: reconocer proactivamente amenazas y vulnerabilidades potenciales que podrían afectar las operaciones u objetivos de la organización.

- Cubre riesgos financieros, operativos, estratégicos y de reputación
- Técnicas: brainstorming, checklists, entrevistas, scenario analysis
- Incluso riesgos improbables se documentan, si el impacto potencial es alto
- Una vez identificados: se documentan y analizan por impacto y probabilidad → sirve para priorizar

### Business Impact Analysis (BIA)

Evalúa los efectos potenciales de interrumpir funciones/procesos críticos del negocio. Sirve para:

- Identificar y priorizar funciones/procesos críticos
- Evaluar impacto/riesgo potencial sobre esos procesos
- Determinar qué tan rápido hay que recuperarlos tras una interrupción

### Métricas clave del BIA

> [!example] RTO (Recovery Time Objective) Tiempo máximo aceptable de inactividad antes de que el impacto sea grave. Ejemplo: sitio de e-commerce tolera máximo 2 horas caído → RTO = 2 horas.

> [!example] RPO (Recovery Point Objective) Máxima pérdida de datos aceptable, medida en tiempo. Ejemplo: institución financiera tolera perder máximo 15 min de datos transaccionales → RPO = 15 min → implica backups al menos cada 15 min.

> [!example] MTTR (Mean Time To Repair) Tiempo promedio para reparar un componente/sistema roto. Menor MTTR = se repara más rápido = menos downtime. Ejemplo: máquina falló 5 veces en el año, cada reparación tardó en promedio 4 horas → MTTR = 4 horas.

> [!example] MTBF (Mean Time Between Failures) Tiempo promedio entre fallas — mide confiabilidad. Mayor MTBF = sistema falla menos seguido = más confiable/bien mantenido. Mismo ejemplo: 5 fallas en el año → MTBF ≈ 2.4 meses (~72 días).

|Sigla|Pregunta que responde|Objetivo ideal|Herramienta asociada|
|---|---|---|---|
|**RTO**|¿Cuánto tiempo podemos estar caídos?|Lo más **bajo** posible|Failover, Disaster Recovery Plan|
|**RPO**|¿Cuánta información podemos perder?|Lo más **bajo** posible|Frecuencia de Backups / Replicación|
|**MTTR**|¿Cuánto tardamos en arreglarlo?|Lo más **bajo** posible|Repuestos a mano, Soporte 24/7|
|**MTBF**|¿Cada cuánto tiempo se rompe?|Lo más **ALTO** posible|Hardware redundante, Calidad|

> [!warning] Para el examen
> 
> - Van a dar un escenario con números (ej: "la empresa tolera X horas caída" o "puede perder Y minutos de datos") y hay que identificar si es RTO o RPO
> - Memorizar bien las 4 siglas: RTO, RPO, MTTR, MTBF — son terreno fértil para preguntas de cálculo o definición
> - Trampa común: confundir **RTO** (tiempo de inactividad) con **RPO** (pérdida de datos) — RTO es "downtime", RPO es "data loss window"
> - Trampa común: **MTTR bajo es bueno** (repara rápido), **MTBF alto es bueno** (falla poco) — dirección opuesta, fácil de mezclar
> - BIA es el proceso que produce estas métricas — no lo confundas con risk assessment en general

---

## 📋 Risk Register

> [!info] Definición Documento que registra riesgos identificados — description, impact, likelihood, outcome, risk level, cost. Herramienta de comunicación entre stakeholders, se actualiza durante todo el ciclo de vida del proyecto. Se parece a la heat map risk matrix.

### Componentes del risk register

|Campo|Qué es|
|---|---|
|**Risk description**|Descripción clara del riesgo|
|**Risk impact**|Consecuencia potencial (costo/tiempo/calidad) — escala low/medium/high|
|**Risk likelihood**|Probabilidad — escala numérica (1-5, 1-10) o descriptiva (rare, unlikely, possible, likely, almost certain)|
|**Risk outcome**|Consecuencia si el riesgo ocurre (impact × likelihood)|
|**Risk level/threshold**|Combinación de impact + likelihood → prioriza qué atender primero (high/medium/low)|
|**Cost**|Impacto financiero del riesgo o de mitigarlo|

### Risk tolerance vs Risk appetite

**Risk tolerance (acceptance)**: cuánta incertidumbre está dispuesta a soportar la organización. "Tolerar/aceptar" = no se define contramedida (no justifica el costo, o la mitigación tiene demora inevitable).

**Risk appetite**: cuánto riesgo persigue activamente la organización para sus objetivos estratégicos. 3 tipos:

- **Expansive**: asume más riesgo por mayor retorno potencial (empresas de crecimiento agresivo)
- **Conservative**: asume menos riesgo aunque implique menor retorno (prioriza estabilidad)
- **Neutral**: equilibrio entre riesgo y retorno

### Otros dos elementos del registro

- **KRI (Key Risk Indicators)**: métricas predictivas que dan alerta temprana de exposición creciente al riesgo, vinculadas al risk appetite. Ejemplo: en un banco, aumento repentino de préstamos en default → señal de mayor riesgo → dispara investigación.
- **Risk owner**: persona/grupo responsable de gestionar el riesgo — lo supervisa, aplica mitigación, actualiza el registro. Ejemplo: PM de un proyecto de construcción es owner de riesgos como demoras por clima o sobrecosto de materiales.

> [!warning] Para el examen
> 
> - **Risk tolerance = cuánto aguanto** | **Risk appetite = cuánto riesgo busco** activamente — no son sinónimos, trampa común
> - Memorizar los 3 tipos de appetite: expansive, conservative, neutral
> - Risk level = impact × likelihood (combinación de ambos, no uno solo)
> - KRI es predictivo/proactivo (alerta antes de que escale) — distinto de solo "medir el riesgo" a posteriori
> - Risk owner = responsable de gestionar, no necesariamente quien causó el riesgo

---

## 🎨 Qualitative Risk Analysis

> [!info] Definición Método subjetivo de evaluación de riesgo basado en **likelihood** e **impact**, clasificados como low/medium/high. Se basa en experiencia/juicio del equipo (no en números duros como el cuantitativo).

- **Likelihood**: probabilidad de que ocurra el riesgo — low/medium/high, basado en experiencia pasada, análisis estadístico u opinión de expertos
- **Impact**: consecuencia si se materializa (costo, tiempo, calidad) — low/medium/high
    - Low = daño menor, funciones esenciales siguen operando
    - Medium = pérdida/daño significativo de activos
    - High = daño mayor, funciones esenciales no operan

> [!example] Dev clave que se va del proyecto (likelihood medium, impact high → mitigación: cross-training, documentación, retención); demora de materiales en construcción de rascacielos (likelihood high, impact high → mitigación: múltiples proveedores, entregas anticipadas, stock de reserva).

> [!warning] Para el examen **Qualitative** = subjetivo/cualitativo (low/med/high) vs **Quantitative** = números concretos ($, %). Risk = likelihood × impact, mismo esquema que ya vimos en risk register/risk level.

---

## 🔢 Quantitative Risk Analysis

> [!info] A diferencia del qualitative (subjetivo, low/med/high), acá se usan **valores numéricos concretos** — decisiones financieras, de seguridad y de programación basadas en cálculo.

### Componentes y fórmulas

|Sigla|Nombre|Qué es|Fórmula|
|---|---|---|---|
|**EF**|Exposure Factor|% del activo que se pierde en un evento (0%-100%)|dato estimado|
|**SLE**|Single Loss Expectancy|Pérdida monetaria esperada en **un solo** evento|Asset Value × EF|
|**ARO**|Annualized Rate of Occurrence|Frecuencia estimada de la amenaza por año|ej: ocurre 1 vez cada 2 años → ARO = 0.5|
|**ALE**|Annualized Loss Expectancy|Pérdida anual esperada|SLE × ARO|

### Ejemplo (tipo de cálculo que puede tomar el examen)

> [!example] Servidor de $10,000 EF de caída = 50%, se cae 1 vez cada 2 años:
> 
> - SLE = $10,000 × 50% = **$5,000**
> - ARO = 1/2 = **0.5**
> - ALE = $5,000 × 0.5 = **$2,500/año**

**Aplicación**: comparar ALE antes/después de una mitigación para ver si vale la pena el gasto. Ejemplo: servidor redundante que falla 1 vez cada 10 años → ALE baja a $500 (ahorro de $2,000/año), pero si el servidor nuevo cuesta $50,000 extra con vida útil de 3 años, no conviene (ahorra $6,000 en 3 años vs $40,000 extra de costo).

> [!warning] Para el examen
> 
> - **Van a pedir que calcules** SLE, ARO o ALE dado un escenario — memorizar las fórmulas de memoria: **SLE = AV × EF**, **ALE = SLE × ARO**
> - Quantitative (números, $) vs Qualitative (low/med/high) — par clásico
> - EF es un **porcentaje**, no un valor monetario — no confundir con SLE
> - ALE es la métrica final que se usa para justificar (o no) el costo de una contramedida — costo de la mitigación vs ahorro en ALE

---

## 🧩 Risk Management Strategies

4 estrategias tras identificar/evaluar un riesgo: **transfer, accept, avoid, mitigate**.

### Transfer (risk sharing)

Trasladar el riesgo a otra parte. No elimina el riesgo, solo mueve la carga financiera (el reputational risk queda en la organización original).

- **Insurance**: método más común — se paga una prima, la aseguradora cubre pérdidas hasta el límite de la póliza. Ej: liability insurance ante una demanda
- **Contractual indemnification clause**: acuerdo donde una parte se compromete a cubrir daños/pérdidas de la otra. Ej: contrato de construcción donde el contratista (no el owner) responde por daños

### Accept

Reconocer el riesgo y decidir no tomar acción. Se usa cuando el costo de mitigar supera la pérdida potencial, o el impacto es poco significativo.

- **Exemption**: la parte queda excluida de una norma/requisito por completo → no soporta el riesgo de incumplimiento. Ej: pymes exentas de ciertos requisitos de reporting financiero
- **Exception**: la parte está sujeta a la norma en general, pero puede evitarla en circunstancias específicas. Ej: excepción para procesar datos personales sin consentimiento bajo ciertas condiciones

### Avoid

Cambiar de plan/estrategia para eliminar el riesgo por completo. Se usa cuando el riesgo es demasiado grande para aceptar o transferir. Ej: no lanzar un producto que podría infringir una patente; no operar en un país políticamente inestable.

### Mitigate

Tomar acción para reducir probabilidad o impacto — la estrategia más común. Ej: training de seguridad laboral, inversión en ciberseguridad.

> [!warning] Para el examen
> 
> - Memorizar las 4: **transfer, accept, avoid, mitigate** — clasificar escenarios es la pregunta típica
> - Transfer ≠ elimina el riesgo, solo lo mueve (financieramente) — trampa común pensar que "transferir" = "sacarse el problema de encima" del todo
> - **Exemption vs exception**: exemption = excluido de la regla completamente; exception = sigue sujeto a la regla, pero se libera en casos puntuales — distinción sutil, favorita para examen
> - **Avoid** = cambiar de plan para que el riesgo ni exista; **Mitigate** = el riesgo sigue existiendo pero se reduce su probabilidad/impacto — no confundir ambos

---

## 📡 Risk Monitoring & Reporting

Última etapa del risk management process.

**Risk monitoring**: seguimiento continuo de riesgos existentes, riesgos residuales, identificación de riesgos nuevos, ejecución de planes de respuesta y evaluación de su efectividad a lo largo del proyecto. Ej: empresa de software monitorea riesgo de plazos, bugs, cambios de demanda con herramientas de PM.

**Risk reporting**: comunicar a los stakeholders resultados de identificación, evaluación, respuesta y monitoreo — normalmente en un risk report. Ej: constructora con reporte mensual de riesgos de seguridad, probabilidad de demoras, impacto financiero, compartido con PMs, ejecutivos y cliente.

### Residual risk vs Control risk

||Residual risk|Control risk|
|---|---|---|
|**Qué es**|Probabilidad + impacto que queda **después** de aplicar mitigación/transfer/acceptance|Qué tan menos efectivo se volvió un control de seguridad **con el tiempo**|
|**Ejemplo**|(riesgo inherente menos la mitigación aplicada)|Antivirus por firmas que pierde efectividad a medida que malware se oculta mejor|

### Por qué importa el monitoring/reporting

- Informed decision-making (asignación de recursos, timelines, dirección estratégica)
- Risk mitigation (detectar riesgo creciente antes de que se vuelva problema)
- Stakeholder communication (gestiona expectativas)
- Regulatory compliance (en muchos sectores el reporting es requisito legal)

> [!warning] Para el examen
> 
> - **Residual risk vs control risk** — par clásico: residual risk = lo que queda después de mitigar; control risk = degradación de un control existente con el tiempo. No son lo mismo
> - Esta es la última etapa del ciclo de risk management — útil para ordenar preguntas de "¿qué va primero?": **identify → assess (qualitative/quantitative) → strategy (transfer/accept/avoid/mitigate) → monitor & report**
> - El ejemplo del antivirus por firmas perdiendo eficacia es un buen anclaje mental para "control risk"