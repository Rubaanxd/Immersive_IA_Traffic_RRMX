# CHANGELOG — Immersive IA Traffic RRMX

Registro de todos los cambios realizados al mod para alimentar el archivo `description.txt` en cada release.

---

## [Unreleased] — En desarrollo (rama `dev`)

### 🚦 Road Events — Carreteras Vivas
**Archivos:** `def/world/journey_road_event_master.sii`, `def/world/journey_road_event.sii`

#### `journey_road_event_master.sii` (NUEVO)
- **`probability[0]`**: 0.017 → `0.035` — Eventos aparecen ~2× más frecuentemente
- **`min_road_events_distance[0]`**: 1500 m → `800 m` — Menos distancia mínima entre eventos; realista en autopistas USA
- **`max_road_events_count[0]`**: 100 → `150` — Más eventos activos simultáneamente
- **`probability[1]`** (decorativos): 0.5 → `0.65` — Más calcomanías y detalles en el asfalto

#### `journey_road_event.sii` (NUEVO — full override del BASE con rebalanceo de pesos)
Eventos potenciados:
- **Policía en arcén** (`j_re.police`): weight 8 → `14` — Muy común en autopistas USA
- **Policía deportivo** (`j_re.police_sp`): weight 8 → `10`
- **Policía country 1-1** (`j_re.pol_cou/pol_ext`): weight 2 → `5`
- **Neumáticos/debris** (`j_re.tire`): weight 5 → `12` — Ubicuo en interstates
- **Basura en 1-1** (`j_re.tire2`): weight 5 → `13`
- **Accidente freeway small** (`j_re.crash1`): weight 6 → `9`
- **Accidente freeway big** (`j_re.acc_hw_b`): weight 10 → `12`
- **Truck-car crash** (`j_re.tr_car_cra`): weight 6 → `8`
- **Obras ciudad** (`j_re.rw_city/city_in`): weight 10 → `12`
- **Obras 1-1** (`j_re.rw_1_1`): weight 7 → `10`
- **Obras semáforo 120m** (`j_re.rw_1_tlw/tln120`): weight 10 → `14`
- **Obras semáforo 80m** (`j_re.rw_1_tlw/tln80`): weight 5 → `8`
- **Obras country 1-1** (`j_re.rw_cou/rw_ext`): weight 3 → `6`
- **Evento urbano** (`j_re.city_ev`): weight 9 → `11`
- **Accidentes country 1-1**: weight +2 a +3 puntos

Eventos reducidos:
- **Árbol caído** (`j_re.tree*`): weight 10 → `5` — Raro en oeste árido de EE.UU.
- **Cessna estrellada** (`j_re.cessna`): weight 3 → `2` — Evento especial/raro
- **Tráiler volcado freeway** (`j_re.trailer`): weight 6 → `5`
- **Tiendas ambulantes** (`j_re.shop*`): weight 10 → `8`

---

### ⚡ Ajuste Global de Velocidad IA
**Archivo:** `def/traffic_data.sii`
- **`ai_speed_coef_preferred`**: `(1.02, 1.22)` → `(1.05, 1.25)`
  - La IA ahora conduce del **5% al 25% por encima del límite**, empujando las velocidades para un comportamiento agresivo y fluido más acorde a las carreteras reales.

---

### 🇲🇽 Adaptación a México (Soporte Mapa Reforma)
**Archivos:** `def/country/[estado]/speed_limits.sii` y `traffic.sii` (NUEVO)
Se crearon definiciones específicas por estado para 12 estados de Reforma (`aguascalientes`, `baja_california`, `baja_california_sur`, `chihuahua`, `coahuila`, `durango`, `jalisco`, `nayarit`, `san_luis_potosi`, `sinaloa`, `sonora`, `zacatecas`).

**1. Límites de velocidad realistas (`speed_limits.sii`)**
- Coches: 110 km/h (Autopista), 90 km/h (Carretera dividida), 80 km/h (Carretera local), 50 km/h (Urbano).
- Camiones pesados: 80 km/h máximo en todas las vías extraurbanas, 40 km/h en ciudad.
- Autobuses: 95 km/h (Autopista), 80 km/h (Carreteras secundarias), 50 km/h (Urbano).
*(Nota: Al usar km/h aquí, se fuerza a que la IA que transita por estos estados respete la ley mexicana).*

**2. Composición de tráfico adaptada (`traffic.sii`)**
- **Menos deportivos/lujo:** Mercedes CE (0.10x), Mustang (0.10x), Tesla (0.05x).
- **Más utilitarios y antiguos:** Pickups Chevy/Sierra (2.00x-2.50x), coches antiguos Mercury (2.00x).
- **Entorno urbano:** Multiplicado el spawn de taxis (8.00x) y autobuses locales (1.50x) dentro de las ciudades.

---

### 🚔 Policía — Multas Realistas
**Archivo:** `def/police_data.sii` (NUEVO)

- **`fine_amounts[0]`** (choque): $900 → `$1,200` — Más realista para EE.UU.
- **`fine_amounts[6]`** (velocidad): $200 → `$350` — Multa promedio en EE.UU. ($150-$400)
- **`offence_probabilty[6]`** (velocidad): `0.0` → `0.15` — Antes NUNCA multaba por velocidad desde patrulla. Ahora 15% de chance si hay policía cerca.
- **`offence_check_delay[6]`** (velocidad): 60 s → `30 s` — Detección más rápida
- **`police_nearby_offence_timer`**: 25 s → `20 s` — Policía más vigilante

---

### 📁 Carpeta `.context/` (NUEVO — solo para desarrollo)
Carpeta de contexto para IA y desarrolladores:
- `README.md` — Guía de la carpeta
- `project_overview.md` — Descripción del proyecto
- `mod_architecture.md` — Mapa de archivos
- `design_decisions.md` — Justificación de decisiones
- `base_reference.md` — Tabla comparativa BASE vs RRMX
- `dev_log.md` — Historial de sesiones de desarrollo

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
