# Comanda `date`

## Definició

La comanda `date` mostra la data i hora actual del sistema. També es pot utilitzar per ajustar la data i hora del sistema o per formatar aquesta informació de manera específica.

## Sintaxi

```bash
date [OPCIONS]... [+FORMAT]
```

## Exemples d'ús

### Mostrar la data i hora actual

```bash
date
```

Això mostrarà alguna cosa com: `Dim Set 10 14:32:45 CEST 2023`

### Mostrar la data amb un format personalitzat

```bash
date +"%d/%m/%Y"
```

Mostrarà la data en format `dia/mes/any`, per exemple: `10/09/2023`

### Mostrar només l'hora actual

```bash
date +"%H:%M:%S"
```

Mostrarà només l'hora actual, per exemple: `14:32:45`

### Mostrar la data i hora en format ISO

```bash
date -I
```

Mostrarà la data en format ISO, per exemple: `2023-09-10`

## Opcions principals

| Opció       | Descripció                                                           |
| ----------- | -------------------------------------------------------------------- |
| `+FORMAT`   | Formata la sortida segons el format especificat                      |
| `-d CADENA` | Mostra la data descrita per CADENA, no la data actual                |
| `-s CADENA` | Estableix la data i hora del sistema amb CADENA                      |
| `-u`        | Mostra o estableix la data en format UTC (Temps Universal Coordinat) |
| `-R`        | Mostra la data en format compatible amb RFC 5322                     |

## Notes

- Per canviar la data i hora del sistema normalment necessitaràs privilegis de superusuari (sudo).
- La comanda `date` és útil en scripts per obtenir marques de temps o per calcular diferències de temps.

## Referències

- Documentació completa: `man date`
- Per més detalls sobre els formats disponibles: `info date`
