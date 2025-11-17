# Firmware Placa Madre Línea Base v0.0.3

Este directorio contiene el código fuente del firmware para la placa de monitoreo ambiental "Placa Madre Rev. D", basada en un microcontrolador ESP32.

## Descripción General

El firmware está diseñado para operar como un sistema de monitoreo ambiental autónomo y robusto. Se encarga de recolectar datos de una amplia gama de sensores, almacenarlos localmente en una tarjeta SD y transmitirlos periódicamente a un servidor remoto a través de una red celular (GSM/LTE). Además, integra la capacidad de capturar y enviar imágenes desde una cámara externa.

## Características Principales

-   **Adquisición de Datos Multi-Sensor:** Integra y lee datos de sensores analógicos y digitales a través de I2C, UART y RS485.
-   **Almacenamiento Local:** Guarda todas las mediciones y los registros de errores en formato CSV en una tarjeta SD para redundancia y análisis posterior.
-   **Comunicaciones Celulares:** Utiliza un módem SIM7600 para enviar datos de sensores e imágenes a un servidor web mediante peticiones HTTP (GET y POST).
-   **Gestión de Cámara Externa:** Controla una cámara conectada por puerto serie para solicitar, recibir y almacenar imágenes.
-   **Robustez y Estabilidad:** Implementa un Watchdog Timer (WDT) para reiniciarse automáticamente en caso de bloqueo. Incluye una máquina de estados para reiniciar el módem si falla repetidamente.
-   **Gestión de Energía:** Controla la alimentación de periféricos como la cámara y el módem para optimizar el consumo.
-   **Interfaz de Depuración:** Ofrece un conjunto de comandos a través del puerto serie para facilitar la depuración y el control manual de funciones clave.
-   **Feedback Visual:** Utiliza un LED RGB (NeoPixel) para indicar el estado del sistema (inicio, éxito, error, etc.).

## Hardware y Librerías Clave

-   **Microcontrolador:** ESP32
-   **Módem:** SIMCom SIM7600 (`TinyGsmClient`)
-   **Sensores Analógicos:** Múltiples `Adafruit_ADS1115` para gases (NO₂, CO, O₃, NO, SO₂).
-   **Sensores Digitales:**
    -   `MHZ19` (CO₂) por UART.
    -   `PMS5003` (Material Particulado) por UART.
    -   Estación Meteorológica y Sensor UV por RS485 (`ModbusMaster`).
    -   Sensor TVOC/SO₂ externo por I2C.
-   **Reloj en Tiempo Real:** `RTC_DS3231` para timestamping preciso.
-   **Almacenamiento:** Tarjeta MicroSD.
-   **Cámara:** Dispositivo externo controlado por UART.

## Estructura del Código y Módulos

El proyecto está modularizado en varios archivos `.ino` para una mejor organización:

-   `PLACAMADRE_LINEA_BASE_V0_0_3.ino`: Archivo principal. Contiene la lógica de `setup()` y `loop()`, la inicialización de todos los periféricos y la orquestación de las tareas principales (leer, guardar, enviar).
-   `sensores.ino`: Agrupa todas las funciones dedicadas a la lectura de los diferentes sensores (ADCs, Modbus, I2C, UART).
-   `datalogger.ino`: Gestiona todas las operaciones de escritura en la tarjeta SD, incluyendo la creación de archivos CSV para datos y logs, y la función para añadir registros.
-   `gsm.ino`: Contiene toda la lógica de comunicación con el módem SIM7600. Esto incluye el envío de comandos AT, la conexión a la red GPRS, el envío de datos por HTTP y la máquina de estados para reiniciar el módem.
-   `cam.ino`: Implementa el protocolo de comunicación serie para solicitar y recibir imágenes de la cámara externa, gestionando la recepción por trozos y los reintentos.
-   `rtc.ino`: Funciones para la gestión del reloj DS3231, incluyendo la sincronización de la hora a partir de la red celular.
-   `neopixel.ino`: Controla el LED RGB para proporcionar feedback visual del estado del sistema.
-   `serialComands.ino`: Define una interfaz de comandos a través del monitor serie para depuración.
-   `auxiliar.ino`: Contiene funciones de ayuda, como la que imprime el motivo del último reinicio del ESP32.
-   `web.ino`: (Actualmente desactivado en el código principal) Implementa un servidor web a través de un punto de acceso WiFi para gestionar los archivos de la SD de forma remota.

## Lógica Operacional

El `loop()` principal opera en base a temporizadores no bloqueantes (`millis()`) y una máquina de estados simple controlada por banderas (`bools`):

1.  **Lectura de Sensores (`leyendoDatos`):** Cada 20 segundos, se leen todos los sensores y se actualizan las variables globales.
2.  **Guardado en SD (`savedSD`):** Cada 60 segundos, se construye una línea de CSV con los últimos datos leídos y se guarda en la tarjeta SD.
3.  **Envío de Datos (`sending`):** Cada 5 minutos, se envían los últimos datos al servidor remoto a través de una petición HTTP GET.
4.  **Gestión de Fotos (`requestedfoto`):** Cada 3 horas, se solicita una foto a la cámara, se recibe, se guarda en la SD y se envía al servidor a través de una petición HTTP POST.

## Comandos de Depuración por Puerto Serie

Conectado a 115200 baudios, puedes usar los siguientes comandos:

-   `h`: Muestra la lista de comandos.
-   `s`: Envía la última foto capturada al servidor.
-   `t`: Sincroniza el reloj RTC con la hora de la red celular.
-   `c`: Enciende la cámara y solicita una foto.
-   `d`: Envía los datos de los sensores al servidor.
-   `e`: Inicia un ciclo de reinicio de energía para el módem.
-   `f`: Simula un error de transmisión para probar el contador de fallos del módem.
-   `g`: Realiza un test de la SIM y actualiza la información de la red.
