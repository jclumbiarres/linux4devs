**ls** (list)

Aquesta comanda mostra una llista dels arxius i directoris dins del directori actual. Si voleu veure més detalls, podeu utilitzar:

* - ls -l, que mostra informació addicional com permisos, propietaris i dates de modificació.​
* - ls –a, Mostra tots els arxius, incloent-hi els arxius ocults (que comencen amb un punt ., com .bashrc o .gitignore).​
```
[jcarlos@Pazuzu ~]$ ls
Descargas   Escritorio  Música      Público
Documentos  Imágenes    Plantillas  Vídeos
[jcarlos@Pazuzu ~]$ ls -l
total 0
drwxr-xr-x 2 jcarlos jcarlos 6 abr  2 15:49 Descargas
drwxr-xr-x 2 jcarlos jcarlos 6 abr  2 15:49 Documentos
drwxr-xr-x 2 jcarlos jcarlos 6 abr  2 15:49 Escritorio
drwxr-xr-x 2 jcarlos jcarlos 6 abr  2 15:49 Imágenes
drwxr-xr-x 2 jcarlos jcarlos 6 abr  2 15:49 Música
drwxr-xr-x 2 jcarlos jcarlos 6 abr  2 15:49 Plantillas
drwxr-xr-x 2 jcarlos jcarlos 6 abr  2 15:49 Público
drwxr-xr-x 2 jcarlos jcarlos 6 abr  2 15:49 Vídeos
[jcarlos@Pazuzu ~]$
```

Algunes opcions útils:

* -l Mostra una llista detallada amb permisos, propietari, mida, etc.​
* -a Mostra tots els fitxers, incloent-hi els fitxers ocults (els que comencen amb un punt).​
* -h Mida de fitxers en format llegible per l'usuari (GB, MB, KB).​