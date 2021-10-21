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
```
Tras hacer la copia, se crean dos carpetas para hacer ambos enlaces el blando y el duro.

```
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor$ mkdir prueba1
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor$ mkdir prueba2
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor$ ls
ejercicios-2.md  gtfs   LICENSE        prueba1  README.md
genes            gtfs2  practica-2.md  prueba2
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor$ ln gtfs2/Drosophila_melanogaster.BDGP6.28.102.gtf prueba1
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor$ ln -s  gtfs2/Drosophila_melanogaster.BDGP6.28.102.gtf prueba2
```
Se revisan que ambos enlaces están adecuadamente y tienen las diferencias entre ellas. En prueba1 se encuentra el enlace duro en prueba1 y el enlace blando en prueba2.
```
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor$ ls -li prueba1
total 137488
115736860 -rwxr-xr-x 2 ccalvo ccalvo 140785169 oct 19 19:07 Drosophila_melanogaster.BDGP6.28.102.gtf
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor$ ls -li prueba2
total 0
115736882 lrwxrwxrwx 1 ccalvo ccalvo 45 oct 20 15:22 Drosophila_melanogaster.BDGP6.28.102.gtf -> gtfs2/Drosophila_melanogaster.BDGP6.28.102.gtf
```

1. ¿Qué ocurre cuando se borra el origen y se intenta acceder al destino?

Al destruir el directorio de origen en nuestro caso "gtfs2", vemos que los enlaces siguen en sus directorios propios "prueba1" y "prueba"
Pero vemos que el enlace duro ha cambiado de rwxr-xr-x 2 a rwxr-xr-x 1.


```
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor$ rm -r gtfs2
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor$ ls -li prueba1
total 137488
115736879 -rwxr-xr-x 1 ccalvo ccalvo 140785169 oct 20 15:21 Drosophila_melanogaster.BDGP6.28.102.gtf
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor$ ls -li prueba2
total 0
115736882 lrwxrwxrwx 1 ccalvo ccalvo 46 oct 20 15:32 Drosophila_melanogaster.BDGP6.28.102.gtf -> gtfs2/Drosophila_melanogaster.BDGP6.28.102.gtf
```
Pero al abrirlos con el editor de texto nano vemos diferencias en el caso del enlace duro (prueba1)
El archivo se abre correctamente y se ve el contenido.

```
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor$ cd prueba1
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor/prueba1$ ls
Drosophila_melanogaster.BDGP6.28.102.gtf
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor/prueba1$ nano Drosophila_melanogaster.BDGP6.28.102.gtf
```

![NANO DROSOPHILAMELANOGASTER ENLACE DURO PRUEBA1](https://user-images.githubusercontent.com/92113002/138104995-313ad56b-2b68-4962-be03-fa9f8857b7e3.png)

En cambio, el enlace blando (prueba2) al abrirlo e intentar editarlo aparece en blanco.

```
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor$ cd prueba2
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor/prueba2$ ls
Drosophila_melanogaster.BDGP6.28.102.gtf
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor/prueba2$ nano drosophila_melanogaster.BDGP6.28.102.gtf
```

![NANO DROSOPHILAMELANOGASTER ENLACE BLANDO](https://user-images.githubusercontent.com/92113002/138105155-3695168e-f53f-441b-a461-03ad6919aea9.png)

3. ¿Qué ocurre cuando se borra el destino y se intenta acceder al origen?

Al borrar los dos destinos de ambos enlaces vemos que al abrir el archivo de origen se abre completo.

```
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor$ ls
ejercicios-2.md  gtfs   LICENSE        prueba1  README.md
genes            gtfs2  practica-2.md  prueba2
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor$ rm -r prueba1
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor$ rm -r prueba2
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor$ cd gtfs2
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor/gtfs2$ ls
Drosophila_melanogaster.BDGP6.28.102.gtf  Homo_sapiens.GRCh38.102.gtf.gz
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor/gtfs2$ nano Drosophila_melanogaster.BDGP6.28.102.gtf
```
![nano original gtfs2](https://user-images.githubusercontent.com/92113002/138108677-57c805d4-f957-4846-acf8-029fec56f7c6.png)


4. ¿Qué ocurre con la otra parte cuando se edita el destino o el origen del enlace?
```
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor$ cd gtfs2
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor/gtfs2$ ls
Drosophila_melanogaster.BDGP6.28.102.gtf  Homo_sapiens.GRCh38.102.gtf.gz
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor/gtfs2$ nano Drosophila_melanogaster.BDGP6.28.102.gtf
```

```
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor/gtfs2$ cd ..
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor$ cd prueba1
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor/prueba1$ nano Drosophila_melanogaster.BDGP6.28.102.gtf
```




6. ¿Qué ocurre cuando copiamos un enlace?

### Respuesta ejercicio 1

## Ejercicio 2
Usa la documentación de `find` para encontrar todos los notebook Jupyter con fecha de última modificación 30 de Noviembre de 2020 que haya en tu directorio HOME. Excluye todos aquellos que se encuentren dentro de directorios ocultos (aquellos que comienzan por un punto `.`). 

### Respuesta ejercicio 2


## Ejercicio 3
Descarga, empleando la orden oportuna, todos los ficheros [de esta URL](ftp://ftp.ensembl.org/pub/release-102/gtf/accipiter_nisus/). 
- Inspecciona el fichero CHECKSUMS y genera los checksums adecuados para asegurarte de que los datos son íntegros. 
- Genera un fichero SHA-1 para todos los ficheros .gz descargados y documenta en esta memoria el comando con el que te descargaste los datos, adjuntando aquí los checksums. 


### Respuesta ejercicio 3
