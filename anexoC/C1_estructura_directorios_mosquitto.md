# C.1. Estructura de directorios de Mosquitto

Para organizar la configuración del broker, se creó la siguiente estructura:

```bash
/home/pi/iot/mosquitto/
   config/
      mosquitto.conf
      acl
   data/
      log/
```

Los directorios cumplen las siguientes funciones:

- **config/:** archivos de configuración del broker.
- **data/:** almacenamiento de la base de datos interna de Mosquitto.
- **log/:** registro de actividad y errores.
