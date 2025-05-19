
**rmdir** (remove directory)

​

rmdir: Elimina un directori buit. Si el directori conté fitxers o altres directoris, s'haurà d'utilitzar 
rm -r.​

rmdir projectes

```
jcarlos@DESKTOP-H7KTRRF:~$ mkdir projectes
jcarlos@DESKTOP-H7KTRRF:~$ ls |  grep projectes
projectes
jcarlos@DESKTOP-H7KTRRF:~$ rmdir projectes
jcarlos@DESKTOP-H7KTRRF:~$ ls |  grep projectes
jcarlos@DESKTOP-H7KTRRF:~$
```