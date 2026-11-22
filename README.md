# ClimaControl IR — Control Multi-Equipo y Horarios Semanales

Control remoto web minimalista (estética oscura *glassmorphism*) para gestionar múltiples aires acondicionados **Lennox** y **Prime** conectados a **Firebase Realtime Database**, con control manual simultáneo y **programación horaria semanal (lunes a viernes)** por equipo.

Está desarrollado en un **único archivo `index.html`** con Tailwind CSS y JavaScript puro (sin pasos de compilación), listo para abrirse en el navegador o publicarse directamente en **GitHub Pages**.

## Características

- **Control manual unificado en una sola vista**: Carátulas independientes para los 5 equipos predeterminados (`Clima 1` a `Clima 5`), con gestión dinámica (agregar, editar nombre/ID o eliminar) guardada en `localStorage`.
- **Sincronización en tiempo real**: Realiza `GET` a `/dispositivos/{id_dispositivo}.json` para cada equipo, inicializa automáticamente nodos faltantes (`encendido: false, marca: "lennox", temperatura: 22, swing: "swing_off", fan: "fan_1"`) y escucha actualizaciones en `/dispositivos.json` mediante `EventSource`.
- **Programación horaria semanal (Lun – Vie)**:
  - Consulta `/horarios/{id_dispositivo}.json` al seleccionar un equipo.
  - Pestañas para **Lunes, Martes, Miércoles, Jueves y Viernes**.
  - Alta de bloques horarios con hora de inicio/fin (`HH:MM`), marca, temperatura (`16–30 °C`), ventilador y oscilación, validando que `fin > inicio` y evitando traslapes.
  - Eliminación individual de bloques y herramienta **Copiar horario a otros días** con guardado automático vía `PUT` en `/horarios/{id_dispositivo}/{dia}.json`.

## Estructura en Firebase Realtime Database

Base URL configurada en `index.html`:

```text
https://almacenamiento-ir-default-rtdb.firebaseio.com
```

### 1. Estado manual (`/dispositivos/{id_dispositivo}.json`)

```json
{
  "comando_id": 1731790000000,
  "encendido": false,
  "marca": "lennox",
  "temperatura": 22,
  "swing": "swing_off",
  "fan": "fan_1"
}
```

### 2. Horarios semanales (`/horarios/{id_dispositivo}/{dia}.json`)

Días válidos: `"lunes"`, `"martes"`, `"miercoles"`, `"jueves"`, `"viernes"`.

```json
[
  {
    "inicio": "07:00",
    "fin": "10:00",
    "marca": "lennox",
    "temperatura": 22,
    "swing": "swing_off",
    "fan": "fan_1"
  }
]
```

## Publicación en GitHub Pages

1. Sube `index.html` a tu repositorio de GitHub.
2. En **Settings → Pages**, selecciona la rama principal (`main`) y la carpeta raíz (`/`).
3. Abre la URL publicada desde cualquier navegador móvil o de escritorio.
