# G.1. Arquitectura general del sistema

La Figura [**Arquitectura del sistema domótico**](ca://s?q=Arquitectura_sistema_domotico) muestra la arquitectura completa del sistema domótico. La **[NodeMCU](ca://s?q=NodeMCU_ESP8266)** actúa como nodo IoT principal, encargado de la lectura de sensores y el control de actuadores. 

La comunicación con el servidor se realiza mediante **[MQTT](ca://s?q=Protocolo_MQTT)**, permitiendo la integración con **[Node‑RED](ca://s?q=NodeRED_IoT)** para:

- **[visualización en tiempo real](ca://s?q=Visualizacion_tiempo_real_NodeRED)**,
- **[control remoto de actuadores](ca://s?q=Control_remoto_actuadores)**,
- **[generación de alertas](ca://s?q=Alertas_NodeRED)**.

![Arquitectura general del sistema domótico](ImagenAnexoG_ArquitecturaNodeMCU.png)

*Figura: Arquitectura general del sistema domótico basado en NodeMCU, MQTT y Node‑RED (elaboración propia con asistencia de IA).*
