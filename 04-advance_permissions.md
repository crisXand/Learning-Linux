# Permisos avanzados
## Realizar un script e intentar ejecutarlo

### Respuesta
```bash
touch greeting.sh
./greeting.sh
```

```text
./greeting.sh: Permiso denegado
```

## Hacerlo ejecutable
Agregar permiso para ejecutarlo

### Respuesta
```bash
chmod u+x ./greeting.sh
```

```text
Hola mundo
```

## Comprender permisos numericos

Ejecutar
```bash
chmod 777 greeting.sh
chmod 755 greeting.sh
chmod 700 greeting.sh
```

Despues de cada cambio ejecuta y explica los cambions

```bash
ls -l
```

### Respuesta
```bash
chmod 777 greeting.sh
ls -l
```

Explicacion

```bash
total 4
-rwxrwxrwx 1 crisandro crisandro 30 jun 13 23:48 greeting.sh
```

Este archivo tiene permiso de escritura (w), lectura(r) y ejecucion (x) para todos los usuarios: propietario (u), groups (g) y otros usuarios (O)

```bash
chmod 755 greeting.sh
ls -l
```
Explicacion

```bash
total 4
-rwxr-xr-x 1 crisandro crisandro 30 jun 13 23:48 greeting.sh
```
Este archivo tiene permisos lectura (r) y ejecucion (x) para todos los usuarios pero solo tiene permisos de ejecucion para el usuario propietario


```bash
chmod 700 greeting.sh
ls -l
```

Salida
```bash
ls -l
total 4
-rwx------ 1 crisandro crisandro 30 jun 13 23:48 greeting.sh
```

Explicacion
Este archivo tiene permisos de permiso de escritura (w), lectura(r) y ejecucion (x) solo para el usuario propietario, mientras que para los otros no tiene ninguno
