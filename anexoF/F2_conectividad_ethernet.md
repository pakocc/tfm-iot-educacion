# F.2. Conectividad mediante Ethernet

La Raspberry Pi se conectó al router del aula mediante cable Ethernet, obteniendo una dirección IP local asignada por DHCP (por ejemplo, `192.168.0.34`). Esta interfaz constituye el canal principal para:

- **[el acceso de los estudiantes a sus instancias de Node‑RED](ca://s?q=Acceso_NodeRED_Ethernet)**,
- **[la comunicación entre contenedores Docker](ca://s?q=Comunicacion_Docker_Ethernet)**,
- **[la interacción con dispositivos IoT conectados a la misma red](ca://s?q=IoT_red_local)**,
- **[la administración del sistema desde el aula](ca://s?q=Administracion_RaspberryPi_Ethernet)**.

El uso de Ethernet garantiza baja latencia y estabilidad, aspectos críticos cuando se gestionan múltiples flujos MQTT simultáneos.
