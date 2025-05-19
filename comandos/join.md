# Comanda Join

## Introducció

La comanda `join` és una eina de GNU/Linux que permet combinar línies de dos fitxers basant-se en un camp comú. És com fer una unió de taules en una base de dades, però treballant amb fitxers de text.

## Sintaxi bàsica

```
join [OPCIONS] FITXER1 FITXER2
```

## Opcions principals

- `-1 CAMP`: Especifica el camp a utilitzar del primer fitxer (per defecte és el primer camp)
- `-2 CAMP`: Especifica el camp a utilitzar del segon fitxer
- `-t CARÀCTER`: Utilitza CARÀCTER com a delimitador de camps (per defecte és espai en blanc)
- `-a NUMFITXER`: També mostra les línies sense parella del fitxer NUMFITXER (pot ser 1 o 2)
- `-e CADENA`: Substitueix els camps que falten per CADENA
- `-o FORMAT`: Especifica el format de sortida

## Exemples bàsics

### Unir dos fitxers pel primer camp

Suposem que tenim dos fitxers:

**usuaris.txt**

```
1 Anna
2 Pere
3 Maria
4 Joan
```

**telèfons.txt**

```
1 611222333
3 644555666
4 677888999
5 600111222
```

Si executem:

```bash
join usuaris.txt telèfons.txt
```

Obtindrem:

```
1 Anna 611222333
3 Maria 644555666
4 Joan 677888999
```

### Especificar un delimitador diferent

Si els nostres fitxers utilitzen comes com a delimitador:

```bash
join -t ',' fitxer1.csv fitxer2.csv
```

### Mostrar totes les línies dels dos fitxers (similar a un FULL OUTER JOIN en SQL)

```bash
join -a 1 -a 2 usuaris.txt telèfons.txt
```

Resultat:

```
1 Anna 611222333
2 Pere
3 Maria 644555666
4 Joan 677888999
5 600111222
```

## Casos d'ús comuns

- Combinar informació de múltiples fonts de dades
- Relacionar fitxers de registre que comparteixen un identificador
- Processar dades estructurades en processos ETL (Extract, Transform, Load)
- Fusionar dades de diferents departaments o sistemes

## Notes importants

- Els fitxers d'entrada han d'estar ordenats segons el camp de combinació
- Si els fitxers no estan ordenats, cal ordenar-los primer amb `sort`
- És molt útil combinar `join` amb altres comandes com `sort`, `cut` o `awk`

## Consells pràctics

- Sempre verifica que els teus fitxers estiguin ordenats correctament abans d'utilitzar `join`
- Utilitza l'opció `-o` quan necessitis un control precís sobre el format de sortida
- Recorda que els camps es numeren des de 1, no des de 0

## Exemple avançat

```bash
# Ordenar primer els fitxers (important!)
sort -k1,1 usuaris.txt > usuaris_ordenats.txt
sort -k1,1 telèfons.txt > telèfons_ordenats.txt

# Unir els fitxers amb format personalitzat
# (mostrar nom i telèfon separats per dos punts)
join -o '1.2,2.2' -t ' ' usuaris_ordenats.txt telèfons_ordenats.txt | tr ' ' ':'
```

Resultat:

```
Anna:611222333
Maria:644555666
Joan:677888999
```

## Conclusió

La comanda `join` és una eina potent per a la manipulació de dades textuals estructurades en entorns UNIX/Linux. Tot i que pot semblar complexa al principi, dominar-la et permet realitzar operacions de combinació de dades sense necessitat de bases de dades o scripts complexos.
