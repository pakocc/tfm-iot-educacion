# G.4. Flujos Node‑RED

**[Node‑RED](ca://s?q=NodeRED_IoT)** se utiliza como plataforma de supervisión, control y generación de alertas del sistema domótico. Su naturaleza visual permite representar de forma clara la lógica de funcionamiento, facilitando tanto la comprensión como la reproducibilidad del sistema en entornos educativos.

Los flujos implementados se organizan en tres bloques principales:

- **[Monitorización](ca://s?q=Monitorizacion_NodeRED)**  
- **[Control](ca://s?q=Control_actuadores_NodeRED)**  
- **[Alertas](ca://s?q=Alertas_NodeRED)**  

En esta sección se describen los flujos desarrollados y se incluye el listado completo en formato JSON para su importación directa en Node‑RED.

---

## G.4.1. Monitorización y dashboard

El dashboard de Node‑RED proporciona una visualización en tiempo real del estado del sistema. Incluye indicadores de:

- **[temperatura](ca://s?q=Temperatura_NodeRED)**,  
- **[humedad](ca://s?q=Humedad_NodeRED)**,  
- **[nivel de gases](ca://s?q=Gases_NodeRED)**,  
- **[estado de la puerta principal](ca://s?q=Puerta_principal_NodeRED)**,  
- **[estado de la puerta corredera](ca://s?q=Puerta_corredera_NodeRED)**,  
- **[alertas activas](ca://s?q=Alertas_activas_NodeRED)**.

Además, incorpora controles interactivos para la apertura y cierre de ambas puertas.

El dashboard se estructura en cinco grupos:

- **[Clima](ca://s?q=Grupo_Clima_NodeRED)**: temperatura y humedad.  
- **[Calidad del aire](ca://s?q=Grupo_Calidad_Aire_NodeRED)**: nivel de gases y alerta asociada.  
- **[Puerta principal](ca://s?q=Grupo_Puerta_Principal_NodeRED)**: estado y botones de control.  
- **[Puerta corredera](ca://s?q=Grupo_Puerta_Corredera_NodeRED)**: estado, semáforo y botones de control.  
- **[Alertas](ca://s?q=Grupo_Alertas_NodeRED)**: última alerta recibida vía MQTT.

El Listado **del flujo JSON del dashboard** se muestra más adelante.

---

## G.4.2. Sistema de alertas

El sistema de alertas se basa en la recepción de mensajes MQTT publicados por la NodeMCU en los topics:

- `casa/alerta/#`

Node‑RED procesa estos mensajes mediante nodos **switch** y **function**, generando:

- notificaciones visuales en el dashboard,  
- envío de correos electrónicos cuando se detectan condiciones anómalas.

Las alertas implementadas son:

- **[Nivel de gases por encima del umbral](ca://s?q=Alerta_gases_NodeRED)**,  
- **[Puerta principal abierta más de 10 segundos](ca://s?q=Alerta_puerta_principal_NodeRED)**,  
- **[Puerta corredera en posición intermedia (posible atasco)](ca://s?q=Alerta_corredera_NodeRED)**.

Cada alerta activa un nodo **e-mail** configurado con un servidor SMTP, permitiendo el envío automático de notificaciones al usuario.

---

## G.4.3. Control de actuadores

Node‑RED permite enviar comandos a la NodeMCU mediante la publicación de mensajes MQTT en los topics:

- `casa/puerta_principal/cmd`  
- `casa/puerta_corredera/cmd`

Los botones del dashboard generan estos mensajes, permitiendo:

- **[abrir o cerrar la puerta principal](ca://s?q=Control_puerta_principal_NodeRED)** (servo SG90),  
- **[abrir, cerrar o detener la puerta corredera](ca://s?q=Control_puerta_corredera_NodeRED)** (motor DC + L293D).

El sistema garantiza una interacción fluida entre el usuario y los actuadores físicos.

---

## G.4.4. Listado completo del flujo Node‑RED

El siguiente listado contiene el flujo completo en formato JSON, listo para ser importado en Node‑RED mediante la opción *Import → Clipboard*.

```json
[
    {
        "id": "eaf4a3113f9eda18",
        "type": "ui-template",
        "z": "863df16f8e7ee144",
        "group": "9f03d8846733a047",
        "page": "",
        "ui": "",
        "name": "IconoBuzzer",
        "order": 3,
        "width": "1",
        "height": "1",
        "head": "",
        "format": "<style>\n    .circle {\n        width: 40px;\n        height: 40px;\n        border-radius: 50%;\n        border: 2px solid #555;\n        background-color: var(--circle-color);\n    }\n</style>\n\n<div class=\"circle\" style=\"--circle-color: {{msg.color}}\"></div>",
        "storeOutMessages": true,
        "passthru": true,
        "resendOnRefresh": true,
        "templateScope": "local",
        "className": "<div class=\"circle {{msg.colorClass}}\"></div>",
        "x": 570,
        "y": 460,
        "wires": [
            [
                "f789862f9a7c210a"
            ]
        ]
    },
    {
        "id": "9f03d8846733a047",
        "type": "ui-group",
        "name": "Domotica/gases",
        "page": "002265da152cd0df",
        "width": "4",
        "height": 1,
        "order": 3,
        "showTitle": true,
        "className": "",
        "visible": "true",
        "disabled": "false",
        "groupType": "default"
    },
    {
        "id": "002265da152cd0df",
        "type": "ui-page",
        "name": "Domotica",
        "ui": "1b916cd489b09672",
        "path": "/domotica",
        "icon": "home",
        "layout": "grid",
        "theme": "510aba22cc4dbd62",
        "breakpoints": [
            {
                "name": "Default",
                "px": "0",
                "cols": "3"
            },
            {
                "name": "Tablet",
                "px": "576",
                "cols": "6"
            },
            {
                "name": "Small Desktop",
                "px": "768",
                "cols": "9"
            },
            {
                "name": "Desktop",
                "px": "1024",
                "cols": "12"
            }
        ],
        "order": 1,
        "className": "",
        "visible": true,
        "disabled": false
    },
    {
        "id": "1b916cd489b09672",
        "type": "ui-base",
        "name": "profesor",
        "path": "/dashboard",
        "appIcon": "",
        "includeClientData": true,
        "acceptsClientConfig": [
            "ui-notification",
            "ui-control"
        ],
        "showPathInSidebar": true,
        "headerContent": "page",
        "navigationStyle": "default",
        "titleBarStyle": "default",
        "showReconnectNotification": true,
        "notificationDisplayTime": 1,
        "showDisconnectNotification": true,
        "allowInstall": false
    },
    {
        "id": "510aba22cc4dbd62",
        "type": "ui-theme",
        "name": "Default Theme",
        "colors": {
            "surface": "#ffffff",
            "primary": "#0094ce",
            "bgPage": "#eeeeee",
            "groupBg": "#ffffff",
            "groupOutline": "#cccccc"
        },
        "sizes": {
            "density": "default",
            "pagePadding": "12px",
            "groupGap": "12px",
            "groupBorderRadius": "4px",
            "widgetGap": "12px"
        }
    },
    {
        "id": "203d814e37aa014e",
        "type": "global-config",
        "env": [],
        "modules": {
            "@flowfuse/node-red-dashboard": "1.30.2"
        }
    }
]
```
