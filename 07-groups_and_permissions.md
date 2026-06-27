# Grupos y permisos 

## Crea un entorno y mira la informacion de grupos :
```bash
mkdir ~/lab-seguridad
cd ~/lab-seguridad
whoami
id 
groups
```
Anota:

UID
GID
Grupos

```text
whoami
crisandro

id
uid=1000(crisandro) gid=1000(crisandro) grupos=1000(crisandro),24(cdrom),25(floppy),27(sudo),29(audio),30(dip),44(video),46(plugdev),108(netdev),113(bluetooth),117(lpadmin),120(scanner)

groups
crisandro cdrom floppy sudo audio dip video plugdev netdev bluetooth lpadmin scanner
```

## Crear usuarios y asignar contrasenia

```bash
sudo useradd -m juan
[sudo] password for crisandro: 
sudo useradd -m maria

sudo passwd juan
Nueva contraseña: 
Vuelva a escribir la nueva contraseña: 
passwd: contraseña actualizada correctamente

ls /home/
crisandro  juan  maria

sudo passwd maria 
Nueva contraseña: 
Vuelva a escribir la nueva contraseña: 
passwd: contraseña actualizada correctamente
```

## Crear grupo y agregar usuarios

```bash
sudo groupadd development
sudo usermod -aG development juan
sudo usermod -aG development maria
 
```

```bash
id juan
uid=1001(juan) gid=1001(juan) grupos=1001(juan),1003(development)
id maria
uid=1002(maria) gid=1002(maria) grupos=1002(maria),1003(development)
```

## Crear directorio compartido llamado projects

```bash
ls -ld projects
drwxr-xr-x 2 crisandro development 4096 jun 27 13:11 projects
sudo chmod 2775 projects

ls -ld projects
drwxrwsr-x 2 crisandro development 4096 jun 27 13:11 projects
```

## Verifica si puedes crear archivos con usuarios pertenecientes al grupo development

```bash
sudo -u maria touch projects/app.py

sudo -u juan touch projects/readme.txt

ls -l projects
total 0
-rw-r--r-- 1 maria development 0 jun 27 16:04 app.py
-rw-r--r-- 1 juan  development 0 jun 27 16:05 readme.txt
```