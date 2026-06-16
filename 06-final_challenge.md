# Desafio final

## Construye esta estructura:

```text
empresa/
├── administracion/
│   └── salarios.txt
├── marketing/
│   └── campaña.txt
└── desarrollo/
    └── codigo.sh
```

Aplica:

salarios.txt: solo lectura para el propietario (400)
campaña.txt: lectura y escritura para propietario (600)
codigo.sh: ejecutable para propietario (700)

```bash
mkdir empresa

cd empresa/

mkdir administracion

mkdir marketing

mkdir desarrollo

touch ./administracion/salarios.txt

touch ./marketing/campania.txt

touch ./desarrollo/codigo.sh

chmod 400 ./administracion/salarios.txt 

chmod 600 ./marketing/campania.txt

chmod 700 ./desarrollo/codigo.sh

find empresa -exec ls -l {} \;
total 12
drwxr-xr-x 2 crisandro crisandro 4096 jun 15 23:21 administracion
drwxr-xr-x 2 crisandro crisandro 4096 jun 15 23:22 desarrollo
drwxr-xr-x 2 crisandro crisandro 4096 jun 15 23:21 marketing
total 0
-rwx------ 1 crisandro crisandro 0 jun 15 23:22 codigo.sh
-rwx------ 1 crisandro crisandro 0 jun 15 23:22 empresa/desarrollo/codigo.sh
total 0
-r-------- 1 crisandro crisandro 0 jun 15 23:21 salarios.txt
-r-------- 1 crisandro crisandro 0 jun 15 23:21 empresa/administracion/salarios.txt
total 0
-rw------- 1 crisandro crisandro 0 jun 15 23:21 campania.txt
-rw------- 1 crisandro crisandro 0 jun 15 23:21 empresa/marketing/campania.txt
```