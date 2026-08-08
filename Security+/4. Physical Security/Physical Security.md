## Intro de la sección

### Objetivos de examen que cubre

- **1.2** — resumir conceptos fundamentales de seguridad (herramientas/conceptos de physical security)
- **2.4** — dado un escenario, analizar indicadores de actividad maliciosa (ataques contra controles físicos)
### Temas que van a tratar (de afuera hacia adentro)
**Perímetro externo:**
- **Bollards** — postes cortos y resistentes para bloquear acceso vehicular
- **Fences** — barreras físicas (postes + alambre/tablas) para delimitar espacio
**Ataques de fuerza bruta física:**
- Forced entry
- Manipulación de dispositivos de seguridad
- Confrontación con guardias
- Embestir una barrera con vehículo
**Vigilancia:**
- **Surveillance systems** = video vigilancia + guardias + iluminación + sensores, y cómo un atacante puede evadirlos/engañarlos.
**Control de acceso a edificios:**
- **Access control vestibule** — sistema de doble puerta controlada electrónicamente donde solo una puerta puede estar abierta a la vez (mantrap).
- **Piggybacking** vs **Tailgating** — distinción clave para el examen:
    - **Piggybacking**: la persona autorizada **deja pasar intencionalmente** a alguien sin acceso (colaboración consciente).
    - **Tailgating**: la persona no autorizada sigue de cerca sin que el autorizado lo sepa/consienta (no hay complicidad).

**Cerraduras (locks):**

- Padlocks, pin-and-tumbler, cerraduras numéricas, inalámbricas, biométricas, cifradas, sistemas de acceso electrónico.
- Demo de **lock picking** en cerraduras pin-and-tumbler, para mostrar qué tan rápido se pueden vulnerar controles simples.
**Access cards:**
- Tarjetas **RFID/NFC** para acceso a oficinas.
- Demo de **card cloning** usando **Flipper Zero** (herramienta de pentesting físico).
---
**Punto clave para memorizar ya**: la diferencia **piggybacking vs tailgating** es un clásico del examen — piggybacking = con consentimiento, tailgating = sin consentimiento/sin que se note.

### Fencing & Bollards — 
**Fencing**: barrera perimetral (madera, metal, chain-link, hormigón) que protege grandes áreas contra **personas**. Tres funciones: disuasión visual, barrera física, y **delay** (retrasa al intruso, dando tiempo a que responda seguridad). Vulnerable a escalar, cortar, o cavar por debajo — se contrarresta con altura, barbed wire/electrificación, materiales resistentes, o malla enterrada.
**Bollards**: postes cortos y robustos (acero/hormigón) que bloquean **vehículos**, no personas. Uso típico: antiterrorismo (evitar vehicle-borne IEDs cerca de edificios) y anti **ram-raiding** (delincuente estrella el auto contra una vitrina para robar). Pueden estar disfrazados (maceteros, las bolas rojas de Target). Se clasifican por rating **ASTM** (cuánta fuerza/velocidad de vehículo detienen sin ceder).
**La distinción que importa para el examen**:
- **Fencing** = contra personas, perímetros grandes
- **Bollards** = contra vehículos, puntos específicos

## Physical Brute Force Attacks —

**Brute force** en física = método directo/violento para vencer barreras (distinto del sentido cyber de "probar todas las combinaciones").
### Las 4 formas
1. **Forced entry** — romper ventanas/puertas/vallas físicamente. Punto débil típico de una puerta: **la cerradura**. Mitigación: vidrio laminado/reforzado, puertas de núcleo sólido con marco metálico, deadbolts.
2. **Tampering with security devices** — no destruir, sino manipular: trabar una puerta de seguridad para que quede abierta, cegar cámaras con pintura/luz/espejos, inutilizar sensores/alarmas. Mitigación clave: **redundancia** (capas de seguridad, así si una falla las demás siguen activas).
3. **Confronting security personnel** — el más grave: agresión física o con armas contra guardias para forzar acceso. Mitigación: entrenamiento en conflict resolution/defensa personal + comunicación rápida para pedir refuerzos.
4. **Ramming barriers with a vehicle** — usar un vehículo para embestir vallas, puertas o el edificio. Poco común salvo targets de alto valor (gobierno, militar, bancos). Mitigación: **bollards** (conecta directo con la lección anterior).
    
**Para el examen**: son 4 categorías concretas que probablemente te pregunten identificar en un escenario — fijate que "tampering" es la única que no es directamente destructiva/violenta, es más sutil (manipular en vez de romper).

## Surveillance Systems — 

**Definición**: sistema organizado para observar y reportar actividad en un área. Combina 4 categorías: video surveillance, security guards, lighting, sensors.
### 1. Video surveillance (CCTV)
- Control **detective** (detecta, no previene).
- **Wired** vs **wireless**: wireless es más fácil de instalar, pero vulnerable a interferencia o **jamming** por un atacante.
- **Indoor vs outdoor** cameras — outdoor debe resistir intemperie, más cara.
- **PTZ (Pan-Tilt-Zoom)**: cámara que un guardia puede mover/ajustar en tiempo real (el clásico joystick de película de atraco).
- Ubicación clave: entradas/salidas de infraestructura crítica — data center, comm closets, puertas del edificio.
### 2. Security guards
La forma más flexible/adaptable: detectan comportamiento sospechoso, responden en tiempo real, toman decisiones, y actúan como disuasión visual.
### 3. Lighting
Subestimada pero clave: reduce sombras/escondites, mejora calidad de video, disuade. **Motion-activated lighting** cumple doble función: ilumina + alerta.
### 4. Sensors — 4 tipos (pregunta clásica de examen)

|Sensor|Cómo funciona|Uso típico|
|---|---|---|
|**Infrared**|Detecta cambios en radiación infrarroja de cuerpos calientes|Efectivo en poca luz/oscuridad|
|**Pressure**|Se activa con peso sobre el sensor (piso/alfombrilla)|Zonas restringidas, detectar entrada|
|**Microwave**|Emite pulsos de microondas y mide el reflejo de objetos en movimiento|Cubre grandes áreas, pero propenso a **falsas alarmas** (alta sensibilidad)|
|**Ultrasonic**|Mide reflexión de ondas ultrasónicas (como ecolocalización de murciélago)|Puertas automáticas, detección de movimiento en interiores|

---
**Para el examen**: memorizá bien los 4 tipos de sensores y su mecanismo — CompTIA suele dar un escenario ("¿qué sensor detecta mejor en la oscuridad?" → infrared) y pedirte identificar cuál es. También tené clara la distinción **CCTV = detective control**, no preventivo.

## Bypassing Surveillance Systems — 
5 técnicas para eludir vigilancia:
1. **Visual obstruction** — bloquear la línea de visión de la cámara: spray/espuma en el lente, sticker/cinta, o interponer objetos (paraguas, globos).
2. **Blinding sensors/cameras** — saturar con luz repentina (linterna potente, láser) para inutilizar temporal/permanentemente. Contra sensores infrarrojos: **calentar la habitación** para engañarlos.
3. **Acoustic interference** — tapar audio con música/ruido fuerte, jammers de frecuencia específicos para micrófonos, o white noise machines.
4. **EMI (Electromagnetic Interference)** — interferir las señales de sistemas de vigilancia **inalámbricos** con jammers, apuntando a bandas específicas (ej: WiFi) para tumbar todo el sistema.
5. **Attacking the physical environment** — explotar el entorno del equipo:
    - Cambiar temperatura de la sala para engañar sensores infrarrojos
    - Cortar la fuente de alimentación (desenchufar, sabotear transformadores) si no hay backup power
    - Provocar un incendio (extremo, ilegal como **arson**, distrae y daña equipos)
**Método adicional**: manipulación física directa (cortar cables) — efectivo pero requiere estar cerca del dispositivo, más riesgo de ser detectado.
### Contramedidas (defensa)
- **Tamper alarms** en cámaras (alertan si alguien las manipula)
- **Backup power / UPS** contra ataques a la alimentación
- **Frequency-hopping encoded signals** contra jamming y eavesdropping
---
**Para el examen**: la clave es asociar cada técnica de ataque con su contramedida específica — CompTIA suele dar un escenario de bypass y preguntar qué control mitigaría ese ataque puntual (ej: "cámara inalámbrica dejó de transmitir de repente" → sugiere EMI/jamming → contramedida: frequency-hopping).

### Access Control Vestibules — resumen para Security+
#### Definición
**Access control vestibule** (mantrap): sistema de **doble puerta** controlada electrónicamente donde solo una puerta puede estar abierta a la vez. Crea un espacio intermedio entre el área no confiable (afuera) y el área confiable (adentro), donde se verifica identidad/credenciales antes de dejar pasar.

**Cómo funciona**: entrás por la puerta exterior → se cierra detrás tuyo → quedás "atrapado" en el medio → se verifica tu identidad → si pasa, se abre la interior; si falla, quedás atrapado hasta que seguridad intervenga.
#### Piggybacking vs Tailgating (repaso reforzado con ejemplos concretos del video)
- **Piggybacking**: hay **complicidad** — la persona autorizada deja pasar conscientemente a alguien no autorizado (a menudo por ingeniería social). Ejemplo real del instructor (pentester): se disfrazaba de delivery con cajas y pedía a un empleado que pase su tarjeta por él — funcionaba ~50% de las veces.
- **Tailgating**: **sin conocimiento/consentimiento** — el no autorizado se cuela justo detrás de alguien que sí pasó su credencial (ej: colarse por un torniquete apenas se abre).
**Por qué el vestibule ayuda contra piggybacking específicamente**: el espacio suele ser lo bastante chico como para que entre **una sola persona** por vez — literalmente no hay lugar físico para que entren dos juntas.
#### Access cards
- Tecnologías: **RFID**, **NFC**, o bandas magnéticas antiguas.
- Autentican identidad contra una base de datos centralizada y validan permisos.
- **Acceso granular por rol**: ejemplo del instructor en la NSA — tener clearance para pasar el vestibule principal no significaba acceso a todas las oficinas; cada oficina individual tenía su propio lector como segunda capa de verificación.
- **Audit trail**: cada swipe queda registrado — clave para investigar breaches después.
#### Security guards (elemento humano)
Complementan la tecnología:
- Disuasión visual
- Backup de verificación si el sistema electrónico falla
- Gestión de visitantes (credenciales temporales)
- Respuesta inmediata ante un breach
---
**Para el examen**: la combinación **vestibule + access cards + guards** es el ejemplo típico de **defense in depth / layered security** en el dominio físico. Y la distinción piggybacking (con complicidad) vs tailgating (sin consentimiento) sigue siendo el punto más preguntado de este tema

## Door Locks —
### Idea central
Todas las defensas de perímetro (fences, bollards, cameras, guards, vestibules) fallan en algún punto — el momento crítico es **cuando alguien ya está dentro del edificio**. Ahí es donde entran los **door locks** como última línea de defensa para proteger data centers, server rooms, network closets, etc.
### Tipos de cerraduras (de más débil a más fuerte)
**1. Padlocks (candados) — pin-and-tumbler** Los más débiles. El instructor demuestra en vivo que un atacante con una **tension wrench + single-pin lockpick** puede abrirlo en ~15 segundos manipulando los pines uno por uno. No sirven para proteger network closets ni gabinetes con info clasificada.
**2. Basic door locks** (dormitorio, baño) Se vencen metiendo una varilla/aguja delgada, o con un destornillador plano/moneda si es de ranura simple.
**3. Traditional key locks** (puerta de entrada de una casa) Algo más complejas, pero un atacante experto las abre igual con lockpicking en 30-60 segundos.
**4. Electronic locks** — mucho más seguras, usan distintos factores:
- **PIN-based**: ej. PIN de 8 dígitos (1 en 100 millones de probabilidad de adivinar al azar). Permite PINs únicos por persona → **audit trail**.
- **Wireless-based**: NFC, WiFi, Bluetooth, RFID (ej: abrir la puerta tocándola con el smartphone).
- **Biometric**: huella, reconocimiento facial, escaneo de retina. Es el factor de autenticación **"algo que sos"** (inherence factor), uno de los 5 factores de autenticación.
**5. Cipher locks** Cerradura mecánica antigua con botones numerados donde hay que ingresar la combinación correcta. Más cara que una cerradura tradicional, pero mayor protección — usada en server rooms/network closets.
### Biometría: conceptos clave para el examen
- **FAR (False Acceptance Rate)**: el sistema autentica erróneamente a alguien que NO debería tener acceso. Ideal: reducirlo a cero aumentando sensibilidad.
- **FRR (False Rejection Rate)**: el sistema rechaza a alguien que SÍ debería tener acceso. Aumentar sensibilidad para bajar el FAR puede subir el FRR (trade-off).
- **CER / EER (Crossover Error Rate / Equal Error Rate)**: el punto donde FAR = FRR. **Cuanto más bajo el CER, mejor el sistema biométrico** — es la métrica clave para comparar sistemas biométricos a la hora de comprarlos.
### Multi-factor en la práctica
Las cerraduras modernas suelen combinar factores: PIN + huella (algo que sabés + algo que sos), o tarjeta + PIN (algo que tenés + algo que sabés) — como en los torniquetes de un access control vestibule.

---
**Para el examen, memorizá bien**:
- Jerarquía de fuerza: padlock < basic lock < traditional key lock < electronic (PIN/wireless/biometric) < cipher lock
- **FAR vs FRR vs CER** — pregunta clásica con escenarios ("el sistema rechazó a un empleado autorizado" = FRR; "dejó entrar a alguien que no debía" = FAR)
- Biometría = factor de **inherence** ("algo que sos")

## Access Card Cloning — 

### Qué es
**Access card cloning**: copiar los datos de una tarjeta **RFID** o **NFC** a otra tarjeta/dispositivo en blanco. La copia se comporta como el original y engaña al sistema de autenticación, sin necesidad de tener nunca la tarjeta física real.
### Los 4 pasos del ataque
1. **Scanning** — leer la tarjeta de la víctima con un lector portátil, a menudo sin contacto ni conocimiento de la víctima. Rango: **NFC ~1-2 cm**, **RFID ~2-10 cm** (más con antena potente).
2. **Data extraction** — sacar el identificador único o datos cifrados de lo escaneado.
3. **Writing to new card/device** — grabar esos datos en una tarjeta en blanco u otro dispositivo. Herramienta que menciona el instructor: **Flipper Zero** (compacto, guarda múltiples credenciales clonadas).
4. **Using the cloned badge** — usar la copia para acceso físico o incluso fraude en pagos NFC.
### Por que es peligroso
- Fácil de ejecutar, sigiloso (no necesitás poseer la tarjeta original), y las herramientas son cada vez más baratas y accesibles → hasta atacantes poco sofisticados pueden hacerlo.
- Consecuencias: acceso físico no autorizado + potencial **fraude financiero** si se clona una tarjeta NFC de pago.

### Mitigaciones (importante para el examen)
1. **Advanced encryption** — muchos sistemas RFID/NFC básicos usan identificadores simples sin cifrado robusto; cifrar los hace mucho más difíciles de clonar.
2. **MFA** — combinar la tarjeta con un segundo factor (PIN, biometría). Aunque clonen la tarjeta, sin el PIN no entran. Ejemplo típico: RFID card (algo que tenés) + PIN de 8 dígitos (algo que sabés).
3. **Actualizar protocolos de seguridad periódicamente** — rotar claves de cifrado y mecanismos de autenticación.
4. **User education** — enseñar a los usuarios sobre el riesgo, y a cuidar dónde guardan sus tarjetas.
5. **RFID-blocking wallets/sleeves** — bloquean físicamente que un escáner lea la tarjeta mientras está guardada.
6. **Monitoreo y auditoría de access logs** — detectar patrones imposibles (ej: acceso registrado mientras el dueño de la tarjeta está confirmado en otra ciudad).
---
**Para el examen**: la defensa **más efectiva y más preguntada** es **MFA** — combinar la tarjeta (algo que tenés) con un PIN o biometría (algo que sabés/sos) neutraliza el clonado porque el atacante clona solo el primer factor, no el segundo.