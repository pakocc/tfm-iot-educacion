# E.6. Publicación y suscripción MQTT

Los tópicos utilizados siguen la estructura definida en el Anexo C y permiten organizar la comunicación MQTT de forma coherente entre sensores y actuadores.

## Publicación de temperatura
```text
aula/user1/sensor/temperatura
```
## Publicación de humedad
```text
aula/user1/sensor/humedad
```
## Suscripción para controlar el LED
```text
aula/user1/actuador/led
```

Estos tópicos mantienen la jerarquía definida en el sistema multiusuario y permiten una comunicación clara entre los dispositivos IoT y el broker MQTT.
