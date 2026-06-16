# Decisiones de Diseño

## Principio rector

> **"Realismo sobre perfección."** Cada ajuste debe justificarse con cómo
> se comporta el tráfico real en carreteras de EE.UU., no en cómo debería
> comportarse un conductor ideal.

---

## IA Behavior

### ¿Por qué `ai_speed_coef_preferred: (1.02, 1.22)` y no menos?

En las interstates de EE.UU., el 85% de los conductores circulan entre
el límite y un 10% por encima. Los más agresivos llegan al 15-20% sobre
el límite. El mínimo de 1.02 asegura que casi nadie va lento.

### ¿Por qué `ai_safety_modifier: -0.25`?

Los conductores americanos mantienen distancias cortas en autopista.
-0.25 refleja ese comportamiento sin llegar al caos de -0.5.

### ¿Por qué `ai_patience_modifier: -0.4`?

La impaciencia alta genera adelantamientos, lo que hace el tráfico
dinámico. -0.4 es agresivo pero no irreal.

---

## Densidad

### ¿Por qué no subir más el `max_vehicle_count`?

3668 ya es un límite alto. Subirlo demasiado impacta FPS sin mejorar
la percepción de tráfico — el spawn/despawn system es el cuello de botella.

### ¿Por qué la madrugada no está completamente vacía?

Las carreteras rurales de EE.UU. no son desiertas a las 3 AM. Hay
camioneros, viajeros nocturnos y vehículos de trabajo. 7-12 coches por
hora en rural es realista.

---

## Road Events

### ¿Por qué `probability[0]: 0.035` (doble del BASE)?

El BASE con 0.017 hace que los eventos sean tan raros que el jugador
puede conducir horas sin ver ninguno. 0.035 sigue siendo conservador
pero genera eventos con suficiente frecuencia para sentir la carretera
viva sin saturar.

### ¿Por qué `min_road_events_distance[0]: 800.0`?

En una autopista americana durante hora pico es común ver 2-3 incidentes
en un tramo de 5 km. 800m entre eventos lo permite sin que se conviertan
en un circo.

### ¿Por qué subir el peso de la policía?

En USA, ver un coche de policía parado en el arcén es de las cosas más
comunes en autopista. El BASE lo tiene con weight 8, lo que lo hace
relativamente raro. Con weight 14 aparece con la frecuencia real.

### ¿Por qué bajar el peso del árbol caído?

La mayoría del mapa de ATS representa el oeste árido/semiárido de EE.UU.
(California, Nevada, Arizona, Wyoming). Los árboles caídos son poco
comunes. En zonas boscosas (Washington, Oregon) sería más apropiado,
pero actualmente no se puede diferenciar por bioma en este sistema.

---

## Police Data

### ¿Por qué activar multas por velocidad (`offence_probabilty[6]: 0.15`)?

El BASE lo tiene en 0.0 — nunca multa por velocidad desde coche patrulla.
Con 0.15 hay un 15% de chance de multa cuando estás acelerando ante una
patrulla visible, lo que añade consecuencias reales al comportamiento
agresivo del jugador sin ser punitivo.

### ¿Por qué $350 de multa por velocidad (subida de $200)?

La multa promedio por exceso de velocidad en EE.UU. es $150-$400 según
el estado. $350 es más realista que $200.

---

## Colores

### ¿Por qué tan específicos (4,900+ colores)?

Los colores genéricos o uniformes rompen la inmersión. La distribución
estadística real del mercado USA 2023 (blanco 26%, gris 23%, negro 22%,
plata 9%, azul 7%, rojo 5%, otros) da una flota de vehículos creíble.

---

## Limitaciones conocidas

1. **No hay overrides por bioma**: Los road events de árbol caído se
   aplican igual en Arizona que en Washington. Limitación del sistema.

2. **No hay eventos nocturnos diferenciados**: Los eventos de policía
   no tienen mayor peso en noche aunque en USA hay más controles nocturnos.
   Pendiente para siguiente iteración.

3. **Vehículos evento limitados**: Solo se pueden crear `_event` para
   vehículos que tienen modelos 3D de evento en el juego base. No se
   pueden crear modelos nuevos sin assets.

4. **`journey_road_event.sii` override completo**: Al hacer override
   del archivo completo, si SCS actualiza el juego base se puede perder
   compatibilidad. Necesita revisión en cada update del juego.
