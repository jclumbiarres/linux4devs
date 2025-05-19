# Comanda `comm` de GNU/Linux

## Descripció

La comanda `comm` (de "compare") és una eina que permet comparar dos arxius ordenats línia per línia. És molt útil quan necessitem saber quines línies són úniques a cada arxiu i quines són comunes entre els dos.

## Sintaxi bàsica

```bash
comm [OPCIONS] ARXIU1 ARXIU2
```

## Funcionament

`comm` mostra la sortida en tres columnes:

1. Línies que només apareixen a l'ARXIU1
2. Línies que només apareixen a l'ARXIU2
3. Línies que apareixen en els dos arxius

## Opcions principals

- `-1`: Suprimeix la primera columna (línies úniques de l'ARXIU1)
- `-2`: Suprimeix la segona columna (línies úniques de l'ARXIU2)
- `-3`: Suprimeix la tercera columna (línies comunes)
- `--check-order`: Comprova que l'entrada estigui correctament ordenada (per defecte)
- `--nocheck-order`: No comprova si l'entrada està ordenada
- `--output-delimiter=CADENA`: Utilitza CADENA com a delimitador de sortida

## Exemples

### Comparar dos arxius i mostrar totes les columnes

```bash
comm arxiu1.txt arxiu2.txt
```

### Mostrar només les línies comunes (tercera columna)

```bash
comm -12 arxiu1.txt arxiu2.txt
```

### Mostrar només les línies úniques de l'arxiu1

```bash
comm -23 arxiu1.txt arxiu2.txt
```

### Mostrar només les línies úniques de l'arxiu2

```bash
comm -13 arxiu1.txt arxiu2.txt
```

### Canviar el delimitador de sortida

```bash
comm --output-delimiter="| " arxiu1.txt arxiu2.txt
```

## Consideracions importants

- Els arxius d'entrada **han d'estar ordenats** abans d'utilitzar `comm`. Pots utilitzar la comanda `sort` per ordenar-los:
  ```bash
  sort arxiu1.txt > arxiu1_ordenat.txt
  sort arxiu2.txt > arxiu2_ordenat.txt
  comm arxiu1_ordenat.txt arxiu2_ordenat.txt
  ```
- Si els arxius no estan ordenats, els resultats poden ser incorrectes.
- A diferència de `diff`, `comm` no mostra els canvis dins les línies, sinó només si la línia completa existeix o no en cada arxiu.

## Casos d'ús habituals

- Comparar llistes d'elements (com arxius, paraules o noms)
- Trobar elements comuns o únics entre dos conjunts de dades
- Validar quines línies falten o sobren entre dos arxius

## Combinació amb altres comandes

`comm` es pot combinar fàcilment amb canonades (pipes) per a operacions més complexes:

```bash
# Comparar llistes de paquets instal·lats en dos sistemes
sort sistema1_paquets.txt > s1.txt
sort sistema2_paquets.txt > s2.txt
comm -23 s1.txt s2.txt > paquets_nomes_sistema1.txt
```

`comm` és una eina senzilla però molt potent per a la comparació d'arxius de text quan necessites identificar diferències a nivell de línia completa.
