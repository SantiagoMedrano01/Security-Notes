## 1. Conceptos base

- **Cryptography**: práctica de escribir/resolver códigos para ocultar el significado real de la información.
- **Encryption**: convertir **plaintext** (texto legible) en **ciphertext** (texto ilegible) mediante un algoritmo + una clave.
- **Cipher**: el algoritmo que realiza la función de cifrado/descifrado.

### Ejemplo pedagógico: ROT13

Cifrado simple que rota cada letra 13 posiciones en el alfabeto (C → P, R → E, etc.). Sirve para ilustrar el concepto central de toda la sección.

### 🔑 La idea más importante de la lección: la seguridad está en la CLAVE, no en el algoritmo

- En ROT13, el algoritmo es "rotar" — pero lo que realmente protege el mensaje es saber que la clave es **13**.
- **Casi todos los algoritmos criptográficos modernos son públicos y de código abierto** (revisados por pares) — su diseño es transparente a propósito. La seguridad **nunca** depende de ocultar el algoritmo (eso sería _"security through obscurity"_, considerado poco confiable).
- La confidencialidad real depende de **mantener la clave en secreto**. Si la clave se compromete, todo el sistema cae sin importar cuán robusto sea el algoritmo.

> **Para el examen**: la idea central de toda esta sección — _"la seguridad de la criptografía vive en la clave, no en el algoritmo"_ — es el principio (conocido como **Kerckhoffs's principle**, aunque el video no lo nombra así) que subyace a casi todas las preguntas de esta parte del temario.

### Key length y key rotation

- **A mayor longitud de clave, mayor seguridad** — y la relación es **exponencial**, no lineal: pasar de 128 bits a 256 bits no duplica la fuerza, la eleva exponencialmente (más resistente a fuerza bruta).
- 128 bits = seguro para la mayoría de aplicaciones hoy; 256 bits = protección mucho mayor.
- **Key rotation**: cambiar claves regularmente mitiga el riesgo de que una clave expuesta por mucho tiempo termine siendo descubierta. Ejemplos reales: rotación anual de claves TLS, algunos cloud providers rotan cada 90 días.
- Buenas prácticas de manejo de claves: almacenarlas en **HSM (Hardware Security Modules)**, cifrarlas en reposo, transmitirlas de forma segura, y auditar/monitorear accesos.

### Los 3 estados de datos (repaso)

Reposo, tránsito, en uso — la encriptación protege en los tres.

### Mapa de la sección completa

- **Symmetric vs Asymmetric algorithms** — misma clave para cifrar/descifrar vs par de claves (pública/privada)
- **Symmetric algorithms**: DES, 3DES, IDEA, AES, Blowfish, Twofish, familia Rivest Cipher (RC)
- **Asymmetric algorithms**: Diffie-Hellman, RSA, Elliptic Curve Cryptography (ECC)
- **Hashing**: MD5, familia SHA, RIPEMD, HMAC
- **PKI (Public Key Infrastructure)** y **digital certificates**
- **Blockchain**: ledger, cryptocurrency, supply chain management
- **Herramientas de cifrado**: TPM, HSM, key management systems, secure enclaves
- **Técnicas de ofuscación**: steganography, tokenization, data masking
- **Ataques criptográficos**: downgrade attacks, collision attacks, birthday attacks, quantum computing threats

---

## 2. Symmetric vs Asymmetric Encryption

### Symmetric encryption

**Una sola clave** para cifrar y descifrar (también llamada _private key encryption_ — ambas partes comparten el mismo secreto).

> Analogía: la llave de tu casa — vos y quien tenga copia pueden entrar/salir por igual.

**Problemas clave (muy preguntados en el examen):**

1. **No repudiation imposible** — si varias personas tienen la misma clave, no podés probar quién hizo qué (ejemplo: laptop robada, cualquiera con la llave pudo haber sido).
2. **Key distribution problem** — cada par de personas que quiere comunicarse necesita su propio par de clave compartida. Con 6 personas (vos + 5 amigos) se necesitan **15 pares distintos de claves** — no escala. Fórmula: `n(n-1)/2` pares para n personas.
3. Ejemplo práctico: contraseña WiFi compartida entre 50 invitados a una fiesta = **cero confidencialidad real**, porque todos tienen el mismo secreto.

**Ventaja principal**: **velocidad** — 100 a 1000 veces más rápido que un algoritmo asimétrico equivalente en seguridad.

### Asymmetric encryption

**Dos claves distintas**: una para cifrar, otra para descifrar. También llamada _public key cryptography_. No necesita compartir un secreto — resuelve el problema de distribución de claves de symmetric.

- **Algoritmos principales**: Diffie-Hellman, RSA, ECC (Elliptic Curve Cryptography).
- **Desventaja**: mucho más lento que symmetric.

### Enfoque híbrido (clave para el examen)

Lo mejor de ambos mundos: se usa **asymmetric** para intercambiar de forma segura una **clave secreta compartida**, y luego se usa **symmetric** con esa clave para cifrar el grueso de la comunicación (mucho más rápido). Este es el modelo que usan la mayoría de las implementaciones reales (ej: TLS/HTTPS funciona así).

### Stream Ciphers vs Block Ciphers

Clasificación ortogonal a symmetric/asymmetric.

||Stream cipher|Block cipher|
|---|---|---|
|**Procesa**|Bit a bit / byte a byte, en flujo continuo|Bloques de tamaño fijo (64, 128, 256 bits)|
|**Mecanismo**|Genera un keystream y lo combina con el plaintext usando **XOR**|Divide el mensaje en bloques; si un bloque es más chico que el tamaño fijo, se usa **padding**|
|**Mejor para**|Comunicación en tiempo real (audio/video streaming)|Uso general — más fácil de implementar|
|**Implementación típica**|Hardware|Software|
|**Seguridad**|Más susceptible a problemas|Más fácil de configurar de forma segura|
|**Relación con symmetric/asymmetric**|Suelen ser symmetric|—|

> **Para el examen**:
> 
> - **Symmetric = 1 clave, rápido, problema de distribución + no repudiation**. **Asymmetric = 2 claves (pública/privada), lento, resuelve distribución**.
> - El **enfoque híbrido** (asymmetric para intercambiar la clave, symmetric para el bulk data) aparece mucho — es literalmente cómo funciona TLS.
> - **Stream vs Block** es una clasificación **independiente** — no confundir con symmetric/asymmetric. Un cipher puede ser symmetric Y block (como AES) o symmetric Y stream (como RC4).

---

## 3. Symmetric Algorithms

Todos son symmetric — la mayoría son block ciphers, **excepto RC4 (stream)**.

|Algoritmo|Tipo|Tamaño de clave|Dato clave|
|---|---|---|---|
|**DES**|Block|64 bits (56 bits efectivos, 8 de paridad)|Usado 1970s-2000s. **Débil hoy** — vulnerable a poder de cómputo moderno. 16 rondas de transposición/sustitución.|
|**3DES**|Block|Efectivamente 112 bits|Aplica DES **3 veces**: encrypt → decrypt → encrypt, con 3 claves distintas de 56 bits. Parche para la debilidad de DES.|
|**IDEA**|Block|128 bits|Bloques de 64 bits. Conocido por usarse en **PGP**. Compitió para reemplazar DES pero **no ganó**.|
|**AES**|Block|128 / 192 / 256 bits|**Ganador** del concurso del NIST para reemplazar DES/3DES. También llamado **Rijndael cipher**. **El más usado hoy** — estándar del gobierno de EE.UU. para info sensible pero no clasificada. **El más fuerte de la lista.**|
|**Blowfish**|Block|32-448 bits|Bloques de 64 bits. Diseñado como reemplazo de DES, pero no tuvo adopción masiva. **Open source, nunca patentado.**|
|**Twofish**|Block|128 / 192 / 256 bits|Bloques de 128 bits. También **open source**, sin patente.|
|**RC4**|**Stream** (único de la lista)|40-2048 bits (variable)|Creado por Ron Rivest. Usado en **SSL** y **WEP** (WiFi).|
|**RC5**|Block|Hasta 2048 bits|También de Ron Rivest.|
|**RC6**|Block|Basado en RC5, más fuerte|También compitió por el puesto de AES, pero **perdió contra Rijndael**.|

**Datos curiosos/contexto:**

- **RC1** nunca se publicó, **RC2** se consideró débil y se descartó, **RC3** fue crackeado antes de publicarse — por eso la familia "activa" es RC4/RC5/RC6.
- El concurso del **NIST** para reemplazar DES tuvo varios candidatos (IDEA, RC6) pero **AES/Rijndael ganó**.

> **Para el examen** (no hace falta memorizar tamaños exactos de bloque/clave, sino):
> 
> 1. **¿Es symmetric o asymmetric?** → Todos estos son symmetric.
> 2. **¿Es block o stream?** → Todos son block **excepto RC4**, el único stream cipher de la lista.
> 3. **AES = el más fuerte y más usado hoy.** Si preguntan "¿cuál elegirías?", la respuesta casi siempre es AES.
> 4. **DES = débil/obsoleto**, suele aparecer como el ejemplo de "qué NO usar hoy".
> 5. **RC4 → asociado a SSL y WEP** — ambos protocolos hoy considerados inseguros/obsoletos, así que RC4 suele aparecer en preguntas sobre vulnerabilidades legacy.

---

## 4. Asymmetric Algorithms

### Concepto base

**Public key cryptography**: par de claves (**public + private**). La clave pública está disponible para cualquiera; la privada solo la tiene el dueño.

### Qué garantiza cada uso de las claves (muy preguntado en el examen)

|Cifrás con...|Obtenés|Por qué|
|---|---|---|
|**Clave pública del receptor**|**Confidentiality**|Solo el receptor tiene la clave privada correspondiente para descifrar — ni siquiera el que cifró puede leerlo de nuevo|
|**Clave privada del remitente**|**Non-repudiation**|Cualquiera puede descifrarlo con tu clave pública (así que no da confidencialidad), pero solo vos tenés esa clave privada → prueba que fuiste vos quien lo firmó|

### Digital Signature = combinar ambos conceptos + integridad

Proceso completo para lograr **confidentiality + integrity + authentication + non-repudiation** a la vez:

1. Generar un **hash digest** del mensaje → da **integrity**.
2. Cifrar ese hash con la **clave privada del remitente** → esto ES la firma digital, da **non-repudiation**.
3. Cifrar el mensaje (o el paquete completo) con la **clave pública del receptor** → da **confidentiality**.

### Los 3 algoritmos asimétricos clave

**1. Diffie-Hellman**

- Usado para **key exchange** — intercambiar de forma segura una clave secreta simétrica antes de establecer un túnel (ej: **VPN/IPSec**).
- **Vulnerable a on-path/MITM attacks** si no se combina con autenticación (password o certificado digital).
- Memorizar: **asimétrico + key exchange + VPN/IPSec**.

**2. RSA**

- Nombrado por sus creadores (Rivest, Shamir, Adleman).
- Usado para **key exchange, encryption y digital signatures**.
- Se basa en la dificultad de factorizar números primos grandes.
- Soporta claves de **1024 a 4096 bits**.
- Ejemplo práctico: los **tokens de seguridad** (hardware que genera un código de 6 dígitos cada 30-60 seg para MFA) usan claves RSA de un solo uso.

**3. ECC (Elliptic Curve Cryptography)**

- Basado en estructura algebraica de curvas elípticas.
- **~6 veces más eficiente que RSA** con seguridad equivalente — una clave ECC de 256 bits equivale en seguridad a una RSA de 2048 bits.
- Por eso se usa mucho en **dispositivos móviles y de bajo consumo** (menos potencia de procesamiento necesaria).
- Variantes:
    - **ECDH** — versión ECC de Diffie-Hellman (key exchange)
    - **ECDHE** — versión "efímera", usa una clave distinta en cada sesión de intercambio
    - **ECDSA** — Elliptic Curve Digital Signature Algorithm, usado por el gobierno de EE.UU. para firmas digitales

> **Para el examen**:
> 
> - La tabla de **"cifrás con clave X → obtenés garantía Y"** es probablemente lo más preguntado de toda la lección — memorizala bien.
> - **Diffie-Hellman = key exchange / VPN**, **RSA = uso general (encryption + signatures)**, **ECC = eficiencia para mobile/low-power**.
> - Relación de eficiencia ECC vs RSA (256 bits ECC ≈ 2048 bits RSA) es un dato específico que CompTIA puede citar directamente.

---

## 5. Hashing

### Definición base

**Hashing**: función criptográfica **unidireccional** — toma una entrada y produce un **message digest** (huella digital) de tamaño fijo. **No se puede revertir** al mensaje original a partir del hash. No da confidencialidad, pero sí da integridad y autenticación/non-repudiation.

**Propiedad clave**: el output siempre tiene la **misma longitud**, sin importar el tamaño de la entrada (1 palabra o 1 millón de palabras dan un hash del mismo largo, según el algoritmo).

### Los algoritmos principales

|Algoritmo|Tamaño del digest|Notas|
|---|---|---|
|**MD5**|128 bits|El más popular históricamente, pero **débil** — 128 bits da espacio limitado de valores únicos → más propenso a **colisiones**|
|**SHA-1**|160 bits|Reduce colisiones respecto a MD5|
|**SHA-2**|224 / 256 / 384 / 512 bits (según variante)|Familia con varios tamaños; 64-80 rondas de cálculo|
|**SHA-3**|224-512 bits (igual rango que SHA-2)|Más seguro: **120 rondas** de cálculo (vs 64-80 de SHA-2)|
|**RIPEMD**|160 / 256 / 320 bits|Open source, compitió con SHA pero nunca alcanzó su popularidad. RIPEMD-160 es la versión más usada|
|**HMAC**|Variable (depende del hash base)|No es un hash por sí solo — se combina con otro algoritmo (ej: HMAC-MD5, HMAC-SHA256) para verificar integridad + autenticidad|

### Collision (concepto clave del examen)

Cuando **dos entradas distintas producen el mismo hash**. Ocurre más en MD5 por su espacio limitado de 128 bits. Es la razón principal por la que se migró a SHA-1/256/512 — **a mayor tamaño de digest, menos colisiones**.

### Demo del video (concepto de avalancha)

Cambiar **una sola letra** en un texto larguísimo (la Constitución de EE.UU.) cambia el hash resultante **completamente**. Esto es lo que hace al hashing útil para **verificar integridad**: si los hashes coinciden, el archivo no fue modificado en tránsito.

### Digital Signature — proceso completo (repaso reforzado)

1. Hashear el mensaje → obtener el digest (ej: con SHA-1).
2. Cifrar ese digest con la **clave privada** del firmante → **esto es la firma digital**.
3. Enviar mensaje + firma digital.
4. El receptor descifra la firma con la **clave pública** del firmante → recupera el digest original.
5. El receptor hashea el mensaje recibido de nuevo y **compara** ambos digests.
6. Si coinciden → **integrity** confirmada (no se modificó) + **non-repudiation** confirmada (solo el firmante pudo haber cifrado con esa clave privada).

**Algoritmos de firma digital**: DSA (gobierno de EE.UU., basado en digest de 160 bits), RSA (más usado comercialmente — rápido, sirve para encryption + signatures + key distribution), ECDSA (versión ECC).

### Code signing

Aplicación práctica de firma digital: desarrolladores de apps (Google Play, App Store) firman su instalador con su clave privada para garantizar que el archivo no fue alterado desde su publicación.

> **Para el examen**:
> 
> - **Hashing = unidireccional, verifica integridad, NO confidencialidad** (no cifra para ocultar, solo genera huella digital).
> - **MD5 = débil/obsoleto** (128 bits, propenso a colisiones) — probablemente aparezca como "qué NO usar".
> - **SHA-256 o SHA-3 = las opciones más seguras hoy** — respuesta típica cuando preguntan "¿cuál es más seguro?"
> - El proceso completo de **digital signature** (hash + cifrado con clave privada) es de los conceptos más integradores de toda la sección — asegurate de poder explicarlo paso a paso.

---

## 6. Hash Attacks & Hardening

### Los 2 ataques principales

**1. Pass-the-Hash Attack** El atacante roba el **hash** de una contraseña (no la contraseña en texto plano) y lo usa directamente para autenticarse — **sin necesidad de crackearlo primero**. Los sistemas Windows tratan el hash como equivalente a la contraseña real durante la autenticación.

- Requiere que el atacante primero escale privilegios o explote una vulnerabilidad para "cosechar" hashes.
- Herramienta clásica mencionada: **Mimikatz** — automatiza la recolección de hashes y el ataque.
- **Mitigación**: solo permitir sistemas operativos confiables en la red, configurar correctamente el **trust** de dominios Windows, parchear estaciones de trabajo, usar **MFA**, aplicar **least privilege**.

**2. Birthday Attack** Busca **colisiones** deliberadamente (dos inputs distintos → mismo hash), aprovechando la **birthday paradox**: en un grupo de solo 23 personas hay ~50% de chance de que dos compartan cumpleaños; con 57 personas, ~99%.

- Aplicado a hashing: si un atacante encuentra otra contraseña que produce el mismo hash que la tuya, puede autenticarse sin saber tu contraseña real.
- **Mitigación**: usar hashes con digest más largo (SHA-256 en vez de MD5) → reduce drásticamente la probabilidad de colisión.

### Técnicas de hardening para hashing/contraseñas

**1. Key stretching** Aplica la función hash **múltiples veces** para fortalecer una clave débil, haciendo el brute-force mucho más lento/costoso. Usado en **WPA, WPA2, PGP**.

**2. Salting** Agregar datos aleatorios (**salt**) a la contraseña antes de hashearla. Así, dos usuarios con la misma contraseña obtienen hashes **distintos**. Frustra:

- **Dictionary attacks** — probar palabras de una lista predefinida
- **Brute force attacks** — probar todas las combinaciones
- **Rainbow table attacks** — tablas precalculadas para revertir hashes; el salt obliga al atacante a calcular una tabla nueva por cada salt, haciéndolo impracticable

**3. Nonce** ("number used once") Número único (a menudo aleatorio) añadido al proceso de autenticación. Asegura que aunque el atacante robe las credenciales, no pueda **reutilizarlas** — protege contra **replay attacks** (reenviar datos capturados para acceso no autorizado).

**4. Límite de intentos de login fallidos** Bloquear la cuenta tras pocos intentos (ej: 3) — mitiga ataques de adivinanza/cracking de contraseñas, aunque genera fricción para usuarios legítimos que se equivocan.

> **Para el examen**:
> 
> - **Pass-the-hash**: el atacante usa el hash directamente, sin crackearlo — específico de entornos Windows/Active Directory.
> - **Birthday attack**: busca colisiones deliberadamente, basado en la paradoja del cumpleaños — memorizá "23 personas = ~50%" como ejemplo clásico.
> - **Salting vs Key stretching**: salting agrega datos aleatorios únicos por usuario; key stretching aplica el hash repetidamente para hacerlo más costoso de crackear — son complementarios, no lo mismo.
> - **Nonce** se asocia específicamente con prevenir **replay attacks**.

---

## 7. PKI (Public Key Infrastructure)

### Definición

PKI = sistema completo de hardware, software, políticas, procedimientos y personas, basado en cifrado asimétrico. **PKI ≠ public key cryptography**: la criptografía de clave pública es solo el proceso de cifrar/descifrar; PKI es todo el sistema alrededor (crear, gestionar, validar los pares de claves y certificados).

### El proceso completo con HTTPS (ejemplo del video)

1. Navegador se conecta a un sitio (ej: diontraining.com) y pide la **clave pública del servidor** a una **Certificate Authority (CA)** — tercero de confianza.
2. El navegador genera una **clave secreta compartida aleatoria** (ej: "51363").
3. Esa clave se cifra con la **clave pública del servidor** (asimétrico) y se envía por internet — nadie puede leerla sin la clave privada correspondiente.
4. El servidor la descifra con su **clave privada**, y ahora **ambos** conocen el mismo secreto compartido.
5. A partir de ahí, cambian a **cifrado simétrico** (ej: AES) para crear el túnel **TLS/SSL** — mucho más rápido para transferir datos en bulk.
6. Resultado: **confidentiality** (solo ambos conocen el secreto compartido) + **authentication** (solo el servidor real tiene su clave privada, así sabés que es quien dice ser) → aparece el candadito en el navegador.

> Este es exactamente el enfoque híbrido que vimos antes: asimétrico para el intercambio inicial de clave, simétrico para el bulk de la comunicación.

### Componentes clave de PKI

- **Certificate Authority (CA)**: tercero de confianza que emite certificados digitales (el dominio la tiene, entonces cuando te llega la public key, si tiene CA es segura, sino no) y mantiene la cadena de confianza entre todas las CAs del mundo.
- **Key escrow**: almacenamiento seguro de claves criptográficas con un **tercero**, para poder recuperarlas si se pierden o en investigaciones legales.
    - Caso de uso: empleado cifra documentos con su certificado personal, se va de la empresa o pierde su clave privada → sin key escrow, esos datos quedan **inaccesibles para siempre**.
    - **Controversia**: si un atacante compromete el key escrow, puede descifrar grandes volúmenes de datos → requiere seguridad y regulación de acceso extremadamente estrictas.

> **Para el examen**:
> 
> - Distinción clave: **PKI = el sistema completo** (CAs, certificados, key escrow, políticas); **Public key cryptography = solo el mecanismo de cifrado/descifrado asimétrico**, que es una pieza dentro de PKI.
> - El flujo HTTPS/TLS es el ejemplo de referencia obligatorio — reconstruilo mentalmente paso a paso porque es prácticamente garantizado que aparezca en el examen de una forma u otra.
> - **Key escrow** es un término específico que puede aparecer solo — recordá que resuelve "¿qué pasa si perdemos la clave privada?" pero introduce riesgo de seguridad centralizado.

---

## 8. Certificados Digitales

### 1. Definición y estándar

- **Certificado Digital**: documento electrónico que vincula una clave pública con la identidad de un usuario o servidor. Usan principalmente el estándar **X.509**.

### 2. Tipos de certificados por alcance

- **Certificado Comodín (Wildcard)**: protege un dominio principal y **todos sus subdominios** de primer nivel (ej: `*.diontraining.com` sirve para `www`, `cursos`, etc.).
    - _Ventaja_: ahorra dinero y gestión.
    - _Riesgo_: si se compromete la clave privada, afecta a todos los subdominios.
- **SAN (Subject Alternative Name)**: permite incluir **múltiples dominios totalmente diferentes** en un solo certificado (ej: `diontraining.com` y `jasondion.com`).

### 3. Modos de autenticación

- **Certificado de una cara (Single-sided)**: solo el servidor demuestra su identidad al cliente (el caso estándar de las páginas web HTTPS).
- **Certificado de doble cara (Dual-sided / Mutual TLS)**: tanto el cliente como el servidor se autentican mutuamente con certificados. Se usa en entornos de altísima seguridad.

### 4. Origen de la confianza

- **Certificado Autofirmado (Self-signed)**: firmado por la misma entidad que lo emitió. Sirve para entornos de prueba o redes internas, pero los navegadores muestran advertencia de riesgo por falta de validación externa.
- **Certificado de Terceros (Third-party)**: emitido por una **Autoridad de Certificación (CA)** de confianza comercial. Es la norma para sitios públicos.
- **Raíz de Confianza (Root of Trust / Cadena de confianza)**: la estructura jerárquica de confianza donde un Certificado Raíz (CA) valida a una CA Intermedia, y esta al certificado final (como un árbol genealógico).

### 5. Entidades de PKI y proceso de solicitud

- **CA (Autoridad de Certificación)**: tercero de confianza que emite y firma certificados.
- **RA (Autoridad de Registro)**: entidad intermedia que verifica la identidad del solicitante antes de pasar la orden a la CA.
- **CSR (Certificate Signing Request)**: archivo de texto codificado que el servidor envía a la CA para pedir su certificado. Incluye la **clave pública** y datos de la empresa, pero **la clave privada NUNCA se envía**.

### 6. Verificación y revocación de certificados

- **CRL (Certificate Revocation List)**: lista pública que mantiene la CA con todos los certificados revocados/cancelados.
- **OCSP (Online Certificate Status Protocol)**: protocolo en tiempo real que permite consultar si un certificado específico está revocado mediante su número de serie (más rápido que descargar toda la lista CRL).
- **Grapado OCSP (OCSP Stapling)**: el servidor web consulta periódicamente su propio estado a la CA y le "grapa" la respuesta firmada al usuario durante el handshake, haciendo la conexión más rápida y privada.
- **HTTP Public Key Pinning (HPKP)**: técnica (hoy en desuso pero evaluada) que asocia una clave pública específica a un sitio web en el navegador para evitar suplantaciones con certificados falsos.

### 7. Custodia y recuperación de claves

- **Agentes de Custodia de Claves (Key Escrow)**: tercero que almacena de forma segura una copia de la clave privada para evitar pérdida de datos si el dueño la pierde (requiere políticas de separación de funciones, ej. 2 administradores).
- **Agentes de Recuperación de Claves (Key Recovery Agent)**: software/rol encargado de restaurar claves dañadas o perdidas a partir del respaldo seguro.

### Un detalle curioso de la criptografía asimétrica

- **Para cifrar datos (privacidad)**: cifrás con la clave **PÚBLICA** del receptor y solo él descifra con su clave **PRIVADA**.
- **Para firmar digitalmente (autenticidad)**: firmás cifrando con tu clave **PRIVADA** (solo vos podés hacerlo) y todo el mundo verifica descifrando con tu clave **PÚBLICA**.
- **Relación de fortaleza ECC vs. RSA**: CompTIA pregunta frecuentemente cuál es la mejor alternativa de cifrado asimétrico para entornos con recursos limitados (smartphones, sensores IoT, tarjetas inteligentes). La respuesta correcta siempre es **ECC** porque una clave ECC de **256 bits** ofrece una seguridad equivalente a una clave RSA de **2048 bits** (o incluso 3072 bits) consumiendo una fracción del procesamiento y la memoria.
- **Verificación de integridad**: la integridad del certificado digital para asegurar que no fue modificado se logra combinando un algoritmo de **Hash (como SHA-256)** con la **firma digital de la CA**.
- **Identificación del sujeto vs. emisor**:
    - _Subject (Sujeto)_: es el propietario del sitio/servidor.
    - _Issuer (Emisor)_: es la Autoridad de Certificación (CA) que garantiza la identidad.
- **Cifrado híbrido en HTTPS**: el certificado digital (usando RSA o ECC) **solo se usa en la fase inicial (Handshake TLS)** para autenticar al servidor y negociar de forma segura una clave simétrica compartida (como AES). El tráfico pesado de la navegación no se cifra con RSA ni ECC, sino con cifrado simétrico por ser más rápido.
- **Aviso de error en el video (mitos de red)**: en el examen, no asumas que un servidor sirve ECC o RSA simplemente detectando el navegador del cliente (móvil vs. PC). La elección de la suite de cifrado (Cipher Suite) depende del soporte que negocian cliente y servidor durante el saludo TLS, siendo ECC la opción moderna recomendada globalmente para ambos entornos.

---

## 9. Blockchain

### Definición

**Blockchain**: ledger compartido e **inmutable** para registrar transacciones, rastrear activos y generar confianza. No es exclusivo de criptomonedas — es una tecnología aplicable a cualquier caso que necesite trazabilidad y confianza descentralizada.

### Estructura de un bloque

Cada bloque contiene:

- El **hash del bloque anterior** (encadena todo el historial — de ahí "block-chain").
- Un **timestamp**.
- Las transacciones, cada una con su propio hash, que se combinan progresivamente (hash de tx0 + hash de tx1 → hash combinado, y así sucesivamente) hasta formar la **estructura del bloque**.

Esta encadenación por hashes es lo que hace que **modificar un bloque pasado sea prácticamente imposible** sin que se note (cambiaría toda la cadena de hashes posteriores).

### Public ledger

Registro que mantiene identidades de participantes (de forma segura/anónima), balances, y el historial completo de transacciones. Es **descentralizado** — funciona como red **peer-to-peer** donde nadie puede alterar los datos sin el permiso/consenso adecuado.

### Smart contracts (contratos digitales)

Contratos **autoejecutables** cuyos términos están escritos directamente en código. Se ejecutan automáticamente cuando se cumplen condiciones predefinidas, sin intermediarios.

- Ejemplo: liberar fondos automáticamente al vendedor cuando el comprador confirma recepción.
- Una vez desplegado, **no puede alterarse** — a prueba de manipulación.
- Plataforma clave mencionada: **Ethereum**.
- Beneficios: transparencia, reduce fraude, reduce costos vs. contratos tradicionales.

### Permissioned blockchain (uso comercial)

Ejemplo destacado: **IBM**, impulsando blockchain para entornos comerciales — a diferencia de blockchains públicas abiertas (como Bitcoin), estas restringen quién puede participar/validar, manteniendo igual la inmutabilidad y transparencia del ledger.

### Caso de uso: Supply chain management

Trazabilidad completa de un producto (ej: alimentos) — dónde/cuándo/cómo se cultivó, cosechó, envió, procesó — todo registrado de forma inmutable en el ledger público. Nadie puede alterar esos datos retroactivamente.

> **Para el examen**:
> 
> - Blockchain se conecta con el resto de la sección de criptografía porque **usa hashing extensivamente** para encadenar bloques — es una aplicación práctica de los conceptos de hash digest e integridad ya vistos.
> - Memorizá: **inmutabilidad + descentralización + transparencia** son las 3 propiedades que blockchain aporta y que CompTIA suele resaltar como sus beneficios centrales.
> - **Smart contract** es un término específico que puede aparecer solo: "código autoejecutable con términos de contrato embebidos, sin intermediarios".
> - Diferenciá **blockchain pública** (cualquiera participa, tipo Bitcoin) de **permissioned blockchain** (acceso restringido, uso comercial tipo IBM).

---

## 10. Herramientas de cifrado: TPM, HSM, KMS, Secure Enclave

Para entender esto de forma ultra clara: imaginá que estas 4 herramientas son **diferentes niveles y formas de proteger "claves" y datos dentro del mundo digital**.

### 1. TPM (Trusted Platform Module)

> **Definición rápida**: un chip pequeño soldado dentro de la placa madre de tu laptop o PC.

**Ejemplo práctico**: tenés tu laptop de trabajo con **Windows y BitLocker** activado. Cuando la encendés, el chip **TPM** verifica primero que nadie haya alterado el hardware ni el sistema operativo. Si todo está limpio, el TPM desbloquea la clave para descifrar tu disco duro. Si alguien te roba la laptop, le saca el disco duro y lo conecta a otra computadora, el disco no se puede leer porque **la clave se quedó atrapada dentro del chip TPM** de tu laptop original.

**Para el examen**: **TPM = protección de hardware en una sola PC/laptop + BitLocker.**

### 2. HSM (Hardware Security Module)

> **Definición rápida**: un equipo físico (como un servidor o tarjeta de expansión) súper potente y extremadamente protegido físicamente contra ataques.

**Ejemplo práctico**: un banco como Visa o Mastercard procesa **millones de transacciones por segundo**. Cada vez que pasás tu tarjeta, el banco necesita firmar y cifrar esa transacción al instante con claves criptográficas súper secretas. Instala un **HSM** en su centro de datos: realiza miles de operaciones de cifrado por segundo y si un hacker intenta abrir físicamente la caja del HSM, el dispositivo se destruye por dentro borrando las claves (_tamper-proof_).

**Para el examen**: **diferencia con TPM** — TPM es para **una** laptop; HSM es un monstruo de alto rendimiento para **servidores de bancos, firmas digitales masivas y grandes empresas**.

### 3. KMS (Key Management System)

> **Definición rápida**: un software o servicio centralizado que actúa como el "gerente de las claves". No es un chip, es el sistema que administra qué pasa con una clave desde que nace hasta que muere.

**Ejemplo práctico**: imaginá que trabajás en Netflix o Spotify. Tienen millones de archivos multimedia cifrados en la nube (AWS/Google Cloud). Usan un **KMS** (como AWS KMS): crea las claves, las distribuye a los servidores de video, las **rota automáticamente cada 90 días**, y cuando una clave ya no sirve, el KMS la elimina de forma segura.

**Para el examen**: palabras clave — _cycle of life_ (ciclo de vida), _key rotation_ (rotación de claves) y gestión centralizada a gran escala.

### 4. Secure Enclave

> **Definición rápida**: un "mini-cerebro" totalmente aislado y ciego dentro del procesador principal de tus dispositivos móviles (iPhones, iPads, procesadores Apple Silicon).

**Ejemplo práctico**: desbloqueás tu iPhone con Face ID o Touch ID. El sensor toma la imagen de tu cara/huella y se la envía única y exclusivamente al **Secure Enclave**, que compara y le dice al procesador principal: _"sí, es el dueño, desbloqueálo"_. Incluso si un hacker infecta tu iPhone con un virus y toma control total del iOS, **nunca podrá robar los datos de tu cara o huella**, porque el procesador principal jamás tiene acceso directo a lo que hay guardado dentro del Secure Enclave.

**Para el examen**: palabras clave — datos biométricos (Face ID, Touch ID), aislamiento del procesador principal, teléfonos/móviles.

### 📊 Resumen para no equivocarte

|Si la pregunta te habla de...|La respuesta es...|
|---|---|
|Cifrado de disco entero en tu laptop (BitLocker)|**TPM**|
|Operaciones de alto rendimiento en un banco o datos financieros altamente críticos|**HSM**|
|Administrar, crear y **rotar automáticamente** miles de claves en la nube|**KMS**|
|Aislar los datos de la huella digital o rostro (biometría) en un celular|**Secure Enclave**|

> **Para el examen**:
> 
> - **TPM = BitLocker** es la asociación directa que probablemente pregunten.
> - **HSM = financial/high-value transactions**, mayor escala que TPM.
> - **KMS = gestión del ciclo de vida completo** de las claves — si la pregunta menciona "rotación automática de claves a gran escala", es KMS.
> - **Secure Enclave = biometría (Face ID/Touch ID)** — si la pregunta menciona datos biométricos aislados del procesador principal, es Secure Enclave.

---

## 11. Obfuscation Techniques

### Steganography

**Ocultar** un mensaje dentro de otro archivo/mensaje ordinario, para que **ni siquiera se sospeche** que existe un mensaje oculto. Objetivo distinto al del cifrado:

- **Encryption**: anuncia "hay algo importante acá, pero no lo podés leer sin la clave".
- **Steganography**: **esconde a plena vista** — nadie sospecha que hay algo escondido.

**Punto clave del examen**: la esteganografía **NO es cifrado** — los datos no están encriptados, solo ocultos. Si sabés dónde buscar, podés extraer el mensaje directamente sin necesitar ninguna clave de descifrado.

**Demo del video**: ocultar un mensaje de texto dentro de una imagen PNG usando una herramienta online — la imagen se ve visualmente idéntica, pero el tamaño del archivo cambia (señal de que podría haber sido modificado). Ejemplo clásico no-digital: el mensaje "acróstico" en anuncios de periódico (primera letra de cada palabra forma el mensaje secreto).

**Uso combinado**: a menudo se usa steganography + encryption juntos — primero cifrás el mensaje, después lo escondés dentro de otro archivo, para una doble capa de protección.

### Tokenization

Sustituir datos sensibles por un **token** sin valor intrínseco. El dato real se guarda aparte, en una bóveda separada, accesible solo por sistemas específicos que pueden mapear token → valor original.

**Ejemplo real**: pago con tarjeta de crédito en una tienda — el comerciante nunca guarda tu número real, solo el token. Si hay un breach, los atacantes solo obtienen tokens inútiles.

**Beneficio de compliance**: reduce el alcance de auditorías como **PCI DSS**, porque los sistemas que solo manejan tokens (no los datos reales) quedan fuera del scope más estricto de la regulación.

### Data Masking

Disfrazar los datos originales manteniendo su **apariencia/formato realista y utilidad**, sin exponer la info real.

**Casos de uso del video**:

- **Testing/desarrollo**: usar nombres/direcciones ficticios pero realistas en vez de datos reales de clientes, para no arriesgar una filtración en entornos no-productivos.
- **Ocultar info a empleados internos**: ejemplo de Dion Training — el soporte al cliente solo ve los **últimos 4 dígitos** de la tarjeta de crédito (los primeros 12 están enmascarados). Mismo patrón con **SSN**: solo se muestran los últimos 4 dígitos de los 9.

### Diferenciando las 3 técnicas

|Técnica|Qué hace|Reversible|
|---|---|---|
|**Steganography**|Esconde datos dentro de otro archivo/mensaje|Sí, si sabés dónde buscar (no requiere clave)|
|**Tokenization**|Reemplaza el dato por un token sin valor, guarda el real aparte|Sí, indirectamente (vía el sistema que mapea token↔valor)|
|**Data Masking**|Disfraza el dato manteniendo formato/apariencia realista|No — es **unidireccional**|

> Estas tres, junto con encryption, conforman el set completo de técnicas de **Securing Data** vistas en la sección — steganography es la única que **no aparece** en la lección anterior de Securing Data, así que prestale atención especial porque es la "nueva" del grupo.

---

## 12. Cryptographic Attacks

### 1. Downgrade Attack (Version Rollback Attack)

Fuerza a un sistema a usar un protocolo/estándar criptográfico **más débil o antiguo** que el que usaría normalmente, explotando que los sistemas modernos mantienen **backward compatibility** con protocolos legacy.

**Cómo funciona**: durante el handshake, dos sistemas negocian qué versión de protocolo usar (la más segura que ambos soporten). Un atacante (Man-in-the-Middle) intercepta y manipula esa negociación, haciendo creer a ambas partes que solo soportan la versión más vieja/débil disponible.

**Ejemplo real (memorizar)**: **POODLE** (Padding Oracle On Downgraded Legacy Encryption) — forzaba el downgrade a **SSL 3.0**, un protocolo viejo e inseguro, aunque TLS estuviera disponible.

**Por qué son peligrosos**: paradójicamente, la compatibilidad hacia atrás (pensada para inclusión/interoperabilidad) es la vulnerabilidad que se explota.

**Mitigación**: eliminar soporte a protocolos legacy inseguros, o usar **version intolerance checks** (el sistema anuncia que solo soporta la última versión; si hay downgrade forzado, se detecta rápido).

### 2. Collision Attack

Busca **dos entradas distintas que produzcan el mismo hash**. Relevante porque el hashing se usa para verificar integridad (comparar hash publicado vs hash calculado tras descargar un archivo).

**Riesgo**: un atacante puede crear un archivo malicioso con el **mismo hash** que uno legítimo, engañando al usuario para que confíe en él.

**Caso histórico**: **MD5** dejó de ser confiable porque investigadores lograron crear colisiones reales — ya no se usa en certificados de seguridad.

**Base teórica**: la **birthday paradox/attack** (ya vista) — explica por qué las colisiones son más probables de lo esperado intuitivamente.

### 3. Quantum Computing Threat

**Qubit**: bit cuántico — a diferencia del bit tradicional (0 o 1), puede representar **múltiples combinaciones simultáneamente** vía **superposición**. Esto da a la computación cuántica poder masivo para resolver **problemas matemáticos complejos** — que es exactamente la base de la criptografía moderna.

**Por qué amenaza la criptografía actual**: los algoritmos **asimétricos** (RSA, ECC) dependen de que factorizar números primos grandes sea **difícil** para computadoras clásicas. Un ordenador cuántico puede resolver ese problema **exponencialmente más rápido**, rompiendo potencialmente RSA/ECC en segundos.

**Estado actual (dato del examen)**: no existen computadoras cuánticas operativas hoy — se estima disponibilidad para gobiernos/grandes empresas recién para **~2030**, y para consumidores finales **fines de 2030s/principios 2040s**. Pero hay que prepararse desde ahora.

### Post-Quantum Cryptography (PQC)

Dos enfoques:

1. **Aumentar el tamaño de clave** en algoritmos simétricos (ej: AES-128 → AES-256) — duplicar la clave eleva **exponencialmente** las combinaciones a forzar.
2. **Algoritmos nuevos resistentes a cuántica** — usan lattice-based cryptography o supersingular isogeny key exchange.

**Estándares del NIST (2022, tras concurso de 6 años)** — para memorizar:

- **Encryption general**: **CRYSTALS-Kyber** (basado en lattice problems, equivalente en fuerza a AES-256).
- **Digital signatures**: **CRYSTALS-Dilithium** (recomendado principal), alternativas: **FALCON**, **SPHINCS+** (este último es el único basado en hash functions, no en lattices).

> **Para el examen**:
> 
> - **Downgrade attack**: memorizá **POODLE + SSL 3.0** como el ejemplo de referencia.
> - **Collision attack**: conectado con **MD5 comprometido** y la **birthday paradox**.
> - **Quantum threat**: amenaza específicamente a **algoritmos asimétricos** (RSA, ECC) porque dependen de factorización de primos — los simétricos se defienden aumentando tamaño de clave.
> - **CRYSTALS-Kyber (encryption) y CRYSTALS-Dilithium (signatures)** son los nombres específicos que probablemente pregunten como estándares NIST post-cuánticos.