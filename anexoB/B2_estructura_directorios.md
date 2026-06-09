# B.2. Estructura de directorios

Para organizar los volúmenes persistentes, se creó la siguiente estructura en la Raspberry Pi:

```bash

/home/pi/iot/
   nodered/
      mudeti/
      alumno1/
      alumno2/
      alumno3/
   mosquitto/
      config/
      data/
      log/

Cada carpeta de Node-RED almacena:

- **flujos creados por el usuario,
- **nodos instalados,
- **credenciales,
- **configuración del runtime.
