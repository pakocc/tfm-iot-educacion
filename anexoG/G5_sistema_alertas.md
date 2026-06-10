# G.5. Sistema de alertas

El sistema domótico implementa un mecanismo de alertas que combina **[notificaciones locales](ca://s?q=Alertas_locales_NodeMCU)** (mediante el zumbador conectado a la NodeMCU) y **[alertas remotas gestionadas desde Node‑RED](ca://s?q=Alertas_remotas_NodeRED)**. Este sistema permite detectar condiciones anómalas y avisar al usuario de forma inmediata, garantizando una supervisión continua del estado de la vivienda.

Las alertas se generan a partir de tres situaciones principales:

- **[Nivel de gases elevado](ca://s?q=Alerta_gases_altos)**: cuando la lectura del sensor supera el umbral configurado.  
- **[Puerta principal abierta durante demasiado tiempo](ca://s?q=Alerta_puerta_principal_tiempo)**: si permanece abierta más de 10 segundos.  
- **[Puerta corredera en posición intermedia](ca://s?q=Alerta_puerta_corredera_intermedia)**: indica un posible atasco o fallo mecánico.

La **[NodeMCU](ca://s?q=NodeMCU_ESP8266)** publica estas alertas en los topics MQTT correspondientes dentro del espacio de nombres: `casa/alerta/#`. **Node‑RED** recibe estos mensajes y ejecuta dos acciones:

1. **[Mostrar la alerta en el dashboard](ca://s?q=Dashboard_alertas_NodeRED)**, permitiendo al usuario visualizar el evento en tiempo real.  
2. **[Enviar una notificación por correo electrónico](ca://s?q=Email_alertas_NodeRED)** mediante un nodo `e-mail` configurado con un servidor SMTP.

Este mecanismo garantiza que el usuario sea informado incluso cuando no se encuentra frente al panel de control. La combinación de alertas locales y remotas proporciona un sistema robusto y adecuado para entornos educativos, donde es fundamental que los estudiantes comprendan la importancia de la supervisión y la detección temprana de fallos.
