# Dev Log — Historial de Sesiones

---

## 2026-06-16 — Sesión 1: Road Events + Police Data

**Rama**: `dev`
**Autor**: IA (Claude) + Rubaan

### Cambios realizados

#### NUEVO: `def/world/journey_road_event_master.sii`
Override del archivo maestro de road events. Duplica la frecuencia de
eventos y reduce la distancia mínima entre ellos para que la carretera
se sienta viva constantemente.

Valores cambiados:
- `probability[0]`: 0.017 → 0.035
- `min_road_events_distance[0]`: 1500.0 → 800.0
- `max_road_events_count[0]`: 100 → 150
- `probability[1]`: 0.5 → 0.65
- `max_road_events_count[1]`: 100 → 120

#### NUEVO: `def/world/journey_road_event.sii`
Override con rebalanceo de pesos de los 60+ tipos de road events.

Cambios principales:
- Policía en arcén: weight 8 → 14 (muy común en USA)
- Basura/neumáticos: weight 5 → 12-13 (ubicuo en autopistas)
- Obras con semáforo 120m: weight 10 → 14
- Árbol caído: weight 10 → 5 (poco común en oeste árido)
- Accidentes de freeway: subidos +2 a +3 puntos
- Eventos ciudad: weight 9 → 11

#### NUEVO: `def/police_data.sii`
Override de multas y comportamiento policial.

Cambios:
- `fine_amounts[0]` (crash): $900 → $1,200
- `fine_amounts[6]` (speeding): $200 → $350
- `offence_probabilty[6]` (speeding): 0.0 → 0.15
- `offence_check_delay[6]` (speeding): 60s → 30s
- `police_nearby_offence_timer`: 25s → 20s

#### NUEVO: `.context/` (carpeta de contexto IA)
- `README.md` — Guía de la carpeta
- `project_overview.md` — Descripción del proyecto
- `mod_architecture.md` — Mapa de archivos
- `design_decisions.md` — Justificación de decisiones
- `base_reference.md` — Valores BASE vs RRMX comparados
- `dev_log.md` — Este archivo

### Estado al final de la sesión

- Rama: `dev`
- Archivos modificados: 3 nuevos `.sii` en `def/`
- Tests pendientes: Iniciar ATS y verificar:
  - [ ] Road events aparecen con mayor frecuencia
  - [ ] Policía visible en arcenes de autopista
  - [ ] Basura/neumáticos en arcenes
  - [ ] Obras con semáforo en carreteras de 1 carril
  - [ ] Multa aplicada al exceder velocidad cerca de policía
  - [ ] No hay crashes del juego (game.log sin errores)

---

## Sesiones anteriores

### v1.0 — 2026-06-07 (Publicación inicial)
- `traffic_data.sii`: Activación de todos los parámetros IA
- `traffic_times/*.sui`: Rush hour, noche logística
- `description.txt`: Redacción bilingüe
- Más de 4,900 colores específicos por vehículo

### [Unreleased — pre v1.0]
- `ai_speed_coef_preferred`: (0.95, 1.10) → (1.02, 1.22)
- `ai_safety_modifier`: -0.15 → -0.25
- `ai_patience_modifier`: -0.3 → -0.4
