# El Comando `touch` de GNU/Linux

## Introducció

El comandament `touch` és una eina fonamental en sistemes GNU/Linux que s'utilitza principalment per a crear fitxers buits i actualitzar les marques de temps dels fitxers existents.

## Sintaxi Bàsica

```bash
touch [OPCIONS] FITXER...
```

## Descripció

`touch` canvia les marques de temps d'accés i modificació de cada FITXER especificat a l'hora actual. Si el FITXER no existeix, es crearà un fitxer buit amb aquest nom, llevat que s'especifiqui l'opció `-c` o `--no-create`.

## Opcions Principals

- `-a`: Canvia només el temps d'accés.
- `-c, --no-create`: No crea fitxers nous.
- `-d, --date=CADENA`: Utilitza CADENA en lloc de l'hora actual.
- `-m`: Canvia només el temps de modificació.
- `-r, --reference=FITXER`: Utilitza les marques de temps d'aquest FITXER en lloc de l'hora actual.
- `-t STAMP`: Utilitza [[CC]YY]MMDDhhmm[.ss] en lloc de l'hora actual.
- `--time=PARAULA`: Estableix el temps especificat per PARAULA: "access", "atime" o "use" (equivalent a -a), o "modify" o "mtime" (equivalent a -m).

## Exemples d'Ús

### Crear un fitxer buit

```bash
touch nou_fitxer.txt
```

### Actualitzar la marca de temps d'un fitxer existent

```bash
touch fitxer_existent.txt
```

### Canviar només el temps d'accés

```bash
touch -a fitxer.txt
```

### Canviar només el temps de modificació

```bash
touch -m fitxer.txt
```

### Utilitzar una data específica

```bash
touch -d "2023-10-15 14:30:00" fitxer.txt
```

### Copiar les marques de temps d'un altre fitxer

```bash
touch -r fitxer_referencia.txt fitxer_destí.txt
```

### Crear múltiples fitxers a la vegada

```bash
touch fitxer1.txt fitxer2.txt fitxer3.txt
```

## Casos Pràctics

- **Desenvolupament Web**: Crear fitxers buits com `index.html`, `style.css` o `app.js` per iniciar un projecte.
- **Scripts**: Tocar un fitxer pot ser utilitzat en scripts per a indicar que una tasca s'ha completat.
- **Actualitzar fitxers sense modificar el contingut**: Útil per a actualitzar marques de temps sense alterar el contingut del fitxer.

## Consideracions

- `touch` és una eina lleugera que forma part de les utilitats bàsiques de GNU Coreutils.
- Modificar les marques de temps pot afectar a processos que depenen d'elles, com les còpies de seguretat o la compilació de programes.
- En sistemes de fitxers moderns, `touch` actualitza també altres atributs de temps com el temps de canvi d'estat (ctime).

## Informació Addicional

El comandament `touch` va ser originalment dissenyat per a actualitzar marques de temps, però l'ús més comú actualment és per a la creació de fitxers buits.
