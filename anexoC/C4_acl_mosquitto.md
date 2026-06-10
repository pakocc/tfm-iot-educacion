# C.4. Archivo de listas de control de acceso (ACL)

El archivo `acl` define los permisos de lectura y escritura para cada usuario:

```conf
# ACL del docente
user mudeti
topic readwrite #

# ACL del alumno 1
user alumno1
topic readwrite aula/user1/#

# ACL del alumno 2
user alumno2
topic readwrite aula/user2/#

# ACL del alumno 3
user alumno3
topic readwrite aula/user3/#
```
Esta configuración garantiza:

- Cada alumno solo puede acceder a su propio espacio.
- No existe posibilidad de interferir en los datos de otros usuarios.
- El docente tiene acceso completo a todos los tópicos.
