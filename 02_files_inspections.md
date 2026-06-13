# Inspeccion de archivos
## Ejercicio 7 Escribir contenido
Agrega texto a pendientes.txt.

```text
Ejemplo:

Comprar café
Estudiar Linux
Hacer backup
```

Respuestas

```bash
cat << 'EOF' > pendientes.txt 
> Comprar cafe
> Estudiar Linux
> Hacer backup
> EOF

cat pendientes.txt
```

## Ejercicio 8 
Averigua cuantas lineas tiene el archivo

```bash
wc --total pendientes.txt
```

## Leer contenido
Mostrar el contenido con cat, less, head, tail

- less permite ver archivos extensos pagina por paginas en lugar de mostrar todo el texto de golpe, es util para leer archivos de logs
- cat: permite ver todo el conetenido de un archivo en pantalla del shell
- Los comandos head y tail se utilizan para mostrar las primeras o las últimas líneas de un archivo. Son especialmente útiles para inspeccionar archivos grandes y logs.

### head

Comando head

Muestra las primeras líneas de un archivo.

Sintaxis
head archivo.txt

Por defecto muestra las primeras 10 líneas.

Ejemplo
head /etc/passwd

Salida:

root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
...

## Ejercicio 10: Buscar texto

Busca la palabra:

Linux

dentro del archivo.

```bash
cat pendientes.txt | grep Linux
```