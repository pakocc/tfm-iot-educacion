# E.4. Esquema de conexión de un LED como actuador

El LED se conectó a la placa NodeMCU de la siguiente forma:

| **[Pin LED](ca://s?q=Pin_LED)** | **[Pin NodeMCU](ca://s?q=Pin_NodeMCU)** |
|---------------------------------|------------------------------------------|
| Ánodo                           | D2 (GPIO4) + resistencia 220 Ω¹          |
| Cátodo                          | GND                                      |

¹ *Si el módulo del actuador LED ya incorpora una resistencia de protección, no es necesario añadir esta resistencia externamente.*

Este actuador permite realizar actividades de control remoto mediante MQTT.
