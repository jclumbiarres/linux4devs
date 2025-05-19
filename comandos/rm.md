**rm** (remove)

Elimina fitxers o directoris. Per eliminar un directori i el seu contingut de manera recursiva, utilitzem rm -r.​

```
jcarlos@DESKTOP-H7KTRRF:~$ rm nombreDirectorio/
rm: cannot remove 'nombreDirectorio/': Is a directory
jcarlos@DESKTOP-H7KTRRF:~$ rm -r nombreDirectorio/
jcarlos@DESKTOP-H7KTRRF:~$
```

Algunes opcions útils:​
    -r: Elimina directoris i el seu contingut de manera recursiva.​
    -f: Força l'eliminació sense demanar confirmació.​
    -i: Demana confirmació abans d'eliminar.​