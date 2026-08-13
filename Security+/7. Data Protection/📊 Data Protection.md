## 1. Data Classification

### Concepto base

La clasificación de datos se basa en **valor para la organización** + **sensibilidad si se divulga**. Quien decide el nivel de clasificación es el **data owner**.

**Por qué clasificar en vez de proteger todo igual**: proteger datos consume recursos (personal, controles de acceso, herramientas técnicas). **Over-classification** (clasificar todo como muy sensible) genera gasto innecesario de tiempo/dinero — hay que ser preciso al asignar nivel.

### Dos esquemas según tipo de organización

#### 1. Comercial (4 niveles, de menor a mayor)

| Nivel            | Descripción                                                  | Ejemplo del video                                                       |
| ---------------- | ------------------------------------------------------------ | ----------------------------------------------------------------------- |
| **Public**       | Sin impacto si se divulga, ya está abierto                   | El curso mismo de Dion Training                                         |
| **Sensitive**    | Impacto mínimo si se filtra                                  | Datos financieros, próximo curso sin lanzar aún (por competencia)       |
| **Private**      | Info relativa a una **entidad individual**, uso solo interno | Registros personales, salarios, SSN de empleados                        |
| **Confidential** | Afecta seriamente si se revela                               | Secretos comerciales, IP, código fuente, preguntas de examen de CompTIA |

> El video menciona también **Critical** como nivel extra para info donde no se puede permitir ningún riesgo — ej. números de tarjeta de crédito, acceso ultra restringido.

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

> **Para el examen**:
> 
> - Memorizá bien **ambos esquemas por separado** — CompTIA puede preguntar "¿qué nivel es X en el esquema comercial vs gubernamental?"
> - El orden comercial: **Public < Sensitive < Private < Confidential (< Critical)**
> - El orden gubernamental: **Unclassified < SBU < Confidential < Secret < Top Secret**
> - Relacioná esto con el próximo tema del temario (Data Ownership, Data States, Data Types) — esta lección es la base conceptual de toda la sección de **Data Protection** (dominios 1.4, 3.3, 4.2, 4.4, 5.1).

---

## 2. Data Ownership

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

> **Para el examen**:
> 
> - La jerarquía completa es: **Data Owner** (decide qué proteger y cómo, alto nivel) → **Data Steward** (asegura clasificación/calidad correcta) → **Data Custodian** (implementa técnicamente la protección) → **Data Controller/Processor** (términos más de compliance/GDPR, deciden y ejecutan el procesamiento) → **Privacy Officer** (supervisa todo lo de privacidad específicamente).
> - Pregunta típica: te dan un escenario (ej: "¿quién es responsable de que los backups estén cifrados?") y tenés que identificar el rol correcto — en ese caso sería **Data Custodian**.
> - Memorizá bien: **Data Owner ≠ IT department** — este es un punto que CompTIA suele usar como distractor en preguntas de examen.

---

## 3. Data States

**3 estados de los datos**, cada uno con su propia estrategia de protección.

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

> **Para el examen**:
> 
> - Los 3 estados y su mecanismo de protección característico: **at rest → encryption (a distintos niveles)**, **in transit → protocolos de túnel (SSL/TLS, VPN, IPSec)**, **in use → application-level encryption + secure enclaves**.
> - **Data in use es el más difícil de proteger** porque necesariamente hay un momento donde los datos están descifrados para poder procesarse — es un punto conceptual que CompTIA suele resaltar.
> - Memorizá los 6 niveles de encryption para data at rest (full disk → partition → file → volume → database → record) — van de más amplio a más granular.

---

## 4. Data Types

### Regulated data (categoría general)

Info controlada por leyes/regulaciones/estándares de industria. Marcos clave: **GDPR** (UE), **HIPAA** (EE.UU., salud).

### Tipos específicos

|Tipo|Qué incluye|Regulación asociada|
|---|---|---|
|**PII** (Personally Identifiable Information)|Nombre, SSN, dirección — cualquier dato que identifique a una persona|Varias leyes de privacidad|
|**PHI** (Protected Health Information)|Historial médico, tratamiento, pagos de salud vinculados a una persona|**HIPAA**|
|**Trade secrets**|Procesos de fabricación, estrategias de marketing, software propietario, listas de clientes — dan ventaja competitiva|Protección legal, sanciones por divulgación no autorizada|
|**Intellectual Property (IP)**|Invenciones, obras literarias/artísticas, diseños, símbolos|Patents, copyrights, trademarks|
|**Legal information**|Procedimientos judiciales, contratos, compliance|Confidencialidad cliente-abogado|
|**Financial information**|Registros de ventas, facturas, docs fiscales, extractos bancarios|**PCI DSS** (Payment Card Industry Data Security Standard)|

### Human-readable vs Non-human-readable

- **Human-readable**: se entiende directamente sin máquina — documentos de texto, spreadsheets.
- **Non-human-readable**: requiere una máquina/programa para interpretarse — código binario, lenguaje máquina. **Igual necesita protección** aunque sea "ilegible a simple vista", porque puede contener info sensible.

> **Para el examen**:
> 
> - Memorizá el par **PII vs PHI** — distinción clásica: PII = identifica a una persona en general; PHI = específicamente ligado a salud/tratamiento/pago médico.
> - Asociá cada tipo de dato con su regulación: **PHI → HIPAA**, **financial → PCI DSS**, **PII/datos personales → GDPR** (en contexto UE).
> - **Trade secrets vs IP**: trade secret es info que la empresa **mantiene en secreto** para ventaja competitiva (no se registra públicamente); IP son creaciones protegidas **formalmente** por patente/copyright/trademark (sí son públicas en su registro, pero protegidas legalmente contra uso no autorizado). Esta distinción es sutil y puede aparecer como trampa de examen.

---

## 5. Data Sovereignty

### Definición

**Data sovereignty**: la información digital está sujeta a las **leyes del país donde se encuentra**. Se volvió especialmente relevante con cloud computing, donde los datos suelen estar almacenados en data centers repartidos por el mundo.

### Ejemplo clave: GDPR

Protege a **cualquier ciudadano de la UE** mientras esté físicamente dentro de la UE/EEE. Aplica a **cualquier organización que maneje datos de ciudadanos de la UE**, sin importar dónde esté ubicada esa organización — el incumplimiento puede traer multas muy altas.

**Punto interesante para el examen**: la protección del GDPR es geográfica sobre la persona, no permanente — si un ciudadano de la UE sale de la UE/EEE, deja de estar protegido por el GDPR en ese momento.

### Data localization laws (variante estricta de sovereignty)

Países como **China** y **Rusia** exigen que los datos se almacenen y procesen **dentro de sus propias fronteras** — no alcanza con cumplir la ley, hay que mantener la infraestructura física ahí. Esto genera desafíos reales para empresas multinacionales que usan cloud services distribuidos globalmente.

### Consideraciones prácticas para una organización

- Saber exactamente **dónde están físicamente** sus data centers
- Rastrear el **flujo de datos entre fronteras** para evitar transferencias ilegales sin consentimiento
- Los servicios cloud a veces **restringen el acceso** de empleados según su ubicación geográfica, lo cual puede chocar con necesidades operativas reales

> **Para el examen**:
> 
> - **Data sovereignty** = las leyes del país donde están los datos aplican, sin importar de dónde es la empresa dueña.
> - **Data localization** = variante más estricta: exige que los datos físicamente **residan** en ese país (China, Rusia son los ejemplos clásicos citados por CompTIA).
> - GDPR es el caso de estudio obligatorio — memorizá que aplica por **ubicación geográfica de la persona**, no por nacionalidad ni por ubicación de la empresa.

---

## 6. Securing Data

8 técnicas para proteger datos:

1. **Geographic restrictions (geofencing)** — límites virtuales que restringen acceso por ubicación. Ej: bloquear logins desde regiones donde no hay empleados. Ayuda a cumplir **data sovereignty**.
2. **Encryption** — texto plano → texto cifrado con algoritmo + clave. **Reversible** con la clave de descifrado correcta. Protege data at rest e in transit.
3. **Hashing** — convierte datos a un valor de tamaño fijo (hash). **Función unidireccional — NO reversible**. Usado para almacenar contraseñas y verificar integridad de archivos.
4. **Masking** — reemplaza parte o todo el contenido de un campo con un placeholder (ej: X). Puede ser parcial (conservar el prefijo de un teléfono, ocultar el resto). **Unidireccional** — método de **de-identification**.
5. **Tokenization** — reemplaza datos sensibles por un **token** no sensible; el dato original se guarda aparte en una DB separada, referenciado por ese token. Uso típico: **procesamiento de pagos** (proteger número de tarjeta de crédito).
6. **Obfuscation** — hacer los datos confusos/ininteligibles para usuarios no autorizados. Es un concepto **paraguas** que puede incluir encryption, masking, pseudonimización.
7. **Segmentation** — dividir la red en segmentos con sus propios controles de seguridad. Si un atacante compromete un segmento, **no puede moverse lateralmente** a otros — limita el daño de una brecha.
8. **Permission restrictions** — definir quién accede a qué y qué puede hacer, vía **ACLs** o **RBAC** (Role-Based Access Control). Reduce riesgo de filtraciones internas.

### La distinción más importante de esta lección

|Técnica|¿Reversible?|
|---|---|
|**Encryption**|✅ Sí (con la clave)|
|**Hashing**|❌ No — unidireccional|
|**Masking**|❌ No — unidireccional (de-identification)|
|**Tokenization**|✅ Sí, pero indirectamente (el dato real vive en otra DB, se recupera vía el token)|

- **Masking**: solo ocultás la vista en pantalla (unidireccional/destructivo).
- **Tokenization**: reemplazás el dato por un _ticket de cambio_ para no procesar el dato sensible en sistemas vulnerables, pero podés recuperar el original en la caja fuerte (_vault_).

> **Para el examen**: CompTIA suele preguntar escenarios donde tenés que elegir la técnica correcta según si necesitás **recuperar el dato original o no**: si necesitás volver al dato real → encryption o tokenization; si solo necesitás verificar/comparar sin revertir → hashing; si solo necesitás ocultar visualmente sin analytics reales → masking.

---

## 7. Data Loss Prevention (DLP)

### Definición

Sistemas que monitorean datos **en uso, en tránsito y en reposo** para detectar/prevenir intentos de robo o filtración.

### Evolución histórica del robo de datos (contexto del video)

Archivador físico (robo limitado a lo que podés cargar) → laptops (robo del dispositivo completo) → discos externos (grandes volúmenes, pero voluminosos/detectables) → USB (mismo volumen, mucho más discreto) → **cloud storage** (Dropbox, Google Drive — podés exfiltrar todo sin necesitar ningún dispositivo físico, desde cualquier parte del mundo). Esta evolución es la razón por la que DLP se volvió crítico.

### Los 4 tipos de DLP

|Tipo|Dónde vive|Qué hace|
|---|---|---|
|**Endpoint DLP**|Software instalado en la estación de trabajo/laptop|Monitorea datos **en uso** en el equipo; detiene o alerta transferencias de archivos según reglas — funciona parecido a un IDS/IPS pero enfocado en datos|
|**Network DLP**|Hardware/software en el **perímetro** de la red|Inspecciona todo el tráfico entrante/saliente, con foco especial en **datos saliendo** que no deberían salir del edificio (data in transit)|
|**Storage DLP**|Software en servidores de los data centers|Inspecciona datos **en reposo** — verifica cifrado/watermarking, detecta accesos en momentos sospechosos (ej: descargas masivas a las 2am fuera de política)|
|**Cloud-based DLP**|Ofrecido como SaaS, integrado al servicio cloud|Protege datos almacenados en servicios cloud (ej: Google Drive con DLP nativo de Google)|

### Modos de operación

DLP puede configurarse en:

- **Detection mode** — solo alerta
- **Prevention mode** — bloquea activamente la transferencia

> **Para el examen**:
> 
> - Los 4 tipos de DLP se distinguen por **dónde se ubican** y **qué estado de datos protegen principalmente**: Endpoint → data in use; Network → data in transit; Storage → data at rest; Cloud → los tres, pero dentro de servicios cloud.
> - Conectá esto directamente con **Data States** (sección 3) — es básicamente la aplicación práctica de esos 3 estados a través de tecnología DLP.
> - El ejemplo de "descarga masiva a las 2am" conecta con el concepto de **out-of-cycle logging/activity** visto en indicadores de malware — mismo patrón de detección, distinto contexto.