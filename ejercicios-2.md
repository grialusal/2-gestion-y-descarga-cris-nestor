# Sesión II - Gestión avanzada y descarga de datos
Herramientas computacionales para bioinformática: UNIX, expresiones regulares y shell script

Edita esta plantilla en formato markdown [Guía aquí](https://guides.github.com/features/mastering-markdown/) como se pide en el guión. 
Cuando hayas acabado, haz un commit de tus cambios y súbelos al repositorio antes de la fecha de entrega señalada. 
Puedes usar el cliente 

======================================
Antes de comenzar, crea


## Ejercicio 1
Crea una copia de la carpeta gtfs. Luego crea enlaces duros y blandos a los ficheros .gtf y responde:
### Respuesta ejercicio 1
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
Se revisan que ambos enlaces están adecuadamente y tienen las diferencias entre ellas. En prueba1 se encuentra el enlace duro y el enlace blando en prueba2.
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

Si editamos el el archivo de origen dando tres espacios en las primeras líneas.
```
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor$ cd gtfs2
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor/gtfs2$ ls
Drosophila_melanogaster.BDGP6.28.102.gtf  Homo_sapiens.GRCh38.102.gtf.gz
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor/gtfs2$ nano Drosophila_melanogaster.BDGP6.28.102.gtf
```
![nano ejer4](https://user-images.githubusercontent.com/92113002/138236618-b4304b6a-733d-4f7c-be93-e0265f6cbfc1.png)

Vemos que se mantiene en el enlace duro dicho cambio.
```
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor/gtfs2$ cd ..
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor$ cd prueba1
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor/prueba1$ nano Drosophila_melanogaster.BDGP6.28.102.gtf
```
![nanoprueba1ejer4](https://user-images.githubusercontent.com/92113002/138236631-06587d3b-46b2-4ea0-b193-02ed0b17e27c.png)

Si revertimos el cambio, es decir, quitamos desde el enlace duro los tres espacios otra vez editando.
```
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor/gtfs2$ cd ..
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor$ cd prueba1
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor/prueba1$ nano Drosophila_melanogaster.BDGP6.28.102.gtf
```
![ejerc4nano1](https://user-images.githubusercontent.com/92113002/138237602-8b07ca76-a874-4ae8-9151-7bc29986e321.png)


Vemos que en el archivo de origen también se han cambiado y los cambios se han mantenido.

```
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor$ cd gtfs2
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor/gtfs2$ ls
Drosophila_melanogaster.BDGP6.28.102.gtf  Homo_sapiens.GRCh38.102.gtf.gz
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor/gtfs2$ nano Drosophila_melanogaster.BDGP6.28.102.gtf
```
![nano2origenejer4](https://user-images.githubusercontent.com/92113002/138237638-38f7e5a0-bf07-4fd1-8dea-881e46721c89.png)

Con respecto al enlace blando:
Repito todo borrando y creando los directorios desde el princpio y establaciendo el enlace blando:
```
nguerrero@cpg3:~$ cp -r gtfs gtfs-2
nguerrero@cpg3:~$ mkdir prueba-2
nguerrero@cpg3:~$ ls gtfs-2
Drosophila_melanogaster.BDGP6.28.102.gtf  Homo_sapiens.GRCh38.102.gtf.gz
nguerrero@cpg3:~$ ln -s gtfs-2/Drosophila_melanogaster.BDGP6.28.102.gtf prueba-2
nguerrero@cpg3:~$ ls -li prueba-2
total 0
223740102 lrwxrwxrwx 1 nguerrero nguerrero 47 Oct 29 02:20 Drosophila_melanogaster.BDGP6.28.102.gtf -> gtfs-2/Drosophila_melanogaster.BDGP6.28.102.gtf
```
Uso nano para colocar 'hola' al final de la primera línea del archivo
```
  GNU nano 5.4    gtfs-2/Drosophila_melanogaster.BDGP6.28.102.gtf *            
#!genome-build BDGP6.28 hola
#!genome-version BDGP6.28
#!genome-build-accession GCA_000001215.4
```

Tras la edicion el enlace blando esta en blanco
```
GNU nano 5.4   prueba-2/Drosophila_melanogaster.BDGP6.28.102.gtf   

```

Para intentar comprender como funciona se borra el enlace blando y se vuelve a crearlo y el documento sigue en blanco, lo que me sorprende: 
```
nguerrero@cpg3:~$ rm prueba-2/Drosophila_melanogaster.BDGP6.28.102.gtf
nguerrero@cpg3:~$ ls -li prueba-2
total 0
nguerrero@cpg3:~$ ln -s gtfs-2/Drosophila_melanogaster.BDGP6.28.102.gtf prueba-2
nguerrero@cpg3:~$ ls -li prueba-2
total 0
223740102 lrwxrwxrwx 1 nguerrero nguerrero 47 Oct 29 02:28 Drosophila_melanogaster.BDGP6.28.102.gtf -> gtfs-2/Drosophila_melanogaster.BDGP6.28.102.gtf
nguerrero@cpg3:~$ nano prueba-2/Drosophila_melanogaster.BDGP6.28.102.gtf 
GNU nano 5.4   prueba-2/Drosophila_melanogaster.BDGP6.28.102.gtf
```
5. ¿Qué ocurre cuando copiamos un enlace?

Cuando copiamos el enlace duro vemos que se copia cambiando el número final del inodo y "rwxr-xr-x 2" cambia por un "rwxr-xr-x 1", pero este nuevo enlace se puede abrir y editar con normalidad como el original que hemos copiado.

```
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor/prueba1$ cp Drosophila_melanogaster.BDGP6.28.102.gtf enlacecopia
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor/prueba1$ ls
Drosophila_melanogaster.BDGP6.28.102.gtf  enlacecopia
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor/prueba1$ ls -li
total 274976
115736883 -rwxr-xr-x 2 ccalvo ccalvo 140785169 oct 21 10:06 Drosophila_melanogaster.BDGP6.28.102.gtf
115736882 -rwxr-xr-x 1 ccalvo ccalvo 140785169 oct 21 10:12 enlacecopia
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor/prueba1$ nano enlacecopia
```
Al intentar copiar con el comando "cp" el enlace blando no nos permite.

```
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor/prueba2$ ls Drosophila_melanogaster.BDGP6.28.102.gtf
Drosophila_melanogaster.BDGP6.28.102.gtf
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor/prueba2$ nano Drosophila_melanogaster.BDGP6.28.102.gtf
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor/prueba2$ cp Drosophila_melanogaster.BDGP6.28.102.gtf enlace2
cp: no se puede efectuar `stat' sobre 'Drosophila_melanogaster.BDGP6.28.102.gtf': No existe el fichero o el directorio
```

Consultamos las opciones del comando de copia "cp" con --help
```
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor/prueba2$ cp --help
```

Encontramos la opción -P que podría cuadrar para la copia de enlaces.

```
  -P, --no-dereference         nunca sigue los enlaces simbólicos en ORIGEN
  -p                            igual que --preserve=mode,ownership,timestamps
      --preserve[=LISTA_ATTR]   conserva si puede los atributos especificados,
                                  (por omisión: mode,ownership,timestamps)
                                  atributos adicionales: context, links, xattr,
                                  all
```
Realizamos la copia y vemos que cambia el inodo pero no cambian los permisos del enlace. También se puede ver que el origen es el mismo.
```
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor/prueba2$ cp -P  Drosophila_melanogaster.BDGP6.28.102.gtf enlace2
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor/prueba2$ ls
Drosophila_melanogaster.BDGP6.28.102.gtf  enlace2
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor/prueba2$ nano enlace2
ccalvo@cpg3:~/2-gestion-y-descarga-cris-nestor/prueba2$ ls -li
total 0
115736881 lrwxrwxrwx 1 ccalvo ccalvo 46 oct 21 09:50 Drosophila_melanogaster.BDGP6.28.102.gtf -> gtfs2/Drosophila_melanogaster.BDGP6.28.102.gtf
115736884 lrwxrwxrwx 1 ccalvo ccalvo 46 oct 21 10:19 enlace2 -> gtfs2/Drosophila_melanogaster.BDGP6.28.102.gtf
```



## Ejercicio 2
Usa la documentación de `find` para encontrar todos los notebook Jupyter con fecha de última modificación 30 de Noviembre de 2020 que haya en tu directorio HOME. Excluye todos aquellos que se encuentren dentro de directorios ocultos (aquellos que comienzan por un punto `.`). 



### Respuesta ejercicio 2

Se usa el flag -newermt para indicar una fecha específica
```
nguerrero@cpg3:~$ find /home/alejandro -name *.ipynb -newermt 11/17/2020
/home/alejandro/P1-matriz-old.ipynb
/home/alejandro/un_cuaderno.ipynb
/home/alejandro/P6-enriquecimiento.ipynb
/home/alejandro/P3-expresion.ipynb
/home/alejandro/P4-expresionDiferencial.ipynb
/home/alejandro/P1-matriz.ipynb
/home/alejandro/P8-edgeR.ipynb
/home/alejandro/P5-coexpresion.ipynb
```
Me devuelva esa lista, pero cuando examino la carpeta veo que sólo un archivo tiene la fecha de modificación 11/17/2020, por lo que creo que cometí un fallo:
```
nguerrero@cpg3:~$ ls -l /home/alejandro
total 2424
-rwxrwxrwx 1 root      root      116305 Jun 14 10:43 P1-matriz-old.ipynb
-rwxrwxrwx 1 root      root       16282 Jun 14 10:43 P1-matriz.ipynb
-rwxrwxrwx 1 root      root      468472 Jun 14 10:43 P3-expresion.ipynb
-rwxrwxrwx 1 root      root      852404 Jun 14 10:43 P4-expresionDiferencial.ipynb
-rwxrwxrwx 1 root      root      445767 Jun 14 10:43 P5-coexpresion.ipynb
-rwxrwxrwx 1 root      root      141667 Jun 14 10:43 P6-enriquecimiento.ipynb
-rwxrwxrwx 1 root      root      417108 Jun 14 10:43 P8-edgeR.ipynb
drwxrwxrwx 3 alejandro alejandro   4096 Oct  9  2020 ps1
-rwxrwxrwx 1 alejandro alejandro   5245 Nov 17  2020 un_cuaderno.ipynb
```
## Ejercicio 3
Descarga, empleando la orden oportuna, todos los ficheros [de esta URL](ftp://ftp.ensembl.org/pub/release-102/gtf/accipiter_nisus/). 
- Inspecciona el fichero CHECKSUMS y genera los checksums adecuados para asegurarte de que los datos son íntegros. 
- Genera un fichero SHA-1 para todos los ficheros .gz descargados y documenta en esta memoria el comando con el que te descargaste los datos, adjuntando aquí los checksums. 


### Respuesta ejercicio 3

```
ccalvo@cpg3:~$ wget -r ftp://ftp.ensembl.org/pub/release-102/gtf/accipiter_nisus/
ACABADO --2021-10-26 14:59:44--
Tiempo total de reloj: 20s
Descargados: 4 ficheros, 12M en 18s (692 KB/s)
```

Tras la descarga entramos en las diferentes carpetas de los ficheros para buscar el archivo CHECKSUMS

```
ccalvo@cpg3:~$ ls
1-toma-de-contacto-cris-nestor    ftp.ensembl.org
2-gestion-y-descarga-cris-nestor
ccalvo@cpg3:~$ cd ftp.ensembl.org
ccalvo@cpg3:~/ftp.ensembl.org$ ls
pub
ccalvo@cpg3:~/ftp.ensembl.org$ cd pub
ccalvo@cpg3:~/ftp.ensembl.org/pub$ ls
release-102
ccalvo@cpg3:~/ftp.ensembl.org/pub$ cd release-102
ccalvo@cpg3:~/ftp.ensembl.org/pub/release-102$ ls
gtf
ccalvo@cpg3:~/ftp.ensembl.org/pub/release-102$ cd gtf
ccalvo@cpg3:~/ftp.ensembl.org/pub/release-102/gtf$ ls
accipiter_nisus
ccalvo@cpg3:~/ftp.ensembl.org/pub/release-102/gtf$ cd accipiter_nisus
ccalvo@cpg3:~/ftp.ensembl.org/pub/release-102/gtf/accipiter_nisus$ ls
Accipiter_nisus.Accipiter_nisus_ver1.0.102.abinitio.gtf.gz  CHECKSUMS
Accipiter_nisus.Accipiter_nisus_ver1.0.102.gtf.gz           README
```

Se inspecciona el fichero y se generan los checksums:

```
ccalvo@cpg3:~/ftp.ensembl.org/pub/release-102/gtf/accipiter_nisus$ shasum Accipiter_nisus.Accipiter_nisus_ver1.0.102.abinitio.gtf.gz
94408e910dd56ef4811dc6b3ee67a6c270f2c544  Accipiter_nisus.Accipiter_nisus_ver1.0.102.abinitio.gtf.gz
ccalvo@cpg3:~/ftp.ensembl.org/pub/release-102/gtf/accipiter_nisus$ md5sum Accipiter_nisus.Accipiter_nisus_ver1.0.102.abinitio.gtf.gz
de00af2a8684985e8fb74fa94454bd15  Accipiter_nisus.Accipiter_nisus_ver1.0.102.abinitio.gtf.gz
ccalvo@cpg3:~/ftp.ensembl.org/pub/release-102/gtf/accipiter_nisus$ sum Accipiter_nisus.Accipiter_nisus_ver1.0.102.abinitio.gtf.gz
28446  3388
```

Se genera el archivo .sha

```
ccalvo@cpg3:~/ftp.ensembl.org/pub/release-102/gtf/accipiter_nisus$ shasum Accipiter_nisus.Accipiter_nisus_ver1.0.102.abinitio.gtf.gz > Accipeter_checksum.sha
ccalvo@cpg3:~/ftp.ensembl.org/pub/release-102/gtf/accipiter_nisus$ cat Accipeter_checksum.sha
94408e910dd56ef4811dc6b3ee67a6c270f2c544  Accipiter_nisus.Accipiter_nisus_ver1.0.102.abinitio.gtf.gz
ccalvo@cpg3:~/ftp.ensembl.org/pub/release-102/gtf/accipiter_nisus$ shasum -c Accipeter_checksum.sha
Accipiter_nisus.Accipiter_nisus_ver1.0.102.abinitio.gtf.gz: OK
ccalvo@cpg3:~/ftp.ensembl.org/pub/release-102/gtf/accipiter_nisus$ nano Accipeter_checksum.sha
ccalvo@cpg3:~/ftp.ensembl.org/pub/release-102/gtf/accipiter_nisus$
ccalvo@cpg3:~/ftp.ensembl.org/pub/release-102/gtf/accipiter_nisus$ shasum Accipiter_nisus.Accipiter_nisus_ver1.0.102.gtf.gz > Accipeter2_checksum.sha
ccalvo@cpg3:~/ftp.ensembl.org/pub/release-102/gtf/accipiter_nisus$ cat Accipeter2_checksum.sha
8a4fb7b736de257798de4b7cc963124555babade  Accipiter_nisus.Accipiter_nisus_ver1.0.102.gtf.gz
ccalvo@cpg3:~/ftp.ensembl.org/pub/release-102/gtf/accipiter_nisus$ shasum -c Accipeter2_checksum.sha
Accipiter_nisus.Accipiter_nisus_ver1.0.102.gtf.gz: OK
```

Checksums:

94408e910dd56ef4811dc6b3ee67a6c270f2c544  Accipiter_nisus.Accipiter_nisus_ver1.0.102.abinitio.gtf.gz
8a4fb7b736de257798de4b7cc963124555babade  Accipiter_nisus.Accipiter_nisus_ver1.0.102.gtf.gz

**Correciones**

En el ejercicio 1, apartado 4, cuando se edita el archivo de origen de un enlace blando y se intenta abrir el enlace se observa que la modificación se mantiene. En el apartado 5, al copiar un enlace blando lo que ocurre es que se copia el arhivo original.

En el ejercicio 2 faltó incluir en el comando `-not -newermt '11/18/2020'` que indicaba solo buscar los archivos modificados el 17/11/2020.

En el ejercicio 3 faltaron las órdenes `--no-directories  --no-parent` .

**Calificación**
Ej 1: 2
Ej 2: 3
Ej 3: 3,33
Nota final: **8,33**
