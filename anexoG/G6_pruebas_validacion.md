# G.6. Pruebas y validación

Con el objetivo de garantizar el correcto funcionamiento del sistema domótico, se realizaron diversas pruebas orientadas a validar tanto la **[lectura de sensores](ca://s?q=Pruebas_sensores_NodeMCU)** como el **[control de actuadores](ca://s?q=Pruebas_actuadores_NodeMCU)**, la **[comunicación MQTT](ca://s?q=Pruebas_MQTT_NodeMCU)** y la **[gestión de alertas](ca://s?q=Pruebas_alertas_NodeRED)**. Estas pruebas permiten demostrar que la arquitectura implementada es estable, reproducible y adecuada para su uso en entornos educativos.

---

## Pruebas de sensores

Se verificó el comportamiento de los sensores conectados a la NodeMCU:

- **[Temperatura y humedad](ca://s?q=Prueba_DHT11)**: se comprobó la estabilidad de las lecturas del sensor DHT11 en diferentes condiciones ambientales.  
- **[Sensor de gases](ca://s?q=Prueba_sensor_gases)**: se evaluó la respuesta ante incrementos controlados de concentración, confirmando la activación de la alerta cuando se superó el umbral configurado.  
- **[Sensor magnético](ca://s?q=Prueba_sensor_magnetico)**: se validó la detección de apertura y cierre de la puerta principal mediante pruebas repetidas.  
- **[Finales de carrera](ca://s?q=Prueba_finales_carrera)**: se confirmó la correcta identificación de las posiciones abierta, cerrada e intermedia de la puerta corredera.

Los resultados mostraron lecturas consistentes y una detección fiable de los estados físicos.

---

## Pruebas de actuadores

Se realizaron pruebas funcionales sobre los actuadores:

- **[Servo de la puerta principal](ca://s?q=Prueba_servo_puerta_principal)**: se verificó la apertura y cierre mediante comandos MQTT enviados desde Node‑RED.  
- **[Motor de la puerta corredera](ca://s?q=Prueba_motor_corredera)**: se evaluó el movimiento en ambos sentidos y la parada de emergencia.  
- **[Semáforo LED](ca://s?q=Prueba_semaforo_LED)**: se confirmó la correspondencia entre el estado de la puerta corredera y la iluminación del LED correspondiente.  
- **[Zumbador](ca://s?q=Prueba_zumbador_NodeMCU)**: se validaron los tres modos de alerta (continuo, intermitente y pitidos).

Los actuadores respondieron correctamente a los comandos y reflejaron el estado del sistema en tiempo real.

---

## Pruebas de comunicación MQTT

Se realizaron pruebas de publicación y suscripción utilizando el broker Mosquitto:

- Se confirmó la recepción de datos de sensores en los topics correspondientes.  
- Se verificó la entrega de comandos desde Node‑RED hacia la NodeMCU.  
- Se evaluó la latencia de comunicación, obteniendo tiempos de respuesta adecuados para un entorno educativo.

La comunicación se mantuvo estable durante todas las pruebas, sin pérdidas de mensajes.

---

## Pruebas del sistema de alertas

Se probaron las tres alertas principales:

- **[Gases altos](ca://s?q=Prueba_alerta_gases)**: se generó una alerta local (zumbador) y remota (correo electrónico).  
- **[Puerta principal abierta](ca://s?q=Prueba_alerta_puerta_principal)**: se confirmó la activación tras superar el tiempo límite.  
- **[Puerta corredera en posición intermedia](ca://s?q=Prueba_alerta_corredera)**: se validó la detección del estado anómalo y la generación de la alerta.

En todos los casos, las alertas se mostraron correctamente en el dashboard y se envió la notificación correspondiente.

---

## Conclusiones de las pruebas

Las pruebas realizadas demuestran que el sistema es **funcional**, **estable** y **adecuado para su uso en actividades docentes**. La combinación de sensores, actuadores, comunicación MQTT y Node‑RED permite a los estudiantes comprender de forma práctica los principios fundamentales de la domótica y del Internet de las Cosas.
