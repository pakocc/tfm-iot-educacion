# D.5. Ejemplo de flujo Node-RED

A continuación se muestra un ejemplo simplificado de flujo utilizado para la lectura del sensor DHT11 y la publicación en MQTT:

```json
[
    {
        "id": "mqtt_pub",
        "type": "mqtt out",
        "topic": "aula/user1/sensor/temperatura",
        "broker": "mqtt_broker"
    },
    {
        "id": "inject",
        "type": "inject",
        "payload": "",
        "repeat": "5",
        "topic": ""
    },
    {
        "id": "function",
        "type": "function",
        "name": "Simulación",
        "func": "msg.payload = Math.random() * 5 + 20;\nreturn msg;"
    }
]
```

Este flujo permite:

- **generar un valor simulado de temperatura**,
- **publicarlo en el tópico MQTT correspondiente**,
- **visualizarlo en un dashboard**.
