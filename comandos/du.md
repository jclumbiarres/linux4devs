# Comandament `du`

## Introducció

El comandament `du` (Disk Usage) és una eina que permet visualitzar l'espai de disc utilitzat pels fitxers i directoris en un sistema Linux. És extremadament útil per identificar quins fitxers o directoris ocupen més espai al disc dur.

## Sintaxi bàsica

```
du [opcions] [fitxer/directori...]
```

Si no s'especifica cap fitxer o directori, `du` analitzarà el directori actual.

## Opcions principals

- `-h, --human-readable`: Mostra les mides en format llegible per humans (KB, MB, GB).
- `-s, --summarize`: Mostra només el total per a cada argument.
- `-a, --all`: Mostra la mida de tots els fitxers, no només dels directoris.
- `-c, --total`: Produeix un gran total al final de la sortida.
- `--max-depth=N`: Especifica la profunditat màxima de directoris a analitzar.
- `-x, --one-file-system`: No travessa diferents sistemes de fitxers.

## Exemples d'ús

### Visualitzar l'espai que ocupa un directori en format llegible

```bash
du -h /home/usuari/Documents
```

### Mostrar només el resum total d'un directori

```bash
du -sh /home/usuari/Documents
```

### Mostrar els 5 directoris més grans dins d'una carpeta

```bash
du -h /home/usuari | sort -rh | head -5
```

### Mostrar l'espai total utilitzat pel directori actual i els subdirectoris

```bash
du -ch .
```

### Visualitzar només el primer nivell de directoris

```bash
du -h --max-depth=1 /home/usuari
```

## Casos pràctics

- **Trobar fitxers grans**: Combinant `du` amb `sort` podem identificar ràpidament quins fitxers o directoris consumeixen més espai.
- **Neteja del sistema**: És ideal per detectar espai que es pot alliberar eliminant arxius innecessaris.
- **Monitoratge de l'espai**: Permet controlar el creixement de directoris específics.

## Notes importants

- El comando `du` calcula l'ús de disc, no la mida aparent dels fitxers. Per tant, pot mostrar valors diferents dels de l'explorador d'arxius.
- L'execució de `du` en directoris molt grans pot trigar un temps considerable.
- Cal tenir permisos suficients per llegir els fitxers i directoris que s'analitzen.
