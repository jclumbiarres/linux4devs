# chmod - Canviar els permisos dels fitxers

## Descripció

El comandament `chmod` (change mode) permet modificar els permisos d'accés d'arxius i directoris en sistemes GNU/Linux i altres sistemes tipus Unix.

## Sintaxi bàsica

```bash
chmod [opcions] mode fitxer(s)
```

## Els permisos en Linux

En Linux, cada fitxer i directori té tres tipus de permisos assignats a tres categories d'usuaris:

- **Propietari (u)**: l'usuari que ha creat el fitxer
- **Grup (g)**: els usuaris que pertanyen al mateix grup
- **Altres (o)**: la resta d'usuaris del sistema

Per a cada categoria, hi ha tres permisos possibles:

- **Lectura (r)**: valor numèric 4
- **Escriptura (w)**: valor numèric 2
- **Execució (x)**: valor numèric 1

## Formes d'utilitzar chmod

### Notació simbòlica

```bash
chmod [qui][operació][permisos] fitxer
```

On:

- **qui**: u (propietari), g (grup), o (altres), a (tots)
- **operació**: + (afegir permís), - (eliminar permís), = (establir permís exacte)
- **permisos**: r (lectura), w (escriptura), x (execució)

### Notació numèrica (octal)

```bash
chmod ### fitxer
```

On cada dígit representa els permisos per al propietari, grup i altres respectivament.
Cada dígit és la suma dels valors: 4 (lectura) + 2 (escriptura) + 1 (execució)

## Exemples pràctics

### Notació simbòlica

```bash
# Donar permís d'execució al propietari
chmod u+x programa.sh

# Afegir permisos de lectura i escriptura al grup
chmod g+rw document.txt

# Eliminar permís d'escriptura per a altres
chmod o-w document.txt

# Establir permisos complets per al propietari i només lectura per a la resta
chmod u=rwx,go=r document.txt
```

### Notació numèrica

```bash
# 755: rwxr-xr-x (propietari tot, grup i altres lectura i execució)
chmod 755 programa.sh

# 644: rw-r--r-- (propietari lectura i escriptura, grup i altres només lectura)
chmod 644 document.txt

# 777: rwxrwxrwx (permisos totals per a tothom - cal usar amb precaució!)
chmod 777 fitxer.txt
```

## Opcions importants

- `-R, --recursive`: Canvia els permisos recursivament en directoris i els seus continguts
- `-v, --verbose`: Mostra un diagnòstic per a cada fitxer processat
- `-f, --silent`: Suprimeix la majoria dels missatges d'error
- `--reference=FITXER`: Utilitza els permisos del FITXER especificat com a referència

## Consells pràctics

- El permís `chmod 777` dona accés complet a tothom i pot representar un risc de seguretat
- Per a scripts, el permís d'execució (`+x`) és necessari
- Els directoris necessiten el permís d'execució (`x`) per a poder ser explorats
- Només el propietari del fitxer o l'administrador (root) pot canviar els permisos
