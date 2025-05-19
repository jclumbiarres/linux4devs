# Comando PS

El comando `ps` (Process Status) s'utilitza per veure els processos que s'estan executant al sistema.

## Sintaxi

```bash
ps [opcions]
```

## Descripció

`ps` és una eina de monitoratge de processos que proporciona una instantània dels processos actuals en el sistema. Sense opcions, mostra només els processos que pertanyen a l'usuari actual i que s'han iniciat en la terminal actual.

## Opcions comunes

- `ps`: Mostra els processos de l'usuari actual a la terminal actual.
- `ps -e` o `ps -A`: Mostra tots els processos del sistema.
- `ps -f`: Mostra informació en format complet (més detallat).
- `ps -l`: Format llarg amb més informació.
- `ps aux`: Format molt detallat que mostra tots els processos de tots els usuaris.
- `ps -u usuari`: Mostra els processos d'un usuari específic.
- `ps -p PID`: Mostra informació del procés amb l'identificador PID especificat.

## Columnes de sortida

Quan s'executa `ps`, pot mostrar diverses columnes amb informació:

- `PID`: Identificador del procés.
- `TTY`: Terminal associada al procés.
- `TIME`: Temps de CPU utilitzat pel procés.
- `CMD`: Ordre que va iniciar el procés.

Amb opcions com `aux`, es mostren més columnes:

- `USER`: Usuari propietari del procés.
- `%CPU`: Percentatge d'ús de CPU.
- `%MEM`: Percentatge d'ús de memòria.
- `VSZ`: Mida de la memòria virtual.
- `RSS`: Memòria física utilitzada.
- `STAT`: Estat del procés (R=running, S=sleeping, Z=zombie, etc.).
- `START`: Hora d'inici del procés.

## Exemples

### Mostrar els processos de l'usuari actual

```bash
ps
```

### Mostrar tots els processos del sistema

```bash
ps -e
```

### Mostrar tots els processos amb informació detallada

```bash
ps aux
```

### Mostrar processos ordenats per ús de CPU

```bash
ps aux --sort=-%cpu
```

### Mostrar processos ordenats per ús de memòria

```bash
ps aux --sort=-%mem
```

### Mostrar processos d'un usuari específic

```bash
ps -u username
```

### Mostrar procés amb un PID específic

```bash
ps -p 1234
```

### Mostrar la jerarquia de processos en forma d'arbre

```bash
ps -ejH
# o
ps axjf
```

## Combinació amb altres comandes

És comú combinar `ps` amb `grep` per filtrar processos:

```bash
ps aux | grep firefox
```

També es pot utilitzar amb `less` per veure els resultats paginats:

```bash
ps aux | less
```

## Notes

- A diferència d'altres comandes Unix, `ps` accepta opcions sense el guió inicial (`-`), amb un guió (`-`) o amb dos guions (`--`), depenent del tipus d'estil que s'utilitzi (estil Unix, BSD o GNU).
- El comando `top` ofereix una alternativa a `ps` si necessites veure informació de processos que s'actualitza en temps real.
- Per matar processos identificats amb `ps`, pots utilitzar la comanda `kill` amb el PID corresponent.
