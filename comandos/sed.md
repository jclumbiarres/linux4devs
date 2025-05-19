`sed` (Stream Editor) és una potent utilitat de línia de comandes a Linux i altres sistemes Unix-like que s'utilitza per realitzar transformacions bàsiques de text en un flux d'entrada (un fitxer o l'entrada d'una altra comanda). Funciona línia per línia i és especialment útil per a substitucions de text, eliminacions i altres manipulacions.

## Sintaxi Bàsica

La sintaxi més comuna de `sed` és:

```bash
sed 'comando' [fitxer...]
```

- `comando`: L'operació que vols realitzar (p. ex., substituir text).
- `[fitxer...]`: Un o més fitxers d'entrada. Si no s'especifica cap fitxer, `sed` llegeix de l'entrada estàndard (stdin).

## Exemples per a Novells

### 1. Substitució de Text

La comanda més utilitzada és `s` per a substituir.

**Sintaxi:** `s/text_antic/text_nou/flags`

- `s`: Indica la comanda de substitució.
- `text_antic`: El text que vols buscar.
- `text_nou`: El text pel qual vols substituir `text_antic`.
- `flags`: Modificadors opcionals. El més comú és `g` (global), que substitueix totes les ocurrències a cada línia, no només la primera.

**Exemple:** Suposem que tenim un fitxer `salutacio.txt` amb el contingut:

```
Hola món!
Aquest és un món meravellós.
```

Per substituir "món" per "planeta" a tot el fitxer:

```bash
sed 's/món/planeta/g' salutacio.txt
```

**Sortida:**

```
Hola planeta!
Aquest és un planeta meravellós.
```

**Nota:** Per defecte, `sed` mostra el resultat a la sortida estàndard (la pantalla) sense modificar el fitxer original.

### 2. Eliminar Línies

La comanda `d` s'utilitza per eliminar línies que coincideixen amb un patró.

**Sintaxi:** `/patró/d`

- `/patró/`: Busca les línies que contenen aquest patró.
- `d`: Indica la comanda d'eliminació.

**Exemple:** Per eliminar totes les línies que contenen la paraula "meravellós" del fitxer `salutacio.txt`:

```bash
sed '/meravellós/d' salutacio.txt
```

**Sortida:**

```
Hola món!
```

### 3. Mostrar Només Línies Específiques (Impressió)

Per defecte, `sed` imprimeix totes les línies després de processar-les. Si vols imprimir només les línies que coincideixen amb un patró, pots utilitzar l'opció `-n` (suprimeix la sortida per defecte) juntament amb la comanda `p` (imprimir).

**Sintaxi:** `sed -n '/patró/p' fitxer`

**Exemple:** Per mostrar només les línies que contenen "Hola" a `salutacio.txt`:

```bash
sed -n '/Hola/p' salutacio.txt
```

**Sortida:**

```
Hola món!
```

### 4. Modificar el Fitxer Original (Edició In-Place)

Si vols que `sed` modifiqui directament el fitxer original en lloc de mostrar el resultat a la pantalla, pots utilitzar l'opció `-i` (in-place).

**Precaució:** Aquesta opció modifica el fitxer directament. És recomanable fer una còpia de seguretat abans d'utilitzar-la si no estàs segur.

**Exemple:** Per substituir "món" per "univers" directament al fitxer `salutacio.txt`:

```bash
# Opcional: Crear una còpia de seguretat
# cp salutacio.txt salutacio.txt.bak

sed -i 's/món/univers/g' salutacio.txt
```

Ara, el contingut de `salutacio.txt` serà:

```
Hola univers!
Aquest és un univers meravellós.
```

Pots crear una còpia de seguretat automàticament amb `-i` afegint una extensió:

```bash
# Modifica salutacio.txt i crea salutacio.txt.bak amb el contingut original
sed -i.bak 's/univers/planeta/g' salutacio.txt
```

`sed` és una eina molt versàtil amb moltes més opcions i comandes. Aquests exemples bàsics t'ajudaran a començar a utilitzar-la per a tasques senzilles de manipulació de text.
