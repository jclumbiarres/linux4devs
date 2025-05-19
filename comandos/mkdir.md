**mkdir** (make directory)

Ús bàsic:​

mkdir nomDirectori​

```
jcarlos@DESKTOP-H7KTRRF:~$ mkdir nombreDirectorio
jcarlos@DESKTOP-H7KTRRF:~$ ls
backup.sh                      bashscripts  joebananas        proyectos
backup_20250404_190839.tar.gz  docker       nombreDirectorio
jcarlos@DESKTOP-H7KTRRF:~$
```

L'opció -p (crear estructura de directoris)​
Serveix per:​
- Crear directoris niats (una carpeta dins d'una altra).​
- No dona error si algun directori ja existeix.​

​Les claus { } et permeten crear diverses carpetes amb una sola comanda.​
Pots combinar –p i {} per estructures complexes​

```
jcarlos@DESKTOP-H7KTRRF:~$ mkdir -p nombreDirectorio/{servicios,servidores,etc}
jcarlos@DESKTOP-H7KTRRF:~$ tree nombreDirectorio/
nombreDirectorio/
├── etc
├── servicios
└── servidores

3 directories, 0 files
```

Errors comuns i consells ​
Si la carpeta ja existeix:​

* Sense -p: et mostrarà un error.​  
* Amb -p: ignora l'error.