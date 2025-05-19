# vmstat - Monitor d'Estat del Sistema Virtual

## Descripció

El comandament `vmstat` (Virtual Memory Statistics) és una eina de monitoratge de rendiment del sistema que proporciona informació sobre la memòria virtual, els processos, els blocs d'E/S, les trampes i l'activitat de la CPU. És especialment útil per obtenir una visió general de l'estat del sistema en temps real.

## Sintaxi

```
vmstat [opcions] [interval [nombre]]
```

## Paràmetres Principals

- **interval**: Temps en segons entre mostres successives.
- **nombre**: Nombre total de mostres a prendre.

## Opcions Comunes

- `-a`: Mostra l'ús de memòria activa/inactiva.
- `-d`: Mostra estadístiques del disc.
- `-f`: Mostra el nombre de forks des de l'inici del sistema.
- `-m`: Mostra estadístiques d'ús de slabinfo.
- `-n`: Mostra només una capçalera una vegada.
- `-s`: Mostra estadístiques de memòria i comptadors varis.
- `-t`: Afegeix una columna de timestamp a cada línia.

## Sortida

La sortida de `vmstat` s'organitza en diferents seccions:

### Processos (procs)

- `r`: Processos executant-se o esperant per executar-se.
- `b`: Processos en estat d'ininterrompibilitat.

### Memòria (memory)

- `swpd`: Memòria virtual utilitzada (KB).
- `free`: Memòria física lliure (KB).
- `buff`: Memòria utilitzada com a buffers (KB).
- `cache`: Memòria utilitzada com a cache (KB).

### Intercanvi (swap)

- `si`: Memòria llegida del disc cap a la memòria (KB/s).
- `so`: Memòria escrita de la memòria cap al disc (KB/s).

### Entrada/Sortida (io)

- `bi`: Blocs rebuts de dispositius de blocs (blocs/s).
- `bo`: Blocs enviats a dispositius de blocs (blocs/s).

### Sistema (system)

- `in`: Interrupcions per segon, incloent-hi el rellotge.
- `cs`: Canvis de context per segon.

### CPU

Percentatges d'ús de la CPU:

- `us`: Temps d'usuari.
- `sy`: Temps de sistema.
- `id`: Temps d'inactivitat.
- `wa`: Temps esperant E/S.
- `st`: Temps robat (en entorns virtualitzats).

## Exemples

### Mostrar informació una sola vegada

```
vmstat
```

### Actualitzar estadístiques cada 2 segons durant 5 mostres

```
vmstat 2 5
```

### Mostrar estadístiques de memòria

```
vmstat -s
```

### Mostrar estadístiques de disc

```
vmstat -d
```

### Mostrar estadístiques amb timestamp

```
vmstat -t 1
```

## Consells d'Ús

- Utilitzeu `vmstat` per diagnosticar problemes de rendiment del sistema.
- L'ús continuat amb un interval permet observar tendències al llarg del temps.
- Un nombre alt a la columna `r` pot indicar una sobrecàrrega de la CPU.
- Valors alts a `si` i `so` indiquen un ús excessiu de swap, que pot degradar el rendiment.
- Un valor alt a `wa` indica possibles colls d'ampolla en E/S.
