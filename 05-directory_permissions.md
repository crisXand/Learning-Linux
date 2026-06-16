# Permisos para directorios

## Crea un directorio publico y otro privado

```bash
mkdir private
mkdir public 

chmod 755 public
chmod 700 private

ls -ld private
drwx------ 2 crisandro crisandro 4096 jun 14 15:52 private

ls -ld public/
drwxr-xr-x 2 crisandro crisandro 4096 jun 14 15:53 public/
```

