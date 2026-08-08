
> [!info] Definición base **Social engineering**: manipulación psicológica para lograr acceso no autorizado a sistemas, datos o espacios físicos — explota a la **persona**, no la tecnología.

---
## 🧠 Motivational Triggers

6 triggers que usan los ingenieros sociales para manipular a sus víctimas:

### 1. Authority

La gente obedece a quien percibe con poder/posición. Ejemplo: atacante se hace pasar por manager, cliente importante, o agente del **IRS**/gobierno amenazando con multas/arresto para sacar info.

### 2. Urgency

Presión de tiempo que hace saltarse procedimientos normales.

> [!example] Ejemplos del video
> 
> - Alguien con cajas "llega tarde a una reunión" pidiendo que le abras la puerta (tailgating facilitado por urgencia)
> - USB entregado con excusa de "necesito imprimir esto YA para mi presentación en 5 minutos" → salteás el escaneo de malware normal
> - Llamada al help desk pidiendo reset de password urgente, saltándose la verificación en persona

### 3. Social proof (consensus)

La gente se guía por lo que hacen los demás. Ejemplo: sitio falso que consigue likes/shares en redes → más gente confía porque "sus amigos ya lo usaron". Mismo principio que reviews de productos/cursos con muchas inscripciones.

### 4. Scarcity

Presión por disponibilidad limitada ("solo quedan 5 cupos", "MacBook a $1000 solo para los primeros 5").

> [!tip] Scarcity vs Urgency **Scarcity = cantidad limitada** · **Urgency = tiempo limitado**

### 5. Liking

La gente confía más en quien le cae bien. Por eso los social engineers suelen ser carismáticos/atractivos. Técnicas: coquetear, fingir amistad, encontrar intereses en común (deportes, música, series) para generar rapport y bajar la guardia de la víctima.

### 6. Fear

Explota ansiedades para forzar acción. Ejemplo clásico: **ransomware** ("paga o pierdes tus archivos") o falsos agentes del FBI amenazando con arresto.

> [!warning] Punto clave para el examen Los triggers se pueden **combinar** — el ejemplo del falso FBI usa **fear + authority** al mismo tiempo, haciendo el ataque más efectivo.

---

## 🎪 Impersonation Attacks

4 formas de impersonation que hay que distinguir bien para el examen:

### 1. Impersonation (general)

El atacante asume la identidad de otra persona para ganar acceso o robar datos. La clave del éxito: **recopilar detalles específicos primero** (nombre, departamento, piso) para sonar creíble.

> [!example] "Soy Mike de IT, tercer piso" convence mucho más que "trabajo en la empresa" — más detalle = más credibilidad falsa.

### 2. Brand impersonation

Versión específica dirigida a hacerse pasar por una **empresa/marca** conocida (logo, lenguaje de marketing, look-and-feel) en emails o sitios de phishing.

> [!example] Eli Lilly (noviembre 2020) Cuenta falsa de Twitter haciéndose pasar por **Eli Lilly** tuiteó que la insulina sería gratis. Se viralizó, inversores vendieron acciones creyendo que era real → caída del 4% en el precio de la acción en <24hs. Pérdida de miles de millones en market cap por un solo tuit falso.

### 3. Typosquatting (URL hijacking / cybersquatting)

Registrar un dominio parecido al legítimo pero con **error tipográfico común**, para capturar usuarios que escriben mal la URL.

- Ejemplos: **gnail.com** en vez de gmail.com, o usar un **cero en vez de la letra O** (Di0ntraining.com vs Diontraining.com).
- Variante: **subdomain hijacking** — registrar algo como `diontraining.azure.com` (dominio de un cloud provider legítimo) aunque la empresa real no use ese proveedor, para que el email parezca oficial.
- **Mitigación**: la organización compra proactivamente sus propias variantes con errores comunes (ejemplo: Accolade registra "acclade.com" y redirige a su sitio real).

### 4. Watering hole attack

Ataque **dirigido y pasivo**: el atacante compromete un sitio/servicio de terceros que **sabe que la víctima usa habitualmente**, en vez de atacarla directamente.

> [!tip] Metáfora Un depredador espera en el abrevadero donde sabe que sus presas van a tomar agua.

- **Pasivo** porque no hay comunicación directa atacante-víctima; el ataque ocurre a través de un sitio confiable comprometido.
- Mitigación: sistemas actualizados, threat intelligence, herramientas de detección de malware avanzadas.

> [!warning] Para el examen Distinción clave — **typosquatting** = la víctima comete el error (escribe mal la URL); **watering hole** = la víctima no comete ningún error, simplemente visita un sitio legítimo que fue comprometido de antemano. Memorizá el caso **Eli Lilly** como ejemplo clásico de **brand impersonation** con impacto financiero real y medible.

---

## 📞 Pretexting

### Qué es

**Pretexting**: crear un escenario/excusa falsa creíble para manipular a la víctima y que revele información. Se diferencia de otras técnicas en que se apoya en una **historia elaborada**, no solo en presión momentánea.

### La técnica clave: "rellenar los huecos"

El atacante no sabe nada de la empresa objetivo, pero:

1. Arranca con un **dato probable/genérico** ("¿siguen usando HP LaserJet?") — asumiendo que la mayoría de empresas tiene algo similar.
2. Si se equivoca, la propia víctima **corrige el dato** ("no, es una Konica Minolta C368") — y ahora el atacante tiene info real, gratis.
3. Con ese dato real, suena **más creíble** todavía y puede pedir el siguiente paso (verificar la IP de la impresora).
4. Cada respuesta de la víctima se usa como munición para la siguiente pregunta — construcción incremental de confianza.

### Por qué funciona

- La recepcionista no tiene motivo para sospechar: son preguntas "inocentes" (modelo de impresora, IP) que no parecen sensibles.
- Pero esos datos "inofensivos" son justo lo que un atacante necesita para reconocimiento (**recon**) antes de un ataque real — ej: la IP de la impresora podría usarse para explotar vulnerabilidades del dispositivo.

### 🛡️ Mitigación clave

**Security awareness training**: entrenar a empleados para **nunca dar información por teléfono**, ni siquiera datos que parecen inocentes (modelo de impresora, IP) — porque cualquier dato "de relleno" alimenta el siguiente paso del ataque.

> [!warning] Punto para memorizar Pretexting ≠ solo mentir — es la técnica de usar **datos parcialmente correctos o plausibles** para que la víctima misma complete la información faltante, sin darse cuenta de que está siendo interrogada.

---

## 🎣 Phishing Family

### Distinción principal: alcance del ataque

|Tipo|Target|Analogía|
|---|---|---|
|**Phishing**|Masivo, sin dirigir (miles/millones de emails al azar)|"Red amplia" — spray and pray|
|**Spear phishing**|Selectivo, grupo/individuo específico con research previo|Cazador que estudió a su presa|
|**Whaling**|Solo ejecutivos de alto nivel (CEO, CFO)|"Caza de ballenas" — pez grande, mayor recompensa|

### Ejemplo clave para distinguir phishing vs spear phishing

- **Phishing**: mandar 1 millón de emails random haciéndose pasar por Bank of America — funciona porque ~1 de cada 5 estadounidenses es cliente BofA, aunque la mayoría de destinatarios no lo sea.
- **Spear phishing**: usar una lista de 500 clientes reales filtrados en un data breach de un banco específico ("Dion Savings and Loan") y mandarles un email dirigido — mucho más difícil de detectar porque el contexto es real.

### Los 6 tipos completos

1. **Phishing** — email masivo, hace pasar por fuente confiable, busca credenciales/datos.
2. **Spear phishing** — versión dirigida, personalizada con info recolectada del target.
3. **Whaling** — spear phishing contra C-level (CEO/CFO). Requiere más preparación pero recompensa mucho mayor — a menudo es el **primer paso** para comprometer una cuenta ejecutiva y lanzar ataques posteriores.
4. **BEC (Business Email Compromise)** — comprometer o suplantar una cuenta corporativa **legítima** (de un ejecutivo/socio confiable) para pedir transferencias no autorizadas o data sensible a Finance/HR.
    
    > [!example] Dato del examen Según el FBI IC3, causó **$2.7 mil millones en pérdidas** el último año reportado, con aumento del 14.5%.
    
5. **Vishing** (voice phishing) — por teléfono, haciéndose pasar por banco/gobierno. Suele ser **más efectivo que el email** porque la gente tiende a ser más confiada/amable por voz.
6. **Smishing** (SMS phishing) — por mensaje de texto, con links o números falsos, jugando con urgencia.

> [!note] **Todos son subtipos de phishing** — phishing es la categoría paraguas, y las otras cinco son variaciones específicas dentro de esa categoría, diferenciadas por **a quién apuntan** o **por qué canal** se ejecutan.

> [!warning] Para el examen La pregunta más común es dar un escenario y pedirte identificar cuál de los 6 es — fijate siempre en **quién es el target** (masivo vs específico vs ejecutivo) y **el canal** (email, teléfono, SMS) para clasificarlo correctamente. **BEC es el que más plata mueve**, por lejos.

---

## 🛑 Phishing Prevention

### Concepto clave

El **phishing** es uno de los attack vectors más usados hoy en día. Se basa en engañar a personas para que revelen información sensible, causando pérdidas económicas y data breaches.

### Anti-phishing campaign

Suele incluir:

- **User training** sobre distintos tipos de ataques: phishing, spear phishing, whaling, business email compromise (BEC), vishing, smishing.
- **Simulated phishing campaign**, realizada por un contratista externo o plataforma SaaS, para dar práctica real a los usuarios.
- **Remedial training** para los usuarios que caen en los correos simulados.
- Debe ser un **esfuerzo continuo** (las amenazas evolucionan constantemente).

### 🔍 Indicadores clave de un email de phishing

1. **Urgency** — presión para actuar rápido (ej: "reclamá tu premio en 4 horas").
2. **Unusual requests** — pedidos de passwords, números de tarjeta, etc. (el soporte técnico o el banco nunca piden esto por email).
3. **Mismatched URL** — el _display text_ de un link puede no coincidir con la URL real. Siempre hay que hacer **hover** sobre el link para ver la URL subyacente antes de hacer clic. Ejemplo típico: "paypal.com/login" que en realidad apunta a "paypal.hacked.xyz" (**brand impersonation**).
4. **Strange/spoofed email addresses** — el _display name_ puede no coincidir con la dirección real; hay que verificar el dominio del remitente.
5. **Poor spelling/grammar** — señal clásica, aunque con IA generativa (ChatGPT, etc.) los atacantes hoy pueden evitar este error fácilmente. Muchos atacantes dejan errores **a propósito** para filtrar y quedarse solo con las víctimas más crédulas (self-selection).

### 🚨 Qué hacer ante un posible phishing

- **Report** el mensaje rápido (a IT/security, ej: [phishing@dominio.com](mailto:phishing@dominio.com)).
- No hacer clic en links ni entregar información.
- Como security professional, al triage:
    - Analizar el mensaje usando los indicadores mencionados.
    - **Notificar a todos los usuarios** (broadcast) porque otros pudieron recibir el mismo correo.
    - Si se hizo clic o se abrió el correo: hacer **investigación rápida** y **triage de sistemas** afectados.
    - Si el ataque tuvo éxito: revisar y actualizar contramedidas (spam filters, más training).

> [!warning] Para el examen, recordá
> 
> - **Vishing** = voice phishing / **Smishing** = SMS phishing / **Whaling** = ataque a ejecutivos de alto nivel / **BEC** = Business Email Compromise.
> - **Typosquatting / URL hijacking** relacionado con URLs mal escritas.
> - **Hovering over links** es la técnica estándar para verificar URLs — recordar "user awareness" como control.
> - Este tema cae dentro del dominio de **Security Awareness / Social Engineering** de Security+.

---

## 💸 Fraud & Scams

### Fraud vs theft (distinción base)

**Fraud**: engaño ilícito para obtener beneficio — la víctima **entrega** sus objetos de valor (info, plata) engañada. Se diferencia del robo común porque no hay acceso forzado; la víctima "coopera" sin saber que la están estafando. Por eso se clasifica como social engineering.

### Identity fraud vs Identity theft (distinción clave para el examen)

- **Identity fraud**: usar info de otra persona para un acto puntual — ej. tomar la tarjeta de crédito robada y hacer cargos con ella.
- **Identity theft**: asumir **completamente** la identidad de la víctima — ej. usar su SSN, nombre y fecha de nacimiento para empezar un trabajo nuevo haciéndose pasar por ella.

> [!note] Nota importante del examen En el uso común la gente usa ambos términos indistintamente (y "identity theft" es el más popular coloquialmente), pero **CompTIA prefiere el término "identity fraud"** para describir ambos casos — tenelo presente si te preguntan terminología específica de Security+.

### Scams — el ejemplo desarrollado: Invoice Scam

> [!example] Mecánica paso a paso
> 
> 1. Atacante llama a un empleado, usa **pretexting** para "verificar" el modelo de impresora/tóner que usan.
> 2. Si el empleado corrige el dato ("no, usamos Lexmark B612"), el atacante ahora tiene info real y suena más creíble.
> 3. Confirma un "pedido" de tóner, el empleado dice "sí, dale" sin pensarlo — **queda grabado diciendo que sí**.
> 4. Días después llega tóner real a la oficina + una **factura legítima** por un precio inflado (ej: $950 por dos cajas que cuestan $100 en retail), **sin devoluciones ni cambios**.
> 5. La empresa termina pagando porque técnicamente "aceptaron" el pedido por teléfono.

**Variante técnica**: factura en PDF adjunta a un email de **spear-phishing** dirigido al departamento de facturación — el PDF tiene código malicioso embebido que instala un **RAT (Remote Access Trojan)** cuando lo abren.

> [!warning] Para el examen
> 
> - **Fraud/scams se consideran técnicas de ingeniería social "low-tech"** — se apoyan en manipulación telefónica/humana, aunque pueden combinarse con malware (como en la variante PDF).
> - El invoice scam es un ejemplo clásico que puede aparecer como escenario: reconocé el patrón (llamada de "verificación" → confirmación grabada → factura inflada sin reembolso).
> - Mitigación clave: entrenar a empleados para **no confirmar pedidos o dar información por teléfono sin verificar** el número/identidad del que llama primero.

---

## 📢 Influence Campaigns

### Definición base

**Influence campaigns**: esfuerzos coordinados para moldear percepción/comportamiento público hacia una causa, persona o grupo. Pueden ser benignas (campañas de salud pública) o maliciosas (manipular elecciones). En ciberseguridad nos enfocamos en las **maliciosas**, típicamente ejecutadas por **nation-state actors** o **hacktivist groups**.

### La distinción clave del examen: Misinformation vs Disinformation

||Intención|Ejemplo del video|
|---|---|---|
|**Misinformation**|Sin intención de dañar — errores honestos que se viralizan|Gente creyendo y compartiendo que hacer gárgaras con agua salada o beber cloro prevenía el COVID-19|
|**Disinformation**|**Deliberada** — creada intencionalmente para engañar y manipular|Campaña rusa en elecciones EE.UU. 2016|

> [!tip] La diferencia no está en si la info es falsa (ambas lo son), sino en la **intención** de quien la origina/comparte.

### Ejemplos clave para memorizar

> [!example] Elecciones EE.UU. 2016 Agentes del Estado ruso crearon cuentas/páginas falsas en Facebook y Twitter, publicando contenido políticamente divisivo e info falsa para manipular la opinión pública hacia el candidato preferido del gobierno ruso. Es el caso de referencia para **disinformation vía nation-state actor**.

> [!example] Twitter Bitcoin scam 2020 Brecha de seguridad comprometió cuentas de alto perfil (Obama, Biden, Musk, Gates). Los atacantes tuitearon desde esas cuentas ofreciendo "duplicar" cualquier Bitcoin enviado a una dirección — la gente confió por la credibilidad de las cuentas hackeadas y perdió su dinero.
> 
> **Punto clave para el examen**: este caso muestra que las influence campaigns **no siempre son políticas** — también pueden usarse para **financial gain** puro (mismo incidente que ya vimos antes como ejemplo de insider threat combinado con atacante externo — dos ángulos distintos).

### 🛡️ Mitigación

- Media literacy (alfabetización mediática)
- Fact-checking prioritario
- Transparencia y accountability
- Regulación adecuada de contenido/publicidad política online

> [!warning] Para el examen La pregunta típica te da un escenario y pregunta "¿es misinformation o disinformation?" — la clave siempre es **¿hubo intención de engañar desde el origen?** Si alguien comparte algo falso creyendo que es verdad = misinformation. Si alguien lo creó a propósito para manipular = disinformation.

---

## 🕵️ Otros ataques de Social Engineering

### 1. Diversion theft

Crear una distracción para robar algo mientras la atención está en otro lado. Versión digital: **DNS spoofing** — manipular el DNS para que una URL legítima redirija a un sitio falso (normalmente combinado con **brand impersonation**), donde se roban credenciales/datos de tarjeta.

### 2. Hoaxes

Engaños/alertas falsas difundidas por redes sociales, email, etc. Suelen combinarse con phishing/impersonation.

> [!example] Alerta de "tu Windows tiene un virus" en una Mac — claro indicio de hoax porque malware de Windows no afecta macOS/Linux.

**Mitigación**: pensamiento crítico, verificar la fuente antes de actuar.

### 3. Shoulder surfing

Espiar directamente para robar info (PIN, contraseñas).

> [!tip] Ojo con el examen No requiere estar físicamente cerca — cámaras de alta potencia o CCTV pueden hacer shoulder surfing a distancia.

**Mitigación**: privacy screens, blindaje de teclados en zonas abiertas.

### 4. Dumpster diving

Buscar en la basura documentos con info sensible.

- Variante moderna: **digital/virtual dumpster diving** — buscar en la papelera de reciclaje o archivos "eliminados" de un sistema.
- **Mitigación**: triturar documentos, política de **clean desk**, borrado seguro de archivos digitales.

### 5. Eavesdropping

Escuchar conversaciones privadas sin conocimiento de las partes. Puede ser físico (escuchar una llamada) o técnico — conecta con **on-path/adversary-in-the-middle attacks**, interceptando comunicación entre dos partes.

**Mitigación**: canales cifrados, encriptación de datos en tránsito.

### 6. Baiting

Dejar un dispositivo infectado (USB) donde la víctima lo encuentre, apostando a la curiosidad humana. Ya lo vimos como técnica de removable device threat vector.

### 7. Piggybacking vs Tailgating

> [!warning] Clave para el examen — con ejemplos nombrados
> 
> - **Tailgating**: **Jane** pasa su tarjeta, el atacante se cuela detrás **sin que ella lo note** — no hay consentimiento.
> - **Piggybacking**: **John**, queriendo ser amable, deja pasar a alguien disfrazado de repartidor con las manos ocupadas — **consentimiento voluntario** aunque no sepa que es un atacante.

> [!note] Dato extra del video El piggybacking es particularmente usado por **insider threats** para entrar sin registrar su propia tarjeta en el log de seguridad — así evitan dejar rastro de su propio acceso.

---

> [!warning] Para el examen Memorizá los 7 términos con su definición corta — CompTIA suele dar escenarios cortos y pedir identificar cuál es cada uno. El par **piggybacking/tailgating** es el más repetido en todo el dominio de social engineering, así que asegurate de tenerlo 100% automático.