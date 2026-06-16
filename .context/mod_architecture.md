# Arquitectura del Mod — Mapa de Archivos

## Estructura raíz

```
Immersive_IA_Traffic_RRMX/
├── .context/               ← Contexto IA (esta carpeta)
├── BASE/                   ← Defs originales del juego (gitignore)
├── def/                    ← Overrides del mod
├── manifest.sii            ← Metadata del mod para ATS
├── description.txt         ← Descripción pública (Steam/mod manager)
├── CHANGELOG.md            ← Historial de cambios (desarrollador)
└── icon.jpg                ← Ícono del mod
```

## Archivos del mod en `def/`

### `def/traffic_data.sii`
**Propósito**: Configuración global del comportamiento de la IA de tráfico.

Parámetros clave modificados:
- `max_vehicle_count: 3668` — Total de vehículos IA simultáneos
- `ai_speed_coef_preferred: (1.02, 1.22)` — Velocidad relativa al límite (102%-122%)
- `ai_safety_modifier: -0.25` — Más agresivo (-1 a 1)
- `ai_patience_modifier: -0.4` — Más impaciente (-1 a 1)
- `ai_horn_delay: (2.0, 4.5)` — Bocina antes (era 4-8s)
- `ai_blink_delay: (2.0, 4.0)` — Intermitentes más rápidos
- `spawn_distance_forward: 550.0` — Distancia de spawn adelante
- `spawn_distance_backward: 200.0` — Distancia de spawn atrás

Referencia BASE: `/BASE/def/def/traffic_data.sii`

---

### `def/world/traffic_rules.sii`
**Propósito**: Define todas las reglas de tráfico del juego (speed limits, prioridades, acceso por tipo de vehículo). Copiado del BASE con extensiones propias.

---

### `def/world/traffic_lane.sii`
**Propósito**: Define tipos de carril (local, dividida, freeway) con sus reglas de densidad y acceso asociadas.

---

### `def/world/traffic_rules_spawn.sui`
**Propósito**: Define las reglas de densidad (`density`) por tipo de vehículo y contexto. Incluye `@include` a los archivos `traffic_times/*.sui`.

---

### `def/world/traffic_times/*.sui` (40 archivos)
**Propósito**: Tablas de densidad hora-a-hora del día para cada tipo de vehículo.
Archivos principales modificados:
- `s_car_u_traffic_times.sui` — Coches ciudad (rush hour amplificado)
- `s_car_l_traffic_times.sui` — Coches rural (madrugada no desierta)
- `s_truck_f_traffic_times.sui` — Camiones autopista (noche logística)
- `s_truck_u_traffic_times.sui` — Camiones ciudad (entregas nocturnas)

---

### `def/world/journey_road_event_master.sii` *(NUEVO en dev)*
**Propósito**: Controla la frecuencia global de road events.

Parámetros:
- `probability[0]` — Probabilidad de spawn de eventos principales
- `min_road_events_distance[0]` — Distancia mínima entre eventos (metros)
- `max_road_events_count[0]` — Máximo de eventos simultáneos
- `probability[1]` — Probabilidad de elementos decorativos
- `min_road_events_distance[1]` — Distancia mínima entre decorativos

Referencia BASE: `/BASE/def/def/world/journey_road_event_master.sii`

---

### `def/world/journey_road_event.sii` *(NUEVO en dev)*
**Propósito**: Rebalanceo de pesos de tipos de road events.

Eventos modificados (solo los `weight` y `min/max_time_constraint`):
- Policía en arcén — mayor peso
- Basura/neumáticos — mayor peso
- Obras con semáforo — mayor peso
- Árbol caído — menor peso (zona oeste seca)

Referencia BASE: `/BASE/def/def/world/journey_road_event.sii`

---

### `def/police_data.sii` *(NUEVO en dev)*
**Propósito**: Override de multas y comportamiento policial.

Referencia BASE: `/BASE/def/def/police_data.sii`

---

### `def/vehicle/ai/*.sui` (97 archivos)
**Propósito**: Definición de cada vehículo IA (acceso a ruedas, chassis, colores, tags, variantes).

Subdirectorios:
- `colors/` — Paletas de colores por modelo
- `range_rover/` — Variantes del Range Rover
- `xc90/` — Variantes del Volvo XC90
- `trailer_chains/` — Remolques encadenados

Archivos `*_event.sui`:
- `a6_crashed_event.sui` — Audi A6 accidentado
- `accord_crashed_event.sui` — Honda Accord chocado (frente y trasero)
- `cadillac_crashed_event.sui` — Cadillac chocado
- `f150_crashed_event.sui` — F-150 accidentado
- `ford_smax_event.sui` — Ford S-Max (puertas abiertas: izq, der, ambas)
- `chevy_low_cab_event.sui` — Chevy Low Cab flatbed (4 variantes de carga)
- `dodge_ram_event.sui` — Dodge Ram evento
- `mack_rd_event.sui` — Mack RD evento
- `lincoln_event.sui` — Lincoln evento
- `transit_2016_event.sui` — Ford Transit evento (múltiples configs)

---

### `def/country/wyoming/` (en progreso)
**Propósito**: Speed limits y reglas específicas para Wyoming.

## Archivos BASE clave (solo referencia)

```
BASE/def/def/
├── traffic_data.sii              ← Valores default IA
├── police_data.sii               ← Multas y detección
├── world/
│   ├── journey_road_event.sii    ← 2029 líneas, ~60 eventos
│   ├── journey_road_event_master.sii
│   ├── journey_cutscene.sii      ← Modelos 3D de eventos (j_cut.*)
│   ├── traffic_rules.sii
│   ├── traffic_rules_spawn.sui
│   └── traffic_lane.sii
```
