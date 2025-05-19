# Àlies de Bash

Un **àlies** a Bash és una drecera o un nom alternatiu per a un comandament o una sèrie de comandaments. Permeten estalviar temps i esforç en teclejar comandaments llargs o complexos que utilitzes sovint.

## Com funcionen?

Quan escrius el nom d'un àlies a la línia de comandaments i prems Enter, Bash el substitueix automàticament pel comandament complet que representa abans d'executar-lo. És una simple substitució de text.

## Crear un àlies

Per crear un àlies temporal (només per a la sessió actual de la terminal), utilitza el comandament `alias` seguit del nom de l'àlies, un signe igual (`=`), i el comandament que vols abreujar entre cometes simples (`'`):

```bash
alias nom_drecera='comandament_llarg_o_complex'
```

**Exemple:**

Per crear un àlies `ll` que executi `ls -alF`:

```bash
alias ll='ls -alF'
```

Ara, en lloc d'escriure `ls -alF`, pots simplement escriure `ll`.

## Fer els àlies permanents

Els àlies creats directament a la terminal desapareixen quan tanques la sessió. Per fer-los permanents, has d'afegir les definicions dels àlies al fitxer de configuració de Bash, que normalment és `~/.bashrc` (o de vegades `~/.bash_profile` o un fitxer dedicat com `~/.bash_aliases` que es carrega des de `~/.bashrc`).

1.  Obre el fitxer `~/.bashrc` amb un editor de text (com `nano`, `vim`, o `gedit`):
    ```bash
    nano ~/.bashrc
    ```
2.  Afegeix les teves definicions d'àlies al final del fitxer, una per línia:
    ```bash
    # Els meus àlies personalitzats
    alias ll='ls -alF'
    alias update='sudo apt update && sudo apt upgrade -y' # Exemple per a sistemes Debian/Ubuntu
    alias ..='cd ..'
    ```
3.  Guarda el fitxer i tanca l'editor.
4.  Per aplicar els canvis a la sessió actual de la terminal sense haver de tancar-la i obrir-la de nou, executa:
    ```bash
    source ~/.bashrc
    ```

A partir d'ara, els àlies estaran disponibles cada cop que obris una nova terminal.

## Llistar àlies definits

Per veure tots els àlies definits actualment a la teva sessió, simplement executa el comandament `alias` sense arguments:

```bash
alias
```

## Eliminar un àlies

Per eliminar un àlies de la sessió actual, utilitza el comandament `unalias`:

```bash
unalias nom_drecera
```

Per exemple, per eliminar l'àlies `ll`:

```bash
unalias ll
```

Si vols eliminar un àlies permanentment, has d'esborrar la seva definició del fitxer `~/.bashrc` (o on l'hagis definit) i després executar `source ~/.bashrc` o reiniciar la terminal.

## Avantatges

- **Conveniència:** Redueixen la quantitat de text a escriure.
- **Memorització:** Faciliten recordar comandaments complexos o amb moltes opcions.
- **Consistència:** Asseguren que sempre executes un comandament amb les mateixes opcions preferides.
