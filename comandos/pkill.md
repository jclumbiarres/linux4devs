# Comanda `pkill`

## Descripció

La comanda `pkill` permet cercar i enviar senyals a processos en execució basant-se en el seu nom o altres atributs, en comptes d'utilitzar l'identificador del procés (PID).

## Sintaxi

```
pkill [opcions] patró
```

## Opcions principals

- `-f`: Compara el patró amb la línia completa d'ordres del procés.
- `-i`: Ignora la distinció entre majúscules i minúscules.
- `-n`: Actua només sobre el procés més recent que compleix el criteri.
- `-o`: Actua només sobre el procés més antic que compleix el criteri.
- `-P ppid`: Actua sobre els processos fills del procés amb ID ppid.
- `-s sid`: Actua sobre processos que pertanyen a la sessió sid.
- `-t term`: Actua sobre processos associats a la terminal term.
- `-u euid`: Actua sobre processos propietat de l'usuari euid.
- `-g group`: Actua sobre processos propietat del grup group.
- `-signal`: Especifica el senyal a enviar (per defecte és SIGTERM (15)).

## Exemples

### Finalitzar un procés pel seu nom

```bash
pkill firefox
```

Això enviarà el senyal SIGTERM a tots els processos amb nom "firefox".

### Finalitzar un procés utilitzant la línia de comandes completa

```bash
pkill -f "python script.py"
```

Això finalitzarà qualsevol procés que contingui "python script.py" a la seva línia de comandes.

### Enviar un senyal específic

```bash
pkill -9 chrome
```

Enviament del senyal SIGKILL (9) a tots els processos "chrome", forçant la seva finalització immediata.

### Finalitzar processos d'un usuari específic

```bash
pkill -u usuari
```

Finalitzarà tots els processos propietat de l'usuari especificat.

## Particularitats

- És similar a `kill`, però permet seleccionar processos pel nom en lloc del PID.
- La comanda és útil quan no es coneix el PID exacte d'un procés.
- És una eina molt potent que permet acabar amb múltiples processos amb una sola ordre.
- Cal anar amb compte quan s'utilitza en entorns de producció, ja que pot finalitzar processos crítics si no s'especifica bé el patró.
