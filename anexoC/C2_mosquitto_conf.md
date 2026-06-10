# C.2. Archivo `mosquitto.conf`

El archivo principal de configuración del broker es el siguiente:

```conf
# Archivo de configuración de Mosquitto

persistence true
persistence_location /mosquitto/data/

log_dest file /mosquitto/log/mosquitto.log

listener 1883
allow_anonymous false

password_file /mosquitto/config/passwd
acl_file /mosquitto/config/acl
```
Los parámetros clave son:

- **allow_anonymous false:** desactiva el acceso sin autenticación.
- **password_file:** archivo con usuarios y contraseñas.
- **acl_file:** archivo con permisos por usuario.
