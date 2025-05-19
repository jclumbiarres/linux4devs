# Comanda `sort`

## Descripció

La comanda `sort` s'utilitza per ordenar línies de text de fitxers o de l'entrada estàndard. Pot ordenar alfabèticament o numèricament, en ordre ascendent o descendent, i amb moltes altres opcions de personalització.

## Sintaxi

```bash
sort [OPCIONS]... [FITXER]...
```

Si no s'especifica cap fitxer o es proporciona '-', `sort` llegeix des de l'entrada estàndard.

## Opcions principals

- `-b, --ignore-leading-blanks`: Ignora els espais en blanc al principi de les línies
- `-f, --ignore-case`: Ignora les majúscules i minúscules
- `-n, --numeric-sort`: Compara segons el valor numèric
- `-r, --reverse`: Inverteix el resultat de les comparacions (ordre descendent)
- `-k, --key=POS1[,POS2]`: Comença l'ordenació en POS1 i finalitza en POS2 (camps)
- `-t, --field-separator=SEP`: Utilitza SEP com a separador de camps (per defecte és espai en blanc)
- `-u, --unique`: Elimina línies duplicades després d'ordenar

## Exemples

### Ordenació bàsica

Ordenar un fitxer alfabèticament:

```bash
sort fitxer.txt
```

### Ordenació numèrica

Ordenar números en ordre numèric (no alfabètic):

```bash
sort -n numeros.txt
```

### Ordenació inversa

Ordenar en ordre descendent:

```bash
sort -r fitxer.txt
```

### Ignorar majúscules i minúscules

```bash
sort -f fitxer.txt
```

### Eliminar duplicats

Ordenar i mostrar només línies úniques:

```bash
sort -u fitxer.txt
```

### Ordenar per una columna específica

Ordenar un fitxer CSV utilitzant la segona columna com a clau d'ordenació:

```bash
sort -t',' -k2,2 fitxer.csv
```

### Ordenació múltiple

Ordenar primer per la segona columna i després per la tercera:

```bash
sort -t',' -k2,2 -k3,3 fitxer.csv
```

### Ordenació numèrica en la tercera columna

```bash
sort -t',' -k3,3n fitxer.csv
```

## Casos d'ús

- Ordenar llistes de noms, números, dates o altres dades
- Preparar dades abans de processar-les amb altres comandes
- Eliminar entrades duplicades
- Ordenar resultats d'altres comandes (utilitzant pipes)

## Consells

- Combina `sort` amb altres comandes mitjançant pipes (`|`) per a fluxos de treball més potents
- Per verificar si un arxiu ja està ordenat, utilitza l'opció `-c`
- La comanda `sort` carrega tot el fitxer a la memòria, així que tingues cura amb fitxers molt grans
