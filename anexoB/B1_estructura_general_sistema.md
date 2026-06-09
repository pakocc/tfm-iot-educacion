# B.1. Estructura general del sistema

La infraestructura se basa en un conjunto de contenedores independientes, cada uno asociado a un usuario (docente o alumno). Cada contenedor ejecuta una instancia de Node-RED con su propio volumen persistente y un puerto asignado de forma exclusiva. Además, se despliega un contenedor adicional para el broker MQTT (Mosquitto).

La estructura general es la siguiente:

- **Contenedor Node-RED del docente**: puerto 1880.
- **Contenedores Node-RED de los alumnos**: puertos 1884, 1885, 1886.
- **Broker MQTT (Mosquitto)**: puerto 1883.
- **Portainer**: puerto 9000 (instalado en el Anexo A).
