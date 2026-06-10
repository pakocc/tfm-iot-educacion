# C.3. Creación de usuarios y contraseñas

Para crear los usuarios del sistema se utilizó el comando:

```bash
mosquitto_passwd -c /home/pi/iot/mosquitto/config/passwd mudeti
mosquitto_passwd /home/pi/iot/mosquitto/config/passwd alumno1
mosquitto_passwd /home/pi/iot/mosquitto/config/passwd alumno2
mosquitto_passwd /home/pi/iot/mosquitto/config/passwd alumno3
```

El archivo __passwd__ queda almacenado en formato cifrado.
