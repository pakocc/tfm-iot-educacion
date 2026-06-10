# F.5. Tabla de accesos a los servicios

En la siguiente tabla se muestran los diferentes accesos a la infraestructura IoT, tanto desde la red local (LAN) como a través de la red privada virtual Tailscale.

| **[Servicio](ca://s?q=Servicio_IoT)** | **Puerto** | **Acceso LAN** | **Acceso Tailscale** |
|--------------------------------------|------------|----------------|------------------------|
| **[Node‑RED profesor](ca://s?q=NodeRED_profesor)** | 1880 | http://192.168.0.34:1880 | http://100.x.x.x:1880 |
| **[Broker MQTT](ca://s?q=Broker_MQTT_Mosquitto)** | 1883 | mqtt://192.168.0.34:1883 | mqtt://100.x.x.x:1883 |
| **[Node‑RED alumno 1](ca://s?q=NodeRED_alumno1)** | 1884 | http://192.168.0.34:1884 | http://100.x.x.x:1884 |
| **[Node‑RED alumno 2](ca://s?q=NodeRED_alumno2)** | 1885 | http://192.168.0.34:1885 | http://100.x.x.x:1885 |
| **[Node‑RED alumno 3](ca://s?q=NodeRED_alumno3)** | 1886 | http://192.168.0.34:1886 | http://100.x.x.x:1886 |
| **[Portainer](ca://s?q=Portainer_contenedores)** | 9000 | http://192.168.0.34:9000 | http://100.x.x.x:9000 |

*Tabla de accesos disponibles a los servicios de la infraestructura IoT.*
