# Comanda TAR (GNU/Linux)

## Introducció

La comanda `tar` (Tape ARchive) és una eina essencial en sistemes GNU/Linux que permet crear, modificar i extreure arxius comprimits. Originalment dissenyada per crear còpies de seguretat en cintes magnètiques, avui en dia s'utilitza principalment per empaquetar arxius en un sol fitxer (amb o sense compressió).

## Sintaxi bàsica

```
tar [opcions] [arxiu-destí] [arxius-origen]
```

## Opcions principals

### Operacions bàsiques

- `-c, --create`: Crea un nou arxiu tar
- `-x, --extract`: Extreu els fitxers d'un arxiu tar
- `-t, --list`: Mostra el contingut d'un arxiu tar sense extreure'l
- `-r, --append`: Afegeix fitxers al final d'un arxiu tar existent
- `-u, --update`: Afegeix fitxers només si són més nous que els existents a l'arxiu

### Opcions de compressió

- `-z, --gzip`: Utilitza gzip per comprimir/descomprimir (extensió .tar.gz o .tgz)
- `-j, --bzip2`: Utilitza bzip2 per comprimir/descomprimir (extensió .tar.bz2)
- `-J, --xz`: Utilitza xz per comprimir/descomprimir (extensió .tar.xz)
- `--zstd`: Utilitza zstd per comprimir/descomprimir (extensió .tar.zst)
- `--lzip`: Utilitza lzip per comprimir/descomprimir (extensió .tar.lz)

### Opcions addicionals

- `-f, --file=ARXIU`: Especifica el nom de l'arxiu tar
- `-v, --verbose`: Mostra els fitxers processats
- `-p, --preserve-permissions`: Preserva els permisos originals dels fitxers
- `-C, --directory=DIR`: Canvia al directori DIR abans de realitzar qualsevol operació
- `--exclude=PATRÓ`: Exclou fitxers que coincideixen amb el patró
- `--exclude-from=FITXER`: Exclou fitxers coincidents amb els patrons al FITXER
- `--keep-old-files`: No sobreescriu fitxers existents durant l'extracció
- `--overwrite`: Sobreescriu fitxers existents durant l'extracció
- `--recursive-unlink`: Elimina els fitxers existents abans d'extreure

## Exemples d'ús

### Crear un arxiu tar

```bash
# Crear un arxiu tar sense compressió
tar -cf arxiu.tar fitxer1 fitxer2 directori/

# Crear un arxiu tar amb compressió gzip
tar -czf arxiu.tar.gz fitxer1 fitxer2 directori/

# Crear un arxiu tar amb compressió bzip2
tar -cjf arxiu.tar.bz2 fitxer1 fitxer2 directori/

# Crear un arxiu tar amb compressió xz (millor compressió però més lenta)
tar -cJf arxiu.tar.xz fitxer1 fitxer2 directori/
```

### Extreure un arxiu tar

```bash
# Extreure un arxiu tar sense compressió
tar -xf arxiu.tar

# Extreure un arxiu amb compressió gzip
tar -xzf arxiu.tar.gz

# Extreure un arxiu amb compressió bzip2
tar -xjf arxiu.tar.bz2

# Extreure en un directori específic
tar -xf arxiu.tar -C /ruta/directori/

# Extreure només arxius específics
tar -xf arxiu.tar fitxer1 directori/fitxer2
```

### Veure contingut d'un arxiu tar

```bash
# Llistar contingut d'un arxiu tar
tar -tf arxiu.tar

# Llistar amb detalls (mode verbose)
tar -tvf arxiu.tar
```

### Afegir fitxers a un arxiu tar existent

```bash
tar -rf arxiu.tar nou_fitxer
```

### Actualitzar fitxers en un arxiu tar

```bash
tar -uf arxiu.tar fitxer_modificat
```

### Excloure fitxers o directoris

```bash
tar -czf backup.tar.gz /home/usuari --exclude=/home/usuari/tmp --exclude="*.log"
```

## Casos d'ús avançats

### Crear còpies de seguretat amb data

```bash
tar -czf backup-$(date +%Y%m%d).tar.gz /directori/a/copiar
```

### Dividir arxius tar grans

```bash
# Crear un arxiu tar gran i dividir-lo en parts de 1GB
tar -cf - directori | split -b 1G - arxiu.tar.part
```

### Comprimir amb diferents nivells de compressió

```bash
# Utilitzar xz amb nivell de compressió màxim
XZ_OPT=-9 tar -cJf arxiu.tar.xz directori/
```

### Conservar permisos i enllaços simbòlics

```bash
tar -cpzf backup.tar.gz --same-owner /directori/origen
```

### Verificar la integritat d'un arxiu tar

```bash
tar -tvf arxiu.tar >/dev/null
```

## Notes importants

- L'opció `-f` ha de ser l'última abans del nom de l'arxiu.
- Els arxius tar no proporcionen encriptació per si sols.
- Les opcions curtes es poden combinar: `-xzf` en lloc de `-x -z -f`.
- Per a fitxers molt grans, les compressions xz o zstd ofereixen millors resultats.
- La compressió gzip és la més ràpida però menys eficient, mentre que xz és més lenta però ofereix millors ràtios de compressió.

## Taula comparativa de formats de compressió

| Format           | Extensió        | Velocitat   | Compressió | Opció tar |
| ---------------- | --------------- | ----------- | ---------- | --------- |
| Sense compressió | .tar            | Molt ràpida | Cap        | -c        |
| gzip             | .tar.gz, .tgz   | Ràpida      | Bona       | -z        |
| bzip2            | .tar.bz2, .tbz2 | Mitjana     | Molt bona  | -j        |
| xz               | .tar.xz         | Lenta       | Excel·lent | -J        |
| zstd             | .tar.zst        | Ràpida      | Molt bona  | --zstd    |

## Compatibilitat

La implementació GNU de `tar` és la més comuna en sistemes Linux, però existeixen algunes diferències amb altres implementacions com BSD tar. Això pot ser rellevant quan es transfereixen arxius entre sistemes diferents.
