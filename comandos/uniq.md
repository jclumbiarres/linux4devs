# Comando `uniq`

## Descripció

El comando `uniq` serveix per filtrar línies duplicades consecutives en un arxiu de text o en la sortida d'altres comandes. El seu nom ve de "unique" (únic en anglès), ja que mostra només les línies úniques o permet manipular les repeticions.

## Sintaxi bàsica

```bash
uniq [OPCIONS] [ENTRADA [SORTIDA]]
```

Si no s'especifica un arxiu d'entrada, `uniq` llegeix de l'entrada estàndard. Si no s'especifica un arxiu de sortida, el resultat s'envia a la sortida estàndard.

## Opcions principals

- `-c, --count`: Mostra el nombre de repeticions de cada línia al principi de cada línia.
- `-d, --repeated`: Mostra només les línies duplicades (que apareixen més d'un cop).
- `-D, --all-repeated[=METHOD]`: Mostra totes les línies duplicades.
- `-f, --skip-fields=N`: Ignora els primers N camps de cada línia.
- `-i, --ignore-case`: Ignora les diferències entre majúscules i minúscules.
- `-s, --skip-chars=N`: Ignora els primers N caràcters de cada línia.
- `-u, --unique`: Mostra només les línies que apareixen una vegada.
- `-w, --check-chars=N`: Compara només els primers N caràcters de cada línia.

## Exemples

### Eliminar línies repetides consecutives

```bash
cat arxiu.txt | uniq > arxiu_sense_repeticions.txt
```

### Mostrar només les línies duplicades

```bash
uniq -d arxiu.txt
```

### Comptar quantes vegades apareix cada línia

```bash
sort arxiu.txt | uniq -c
```

### Mostrar només les línies úniques (no repetides)

```bash
uniq -u arxiu.txt
```

### Ignorar majúscules/minúscules al comparar

```bash
uniq -i arxiu.txt
```

## Consideracions importants

- `uniq` només detecta línies duplicades **consecutives**. Per això, normalment s'utilitza després de `sort`:

```bash
sort arxiu.txt | uniq
```

- Per comptar totes les línies repetides d'un arxiu (no només les consecutives):

```bash
sort arxiu.txt | uniq -c
```

## Aplicacions pràctiques

1. **Analitzar logs**: Comptar el nombre d'errors únics en un arxiu de log.
2. **Estadístiques**: Comptar ocurrències d'ítems en una llista.
3. **Neteja de dades**: Eliminar entrades duplicades d'un arxiu de dades.
4. **Identificar repeticions**: Trobar elements que es repeteixen en un conjunt de dades.

## Exemple complet

Suposem que tenim un arxiu `visites.txt` amb llocs visitats:

```
Barcelona
Barcelona
Madrid
València
València
València
Girona
Barcelona
```

Si executem:

```bash
sort visites.txt | uniq -c
```

Obtindrem:

```
3 Barcelona
1 Girona
1 Madrid
3 València
```

Aquest resultat ens mostra cada ciutat i quantes vegades apareix a l'arxiu.
