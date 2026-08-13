
> [!info] Overview de la sección Cubre los objetivos **2.2** (threat vectors y attack surfaces), **2.3** (tipos de vulnerabilidades) y **5.3** (procesos de evaluación y gestión de riesgo de terceros).

### Temas que vienen en las próximas lecciones

- **Fundamentos** de third-party vendor risk
- **Supply chain risk**: vulnerabilidades en cadenas de suministro globales
- **Supply chain attacks**: ejemplos reales — hardware counterfeiting, chip washing, y el caso **SolarWinds** (software-based compromise)
- **Vendor assessments**: penetration testing de proveedores, right-to-audit clauses, evidencia de auditorías internas/externas
- **Vendor selection & monitoring**: proceso de selección y vigilancia continua post-onboarding
- **Contratos y acuerdos**: SLA, MOU, MOA, NDA, BPA
- Quiz final de la sección

---

## 🏭 Supply Chain Risks

> [!info] 3 categorías de riesgo en la cadena de suministro: **hardware manufacturers**, **software developers/vendors**, **service providers/MSPs**.

### Hardware manufacturers

- Productos (routers, switches) están compuestos por cientos de componentes de distintos proveedores → cada uno es una vulnerabilidad potencial si está manipulado o viene de un vendor poco confiable
- Hay que rastrear el origen de los componentes para determinar la integridad del dispositivo completo
- **Trusted Foundry program**: usado por entidades con apetito de riesgo mínimo (ej: Department of Defense) — garantiza que el hardware fue verificado rigurosamente como auténtico y que los microprocesadores solo hacen lo que deben (sin desviación del baseline conocido)
- Riesgo de comprar hardware de **fuentes secundarias/aftermarket**: más barato, pero riesgo alto de dispositivos falsificados o manipulados (código modificado con troyanos, acceso remoto no autorizado, fallas operativas)

### Software developers/vendors

- Todo software instalado en la red debe verificarse: licencia correcta, autenticidad, libre de vulnerabilidades/bugs conocidos, escaneado con antivirus/antimalware
- **Open source** es más fácil de auditar (código fuente disponible)
- **Proprietary software** (ej: Microsoft Office) también se puede escanear/evaluar contra ataques conocidos, aunque no se tenga el código fuente

### Service providers / MSPs

- Especialmente riesgosos con SaaS: confiás acceso a tus datos a un tercero
- Preguntas clave: ¿son sólidos sus protocolos de ciberseguridad? ¿mantiene confidencialidad e integridad de los datos? ¿está equipado para cooperar en incident response/forensics si hay una brecha?
- La decisión depende del **risk appetite** de la organización

> [!warning] Para el examen
> 
> - Memorizar las 3 categorías: hardware, software, service providers/MSP
> - **Trusted Foundry** es un término específico asociado al DoD — puede aparecer como ejemplo puntual
> - Concepto clave para recordar: "la cadena es tan fuerte como su eslabón más débil" — filosofía central de supply chain risk
> - Vendor selection no es solo costo — due diligence, track record histórico y compromiso con seguridad también entran en la decisión

---

## 💥 Supply Chain Attacks

> [!info] Definición Atacar el eslabón más débil de la cadena de suministro (un proveedor/vendor) para llegar a un objetivo principal mejor defendido, en vez de atacarlo directamente.

### Ejemplos reales (importantes para el examen)

> [!example] Cisco chip washing (2000s-2010s) Falsificadores tomaban chips Cisco viejos y los "lavaban" (chip washing = re-empaquetar un chip con contenido más barato o con malware embebido). Vendidos en mercado secundario como routers/switches falsificados → mejor caso: hardware fallido; peor caso: backdoor permanente para un threat actor.

> [!example] Rootkits preinstalados Por proveedores extranjeros de hardware → backdoor de fábrica.

> [!example] SolarWinds (2021) Atacantes se infiltraron en el sistema de actualización de SolarWinds Orion (software de monitoreo/gestión de redes) y distribuyeron malware a través de las actualizaciones legítimas a miles de clientes, incluyendo agencias de gobierno de EE.UU. Es el caso clásico de software-based supply chain attack — no apuntaba a un solo objetivo sino a comprometer masivamente vía un solo punto de confianza.

### CHIPS Act (2022)

Ley federal de EE.UU. (~$280B en fondos) para reducir la dependencia de semiconductores fabricados en el extranjero: $39B en subsidios de manufactura, 25% de crédito fiscal en equipos, $13B en investigación/formación. Objetivo: cadena de suministro de semiconductores más resiliente (chips están en todo: celulares, autos, dispositivos médicos, sistemas de defensa).

### 🛡️ Mitigaciones

1. **Vendor due diligence** — evaluar postura de ciberseguridad y prácticas de supply chain del proveedor antes de contratarlo
2. **Monitoreo y auditorías periódicas** — detección temprana de actividad sospechosa
3. **Educación y colaboración** — compartir inteligencia de amenazas con el sector
4. **Contractual safeguards** — cláusulas de ciberseguridad con consecuencias legales por incumplimiento

> [!warning] Para el examen
> 
> - **Memorizar el caso SolarWinds** — es prácticamente garantizado como ejemplo en preguntas de supply chain attack
> - **Chip washing** es un término específico — no confundir con "counterfeiting" en general
> - CHIPS Act: recordar que es sobre semiconductores, no ciberseguridad directamente — es una respuesta de política pública al riesgo de supply chain
> - Las 4 mitigaciones son candidatas típicas para preguntas de "¿cuál NO es una estrategia de mitigación de supply chain risk?"

---

## 🔍 Vendor Assessment

### Tipos de terceros

|Término|Qué es|Ejemplo|
|---|---|---|
|**Vendors**|Empresas/individuos que proveen bienes o servicios|Microsoft, Oracle (software)|
|**Suppliers**|Participan en producción/entrega de partes de un producto|Fabricante de PCs con proveedores de CPU, memoria, discos|
|**MSP** (Managed Service Provider)|Contratado para gestionar servicios de IT en nombre de la empresa|AWS, Google Cloud|

> [!example] Vendor vs Supplier — Caso Dell Imaginá que tu empresa es **Dell** y vendés laptops:
> 
> 1. **Intel y Samsung son tus _Suppliers_** — le suministran a Dell los procesadores (CPUs) y las memorias RAM. Dell toma esas partes, las ensambla y fabrica la laptop. Pertenecen a la **cadena de suministro** del producto.
> 2. **Microsoft es tu _Vendor_** — tu empresa (Dell) le compra a Microsoft licencias de _Office 365_ o programas de recursos humanos para que tus propios empleados trabajen en la oficina.

### Herramientas de evaluación de proveedores

- **Penetration testing del proveedor**: ciberataque simulado contra los sistemas del vendor, para validar que se toma en serio su propia postura de seguridad — el riesgo del proveedor se vuelve tu riesgo una vez que integrás su software/hardware.
- **Right-to-audit clause**: cláusula contractual que da a la organización el derecho de evaluar los procesos internos del proveedor y verificar que cumple los estándares acordados. No es desconfianza, es transparencia — filosofía "trust but verify".
- **Internal audits**: autoevaluación que hace el propio proveedor de sus prácticas contra estándares de industria o requisitos de la organización. Útil, pero puede faltarle rigor/objetividad.
- **Independent assessments**: evaluación hecha por un tercero neutral, sin interés en las operaciones del vendor ni de la organización. Ejemplo: ISO (International Organization for Standardization) evaluando un data center contra estándares globales.
- **Supply chain analysis**: examina toda la cadena de suministro del proveedor, no solo sus prácticas directas — ej: rastrear el origen de cada componente de hardware para descartar piezas falsificadas o manipuladas.

> [!warning] Para el examen
> 
> - Distinguir **vendor vs supplier vs MSP** — son categorías separadas de terceros, favoritas para preguntas de definición
> - **Internal audit vs independent assessment**: internal = el proveedor se autoevalúa; independent = evalúa un tercero neutral sin conflicto de interés — par clásico de confundir
> - "Right-to-audit clause" es un término específico de examen — recordalo asociado a contratos, no a auditorías en sí
> - Frase ancla: **"trust but verify"** — resume la filosofía de todo vendor assessment

---

## 🧭 Vendor Selection & Monitoring

### Selección de proveedores

- **Due diligence**: evaluación que va más allá de credenciales superficiales — estabilidad financiera, historial operativo, testimonios de clientes, prácticas en el terreno. Ej: proveedor de packaging ecológico → verificar no solo certificaciones sino gestión de residuos y sourcing de materiales.
- **Conflict of interest**: cuando relaciones personales/financieras de quien decide pueden sesgar la selección. Mitigación: exigir disclosure o excluir del proceso a la parte con conflicto.
- **Vendor questionnaires**: documentos que completan los proveedores potenciales con info sobre operaciones, capacidades, cumplimiento — permite comparar proveedores bajo criterios estandarizados. Ej: para cloud provider — redundancia de datos, protocolos de seguridad, SLAs de uptime, planes de disaster recovery.
- **Rules of engagement**: guías que dictan los términos de interacción entre organización y proveedores potenciales — protocolos de comunicación, políticas de intercambio de datos, límites de negociación.
    
    > [!example] Dion Training no acepta propuestas/emails no solicitados de vendors — solo responde a RFPs que ellos mismos publican.
    

### Supervisión continua

- **Performance reviews**: evaluaciones periódicas contra estándares/objetivos del contrato. Ej: revisar calidad de materiales, cumplimiento de plazos de entrega, impacto ambiental.
- **Feedback loops**: comunicación bidireccional — la organización da feedback sobre calidad, el proveedor propone mejoras al proceso de adquisición.

> [!warning] Para el examen
> 
> - Memorizar los términos: **due diligence, conflict of interest, vendor questionnaires, rules of engagement, performance reviews, feedback loops**
> - Selección de proveedor no termina en la firma del contrato — el monitoreo continuo es igual de importante, porque el mercado y el proveedor cambian con el tiempo
> - Conflict of interest es candidato típico de pregunta de escenario ("¿qué principio se viola si...?")

---

## 📄 Contracts & Agreements

7 tipos de documentos que estructuran la relación con un vendor/tercero:

|Sigla/Nombre|Qué es|Ejemplo|
|---|---|---|
|**Basic contract**|Formaliza roles, responsabilidades y consecuencias por incumplimiento|Dev de software y cliente: pagos, plazos, specs|
|**SLA** (Service Level Agreement)|Define el nivel de servicio esperado, con penalidades si no se cumple|Downtime de servidor no debe superar 2h/mes o hay penalidad|
|**MOA** (Memorandum of Agreement)|Más formal, define responsabilidades específicas de cada parte|Campaña de marketing conjunta: quién hace contenido, distribución, financiamiento|
|**MOU** (Memorandum of Understanding)|Menos vinculante, declaración de intención mutua sin detalles exactos|Dos orgs expresando intención de explorar una futura alianza|
|**MSA** (Master Service Agreement)|Acuerdo global con términos generales para múltiples transacciones futuras|Relación recurrente con cliente, sin redactar contrato nuevo cada vez|
|**SOW** (Statement of Work)|Detalles de un proyecto específico: entregables, cronograma, hitos (también "scope of work")|Complementa al MSA con el detalle puntual de cada proyecto|
|**NDA** (Non-Disclosure Agreement)|Protege info sensible compartida antes de una asociación formal|Startup compartiendo tecnología propietaria con un inversor|
|**BPA** (Business Partnership Agreement)|Para cuando dos entidades combinan recursos — reparto de ganancias, toma de decisiones, exit strategy|Dos empresas lanzando un producto juntas; también llamado Joint Venture (JV)|

> [!warning] Para el examen
> 
> - **MOA vs MOU** — par clásico: MOA es formal y específico en responsabilidades; MOU es una intención mutua, menos vinculante y sin detalle
> - **MSA vs SOW** — trabajan juntos: MSA = términos generales recurrentes; SOW = detalle de un proyecto puntual específico
> - Memorizar las 8 siglas: SLA, MOA, MOU, MSA, SOW, NDA, BPA (+ contrato básico)
> - **BPA = Joint Venture (JV)** — sinónimos, puede aparecer con cualquiera de los dos nombres en el examen