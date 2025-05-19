# Comanda `find`

La comanda `find` és una eina molt potent que ens permet cercar arxius i directoris en el sistema de fitxers segons diferents criteris com el nom, la mida, la data de modificació, etc.

## Sintaxi bàsica

```bash
find [directori] [opcions] [criteri] [acció]
```

- **directori**: El lloc on començar la cerca. Si no s'especifica, s'utilitza el directori actual (`.`).
- **opcions**: Modificadors de comportament de la cerca.
- **criteri**: Condicions que han de complir els fitxers per ser seleccionats.
- **acció**: Què fer amb els fitxers trobats (per defecte, mostrar-los).

## Exemples bàsics

### Cercar fitxers pel nom

```bash
# Buscar tots els arxius que es diuen "fitxer.txt" a partir del directori actual
find . -name "fitxer.txt"

# Buscar tots els arxius amb extensió .jpg
find . -name "*.jpg"

# Cercar ignorant majúscules/minúscules
find . -iname "Fitxer.txt"
```

### Cercar per tipus de fitxer

```bash
# Buscar només directoris
find . -type d

# Buscar només arxius regulars
find . -type f

# Buscar enllaços simbòlics
find . -type l
```

### Cercar per mida

```bash
# Buscar fitxers més grans que 5MB
find . -size +5M

# Buscar fitxers més petits que 100KB
find . -size -100k

# Buscar fitxers exactament de 1GB
find . -size 1G
```

### Cercar per temps

```bash
# Fitxers modificats en els últims 7 dies
find . -mtime -7

# Fitxers accedits fa més de 30 dies
find . -atime +30
```

## Accions comunes

```bash
# Mostrar detalls de cada fitxer trobat
find . -name "*.txt" -ls

# Eliminar tots els fitxers .tmp
find . -name "*.tmp" -delete

# Executar una comanda per cada fitxer trobat
find . -name "*.jpg" -exec chmod 644 {} \;
```

## Combinacions avançades

Podem combinar criteris amb operadors lògics:

```bash
# Fitxers més grans que 1MB i amb extensió .log
find . -size +1M -and -name "*.log"

# Fitxers .jpg o .png
find . -name "*.jpg" -or -name "*.png"

# Tots els fitxers excepte els .git
find . -not -path "*.git*"
```

## Consells

- Utilitzeu cometes quan feu servir patrons amb comodins per evitar que la shell els interpreti.
- La comanda `find` pot ser lenta en sistemes de fitxers grans; considereu limitar la profunditat amb `-maxdepth`.
- Feu servir `-exec` amb precaució, especialment amb comandes que modifiquen o eliminen fitxers.
