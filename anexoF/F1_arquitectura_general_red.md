# F.1. Arquitectura general de red

La infraestructura combina tres canales de comunicación que permiten un modelo híbrido, flexible y seguro:

- **[Red local Ethernet (LAN)](ca://s?q=Red_local_Ethernet)**: canal principal para estudiantes y dispositivos IoT, proporcionando baja latencia y estabilidad.
- **[Red Wi‑Fi](ca://s?q=Red_WiFi_IoT)**: interfaz secundaria que facilita la movilidad y el acceso desde dispositivos móviles.
- **[Red privada virtual Tailscale](ca://s?q=Acceso_remoto_Tailscale)**: mecanismo de acceso remoto seguro para el docente, sin necesidad de abrir puertos en el router.

La Raspberry Pi actúa como servidor central de la infraestructura, alojando:

- **[el broker MQTT (Mosquitto)](ca://s?q=Broker_MQTT_Mosquitto)**,
- **[las instancias multiusuario de Node‑RED](ca://s?q=NodeRED_multiusuario)**,
- **[Portainer para la gestión de contenedores](ca://s?q=Portainer_gestion_contenedores)**.

Este diseño permite una administración eficiente, un acceso seguro y una experiencia fluida para el alumnado en actividades IoT.
