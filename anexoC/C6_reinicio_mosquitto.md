# C.6. Reinicio del servicio Mosquitto

Tras modificar la configuración, es necesario reiniciar el contenedor:

```bash
docker restart mosquitto
```
Para comprobar el estado del broker:

```bash
docker logs mosquitto
