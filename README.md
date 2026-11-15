ClimaControl IR
Control remoto web minimalista (estética oscura glassmorphism) para aires acondicionados Lennox y Prime, conectado en tiempo real con Firebase Realtime Database.
Está diseñado en un único archivo index.html con Tailwind CSS y JavaScript puro (sin pasos de compilación), por lo que puede abrirse directamente en el navegador o publicarse en GitHub Pages.
Características
Sincronización en tiempo real: Al abrir la página realiza un GET inicial a estado_dispositivo.json y mantiene una conexión activa mediante EventSource (con respaldo automático por sondeo y botón manual Actualizar).
Selector de marca: Alterna entre lennox y prime.
Encendido / Apagado: Envía "encendido": true o false.
Control de temperatura: Rango de 16 °C a 30 °C con botones - / + y soporte de teclado (+, -, flecha arriba/abajo).
Velocidad de ventilador: Opciones visuales para fan_auto, fan_1, fan_2 y fan_3.
Oscilación (Swing): Alterna entre swing_on y swing_off.
Emisión inmediata: Cada interacción genera un nuevo comando_id (Date.now()) y envía una petición PUT a Firebase mostrando «Señal enviada».
Estructura en Firebase Realtime Database
Endpoint configurado en index.html (FIREBASE_URL):
Text
https://almacenamiento-ir-default-rtdb.firebaseio.com/estado_dispositivo.json
Objeto JSON enviado y consultado:
JSON
{
  "comando_id": 1731628800000,
  "encendido": true,
  "marca": "lennox",
  "temperatura": 22,
  "swing": "swing_off",
  "fan": "fan_auto"
}
Campo	Tipo	Valores permitidos
comando_id	number	Timestamp en milisegundos (Date.now())
encendido	boolean	true | false
marca	string	"lennox" | "prime"
temperatura	number	Entero entre 16 y 30
swing	string	"swing_on" | "swing_off"
fan	string	"fan_auto" | "fan_1" | "fan_2" | "fan_3"
Uso y publicación en GitHub Pages
Sube index.html a tu repositorio de GitHub.
(Opcional) Si usas otra base de datos, actualiza la constante FIREBASE_URL en el <script> de index.html.
En GitHub, ve a Settings → Pages, selecciona la rama principal (main) y la carpeta raíz (/).
Tu control remoto quedará disponible en https://<tu-usuario>.github.io/<tu-repositorio>/.
