# Project Overview — Immersive IA Traffic RRMX

## Qué es este mod

**Immersive IA Traffic RRMX** es un mod para **American Truck Simulator (ATS)**
que reemplaza y mejora el sistema de tráfico de IA del juego base.

## Objetivo

Hacer que el tráfico de ATS se sienta como el tráfico real de carreteras
estadounidenses: vivo, impredecible, con personalidad por conductor, con
eventos de carretera frecuentes y con densidades que cambian según la hora
del día y la zona.

## Juego objetivo

- **American Truck Simulator (ATS)** — SCS Software
- Motor: SCS Engine (`.sii` / `.sui` definition files)
- Versión base de los defs: extraída en `/BASE/` (ignorada por git)

## Stack tecnológico

- Archivos de definición `.sii` (SiiNunit format)
- Archivos include `.sui`
- Sin scripts ni código compilado — solo datos declarativos
- Git para control de versiones

## Estructura de ramas

```
main     ← versión publicada en Steam Workshop
dev      ← desarrollo activo, pruebas (rama actual de trabajo)
```

## Mecánicas que modifica el mod

1. **Comportamiento IA global** (`def/traffic_data.sii`)
   - Velocidades preferidas sobre el límite
   - Agresividad, paciencia, bocinas, intermitentes

2. **Densidad dinámica por hora** (`def/world/traffic_times/*.sui`)
   - 40 archivos de densidad, uno por tipo de vehículo y contexto
   - Rush hour, noche logística, madrugada rural

3. **Road events** (`def/world/journey_road_event*.sii`)
   - Accidentes, obras, policía, basura, árboles
   - Frecuencia y distribución de tipos

4. **Colores realistas** (`def/vehicle/ai/colors/*.sui`)
   - Distribución estadística real del mercado USA 2023

5. **Policía** (`def/police_data.sii`)
   - Multas, probabilidades, radares

6. **Reglas por país/estado** (`def/country/`)
   - Speed limits por tipo de vía y vehículo
