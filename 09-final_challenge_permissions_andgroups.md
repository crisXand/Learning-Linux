# Desafío final

Simula una empresa:

empresa/
├── administracion/
├── desarrollo/
├── marketing/
└── compartido/

Requisitos:

Grupo administracion
Grupo desarrollo
Grupo marketing
Usuarios para cada área
Cada departamento sólo accede a su carpeta
`compartido` accesible para todos
SGID en todas las carpetas departamentales
Sticky Bit en `compartido`
ACL para que el gerente pueda leer todo

## Procedimiento

### Creando carpetas, grupos y usuarios

```bash
#Groups
mkdir administration

mkdir development

mkdir marketing

mkdir shared

sudo groupadd development
sudo groupadd administration
sudo groupadd marketing

#users
sudo useradd -m diana
sudo useradd -m Jonh
sudo useradd -m Carla
sudo useradd -m gerente

# change groups of the folders
sudo chgrp administration administration

sudo chgrp development development/

sudo chgrp marketing marketing/

#add users to groups
sudo usermod -aG marketing diana

sudo usermod -aG development Jonh

sudo usermod -aG marketing Carla

sudo -u Carla groups
Carla administration marketing
sudo gpasswd -d Carla marketing
Eliminando al usuario Carla del grupo marketing
sudo -u Carla groups
Carla administration

#Change permissions 
sudo chmod 2770 administration

sudo chmod 2770 marketing/

sudo chmod 2770 development/

sudo chmod 1777 shared/

#ACL para que el gerente pueda leer todo

setfacl -d -m u:gerente:rx development/

setfacl -d -m u:gerente:rx marketing

setfacl -d -m u:gerente:rx administration/

getfacl administration

id diana
uid=1003(diana) gid=1006(diana) grupos=1006(diana),1005(marketing)
id Jonh
uid=1004(Jonh) gid=1007(Jonh) grupos=1007(Jonh),1003(development)
id Carla
uid=1005(Carla) gid=1008(Carla) grupos=1008(Carla),1004(administration)
id gerente
uid=1006(gerente) gid=1009(gerente) grupos=1009(gerente)

# user gerente can see any file on development
sudo -u gerente cat ./development/index.html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>

</body>
</html>

# user diana cant create a new file on development
sudo -u diana touch development/report.txt
touch: no se puede efectuar `touch' sobre 'development/report.txt': Permiso denegado

# The user 'jonh' can create files in their corresponding folder.
sudo -u Jonh touch ./development/index.html

# verify inheritance of SGID

sudo -u Carla touch administration/report.txt
[sudo] password for crisandro: 
ls -l administration/
total 0
-rw-rw----+ 1 Carla administration 0 jul  4 14:00 report.txt

```