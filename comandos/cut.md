````markdown
# cut

La comanda `cut` s'utilitza per extreure seccions de cada línia d'un fitxer o d'una entrada estàndard. Pot extreure parts basant-se en bytes, caràcters o camps delimitats per un caràcter específic.

## Sintaxi Bàsica

```bash
cut [OPCIÓ]... [FITXER]...
```
````

Si no s'especifica cap `FITXER`, o si `FITXER` és `-`, llegeix de l'entrada estàndard.

## Opcions Principals

- `-b LLISTA`: Selecciona només els bytes especificats a `LLISTA`. La llista pot ser un número, un rang (`N-M`), o una llista separada per comes (`N,M,P`, `N-M,P`).
- `-c LLISTA`: Selecciona només els caràcters especificats a `LLISTA`. Similar a `-b` però amb caràcters.
- `-f LLISTA`: Selecciona només els camps especificats a `LLISTA`. Els camps estan separats per un delimitador (per defecte, el tabulador).
- `-d DELIMITADOR`: Utilitza `DELIMITADOR` en lloc del tabulador com a separador de camps quan s'usa `-f`.
- `--complement`: Complementa el conjunt de bytes, caràcters o camps seleccionats. És a dir, selecciona tot _excepte_ el que s'ha especificat.
- `-s` o `--only-delimited`: No imprimeix línies que no continguin el delimitador (només útil amb `-f`).

## Exemples

Suposem que tenim un fitxer `dades.txt` amb el següent contingut:

```
nom:cognom:edat:ciutat
anna:sole:25:barcelona
pere:vila:30:girona
joan:font:22:lleida
```

1.  **Extreure els noms (primer camp) usant `:` com a delimitador:**

    ```bash
    cut -d ':' -f 1 dades.txt
    ```

    Sortida:

    ```
    nom
    anna
    pere
    joan
    ```

2.  **Extreure el nom i la ciutat (camps 1 i 4):**

    ```bash
    cut -d ':' -f 1,4 dades.txt
    ```

    Sortida:

    ```
    nom:ciutat
    anna:barcelona
    pere:girona
    joan:lleida
    ```

3.  **Extreure els primers 4 caràcters de cada línia:**

    ```bash
    cut -c 1-4 dades.txt
    ```

    Sortida:

    ```
    nom:
    anna
    pere
    joan
    ```

4.  **Extreure tot excepte el tercer camp (edat):**

    ```bash
    cut -d ':' -f 3 --complement dades.txt
    ```

    Sortida:

    ```
    nom:cognom:ciutat
    anna:sole:barcelona
    pere:vila:girona
    joan:font:lleida
    ```

5.  **Llegir des de l'entrada estàndard:**

    ```bash
    echo "un:dos:tres:quatre" | cut -d ':' -f 2,4
    ```

    Sortida:

    ```
    dos:quatre
    ```
