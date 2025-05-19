# El Comando `tr` (translate)

## Introducció

El comando `tr` (abreviatura de "translate" o traduir) és una eina de línia de comandes en sistemes GNU/Linux que s'utilitza per traduir, esborrar o comprimir caràcters. És especialment útil per a manipular text i fer substitucions caràcter per caràcter en un flux de text.

## Sintaxi bàsica

```bash
tr [OPCIONS] CONJUNT1 [CONJUNT2]
```

On:

- `CONJUNT1` són els caràcters que es volen buscar.
- `CONJUNT2` són els caràcters de substitució.

## Descripció

`tr` llegeix text de l'entrada estàndard (stdin) i escriu el resultat a la sortida estàndard (stdout). No accepta directament noms de fitxers com a argument; s'ha d'utilitzar la redireccióo una canonada (pipe).

## Opcions principals

- `-c`, `--complement`: Utilitza el complement del CONJUNT1.
- `-d`, `--delete`: Esborra els caràcters del CONJUNT1 en lloc de traduir-los.
- `-s`, `--squeeze-repeats`: Substitueix cada seqüència de caràcters repetits del CONJUNT1 per una sola instància.
- `-t`, `--truncate-set1`: Trunca CONJUNT1 a la longitud de CONJUNT2.

## Classes de caràcters predefinits

`tr` permet utilitzar classes de caràcters predefinits, com:

- `[:alnum:]`: Tots els caràcters alfanumèrics.
- `[:alpha:]`: Totes les lletres.
- `[:digit:]`: Tots els dígits.
- `[:lower:]`: Totes les lletres minúscules.
- `[:upper:]`: Totes les lletres majúscules.
- `[:space:]`: Tots els espais en blanc.

## Exemples d'ús

### Convertir text a majúscules

```bash
echo "hola món" | tr "[:lower:]" "[:upper:]"
```

Resultat: `HOLA MÓN`

### Convertir text a minúscules

```bash
echo "HOLA MÓN" | tr "[:upper:]" "[:lower:]"
```

Resultat: `hola món`

### Eliminar caràcters específics

```bash
echo "Hola, Món!" | tr -d ","
```

Resultat: `Hola Món!`

### Eliminar tots els dígits

```bash
echo "El meu telèfon és 123456789" | tr -d "[:digit:]"
```

Resultat: `El meu telèfon és `

### Comprimir espais en blanc múltiples

```bash
echo "Hola    món    com    estàs?" | tr -s " "
```

Resultat: `Hola món com estàs?`

### Substituir caràcters específics

```bash
echo "La programació és divertida" | tr "aeiou" "12345"
```

Resultat: `L1 pr4gr1m1c3ó és d3v2rt3d1`

### Eliminar caràcters de nova línia

```bash
cat fitxer.txt | tr -d "\n"
```

Aquest comando elimina tots els salts de línia d'un fitxer.

## Casos d'ús comuns

1. **Normalització de text**: Eliminar caràcters no desitjats, convertir entre majúscules i minúscules.
2. **Processament de dades**: Netejar dades abans d'analitzar-les.
3. **Scripts de shell**: Manipulació bàsica de text dins de scripts.
4. **Conversions de codificació**: Canviar conjunts de caràcters específics.

## Consells i trucs

- El comando `tr` processa el text caràcter per caràcter, no paraula per paraula.
- Per manipular un fitxer, utilitza redireccions: `tr 'a' 'A' < entrada.txt > sortida.txt`.
- Utilitza cometes simples ('') per evitar que la shell interpreti caràcters especials.
- Per traduir caràcters especials com tabulacions o noves línies, utilitza notació d'escapament: `\t`, `\n`.

## Limitacions

- No pot fer correspondències basades en expressions regulars complexes.
- No pot fer substitucions basades en la posició dins del text.
- No modifica fitxers directament; sempre es necessita redirecció.
