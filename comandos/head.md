# Comanda `head`

## Descripció

La comanda `head` s'utilitza per mostrar les primeres línies d'un fitxer de text. Per defecte, mostra les primeres 10 línies, però aquest número es pot canviar amb opcions específiques.

## Sintaxi bàsica

```bash
head [OPCIONS]... [FITXER]...
```

## Opcions principals

- `-n NUM` o `--lines=NUM`: Mostra les primeres NUM línies en lloc de les 10 per defecte
- `-c NUM` o `--bytes=NUM`: Mostra els primers NUM bytes
- `-q` o `--quiet`: No mostra els capçals amb els noms dels fitxers
- `-v` o `--verbose`: Sempre mostra els capçals amb els noms dels fitxers

## Exemples

### Mostrar les primeres 10 línies d'un fitxer

```bash
head head.md
```

### Mostrar només les primeres 5 línies

```bash
head -n 5 head.md
```

### Mostrar els primers 100 bytes

```bash
head -c 100 head.md
```

### Mostrar les primeres línies de múltiples fitxers

```bash
head -n 3 head.md comandos/ls.md
```

## Casos d'ús

- Visualitzar ràpidament l'inici d'un fitxer sense haver d'obrir-lo completament
- Veure les capçaleres de fitxers de registre (logs)
- Examinar les primeres línies d'un conjunt de dades
- Comprovar el format o l'estructura d'un fitxer

## Combinacions amb altres comandes

`head` es pot combinar amb altres comandes utilitzant el pipe (`|`):

```bash
# Mostrar les primeres 5 línies del resultat de ls ordenat
ls -la | sort | head -n 5

# Mostrar les primeres línies d'un fitxer comprimit sense descomprimir-lo
zcat fitxer.gz | head
```

## Diferència amb `tail`

Mentre que `head` mostra el principi d'un fitxer, la comanda `tail` mostra les últimes línies. Són comandes complementàries.
