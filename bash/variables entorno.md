# Variables d'Entorn a Bash

Les variables d'entorn a Bash (i altres intèrprets d'ordres Unix-like) són variables dinàmiques que afecten el comportament dels processos a l'ordinador. Formen part de l'entorn en què s'executa un procés.

## Què són?

- Són parells **clau-valor** (nom=valor).
- Són **heretades** pels processos fills. Quan un programa n'inicia un altre, el nou procés rep una còpia de les variables d'entorn del pare.
- Contenen informació útil com ara les rutes de cerca de programes (`PATH`), el directori personal de l'usuari (`HOME`), l'idioma preferit (`LANG`), etc.

## Com llistar les variables d'entorn

Pots veure les variables d'entorn definides a la teva sessió actual amb les ordres següents:

- `env`: Mostra totes les variables d'entorn.
- `printenv`: Similar a `env`. També pots passar-li un nom de variable per veure només el seu valor (`printenv HOME`).
- `declare -x`: Mostra les variables marcades per a exportació (variables d'entorn).
- `echo $NOM_VARIABLE`: Mostra el valor d'una variable específica (p. ex., `echo $PATH`).

## Com accedir al valor d'una variable

S'accedeix al valor d'una variable posant el símbol `$` davant del seu nom:

```bash
echo $HOME
echo "L'intèrpret d'ordres actual és: $SHELL"
echo "Estic al directori: ${PWD}" # Les claus {} són opcionals però recomanades per claredat
```

## Exemples comuns de variables d'entorn

| Variable | Descripció                                                                 |
| :------- | :------------------------------------------------------------------------- |
| `PATH`   | Llista de directoris on l'intèrpret cerca els executables.                 |
| `HOME`   | El directori personal de l'usuari actual.                                  |
| `USER`   | El nom de l'usuari actual.                                                 |
| `SHELL`  | La ruta a l'intèrpret d'ordres de l'usuari.                                |
| `PWD`    | El directori de treball actual (Present Working Directory).                |
| `LANG`   | La configuració regional (idioma, format de data/hora, etc.).              |
| `TERM`   | El tipus de terminal que s'està utilitzant.                                |
| `EDITOR` | L'editor de text preferit per defecte (usat per algunes ordres com `git`). |
| `PS1`    | Defineix l'aparença del prompt de l'intèrpret d'ordres.                    |

## Com definir variables d'entorn

### 1. Temporalment (només per a una ordre)

Pots definir una variable d'entorn només per a l'execució d'una única ordre:

```bash
MYVAR="Hola" echo $MYVAR # Això no funcionarà com s'espera directament amb echo
MYVAR="Hola" printenv MYVAR # Això tampoc, printenv és un programa extern
MYVAR="Hola" bash -c 'echo $MYVAR' # Funciona perquè es crea un nou procés bash
```

### 2. Per a la sessió actual

Per definir una variable que estigui disponible durant tota la sessió actual de l'intèrpret i per als processos que iniciïs des d'ell, utilitza `export`:

```bash
# Primer definim una variable local (només visible a l'intèrpret actual)
MI_VARIABLE="Valor secret"

# Ara l'exportem perquè sigui una variable d'entorn
export MI_VARIABLE

# O directament en una sola línia
export UNA_ALTRA_VARIABLE="Un altre valor"

# Comprovar que existeix
echo $MI_VARIABLE
printenv MI_VARIABLE
```

### 3. Permanentment

Perquè una variable d'entorn estigui disponible cada cop que iniciïs sessió, has d'afegir la comanda `export` a un dels fitxers d'inicialització de Bash. Els més comuns són:

- `~/.bashrc`: S'executa per a cada nova instància d'intèrpret interactiu no de login. És el lloc més comú per a usuaris d'escriptori.
- `~/.bash_profile` o `~/.profile`: S'executa per a les sessions d'intèrpret de login (p. ex., quan et connectes via SSH o a una consola tty). Sovint, `.bash_profile` crida a `.bashrc` si existeix.

**Exemple (afegir a `~/.bashrc`):**

```bash
# Afegir al final del fitxer ~/.bashrc
export JAVA_HOME="/usr/lib/jvm/java-11-openjdk-amd64"
export PATH="$PATH:$JAVA_HOME/bin"
```

Després de modificar aquests fitxers, has de:

- Tancar i obrir una nova terminal.
- O executar `source ~/.bashrc` (o el fitxer modificat) a la terminal actual per aplicar els canvis immediatament.

## Diferència entre Variables de Shell i Variables d'Entorn

- **Variables de Shell:** Només existeixen dins de la instància actual de l'intèrpret. No s'hereten pels processos fills. Es creen sense `export`.
  ```bash
  mi_var_local="Soc local"
  ```
- **Variables d'Entorn:** Són variables de shell que han estat marcades amb `export` per ser passades als processos fills.
  ```bash
  export mi_var_entorn="Soc d'entorn"
  ```

Les variables d'entorn són fonamentals per configurar l'entorn d'execució dels programes a Linux i altres sistemes Unix-like.
