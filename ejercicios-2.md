# Sesión II - Gestión avanzada y descarga de datos
Herramientas computacionales para bioinformática: UNIX, expresiones regulares y shell script

Edita esta plantilla en formato markdown [Guía aquí](https://guides.github.com/features/mastering-markdown/) como se pide en el guión. 
Cuando hayas acabado, haz un commit de tus cambios y súbelos al repositorio antes de la fecha de entrega señalada. 
Puedes usar el cliente 

======================================
Antes de comenzar, crea


## Ejercicio 1
Crea una copia de la carpeta gtfs. Luego crea enlaces duros y blandos a los ficheros .gtf y responde:

```
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor$ cp -r gtfs gtfs2
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor$ ls
ejercicios-2.md  genes  gtfs  gtfs2  LICENSE  practica-2.md  README.md
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor$ mkdir prueba1
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor$ mkdir prueba2
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor$ ls
ejercicios-2.md  gtfs   LICENSE        prueba1  README.md
genes            gtfs2  practica-2.md  prueba2
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor$ ln gtfs/Drosophila_melanogaster.BDGP6.28.102.gtf prueba1
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor$ ln -s  gtfs/Drosophila_melanogaster.BDGP6.28.102.gtf prueba2
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor$ ls -li prueba1
total 137488
115736860 -rwxr-xr-x 2 ccalvo ccalvo 140785169 oct 19 19:07 Drosophila_melanogaster.BDGP6.28.102.gtf
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor$ ls -li prueba2
total 0
115736882 lrwxrwxrwx 1 ccalvo ccalvo 45 oct 20 15:22 Drosophila_melanogaster.BDGP6.28.102.gtf -> gtfs/Drosophila_melanogaster.BDGP6.28.102.gtf
```

1. ¿Qué ocurre cuando se borra el origen y se intenta acceder al destino?
2. ¿Qué ocurre cuando se borra el destino y se intenta acceder al origen?
3. ¿Qué ocurre con la otra parte cuando se edita el destino o el origen del enlace?
4. ¿Qué ocurre cuando copiamos un enlace?

### Respuesta ejercicio 1

## Ejercicio 2
Usa la documentación de `find` para encontrar todos los notebook Jupyter con fecha de última modificación 30 de Noviembre de 2020 que haya en tu directorio HOME. Excluye todos aquellos que se encuentren dentro de directorios ocultos (aquellos que comienzan por un punto `.`). 

### Respuesta ejercicio 2


## Ejercicio 3
Descarga, empleando la orden oportuna, todos los ficheros [de esta URL](ftp://ftp.ensembl.org/pub/release-102/gtf/accipiter_nisus/). 
- Inspecciona el fichero CHECKSUMS y genera los checksums adecuados para asegurarte de que los datos son íntegros. 
- Genera un fichero SHA-1 para todos los ficheros .gz descargados y documenta en esta memoria el comando con el que te descargaste los datos, adjuntando aquí los checksums. 


### Respuesta ejercicio 3
