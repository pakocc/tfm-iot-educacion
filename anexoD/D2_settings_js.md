# D.2. Archivo `settings.js`

El archivo `settings.js` controla la configuración interna de Node-RED.  
A continuación se muestra un fragmento adaptado para habilitar autenticación web por usuario:

```js
adminAuth: {
    type: "credentials",
    users: [
        {
            username: "mudeti",
            password: "$2b$08$xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
            permissions: "*"
        },
        {
            username: "alumno1",
            password: "$2b$08$xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
            permissions: "*"
        },
        {
            username: "alumno2",
            password: "$2b$08$xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
            permissions: "*"
        },
        {
            username: "alumno3",
            password: "$2b$08$xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
            permissions: "*"
        }
    ]
},
```
Los valores de password corresponden a hashes bcrypt generados mediante:
```bash
node-red-admin hash-pw
