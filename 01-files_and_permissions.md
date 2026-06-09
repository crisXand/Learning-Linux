# Ejercicios basicos sobre archivos y permisos

## Ejercicio 1
Crea la siguiente estructura

```text
proyecto/
├── documentos/
├── imagenes/
└── backups/
```

### Respuesta

```bash
mkdir proyecto
cd proyecto
mkdir documentos
mkdir imagenes
mkdir backups
cd ..
tree
```

## Crear archivos
Dentro de documentos crea, luego verifica que existen

```text
notas.txt
tareas.txt
ideas.txt
```

### Respuesta

```bash
cd documentos
touch notas.txt
touch tareas.txt
touch ideas.tx
ls -l
```

## Ejercicio 4: Mover archivos
Mueve ideas.txt a backups

```bash
cd documentos
mv ideas.txt ../backups
cd ..
tree
```

## Ejercicio 5: Renombrar archivos
Renombra: tareas.txt por pendientes.txt

```bash
cd documentos
mv tareas.txt pendientes.txt
ls -l
```

## Ejercicio 6
Borrar notas.txt y comprobar que ya no existe

```bash
rm notas.txt 
ls -l
```


