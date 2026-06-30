# ACLS

## Dar acceso a usuarios en especifico

Crear un archivo y dar permisos escritura y lectura para el owner y lectura para juean
Dejar evidencia del proceso

```bash
touch 08-acls/secrets.txt

chmod 600 ./08-acls/secrets.txt 

sudo setfacl -m u:juan:r 08-acls/secrets.txt 

setfacl -m u:juan:x . #Hay que dar permiso de ejecucion tambien al directorio contendor

sudo -u juan cat secrets.txt 

```

## Eliminar acl

```bash
sudo setfacl -x u:juan secrets.txt
[sudo] password for crisandro: 
getfacl secrets.txt 
# file: secrets.txt
# owner: crisandro
# group: crisandro
user::rw-
group::---
mask::---
other::---

```

## Investigar SUID

Buscar binarios SUID:

```bash
find /usr/bin -perm -4000 -type f 2>/dev/null
```

```text
/usr/bin/sudo
/usr/bin/chfn
/usr/bin/chsh
/usr/bin/pkexec
/usr/bin/ntfs-3g
/usr/bin/su
/usr/bin/newgidmap
/usr/bin/umount
/usr/bin/fusermount3
/usr/bin/mount
/usr/bin/newuidmap
/usr/bin/gpasswd
/usr/bin/nvidia-modprobe
/usr/bin/passwd
/usr/bin/newgrp
```

Escoge tres comandos y averigua:

quién es el propietario
para qué necesitan SUID

```bash
ls -l /usr/bin/sudo
-rwsr-xr-x 1 root root 182600 feb  6 12:58 /usr/bin/sudo
ls -l /usr/bin/passwd
-rwsr-xr-x 1 root root 63960 abr 18  2025 /usr/bin/passwd
ls -l /usr/bin/mount
-rwsr-xr-x 1 root root 55528 mar 28  2024 /usr/bin/mount
```

El propietario de los archivos es el usuario root
Todos lo archivos tienen el permiso s, esto quiere decir que cualquier usuario puede ejecutar los archivos sin ser root

## Investigar SGID

Buscar:

```bash
find /usr/bin -perm -2000 -type f 2>/dev/null
```

Analiza algunos resultados.

### Respuesta

```bash
find /usr/bin -perm -2000 -type f 2>/dev/null
/usr/bin/dotlockfile
/usr/bin/crontab
/usr/bin/chage
/usr/bin/ssh-agent
/usr/bin/expiry
ls -l /usr/bin/chage
-rwxr-sr-x 1 root shadow 80256 abr 18  2025 /usr/bin/chage
ls -l /usr/bin/crontab
-rwxr-sr-x 1 root crontab 43568 feb 22  2021 /usr/bin/crontab
ls -l /usr/bin/ssh-agent
-rwxr-sr-x 1 root ssh 354440 abr 16 10:19 /usr/bin/ssh-agent
```

El bit SGID (Set Group ID) hace que un programa se ejecute utilizando el grupo propietario del archivo, en lugar del grupo del usuario que lo ejecuta. Esto permite acceder de forma controlada a recursos compartidos del sistema sin otorgar privilegios completos de administrador.

Ejemplos:

/usr/bin/crontab
Propietario: root
Grupo: crontab
Utiliza SGID para crear y modificar los archivos de tareas programadas almacenados en directorios accesibles únicamente por el grupo crontab.

/usr/bin/wall (si está presente)
Propietario: root
Grupo: tty
Utiliza SGID para poder escribir mensajes en los terminales de otros usuarios.
/usr/bin/ssh-agent (si está presente)
Propietario: root
Grupo: relacionado con SSH (varía según la distribución)
Utiliza SGID para acceder a recursos controlados por ese grupo durante la gestión de claves SSH.


## Investigar Sticky Bit

Ver:

ls -ld /tmp

Explica:

quién puede escribir
quién puede borrar
por qué existe el Sticky Bit

```bash
ls -ld /tmp
drwxrwxrwt 20 root root 12288 jun 29 23:06 /tmp
```

En este directorio pueden escribir root, los pertenecientes al grupo root y others
Los ususarios root y los del grupo root pueden borrar archivos
Ademas otros usuarios pueden borrar pero por el permiso `t` solo pueden borrar los archivos de los cuales son owners

El permiso Sticky Bit existe porque en linux para borrar archivos basta con tener permisos de escritura en la carpeta contenedora de este, y este permiso 
evita que si usuario debe borrar archivos de una carpeta, solo los haga sobre los archivos de los cuales es duenio