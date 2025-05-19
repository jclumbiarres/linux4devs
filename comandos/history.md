# Comanda `history`

## Descripció

La comanda `history` en Linux mostra una llista de les comandes que has escrit anteriorment en el terminal. És molt útil per recordar comandes que has fet servir abans i que potser vols repetir.

## Sintaxi

```bash
history [opcions]
```

## Opcions principals

- `-c`: Esborra tota la llista d'historial
- `-d núm`: Elimina l'entrada específica número "núm" de l'historial
- `-a`: Afegeix les noves comandes al fitxer d'historial
- `-r`: Llegeix el contingut del fitxer d'historial

## Exemples

Mostrar tot l'historial de comandes:

```bash
history
```

Mostrar les últimes 10 comandes:

```bash
history 10
```

Esborrar tot l'historial:

```bash
history -c
```

Eliminar una entrada específica (per exemple, la número 43):

```bash
history -d 43
```

## Consells pràctics

- Pots executar una comanda de l'historial escrivint `!número`, on "número" és el número de l'entrada a l'historial.
- Pots executar l'última comanda que comença amb una lletra específica escribint `!lletra`. Per exemple, `!l` executarà l'última comanda que comença amb "l".
- Pots utilitzar `!!` per repetir l'última comanda.

## Fitxer d'historial

L'historial es guarda normalment al fitxer `~/.bash_history` (o similar depenent del teu shell).
