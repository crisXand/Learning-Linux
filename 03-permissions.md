# Permisos basicos
## Inspeccionar permisos
Revisar los permisos de ideas.txt

### Respuesta

```bash
cd backups
ls -l 
```

## Quitar permiso de lectura

```bash
chmod u-r ideas.txt
cat ideas.txt
ls -l ideas.txt
```

## Restaurar Permisos
Devolver el permiso al archivo ideas.txt

```bash
chmod u+r ideas.txt
ls -l ide
```

## Covierte un archivo en solo lectura
Convierte el archivo pendientes.txt a modo solo lectura

```bash
chmod 444 pendientes.txt
```

## Volver al archivo a su modo lectura y escritura

```bash
chmod 644 pendientes.txt
```