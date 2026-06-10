# D.4. Configuración del runtime

Node-RED almacena su configuración en el archivo `settings.js`.  
Algunos parámetros relevantes utilizados en la infraestructura son:

- **[flowFile](ca://s?q=flowFile_NodeRED)**: define el archivo donde se guardan los flujos.
- **[credentialSecret](ca://s?q=credentialSecret_NodeRED)**: clave utilizada para cifrar credenciales.
- **[uiPort](ca://s?q=uiPort_NodeRED)**: puerto de acceso a la interfaz web.
- **[editorTheme](ca://s?q=editorTheme_NodeRED)**: opciones de personalización del editor.

Ejemplo:

```js
flowFile: "flows.json",
credentialSecret: "iot2026",
uiPort: process.env.PORT || 1880,
```
