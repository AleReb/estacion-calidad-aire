# Estación Multiparamétrica de Calidad del Aire

La estación integra sensores **electroquímicos**, **ópticos** y **meteorológicos** en una estructura vertical compacta. El sistema recolecta, almacena y transmite datos **en tiempo casi real**, lo que permite correlacionar calidad del aire y condiciones meteorológicas. Actualmente se encuentra en construcción con pruebas de campo; todos los sensores cuentan con especificaciones validadas y se calibran antes de entrar en operación.

## Características destacadas
- Soporte tipo torre de 2–5 m con exposición 360° y altura de medición a 1,5 m sobre nivel del suelo.
- Alimentación autónoma mediante panel solar y banco de baterías.
- Comunicaciones GSM/4G complementadas con almacenamiento local en microSD.
- Plataforma única con sensores sincronizados y módulos accesibles para reemplazo rápido.
- Incluye colectores para muestreo pasivo de material particulado sedimentable (conforme a Resolución Exenta N° 1449 del MMA, 2023).

## Sensores integrados
| Tipo | Modelo | Rango / Límite | Precisión / Resolución | Tecnología |
| --- | --- | --- | --- | --- |
| PM1.0/2.5/10 | Plantower PMS5003ST | 1 µg/m³ (límite) | ±1 µg/m³ | Óptico láser |
| O₃ | Alphasense OX-B431 | 1 ppb (límite) | ±1 ppbv | Amperométrico |
| NO₂ | Alphasense NO2-B43F | 1 ppb (límite) | ±1 ppbv | Amperométrico |
| CO | Alphasense CO-B4 | 1 ppm (límite) | ±1 ppmv | Amperométrico |
| NO | Alphasense NO-B4 | 1 ppb (límite) | ±1 ppbv | Amperométrico |
| CO₂ | Winsen MH-Z19B/MH-Z19C | 1 ppm (resolución) | — | Infrarrojo NDIR |
| VOC (totales) | Winsen ZE40A-TVOC | 0–2 ppm | 0.01 ppm | PID/MOS |
| SO₂ | Alphasense SO2-B4 (objetivo) | 5 ppb (error) | — | Electroquímico |
| Meteo (T, HR, P, VV, DV, precipitación, radiación, UV, luz) | ComWinTop CWT-UWD-SDTHAPSIR / CWT-UR-S | Según ficha | Ver ficha | RS485 (Modbus) |

## Aplicaciones
- Monitoreo ciudadano y municipal.
- Validación de sensores de bajo costo.
- Correlación con estaciones de referencia.
- Evaluación de impactos urbanos o industriales.

## Guía rápida del repositorio
- `01-requisitos-interesados/`: necesidades y casos de uso basados en el brochure técnico.
- `02-requisitos-sistema/`: requisitos funcionales/no funcionales y especificaciones (contaminantes, soporte meteo, emergentes).
- `03-diseño-arquitectura/`: decisiones, vistas de arquitectura y espacio para diagramas.
- `04-diseño-detallado/`: definición preliminar de hardware, firmware y gestión de datos.
- `05-implementacion/`: árbol para hardware (PCB, carcasas, componentes), firmware (PlatformIO) y software (backend/frontend/scripts).
- `06-10/`: integración, verificación, validación, despliegue y operación/mantenimiento.
- `documentacion/`, `datos/`, `herramientas/`, `configuracion/`: repositorios para datasheets, datasets EPA/WMO, utilidades y perfiles de configuración.
- `gestion-proyecto/planificacion/roles-responsabilidades.md`: lista actualizada de cargos, incluyendo QA/QC y administración de datos.

## Cómo colaborar (incluye uso con Codex)
1. Clona este repositorio y revisa el README antes de abrir Codex.
2. Abre una sesión de Codex desde la raíz (`codex run`), y revisa los archivos en `gestion-proyecto/planificacion/` para conocer roles y tareas pendientes.
3. Documenta nuevas decisiones en la carpeta correspondiente (por ejemplo, requisitos → `02-...`, hardware → `04-diseño-detallado/...`).
4. Añade contenidos reales en los documentos vacíos; si no existe información todavía, deja una nota explícita indicando que está pendiente (mantén el estilo usado hasta ahora).
5. Usa `.gitkeep` para conservar directorios vacíos si agregas nuevos subcontenidos.
6. Antes de hacer commit, ejecuta `git status` para revisar qué archivos cambiaste y organiza los mensajes de commit por área (requisitos, arquitectura, firmware, etc.).

## Contacto
Proyecto en desarrollo: **Estación Multiparamétrica de Monitoreo Ambiental**  \
Contacto: [luis.gomez@udd.cl](mailto:luis.gomez@udd.cl)
