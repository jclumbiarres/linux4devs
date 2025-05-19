# Comanda `xargs` a GNU/Linux

`xargs` és una eina molt potent que llegeix elements des de l'entrada estàndard i executa una comanda (per defecte `/bin/echo`) utilitzant aquests elements com a arguments.

## Sintaxi bàsica

```bash
xargs [opcions] [comanda [arguments inicials]]
```

## Descripció

La comanda `xargs` és una utilitat que construeix i executa línies de comandes a partir de l'entrada estàndard. Si no s'especifica cap comanda, s'executarà `/bin/echo` per defecte. És especialment útil per processar llargues llistes d'elements que podrien superar les limitacions dels arguments de la línia de comandes.

## Opcions principals

| Opció                     | Descripció                                                                                               |
| ------------------------- | -------------------------------------------------------------------------------------------------------- |
| `-0`, `--null`            | Tracta l'entrada com a delimitada per caràcters nuls (útil amb `find -print0`)                           |
| `-d`, `--delimiter=DELIM` | Utilitza DELIM com a delimitador en lloc d'espai en blanc                                                |
| `-I [REEMPLAÇ]`           | Substitueix REEMPLAÇ (per defecte `{}`) a les posicions INICIALS per noms llegits de l'entrada estàndard |
| `-L MÀXIM`                | Utilitza com a màxim MÀXIM línies no buides per línia de comanda                                         |
| `-n MÀXIM`                | Utilitza com a màxim MÀXIM arguments per línia de comanda                                                |
| `-P MÀXIM`                | Executa fins a MÀXIM processos simultàniament                                                            |
| `--verbose`               | Mostra les comandes abans d'executar-les                                                                 |

## Exemples d'ús

### Exemple bàsic

```bash
echo "fitxer1 fitxer2 fitxer3" | xargs rm
```

Aquest exemple elimina els fitxers anomenats "fitxer1", "fitxer2" i "fitxer3".

### Utilitzant delimitadors personalitzats

```bash
echo "fitxer1,fitxer2,fitxer3" | xargs -d, rm
```

Aquest exemple utilitza la coma com a delimitador.

### Treballar amb fitxers que tenen espais

```bash
find . -name "*.txt" -print0 | xargs -0 rm
```

L'opció `-print0` de `find` i l'opció `-0` de `xargs` treballen juntes per manejar correctament els noms de fitxers amb espais.

### Substituir cadenes

```bash
echo "file1 file2 file3" | xargs -I {} mv {} {}.bak
```

Aquest exemple afegeix l'extensió ".bak" a cada fitxer.

### Execució paral·lela

```bash
find . -name "*.jpg" | xargs -P 4 -I {} convert {} {}.png
```

Aquest exemple converteix tots els fitxers JPG a PNG utilitzant quatre processos en paral·lel.

### Limitar el nombre d'arguments

```bash
cat fitxers.txt | xargs -n 2 cp -t /directori/desti
```

Aquest exemple copia els fitxers a un directori de destí, però només passa 2 arguments per comanda.

## Casos d'ús comuns

1. **Processament de fitxers en lot**: Executar comandes sobre molts fitxers
2. **Esborrat segur**: Eliminar fitxers amb noms complexos o amb espais
3. **Execució paral·lela**: Accelerar operacions executant-les simultàniament
4. **Processar sortides de comandes**: Manipular dades generades per altres comandes

## Precaucions

- Tingues cura quan utilitzis `xargs` amb comandes destructives com `rm`
- Utilitza sempre `--verbose` per veure què s'està executant quan proves comandes
- Per a fitxers amb noms que contenen caràcters especials, utilitza l'opció `-0` juntament amb `find -print0`

## Compatibilitat

`xargs` és part del paquet GNU Coreutils i està disponible a pràcticament totes les distribucions GNU/Linux. Les opcions poden variar lleugerament entre versions.
