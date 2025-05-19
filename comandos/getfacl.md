# getfacl

## Descripció

El comando `getfacl` (get file access control lists) mostra les llistes de control d'accés (ACLs) dels fitxers i directoris. Les ACLs proporcionen un mecanisme més detallat per gestionar els permisos en comparació amb els permisos tradicionals d'Unix (rwx).

## Sintaxi

```
getfacl [opcions] fitxer...
```

## Opcions principals

- `-a, --access`: Mostra només les ACLs d'accés (comportament predeterminat).
- `-d, --default`: Mostra només les ACLs predeterminades.
- `-c, --omit-header`: No mostris els comentaris de capçalera.
- `-e, --all-effective`: Mostra tots els permisos efectius.
- `-R, --recursive`: Opera recursivament en directoris.
- `-n, --numeric`: Mostra IDs numèrics d'usuari/grup en comptes de noms.
- `-p, --absolute-names`: No elimina el prefix "/" dels noms de ruta.

## Exemples

### Mostrar les ACLs d'un fitxer

```bash
getfacl fitxer.txt
```

### Mostrar les ACLs sense mostrar la capçalera

```bash
getfacl -c fitxer.txt
```

### Mostrar només les ACLs predeterminades

```bash
getfacl -d directori
```

### Mostrar ACLs amb IDs numèrics

```bash
getfacl -n fitxer.txt
```

### Mostrar les ACLs recursivament per un directori

```bash
getfacl -R directori
```

## Format de sortida

La sortida típica de `getfacl` té el següent format:

```
# file: nom_del_fitxer
# owner: propietari
# group: grup
user::rwx       # permisos del propietari
user:nom:rwx    # permisos específics per usuaris
group::rwx      # permisos del grup
group:nom:rwx   # permisos específics per grups
mask::rwx       # màscara efectiva de permisos
other::rwx      # permisos per altres usuaris
```

## Notes

- Les ACLs només funcionen en sistemes de fitxers que les suporten (ext2/3/4, XFS, JFS, etc.).
- Per modificar les ACLs, s'utilitza el comando `setfacl`.
- Per utilitzar ACLs en un sistema de fitxers, aquest ha de ser muntat amb l'opció `acl`.
- El comando `getfacl` treballa conjuntament amb `setfacl` per gestionar els permisos avançats.
