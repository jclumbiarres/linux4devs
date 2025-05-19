# Comanda `free` - Mostra l'estat de la memòria del sistema

La comanda `free` és una eina del sistema GNU/Linux que mostra la quantitat de memòria lliure i utilitzada en el sistema. Això inclou tant la memòria RAM física com l'espai de intercanvi (swap).

## Sintaxi

```
free [opcions]
```

## Descripció

`free` proporciona informació sobre la memòria del sistema, incloent la memòria total, utilitzada, lliure, compartida, en cache i disponible. També mostra informació sobre l'espai de intercanvi (swap).

Per defecte, les quantitats es mostren en kilobytes, però això pot canviar-se amb les opcions.

## Opcions principals

- `-b, --bytes`: Mostra la memòria en bytes.
- `-k, --kilo`: Mostra la memòria en kilobytes (predeterminat).
- `-m, --mega`: Mostra la memòria en megabytes.
- `-g, --giga`: Mostra la memòria en gigabytes.
- `-h, --human`: Mostra la informació en format llegible per humans, amb unitats automàtiques.
- `-s N, --seconds=N`: Actualitza contínuament la informació cada N segons.
- `-t, --total`: Afegeix una línia amb els totals.
- `--si`: Utilitza potències de 1000 en lloc de 1024 per a les unitats.

## Sortida explicada

```
              total        used        free      shared  buff/cache   available
Mem:        16303788     9727168     1608172      436056     4968448     5743744
Swap:        4194304      111616     4082688
```

- `total`: Quantitat total de memòria física o swap.
- `used`: Memòria en ús actualment.
- `free`: Memòria que no està sent utilitzada.
- `shared`: Memòria compartida per múltiples processos.
- `buff/cache`: Memòria utilitzada per buffers i cache del sistema.
- `available`: Estimació de quanta memòria està disponible per iniciar noves aplicacions sense utilitzar swap.

## Exemples d'ús

### Mostrar la informació de memòria bàsica

```bash
free
```

### Mostrar la informació en megabytes

```bash
free -m
```

### Mostrar la informació en format llegible per humans

```bash
free -h
```

### Actualitzar la informació cada 5 segons

```bash
free -s 5
```

### Mostrar la informació amb una línia de totals

```bash
free -t
```

## Notes

- La memòria `buff/cache` pot ser alliberada pel sistema quan sigui necessària, de manera que és important tenir-la en compte quan s'avalua l'ús real de memòria.
- La columna `available` (disponible) és una estimació més precisa de la memòria realment disponible que la columna `free`, ja que té en compte la memòria que pot ser alliberada de la cache.

## Consell pràctic

Si el teu sistema sembla lent, comprova la quantitat de memòria disponible. Si la memòria disponible és molt baixa i l'ús de swap és alt, podries necessitar més RAM o tancar algunes aplicacions per millorar el rendiment.
