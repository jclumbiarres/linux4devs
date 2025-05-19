# Comanda `setfacl`

La comanda `setfacl` (set file access control lists) s'utilitza al sistema operatiu GNU/Linux per a gestionar les Llistes de Control d'Accés (ACL) dels fitxers i directoris. Les ACL proporcionen un control d'accés més detallat que els permisos estàndard d'Unix (usuari, grup, altres).

## Sintaxi bàsica

```
setfacl [opcions] [acció] [especificació-acl] fitxer...
```

## Descripció

Les llistes de control d'accés (ACL) permeten assignar permisos a usuaris i grups específics més enllà del model tradicional de permisos Unix. Això resulta especialment útil quan necessitem gestionar permisos més complexos.

## Opcions principals

| Opció | Descripció                                                           |
| ----- | -------------------------------------------------------------------- |
| `-m`  | Modifica l'ACL existent (afegeix o actualitza entrades)              |
| `-x`  | Elimina entrades de l'ACL                                            |
| `-b`  | Elimina totes les entrades ACL                                       |
| `-R`  | Aplica els canvis recursivament (a tots els subdirectoris i fitxers) |
| `-d`  | Opera sobre les ACL per defecte (només per a directoris)             |

## Format de les ACL

Les especificacions d'ACL tenen aquest format:

- `u:nom_usuari:permisos` - Permís per a un usuari específic
- `g:nom_grup:permisos` - Permís per a un grup específic
- `o::permisos` - Permisos per als altres (equivalents als permisos tradicionals)
- `m::permisos` - Màscara efectiva de permisos

Els `permisos` són combinacions de `r` (llegir), `w` (escriure) i `x` (executar).

## Exemples d'ús

### Donar permisos a un usuari específic

```bash
# Donar permisos de lectura i escriptura a l'usuari "maria" al fitxer "document.txt"
setfacl -m u:maria:rw document.txt
```

### Establir permisos per a diversos usuaris i grups

```bash
# Assignar diferents permisos a diversos usuaris/grups en un sol comando
setfacl -m u:joan:rw,g:projecte:r,u:pau:r-- document.txt
```

### Eliminar permisos ACL d'un usuari

```bash
# Eliminar els permisos ACL de l'usuari "joan"
setfacl -x u:joan document.txt
```

### Aplicar recursivament a tot un directori

```bash
# Donar permisos de lectura al grup "estudiants" a tot el directori "projecte"
setfacl -R -m g:estudiants:r projecte/
```

### Establir ACL per defecte en un directori

```bash
# Els nous fitxers creats al directori heretaran aquests permisos
setfacl -d -m g:projecte:rw projecte/
```

### Eliminar totes les ACL

```bash
# Eliminar completament totes les ACL d'un fitxer
setfacl -b document.txt
```

## Comprovació de les ACL

Pots utilitzar la comanda `getfacl` per a veure les ACL assignades a un fitxer:

```bash
getfacl document.txt
```

## Notes importants

1. Has de tenir els permisos adequats per a modificar les ACL (normalment ser propietari o root).
2. El sistema de fitxers ha de tenir suport per a ACL (la majoria dels sistemes de fitxers moderns com ext4, XFS i Btrfs ho suporten).
3. En alguns sistemes, potser necessitis muntar el sistema de fitxers amb l'opció `acl` (en distribucions modernes, sol estar activat per defecte).
