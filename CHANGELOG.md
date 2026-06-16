# CHANGELOG — Immersive IA Traffic RRMX

Registro de todos los cambios realizados al mod para alimentar el archivo `description.txt` en cada release.

---

## [Unreleased] — En desarrollo

### 🚗 Comportamiento de velocidad del tráfico AI
**Archivo:** `def/traffic_data.sii`

- **`ai_speed_coef_preferred`**: `(0.95, 1.10)` → `(1.02, 1.22)`
  - El rango completo ahora está **por encima del límite de velocidad**, haciendo que la gran mayoría del tráfico circule más rápido que el límite indicado, como ocurre en la realidad en carreteras de EE.UU.
  - Mínimo: 102% del límite (casi nadie va lento)
  - Máximo: 122% del límite (los conductores más agresivos van ~20% sobre el límite)

### 🧠 Comportamiento de seguridad y paciencia AI
**Archivo:** `def/traffic_data.sii`

- **`ai_safety_modifier`**: `-0.15` → `-0.25`
  - Los vehículos mantienen distancias más reducidas y frenan de forma más abrupta, reflejando el comportamiento real a velocidades elevadas.

- **`ai_patience_modifier`**: `-0.3` → `-0.4`
  - Mayor impaciencia general: los vehículos AI adelantan con más frecuencia, esperan menos tiempo en cruces y usan el claxon antes al sentirse bloqueados.

---

## [v1.0] — 2026-06-07 · Primera versión publicada

### 🧠 Comportamiento de IA — `def/traffic_data.sii`

Parámetros que estaban comentados/desactivados fueron activados y ajustados:

- **`ai_safety_modifier`**: comentado (`0.3` implícito) → `-0.15`
  - Conductores más agresivos: distancias de frenado más cortas, se pegan más a otros vehículos imitando tráfico real.

- **`ai_patience_modifier`**: comentado (`0.0` implícito) → `-0.3`
  - Más impaciencia: adelantamientos más frecuentes, menos tiempo esperando en cruces.

- **`ai_speed_coef_preferred`**: no existía → `(0.95, 1.10)`
  - Rango dinámico de velocidades: algunos conductores van ~5% bajo el límite, los más impacientes hasta 10% sobre él.

- **`ai_horn_delay`**: comentado `(4.0, 8.0)` → `(2.0, 4.5)`
  - Bocinas más rápidas ante bloqueos (2-4.5 segundos en lugar de 4-8 segundos).

- **`ai_blink_delay`**: comentado `(3.0, 6.0)` → `(2.0, 4.0)`
  - Intermitentes al ceder el paso más reactivos.

- **`ai_yield_max_speed`**: comentado `(18.0, 26.0)` → `(15.0, 22.0)`
  - Velocidad máxima más baja para activar el ceder el paso (más realista en vías estrechas).

- **`ai_yield_wait_time`**: comentado `(20.0, 30.0)` → `(10.0, 20.0)`
  - Los conductores esperan menos antes de ceder el paso.

- **`ai_yield_timeout`**: comentado `(3.0, 5.0)` → `(2.0, 3.0)`
  - El timeout de ceder el paso es más corto: abortan antes si el otro no avanza.

---

### 🚦 Densidad de tráfico dinámica — `def/world/traffic_times/`

#### `s_car_u_traffic_times.sui` — Coches en ciudad (hora pico)
- **07:00 – 07:30**: límite subido de ~199 a **230 coches** simultáneos (atasco matutino masivo).
- **17:00 – 17:30**: límite subido de ~173 a **210 coches** simultáneos (salida de trabajo).

#### `s_car_l_traffic_times.sui` — Coches en carretera rural (noche)
- **00:00 – 04:00**: frecuencia subida de casi cero (~1-2 coches) a **7-12 coches por hora** (campo no completamente desierto).
- **21:00 – 23:00**: también incrementado levemente para una transición más natural.

#### `s_truck_f_traffic_times.sui` — Camiones en autopista (noche)
- **00:00 – 04:00**: frecuencia subida de 15-23 a **30-35 camiones** simultáneos (rutas logísticas nocturnas dominando las highways).
- **21:00 – 23:00**: también aumentado para una rampa progresiva.

#### `s_truck_u_traffic_times.sui` — Camiones en ciudad (noche)
- **00:00 – 04:00**: frecuencia subida de ~20 a **50-60 camiones** en ciudad (entregas y distribución nocturna).
- **21:00 – 23:00**: también incrementado.

---

### 📄 Archivos de texto — `description.txt`
- Reescrita la descripción completa del mod con identidad **Immersive Traffic - RRMX**.
- Incluida versión en **inglés y español**.
- Documentadas todas las features: comportamiento de IA, densidad dinámica, distribución de colores real (estadísticas EE.UU. 2023).

---

> **Uso:** Al preparar una nueva versión, copiar la sección `[Unreleased]` al archivo `description.txt`,
> asignarle número de versión y fecha, y vaciar esta sección para el siguiente ciclo.
