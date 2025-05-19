# Canonades (pipelines) i redireccionaments a GNU/Linux

Les canonades (pipelines) i els redireccionaments són eines essencials a GNU/Linux que permeten controlar el flux de dades entre comandes i fitxers. Aquestes funcionalitats ens ajuden a combinar comandes simples per crear operacions complexes.

## Redireccionament d'entrada i sortida

### Redireccionament de sortida `>`

El símbol `>` redirigeix la sortida d'una comanda a un fitxer. Si el fitxer ja existeix, es sobreescriurà amb el nou contingut.

```bash
ls -l > llista_fitxers.txt
```

Aquest exemple guarda la llista de fitxers del directori actual al fitxer `llista_fitxers.txt`.

### Redireccionament de sortida amb afegiment `>>`

El símbol `>>` redirigeix la sortida d'una comanda a un fitxer, però afegeix el contingut al final en lloc de sobreescriure'l.

```bash
echo "Nova línia" >> notes.txt
```

Aquesta comanda afegeix el text "Nova línia" al final del fitxer `notes.txt`.

### Redireccionament d'entrada `<`

El símbol `<` permet que una comanda llegeixi l'entrada des d'un fitxer en lloc de des del teclat.

```bash
sort < llista_noms.txt
```

Aquesta comanda ordena el contingut del fitxer `llista_noms.txt`.

## Canonades (Pipelines) `|`

El símbol `|` (pipe) permet enviar la sortida d'una comanda com a entrada d'una altra comanda. Això facilita encadenar diverses comandes per realitzar tasques complexes.

```bash
ls -l | grep "maig" | sort -r
```

En aquest exemple:

1. `ls -l` llista els fitxers en format llarg
2. `grep "maig"` filtra només les línies que contenen la paraula "maig"
3. `sort -r` ordena les línies resultants en ordre invers

## Exemples pràctics

### Exemple 1: Comptar fitxers en un directori

```bash
ls | wc -l
```

Aquest exemple compta el nombre de fitxers i directoris al directori actual.

### Exemple 2: Buscar processos específics

```bash
ps aux | grep firefox
```

Aquesta comanda mostra tots els processos de Firefox que s'estan executant.

### Exemple 3: Extreure informació i guardar-la

```bash
cat /etc/passwd | grep home | cut -d: -f1 > usuaris_amb_home.txt
```

Aquest exemple:

1. Llegeix el fitxer `/etc/passwd`
2. Filtra només les línies que contenen "home"
3. Extreu el primer camp (nom d'usuari) utilitzant `:` com a delimitador
4. Guarda el resultat al fitxer `usuaris_amb_home.txt`

## Combinació de redireccionaments i canonades

Es poden combinar redireccionaments i canonades en una mateixa línia de comandes:

```bash
cat fitxer.txt | sort | uniq > resultat_ordenat_sense_duplicats.txt
```

Aquest exemple llegeix `fitxer.txt`, ordena el seu contingut, elimina les línies duplicades i guarda el resultat a `resultat_ordenat_sense_duplicats.txt`.

## Redireccionament d'errors

A més dels redireccionaments estàndard, també podem redirigir els errors:

- `2>` redirigeix només els errors (sortida d'error estàndard)
- `2>&1` redirigeix els errors al mateix lloc que la sortida estàndard

```bash
ls /directori/inexistent 2> errors.txt
find / -name "fitxer" > resultats.txt 2> errors.txt
```
