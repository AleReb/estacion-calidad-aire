# Casos de uso

## CU-01: Monitoreo ciudadano y municipal
- **Actor principal:** Programas municipales de calidad del aire.
- **Objetivo:** Obtener datos continuos de contaminantes y variables meteorológicas en una única plataforma.
- **Resumen:** La estación se instala en una torre de 2–5 m, opera con panel solar + baterías y envía datos por GSM/4G con respaldo en microSD.

## CU-02: Validación de sensores de bajo costo
- **Actor principal:** Equipos de QA/QC.
- **Objetivo:** Comparar lecturas de sensores de bajo costo contra los sensores electroquímicos y ópticos calibrados de la estación.
- **Resumen:** Los sensores cuentan con especificaciones validadas y se calibran antes de operar, permitiendo establecer referencias en tiempo casi real.

## CU-03: Correlación con estaciones de referencia
- **Actor principal:** Investigadores o agencias ambientales.
- **Objetivo:** Analizar el comportamiento de contaminantes criterio frente a datos oficiales de referencia.
- **Resumen:** El sistema transmite datos casi en tiempo real y mantiene almacenamiento local, facilitando la comparación histórica.

## CU-04: Evaluación de impacto urbano/industrial
- **Actor principal:** Evaluadores ambientales.
- **Objetivo:** Medir eventos significativos (por ejemplo CO y SO₂ por sobre sus límites de detección) junto con variables meteorológicas RS485 (Modbus).
- **Resumen:** La integración de sensores sincronizados y los equipos de muestreo pasivo permiten caracterizar eventos urbanos o industriales.
