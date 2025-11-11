# Decisiones de diseño registradas

1. **Sincronización en plataforma única:** Se decidió integrar todos los sensores (electroquímicos, ópticos y meteorológicos) en la misma plataforma para garantizar análisis en tiempo casi real.
2. **Energía autónoma:** El uso de panel solar + banco de baterías responde a la necesidad explícita de operación autónoma indicada en el brochure.
3. **Comunicaciones GSM/4G + microSD:** La combinación permite transmisión remota y respaldo local, tal como se describe en la configuración del sistema.
4. **Selección Plantower PMS5003ST:** Se escogió por su límite de detección de 1 µg/m³ y precisión ±1 µg/m³ para PM₁.₀, PM₂.₅ y PM₁₀.
5. **Selección Alphasense serie B4/B43F:** La decisión garantiza límites de detección de 1 ppb (1 ppm para CO) con precisión ±1 ppbv (±1 ppmv para CO) y estabilidad declarada.
6. **Integración RS485 (Modbus):** La estación digital multiparámetro RS485 proporciona las variables meteorológicas requeridas y facilita la conexión con el datalogger.
7. **Muestreo pasivo complementario:** Se incorpora un sistema compatible con Resolución Exenta N° 1449 (MMA, 2023) para material particulado sedimentable.
