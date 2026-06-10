# D.1. Estructura de volúmenes persistentes

Cada instancia de Node-RED utiliza un volumen independiente que almacena:

- **[flows.json](ca://s?q=Flows_json_NodeRED)**: flujos creados por el usuario.
- **[flows_cred.json](ca://s?q=Flows_cred_NodeRED)**: credenciales cifradas.
- **[nodos instalados](ca://s?q=Nodos_instalados_NodeRED)**.
- **[configuración del runtime](ca://s?q=Runtime_NodeRED)**.
- **[archivos de autenticación](ca://s?q=Autenticacion_NodeRED)**.

La estructura general es:

```bash
/home/pi/iot/nodered/
   mudeti/
   alumno1/
   alumno2/
   alumno3/
```

Cada carpeta corresponde a un contenedor independiente.
