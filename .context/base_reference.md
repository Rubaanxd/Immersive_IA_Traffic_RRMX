# Referencia de Valores BASE del Juego

> Valores extraídos de `/BASE/def/def/` para comparación rápida.
> Útil para entender el impacto de cada ajuste.

---

## `traffic_data.sii` — Valores BASE vs RRMX

| Parámetro | BASE | RRMX |
|-----------|------|------|
| `max_vehicle_count` | 50 | **3668** |
| `spawn_distance_forward` | 600.0 | **550.0** |
| `spawn_distance_backward` | 200.0 | 200.0 |
| `spawn_distance_min` | 80.0 | **125.0** |
| `remove_distance_forward` | 800.0 | **700.0** |
| `remove_distance_backward` | 250.0 | **300.0** |
| `remove_distance_min` | 150.0 | **200.0** |
| `ai_drag_length_limits[0]` | 6.0 | **5.5** |
| `ai_drag_length_limits[1]` | 10.0 | **11.0** |
| `ai_safety_modifier` | comentado (0.3) | **-0.25** |
| `ai_patience_modifier` | comentado (0.0) | **-0.4** |
| `ai_speed_coef_preferred` | no existía | **(1.02, 1.22)** |
| `ai_horn_delay` | comentado (4.0, 8.0) | **(2.0, 4.5)** |
| `ai_blink_delay` | comentado (3.0, 6.0) | **(2.0, 4.0)** |
| `ai_yield_max_speed` | comentado (18.0, 26.0) | **(15.0, 22.0)** |
| `ai_yield_wait_time` | comentado (20.0, 30.0) | **(10.0, 20.0)** |
| `ai_yield_timeout` | comentado (3.0, 5.0) | **(2.0, 3.0)** |

---

## `journey_road_event_master.sii` — Valores BASE vs RRMX

| Parámetro | BASE | RRMX |
|-----------|------|------|
| `max_road_events_count[0]` | 100 | **150** |
| `min_road_events_distance[0]` | 1500.0 m | **800.0 m** |
| `probability[0]` | 0.017 | **0.035** |
| `max_road_events_count[1]` | 100 | **120** |
| `min_road_events_distance[1]` | 30.0 m | 30.0 m |
| `probability[1]` | 0.5 | **0.65** |

---

## `police_data.sii` — Valores BASE vs RRMX

| Parámetro | BASE | RRMX |
|-----------|------|------|
| `fine_amounts[0]` — crash | 900 | **1200** |
| `fine_amounts[6]` — speeding | 200 | **350** |
| `offence_probabilty[6]` — speeding | **0.0** | **0.15** |
| `offence_check_delay[6]` — speeding | 60 s | **30 s** |
| `offence_police_check_delay[6]` — speeding | 3 s | **2 s** |
| `police_nearby_fine_rate` | 2 | **2** |
| `police_nearby_offence_timer` | 25.0 | **20.0** |

---

## `journey_road_event.sii` — Weights BASE vs RRMX

| Evento | Descripción | Weight BASE | Weight RRMX |
|--------|-------------|-------------|-------------|
| `j_re.crash_in` | Accidente ciudad inner | 6 | 6 |
| `j_re.crash_ci` | Accidente ciudad | 6 | 6 |
| `j_re.acc_cou_s` | Accidente country 1-1 small | 1 | **3** |
| `j_re.acc_cou_b` | Accidente country 1-1 big | 3 | **4** |
| `j_re.acc_ext_s` | Accidente 1-1E small | 1 | **2** |
| `j_re.acc_ext_b` | Accidente 1-1E big | 3 | **4** |
| `j_re.acc_ext2_b` | Accidente 1-1E big2 | 3 | **4** |
| `j_re.crash1` | Accidente freeway small | 6 | **9** |
| `j_re.trailer` | Tráiler volcado freeway | 6 | **5** |
| `j_re.acc_hw_b` | Accidente freeway big | 10 | **12** |
| `j_re.tr_car_cra` | Truck-car crash freeway | 6 | **8** |
| `j_re.cessna` | Cessna estrellada | 3 | **2** |
| `j_re.tree` | Árbol caído (ambos) | 10 | **5** |
| `j_re.tree_r` | Árbol caído derecha | 10 | **5** |
| `j_re.tree_l` | Árbol caído izquierda | 10 | **5** |
| `j_re.rsfe` | Obras freeway small | — | — |
| `j_re.rcfe` | Obras freeway mill | — | — |
| `j_re.r1fe` | Obras freeway random | — | — |
| `j_re.r2fe` | Obras freeway random2 | — | — |
| `j_re.rw_city` | Obras ciudad small | 10 | **12** |
| `j_re.rw_city_in` | Obras ciudad inner | 10 | **12** |
| `j_re.rw_1_1` | Obras 1-1 | 7 | **10** |
| `j_re.tripod` | Limpieza canal | 9 | **7** |
| `j_re.tripod_r` | Limpieza canal inner | 9 | **7** |
| `j_re.police` | Policía arcén | 8 | **14** |
| `j_re.police_sp` | Policía deportivo | 8 | **10** |
| `j_re.pol_cou` | Policía country 1-1 | 2 | **5** |
| `j_re.pol_ext` | Policía 1-1E | 2 | **5** |
| `j_re.shop` | Tienda ambulante | 10 | **8** |
| `j_re.shop_l` | Tienda izquierda | 10 | **8** |
| `j_re.shop_r` | Tienda derecha | 10 | **8** |
| `j_re.city_ev` | Evento ciudad | 9 | **11** |
| `j_re.tire` | Neumático dañado | 5 | **12** |
| `j_re.tire2` | Basura en 1-1 | 5 | **13** |
| `j_re.channels` | Canales drenaje | 10 | 10 |
| `j_re.road_decals` | Calcomanías carretera | 10 | 10 |
| `j_re.rw_1_tlw80` | Obras semáforo 80m wide | 5 | **8** |
| `j_re.rw_1_tln80` | Obras semáforo 80m narrow | 5 | **8** |
| `j_re.rw_1_tlw120` | Obras semáforo 120m wide | 10 | **14** |
| `j_re.rw_1_tln120` | Obras semáforo 120m narrow | 10 | **14** |
| `j_re.rw_cou` | Obras roadwork 1-1 | 3 | **6** |
| `j_re.rw_ext` | Obras roadwork 1-1E | 3 | **6** |
| `j_re.rw_g` | Géiser/tubería rota | 3 | **4** |

---

## Tipos de Road Events — Guía Rápida

### Cómo funciona el sistema `j_re.*`

```
journey_events_road_event : j_re.NOMBRE
{
    weight: N.0             ← Mayor = más frecuente (relativo)
    traffic_block: true     ← Bloquea carril (tráfico desvía)
    slow_down_passing: true ← Tráfico reduce velocidad al pasar
    min_duration: 1440      ← Duración mínima (min de juego) = 1 día
    area_tag: urban         ← Solo en zonas urbanas
    min_time_constraint: 480    ← Solo después de las 8:00 AM
    max_time_constraint: 1080   ← Solo antes de las 18:00 PM
    outer_lane_allowed: true    ← Puede aparecer en carril exterior
    inner_lane_allowed: true    ← Puede aparecer en carril interior
    tunnel_forbidden: true      ← No en túneles
    bridge_forbidden: true      ← No en puentes
    
    parents[]: j_re.super_parent    ← Herencia de config base
    layer_cutscenes[]: j_cut.NOMBRE ← Modelo 3D del evento
}
```

### Cutscenes disponibles (modelos 3D en `j_cut.*`)

Los eventos solo pueden usar cutscenes definidas en `journey_cutscene.sii`.
No se pueden crear cutscenes nuevas con solo `.sii` — requieren assets 3D.
