# Comanda `wc` a GNU/Linux

## Introducció

La comanda `wc` (word count) és una eina de GNU/Linux que serveix per comptar línies, paraules i bytes o caràcters en un fitxer. És una utilitat fonamental per a l'anàlisi de text i és part dels paquets bàsics d'eines de processament de text en sistemes Unix/Linux.

## Sintaxi bàsica

```bash
wc [OPCIONS] [FITXER...]
```

Si no s'especifica cap fitxer, o si s'utilitza "-" com a fitxer, `wc` llegeix de l'entrada estàndard.

## Opcions principals

| Opció                     | Descripció                                                                         |
| ------------------------- | ---------------------------------------------------------------------------------- |
| `-c`, `--bytes`           | Mostra el recompte de bytes                                                        |
| `-m`, `--chars`           | Mostra el recompte de caràcters                                                    |
| `-l`, `--lines`           | Mostra el recompte de línies                                                       |
| `-w`, `--words`           | Mostra el recompte de paraules                                                     |
| `-L`, `--max-line-length` | Mostra la longitud de la línia més llarga                                          |
| `--files0-from=F`         | Llegeix els noms dels fitxers des del fitxer F; cada nom acaba amb un caràcter nul |
| `--help`                  | Mostra l'ajuda i surt                                                              |
| `--version`               | Mostra informació sobre la versió i surt                                           |

## Exemples d'ús

### Recompte estàndard (línies, paraules, bytes)

```bash
wc fitxer.txt
```

Aquesta comanda mostra el recompte de línies, paraules i bytes del fitxer `fitxer.txt` en aquest ordre.

### Comptar només línies

```bash
wc -l fitxer.txt
```

### Comptar només paraules

```bash
wc -w fitxer.txt
```

### Comptar només bytes

```bash
wc -c fitxer.txt
```

### Comptar només caràcters

```bash
wc -m fitxer.txt
```

### Trobar la longitud de la línia més llarga

```bash
wc -L fitxer.txt
```

### Comptar múltiples fitxers

```bash
wc fitxer1.txt fitxer2.txt fitxer3.txt
```

En aquest cas, `wc` mostrarà els recomptes per a cada fitxer i també un total.

### Combinació amb altres comandes

```bash
cat fitxer.txt | wc -l
```

Aquesta comanda compta les línies de la sortida de `cat fitxer.txt`.

```bash
find . -type f -name "*.txt" | wc -l
```

Aquesta comanda compta el nombre de fitxers amb extensió ".txt" al directori actual i subdirectoris.

## Exemples pràctics

### Comptar el nombre de línies en un fitxer de registre

```bash
wc -l /var/log/syslog
```

### Comptar el nombre d'usuaris al sistema

```bash
cat /etc/passwd | wc -l
```

### Comptar el nombre de fitxers en un directori

```bash
ls | wc -l
```

### Comptar el nombre de processos en execució

```bash
ps aux | wc -l
```

## Detalls tècnics

- `wc` considera una paraula com una cadena de caràcters delimitats per espais.
- Una línia es determina per un caràcter de nova línia (`\n`).
- El recompte de bytes pot ser diferent del recompte de caràcters en fitxers amb codificació multibyte com UTF-8.

## Sortida

La sortida estàndard de `wc` sense opcions és:

```
[nombre_de_línies] [nombre_de_paraules] [nombre_de_bytes] [nom_del_fitxer]
```

## Conclusions

La comanda `wc` és una eina versàtil i potent per analitzar fitxers de text i sortides de comandes. La seva simplicitat i eficiència la fan imprescindible per a tasques bàsiques de processament de text i estadístiques de fitxers en entorns GNU/Linux.
