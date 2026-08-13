## ⚖️ Tensión Seguridad vs. Comodidad

La seguridad es difícil de mantener no solo por _hackers_ externos, sino por amenazas internas (_insider threats_). Existe un conflicto constante: a mayor _usability_, menor es el _security posture_ (y viceversa).

### Definiciones básicas

- **Information Security**: Protege los datos en sí.
- **Information Systems Security**: Protege los dispositivos y redes que procesan esos datos.

---

## 🛡️ Modelo CIA / CIANA

> [!info]
> 
> - **CIA Triad**: _Confidentiality_ (acceso solo autorizado), _Integrity_ (datos intactos) y _Availability_ (recursos accesibles).
> - **CIANA**: Añade _Non-repudiation_ (no poder negar una acción) y _Authentication_.

## 🔑 Modelo AAA

_Authentication_ (verificar identidad), _Authorization_ (permisos de acceso) y _Accounting_ (registro y auditoría de actividades).

## 🏰 Security Controls y Zero Trust

Se presentan categorías de controles (_technical, management, operational, physical_) y tipos (_preventive, deterrent, detective, corrective, compensatory, directive_), además del modelo _Zero Trust_ (verificar siempre por defecto mediante el _control plane_ y el _data plane_).

---

## ⚠️ Threat vs Vulnerability vs Risk

- **Threat**: Cualquier factor externo (cyberattacks, natural disasters) fuera de nuestro control directo que puede causar daño a un sistema. No se pueden evitar por completo, pero se busca minimizar su impacto.
- **Vulnerability**: Debilidad interna en el diseño, implementación o configuración de un sistema (software bugs, misconfigurations, unpatched systems). La organización sí tiene control sobre ellas para corregirlas o mitigarlas.
- **Risk**: Es la intersección donde se cruzan una _threat_ y una _vulnerability_. Si hay una amenaza pero no existe una vulnerabilidad asociada (o viceversa), no existe un riesgo real.

### Risk Management

Consiste en tomar decisiones diarias para manejar el riesgo sobre los sistemas. Sus cuatro respuestas principales son:

|Respuesta|Descripción|Ejemplo|
|---|---|---|
|**Mitigate**|Reducir el impacto o la probabilidad|—|
|**Transfer**|Trasladar el riesgo|Contratar un _cyberinsurance_ para que una aseguradora cubra los costos financieros si hay un ataque|
|**Avoid**|Evitar la actividad riesgosa|Prohibir el uso de memorias USB en la empresa para eliminar ese vector de ataque|
|**Accept**|Asumir el riesgo|Asumir el riesgo de mantener un servidor antiguo secundario sin actualizar porque el costo de cambiarlo es mayor al daño posible|

> [!tip] Objetivo principal Garantizar la _service continuity_, proteger los datos y mantener la postura de seguridad global minimizando las vulnerabilidades o aplicando medidas paliativas.

---

## 🤐 Confidentiality (primer pilar de la CIA Triad)

> [!info] Concepto clave Proteger la información frente al acceso o divulgación no autorizados (_"keeping data secret"_).

### Importancia

- Protege la privacidad personal (_personal privacy_).
- Mantiene la ventaja competitiva (_competitive advantage_).
- Garantiza el cumplimiento normativo (_regulatory compliance_ como PII o PHI).

### Métodos para garantizarla

- **Encryption**: Convertir _plaintext_ a _ciphertext_ mediante claves (método principal).
- **Access Controls**: Restringir permisos de usuario (lectura/escritura).
- **Data Masking**: Ocultar parte de los datos sensibles (ej. mostrar solo los últimos 4 dígitos de una tarjeta).
- **Physical Security**: Cerraduras, biometría en _server rooms_ o cámaras para proteger dispositivos e información física.
- **Training & Awareness**: Capacitación continua para prevenir el _human error_ y la negligencia.

---

## ✅ Integrity (segundo pilar de la CIA Triad)

> [!info] Concepto clave Garantizar que los datos y sistemas se mantengan exactos, completos e inalterados (_"accurate and unchanged"_) desde su estado original, a menos que sean modificados intencionalmente por alguien autorizado.

### Importancia

- **Data Accuracy**: Asegura que las decisiones empresariales se tomen con información correcta.
- **Maintain Trust**: Previene la pérdida de confianza de los usuarios si los datos sufren alteraciones (ej. cambios no autorizados en saldos bancarios).
- **System Operability**: Evita fallos, comportamientos inesperados o caídas del sistema causadas por datos corruptos o alterados.

### Métodos para garantizarla

- **Hashing**: Genera un valor o huella digital (_hash digest_) de tamaño fijo. Cualquier cambio mínimo en los datos cambia drásticamente el resultado (técnica principal).
- **Digital Signatures**: Cifra el _hash digest_ usando una _private key_ para validar tanto _integrity_ como _authenticity_.
- **Checksums**: Verifica la integridad de los datos durante su transmisión mediante la comparación de valores antes y después del envío.
- **Access Controls**: Restringe permisos para que solo personal autorizado pueda modificar o escribir datos.
- **Periodic Audits**: Revisiones sistemáticas de _logs_ y operaciones para detectar discrepancias o cambios no autorizados en el sistema.

---

## 🟢 Availability (tercer pilar de la CIA Triad)

> [!info] Concepto clave Garantizar que la información, sistemas y recursos estén operativos y accesibles para los usuarios autorizados cuando los necesiten (_"always available"_).

### 📊 Métrica de disponibilidad ("Nines of Availability")

|Nivel|Downtime anual permitido|
|---|---|
|**99% (Two Nines)**|Más de 3.5 días|
|**99.9% (Three Nines)**|Hasta 8.76 horas|
|**99.999% (Five Nines)**|_Gold standard_ — máximo 5.26 minutos|

### Importancia

- **Business Continuity**: Evita pérdidas financieras por minutos de inactividad.
- **Customer Trust**: Previene la migración de clientes a la competencia por falta de acceso al servicio.
- **Reputation**: Mantiene la imagen y credibilidad de la organización a largo plazo.

### Redundancy (método principal)

> [!tip] Concepto Duplicación de componentes críticos para evitar _single points of failure_.

- **Server Redundancy**: _Load balancing_ o _failover_ entre múltiples servidores.
- **Data Redundancy**: Almacenamiento distribuido (RAID, _backups_ locales y _cloud_).
- **Network Redundancy**: Múltiples proveedores e itinerarios de red.
- **Power Redundancy**: Generadores y sistemas UPS (_Uninterruptible Power Supply_).

---

## ✍️ Non-repudiation

> [!info] Definición Medida de seguridad que evita que una entidad niegue su participación en una comunicación o transacción digital.

**Mecanismo principal**: Se logra mediante el uso de **digital signatures**, las cuales combinan un **hash** del mensaje cifrado con la **private key** del usuario a través de **asymmetric encryption**.

### Importancia

1. **Authenticity**: Confirma la identidad del emisor y previene la _impersonation_.
2. **Integrity**: Valida que el contenido no haya sido alterado en tránsito.
3. **Accountability**: Aporta trazabilidad e imputabilidad irrefutable sobre las acciones realizadas.

### ¿Por qué la integridad es un pilar propio y no solo un complemento?

> [!example] Podés tener integrity SIN non-repudiation Un archivo subido a un servidor puede incluir un **hash** público. Cualquiera puede descargarlo y verificar su _integrity_ (comprobar que no está corrupto ni alterado). Pero ese hash no te dice quién creó el archivo ni te impide negar su autoría; solo valida el estado del archivo.

> [!example] NO podés tener non-repudiation SIN integrity Para probar legal o técnicamente que vos firmaste un documento, el sistema debe demostrar primero que el documento no cambió un solo bit desde que aplicaste tu _private key_. Si el contenido cambió, la _digital signature_ se rompe y el _non-repudiation_ se destruye.

> [!tip] En la **CIA triad**, la _integrity_ es un objetivo de seguridad fundamental y amplio por sí mismo. El _non-repudiation_ es un servicio avanzado de seguridad que se construye combinando _integrity_ (vía hashes) con _authenticity_ (vía claves privadas).

---

## 🪪 Authentication

> [!info] Definición Medida de seguridad que verifica que un usuario o entidad sea quien dice ser.

### Factores de autenticación

|Factor|Descripción|Ejemplo|
|---|---|---|
|**Knowledge factor** (_something you know_)|Información memorable|username, password|
|**Possession factor** (_something you have_)|Objetos físicos o dispositivos|ID card, código enviado al smartphone|
|**Inherence factor** (_something you are_)|Características físicas o biométricas|facial recognition, fingerprint|
|**Action factor** (_something you do_)|Acciones o patrones de conducta únicos|dinámica de escritura, forma de caminar|
|**Location factor** (_somewhere you are_)|Ubicación geográfica|geofencing, restricciones por país|

### Conceptos clave

- **Multi-Factor Authentication (MFA)** o **Two-Factor Authentication (2FA)**: Combinación de dos o más factores para aumentar la seguridad.
- **Propósito**: Evitar el _unauthorized access_, proteger la _privacy_ del usuario y validar el uso legítimo de _shared resources_.

---

## 🎟️ Authorization

> [!info] Definición Determina los permisos y privilegios concedidos a una identidad autenticada, definiendo qué acciones puede realizar dentro de un sistema (_what you can do_).

### Conceptos clave

- **Role-Based Access Control (RBAC) / Rule-Based / Attribute-Based**: Mecanismos que definen los accesos según la función, reglas o atributos del usuario.
- **Backend systems**: Áreas restringidas del sistema a las que solo acceden roles específicos como _system administrators_ o _content moderators_.

### Importancia

1. **Protect sensitive data**: Restringe la información confidencial solo a personal autorizado.
2. **Maintain system integrity**: Evita modificaciones accidentales o maliciosas al limitar los privilegios de configuración.
3. **Streamline user experience**: Muestra a cada usuario únicamente las opciones e interfaces relevantes para su rol.

---

## 📋 Accounting

> [!info] Definición Se centra en monitorear, rastrear y registrar detalladamente todas las actividades de los usuarios o entidades dentro de un sistema (_what you did_).

### Conceptos clave

- **Audit trail**: Registro cronológico de eventos para rastrear cambios, anomalías o accesos no autorizados.
- **Compliance**: Cumplimiento de regulaciones legales sobre protección de datos y privacidad mediante registros exhaustivos.
- **Forensic analysis**: Investigación post-incidente para entender cómo ocurrió una brecha de seguridad y evitar su repetición.
- **Resource optimization**: Seguimiento del uso de recursos (_cloud storage_, _bandwidth_) para mejorar el rendimiento y reducir costos.
- **User accountability**: Fomento de la responsabilidad al saber que las acciones son rastreables (_transparency_).

### Tecnologías principales

- **Syslog servers**: Centralizan y agregan registros (_logs_) de múltiples dispositivos para detectar patrones.
- **Network analyzers** (ej. Wireshark): Capturan y analizan el _network traffic_ en tiempo real.
- **Security Information and Event Management (SIEM)**: Correlaciona y analiza alertas de seguridad en tiempo real en toda la infraestructura.

> [!tip] Resumen La contabilidad se utiliza para garantizar que cada acción dentro de un sistema sea rastreada y registrada. Este meticuloso mantenimiento de registros proporciona transparencia, permite el cumplimiento de la normativa, ayuda en el análisis forense, garantiza la optimización de los recursos y responsabiliza a los usuarios de sus acciones. Del mismo modo que en el mundo digital se desea un extracto detallado de las transacciones bancarias para garantizar la transparencia financiera, la contabilidad es un testimonio de la integridad y seguridad de un sistema.

---

## 🗂️ Security Control Categories

> [!info] Clasifican los controles para lograr una postura de seguridad integral en la organización (_holistic approach_).

- **Technical controls**: Mecanismos de software y hardware que actúan de forma automatizada (p. ej., firewalls, antivirus, encryption, Intrusion Detection Systems - IDS).
- **Management controls** (o _administrative controls_): Gobernanza, estrategia y toma de decisiones alineadas al riesgo del negocio (p. ej., risk assessments, security policies, incident response strategies).
- **Operational controls**: Procedimientos del día a día guiados por procesos y acciones humanas (p. ej., backup procedures, account reviews, cambio periódico de passwords, programas de awareness training).
- **Physical controls**: Medidas tangibles en el mundo real para proteger activos físicos e infraestructura (p. ej., surveillance cameras, biometric scanners, guardias de seguridad, destrucción de documentos).

## 🎛️ Security Control Types

> [!info] Clasifican las medidas de protección según su función estratégica y el momento en el que actúan frente a un incidente.

|Tipo|Descripción|Ejemplo|
|---|---|---|
|**Preventive**|Medidas proactivas que bloquean la amenaza antes de que ocurra|firewalls, access controls|
|**Deterrent**|Desaniman o disuaden al atacante al visibilizar las consecuencias|carteles de advertencia, warning banners|
|**Detective**|Monitorean e identifican actividades sospechosas en tiempo real o tras el suceso|IDS, video surveillance|
|**Corrective**|Mitigan el daño y restauran el sistema a la normalidad una vez detectada la amenaza|antivirus aislando/eliminando malware, restauración de backups|
|**Compensating**|Soluciones alternativas que suplen la imposibilidad de aplicar el control primario ideal|usar VPN sobre WPA2 en legacy systems que no soportan WPA3|
|**Directive**|Dictan, guían o exigen comportamientos mediante normas y reglamentos|Acceptable Use Policy (AUP), políticas de seguridad|

> [!tip] Cada tipo de control ayuda a complementar a los demás y a crear un mayor nivel de seguridad general. Los controles preventivos sientan las bases, los controles disuasorios disuaden de las amenazas, los controles detectivescos vigilan, los controles correctivos intervienen en caso de emergencia, los controles compensatorios ofrecen refuerzos y mitigaciones, y los controles directivos guían todo el proceso.

---

## 🏯 Zero Trust

### La idea central

Antes, la seguridad de redes funcionaba como un castillo medieval: ponés murallas fuertes (firewalls, IPS, defensas perimetrales) alrededor de todo, y una vez que estás adentro del castillo, sos de confianza. Ese modelo se llama **perimeter-based security**.

El problema es que hoy en día ya no hay un "adentro" claro: la gente labura desde casa, usa la nube, se conecta desde el celu, terceriza servicios. Eso se llama **deperimeterization** — se diluyó el perímetro. Entonces las murallas del castillo ya no alcanzan, porque un atacante puede "volar por encima" (conectarse remoto, robar una credencial, etc.) sin pasar por la muralla.

### La solución: Zero Trust

En vez de confiar en alguien porque "ya está adentro de la red", el mantra es: **"never trust, always verify"** — no confiás en nada, verificás todo, siempre. Da igual si el usuario está en la oficina o conectándose desde afuera: siempre se re-verifica identidad y permisos, en cada transacción.

### Las dos partes de la arquitectura

**Control plane** (define las reglas):

- **Adaptive identity**: no alcanza con verificar una vez, se evalúa continuamente el comportamiento, dispositivo, ubicación del usuario.
- **Threat scope reduction**: dar acceso solo a lo mínimo necesario (principio de least privilege), así si te roban una credencial, el daño queda limitado.
- **Policy-driven access control**: reglas claras según el rol de cada usuario.
- **Secured zones**: zonas aisladas donde solo entra quien tiene permiso.
- Dentro del control plane están el **policy engine** (el "libro de reglas" que decide si la solicitud cumple) y el **policy administrator** (quien gestiona esas políticas).

**Data plane** (ejecuta las reglas):

- El **subject/system** es quien pide acceso (usuario, app, dispositivo).
- El **policy enforcement point** es el que finalmente permite o bloquea el acceso, según lo que decidió el policy engine.

> [!tip] Control plane vs Data plane
> 
> - **Control plane = el cerebro que decide.** Es donde se definen las reglas, se evalúa el contexto (identidad, dispositivo, comportamiento) y se decide si algo debería tener acceso o no. Es lógica, políticas, inteligencia.
> - **Data plane = el músculo que ejecuta.** Es donde realmente pasa el tráfico, donde el usuario intenta tocar el recurso, y donde se aplica —a rajatabla— lo que el control plane decidió. No piensa, solo cumple la orden: permite o bloquea.

### 📝 Resumen compacto

> [!info] **Zero Trust**: modelo de seguridad que asume que ningún usuario/sistema es confiable por default, sin importar si está dentro o fuera de la red. Reemplaza el viejo modelo de _perimeter security_ (castillo con murallas), que quedó obsoleto por la _deperimeterization_ (cloud, remote work, mobile, outsourcing).
> 
> Mantra: _never trust, always verify_
> 
> - **Control plane**: define políticas
>     - Adaptive identity (verificación continua y contextual)
>     - Threat scope reduction (least privilege)
>     - Policy-driven access control
>     - Secured zones
>     - Componentes: policy engine + policy administrator
> - **Data plane**: aplica políticas
>     - Subject/system (quien pide acceso)
>     - Policy enforcement point (quien concede/deniega el acceso)

---

## 📊 Gap Analysis

> [!info] Definición Proceso para evaluar la diferencia entre el estado actual y el estado deseado de una organización, con el fin de identificar mejoras.

### Pasos

1. Definir el alcance
2. Recolectar datos del estado actual
3. Analizar y detectar los gaps
4. Armar plan de acción (metas + timeline)

### Tipos

- **Technical gap analysis**: infraestructura (ej: red no soporta encryption in transit o Zero Trust)
- **Business gap analysis**: procesos de negocio (ej: gestión de datos, forecasting)

> [!tip] En la práctica Se suele alimentar de un **vulnerability assessment**, y el output accionable es un **POA&M** (Plan of Action and Milestones) que prioriza y asigna recursos/plazos a cada gap detectado.