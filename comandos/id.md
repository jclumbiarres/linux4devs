# Comanda `id`

## Descripció

La comanda `id` mostra la identitat de l'usuari actual o d'un usuari específic, incloent l'identificador d'usuari (UID), l'identificador de grup principal (GID), i els grups secundaris als quals pertany.

## Sintaxi

```
id [OPCIONS]... [USUARI]
```

## Opcions principals

- `-u, --user`: Mostra només l'ID d'usuari (UID)
- `-g, --group`: Mostra només l'ID del grup principal (GID)
- `-G, --groups`: Mostra tots els IDs dels grups als quals pertany l'usuari
- `-n, --name`: Mostra el nom en lloc del número (amb -u, -g o -G)
- `-r, --real`: Mostra l'ID real en lloc de l'efectiu
- `-Z, --context`: Mostra el context de seguretat SELinux (si està disponible)

## Exemples

### Mostrar tota la informació de l'usuari actual

```bash
id
```

Resultat:

```
uid=1000(joan) gid=1000(joan) grups=1000(joan),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev)
```

### Mostrar només l'UID de l'usuari actual

```bash
id -u
```

Resultat:

```
1000
```

### Mostrar el nom d'usuari en lloc del número

```bash
id -un
```

Resultat:

```
joan
```

### Mostrar informació d'un altre usuari

```bash
id maria
```

Resultat:

```
uid=1001(maria) gid=1001(maria) grups=1001(maria),29(audio)
```

### Mostrar tots els grups d'un usuari

```bash
id -Gn joan
```

Resultat:

```
joan adm cdrom sudo dip plugdev
```

## Usos pràctics

- Verificar la identitat amb què s'executa un script o programa
- Comprovar els permisos i grups d'un usuari específic
- Diagnosticar problemes de permisos relacionats amb grups
- Script d'automatització que necessiten conèixer l'usuari que els executa

## Notes importants

- Cada usuari té un UID únic al sistema
- El superusuari (root) sempre té l'UID 0
- Els UIDs per sota de 1000 generalment estan reservats per a comptes de sistema
- Els UIDs d'usuaris regulars normalment comencen a partir de 1000
