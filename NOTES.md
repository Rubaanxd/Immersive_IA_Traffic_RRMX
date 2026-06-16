# Notas para Modders y Mantenedores (RRMX) 🛠️

Este documento está diseñado para ayudar a futuros desarrolladores a entender la arquitectura del mod **Immersive IA Traffic - RRMX** y poder modificarlo o expandirlo fácilmente sin romper funcionalidades base.

---

## 1. Regla de Oro: Nomenclatura `.rrmx.sii`
**NUNCA sobrescribas los archivos base de mapas modificados si no es estrictamente necesario.** 
Para añadir tráfico o límites de velocidad por estado, siempre debes nombrar tus archivos con el sufijo `.rrmx.sii` (ej. `traffic.rrmx.sii` o `speed_limits.rrmx.sii`). 
- **¿Por qué?** El motor de SCS lee todos los archivos `.sii` de una carpeta. Al usar nuestro propio sufijo, evitamos borrar los spawns de vehículos especiales (como policías o autobuses locales) que mods como *Reforma* incluyen en sus propios `traffic.sii`.

---

## 2. Ajuste de Velocidad y Comportamiento de IA
**Archivo:** `def/traffic_data.sii`

Todos los ajustes psicológicos de la IA están aquí. No trates de ajustarlo por país, el motor solo acepta estos valores globalmente.
- `ai_speed_coef_preferred`: Determina el rango de velocidad sobre el límite legal. Actualmente `(1.10, 1.30)` significa que todos van entre 10% y 30% más rápido.
- `ai_patience_modifier`: Rango `<-1;1>`. Valores negativos (ej. `-0.4`) hacen a la IA tocar el claxon rápido y rebasar de inmediato.
- `ai_safety_modifier`: Rango `<-1;1>`. Valores negativos (ej. `-0.25`) acortan la distancia de frenado y provocan que la IA se pegue más al coche de enfrente.

---

## 3. Manejo de Densidades y Horarios (Rush Hour)
**Archivo:** `def/world/traffic_rules_spawn.sui`

El sistema de densidad dinámica no requiere programación por países. Se basa enteramente en **tags de carril** (`freeway`, `local`, `city`).
- Si deseas aumentar el tráfico nocturno de camiones pesados, edita los arrays en `traffic_rule_data : traffic_rule.s_truck_f`.
- Los multiplicadores de frecuencia (ej. x3 a las 17:00) están configurados en arrays de 24 horas.
- Todo mod de mapa (Reforma, Promods, etc.) hereda estas densidades automáticamente siempre y cuando usen carriles de asfalto estándar de SCS.

---

## 4. Road Events (Eventos de Carretera)
**Archivos:** `def/world/journey_road_event_master.sii` y `def/world/journey_road_event.sii`

- **Frecuencia Base:** `journey_road_event_master.sii` dicta qué tan seguido aparece *cualquier* evento. Usa `min_road_events_distance` para evitar que la carretera se sature demasiado (actualmente 800m).
- **Balanceo (Weights):** `journey_road_event.sii` es un *override* completo del juego base. Si SCS actualiza este archivo en un parche futuro (agregando nuevos eventos), este archivo **quedará obsoleto y deberá ser recreado**. 
- Los pesos (`weight`) son relativos. Si un evento tiene weight 14 (como los policías) y otro tiene 7, el policía tiene exactamente el doble de probabilidad de aparecer.

---

## 5. Expandiendo el Mod a Nuevos Mapas (Ej. Canadá, Alaska)
Si quieres agregar soporte para Promods Canada u otro mapa de extensión:
1. Averigua cómo el mod nombra sus carpetas de estados en la base de datos (ej. `def/country/british_columbia`).
2. Crea la carpeta equivalente.
3. Crea `speed_limits.rrmx.sii` y define las velocidades en **km/h**.
4. Crea `traffic.rrmx.sii` y usa el formato `country_traffic_info` para alterar los spawns. (Ej. subir `spawn_ratio` de camionetas de tala o camiones de nieve si existen).

---

## 6. Limitaciones Conocidas del Motor (Hardcoded)
- **Multas Policiales:** `def/police_data.sii` es 100% global. No puedes cobrar en pesos mexicanos en Sonora y en dólares en Arizona, ni tener umbrales diferentes. Las multas son universales.
- **Colores de Vehículos:** Los colores de los vehículos de IA no pueden ajustarse por región fácilmente mediante `traffic.sii`. Requiere clonar el modelo 3D en `def/vehicle/ai/` y crear una variante exclusiva para un país.
