# D.3. Asignación de puertos

Cada instancia de Node-RED se expone en un puerto distinto para permitir el acceso simultáneo de varios usuarios:

- **[Docente](ca://s?q=Puerto_NodeRED_docente)**: `1880`
- **[Alumno 1](ca://s?q=Puerto_NodeRED_alumno1)**: `1884`
- **[Alumno 2](ca://s?q=Puerto_NodeRED_alumno2)**: `1885`
- **[Alumno 3](ca://s?q=Puerto_NodeRED_alumno3)**: `1886`

Ejemplo de mapeo en Docker:

```yaml
ports:
  - "1884:1880"
