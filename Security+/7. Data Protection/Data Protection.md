## Data Classification —

### Concepto base

La clasificación de datos se basa en **valor para la organización** + **sensibilidad si se divulga**. Quien decide el nivel de clasificación es el **data owner**.

**Por qué clasificar en vez de proteger todo igual**: proteger datos consume recursos (personal, controles de acceso, herramientas técnicas). **Over-classification** (clasificar todo como muy sensible) genera gasto innecesario de tiempo/dinero — hay que ser preciso al asignar nivel.

### Dos esquemas según tipo de organización

#### 1. Comercial (4 niveles, de menor a mayor)

|Nivel|Descripción|Ejemplo del video|
|---|---|---|
|**Public**|Sin impacto si se divulga, ya está abierto|El curso mismo de Dion Training|
|**Sensitive**|Impacto mínimo si se filtra|Datos financieros, próximo curso sin lanzar aún (por competencia)|
|**Private**|Info relativa a una **entidad individual**, uso solo interno|Registros personales, salarios, SSN de empleados|
|**Confidential**|Afecta seriamente si se revela|Secretos comerciales, IP, código fuente, preguntas de examen de CompTIA|

_(el video menciona también **Critical** como nivel extra para info donde no se puede permitir ningún riesgo — ej. números de tarjeta de crédito, acceso ultra restringido)_

#### 2. Gubernamental/Militar (5 niveles, de menor a mayor)

|Nivel|Impacto si se divulga|Ejemplo|
|---|---|---|
|**Unclassified**|Ninguno — puede hacerse público (ej: **FOIA** — Freedom of Information Act en EE.UU.)|Info pública del gobierno|
|**Sensitive but Unclassified (SBU)**|No afecta seguridad nacional, pero sí a los individuos involucrados|Historiales médicos de militares|
|**Confidential**|Afecta **seriamente** al gobierno|Secretos comerciales gubernamentales|
|**Secret**|**Podría dañar seriamente** la seguridad nacional|Planes de despliegue militar, postura defensiva|
|**Top Secret**|Máximo nivel — dañaría gravemente la seguridad nacional|Planos de sistemas de armamento|

**Nota de matiz del video**: la diferencia entre Confidential/Secret/Top Secret está en la **gravedad progresiva** del daño potencial ("afecta seriamente" → "podría dañar seriamente" → "dañaría gravemente").

### Data lifecycle (mencionado al cierre)

Los datos no se guardan para siempre — la organización necesita políticas claras sobre:

- **Cómo** se almacenan
- **Cuándo/cuánto tiempo** se retienen
- **Cómo** se destruyen al final

Además de cumplir requisitos legales de retención según jurisdicción y tipo de organización.

---

**Para el examen**:

- Memorizá bien **ambos esquemas por separado** — CompTIA puede preguntar "¿qué nivel es X en el esquema comercial vs gubernamental?"
- El orden comercial: **Public < Sensitive < Private < Confidential (< Critical)**
- El orden gubernamental: **Unclassified < SBU < Confidential < Secret < Top Secret**
- Relacioná esto con el próximo tema del temario (Data Ownership, Data States, Data Types) — esta lección es la base conceptual de toda la sección de **Data Protection** (dominios 1.4, 3.3, 4.2, 4.4, 5.1).

## Data Ownership — resumen para Security+

### Los 6 roles (de arriba hacia abajo en jerarquía)

|Rol|Quién es|Responsabilidad|
|---|---|---|
|**Data Owner**|Ejecutivo senior (no IT)|Responsabilidad **última** de CIA (confidentiality, integrity, availability) del activo. Define cómo se etiqueta y qué controles aplicar.|
|**Data Controller**|Entidad que decide propósito/método|Decide **para qué y cómo** se recolectan/almacenan/usan los datos, y garantiza legalidad. **No puede delegar** la responsabilidad ante una violación de privacidad.|
|**Data Processor**|Grupo/individuo contratado|Ejecuta la recolección/almacenamiento/análisis **siguiendo instrucciones** del Data Controller.|
|**Data Steward**|Trabaja para el Data Owner|Se enfoca en la **calidad de los datos y metadata** — asegura el etiquetado y clasificación correctos.|
|**Data Custodian**|Típicamente sysadmin/IT|Gestiona el **sistema técnico** donde se almacenan los datos: access control, encryption, backups — según los requisitos que fija el Data Owner.|
|**Privacy Officer**|Supervisa todo lo relacionado a privacidad|Maneja **PII, SPI, PHI**; responsable directo si hay un data breach relacionado a privacidad; asegura cumplimiento legal, purpose limitation, consent, data minimization, sovereignty, retention.|

### Punto clave del video: ¿quién debería ser el Data Owner?

**Error común**: muchas organizaciones ponen al **CIO/departamento de IT** como data owner de todo. El instructor dice que está **mal** — IT conoce los **sistemas**, no el **contexto de negocio** de los datos. IT debería ser el **Data Custodian**, no el Data Owner.

**Regla correcta**: el Data Owner debe ser alguien del área de negocio que **entiende el contenido y contexto** de esos datos específicos.

- Ejemplo: datos contables → el jefe de Contabilidad/CFO es el data owner, no IT.
- Empresa de software → el departamento de diseño de software.
- Cada departamento puede tener su propio data owner sobre su información específica.

---

**Para el examen**:

- La jerarquía completa es: **Data Owner** (decide qué proteger y cómo, alto nivel) → **Data Steward** (asegura clasificación/calidad correcta) → **Data Custodian** (implementa técnicamente la protección) → **Data Controller/Processor** (términos más de compliance/GDPR, deciden y ejecutan el procesamiento) → **Privacy Officer** (supervisa todo lo de privacidad específicamente).
- Pregunta típica: te dan un escenario (ej: "¿quién es responsable de que los backups estén cifrados?") y tenés que identificar el rol correcto — en ese caso sería **Data Custodian**.
- Memorizá bien: **Data Owner ≠ IT department** — este es un punto que CompTIA suele usar como distractor en preguntas de examen.
## Data States —

**3 estados de los datos**, cada uno con su propia estrategia de protección:

### 1. Data at Rest

Datos almacenados sin moverse (disco duro, servidores, bases de datos). Target primario para atacantes por su naturaleza estática.

**Protección: encryption**, con varios niveles de granularidad:

|Tipo|Alcance|
|---|---|
|**Full disk encryption**|Todo el disco duro. Cifrado cuando está apagado, descifrado al loguearse.|
|**Partition encryption**|Solo particiones específicas (ej: solo la unidad D)|
|**File encryption**|Un archivo individual puntual|
|**Volume encryption**|Un conjunto seleccionado de archivos/directorios|
|**Database encryption**|Nivel columna, fila o tabla completa|
|**Record encryption**|Campos específicos dentro de un registro — útil cuando distintos usuarios tienen distintos niveles de acceso sobre la misma DB|

### 2. Data in Transit (a.k.a. Data in Motion)

Datos moviéndose activamente (internet, red privada). Vulnerables a **interception** durante el trayecto.

**Protección: transport/communication encryption**:

- **SSL/TLS** — protocolos criptográficos para navegación web, email, transferencias
- **VPN** — conexión segura sobre una red menos segura
- **IPSec** — autentica y cifra cada paquete IP en el flujo de datos

### 3. Data in Use

Datos siendo activamente creados, leídos, actualizados o eliminados (**CRUD**). El estado más pasado por alto, pero igual de vulnerable — el desafío es que **hay que descifrarlos para poder procesarlos**.

**Protección**:

- **Application-level encryption**
- **Access controls**
- **Secure enclaves** — entorno aislado donde se procesan los datos protegidos
- Ejemplo mencionado: **Intel Software Guard (SGX)** — cifra datos mientras existen en memoria, para que procesos no confiables no puedan leerlos

---

**Para el examen**:

- Los 3 estados y su mecanismo de protección característico: **at rest → encryption (a distintos niveles)**, **in transit → protocolos de túnel (SSL/TLS, VPN, IPSec)**, **in use → application-level encryption + secure enclaves**.
- **Data in use es el más difícil de proteger** porque necesariamente hay un momento donde los datos están descifrados para poder procesarse — es un punto conceptual que CompTIA suele resaltar.
- Memorizá los 6 niveles de encryption para data at rest (full disk → partition → file → volume → database → record) — van de más amplio a más granular.