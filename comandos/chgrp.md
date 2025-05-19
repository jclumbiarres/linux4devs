# chgrp - Canvia el grup propietari d'arxius i directoris

## Descripció

El comandament `chgrp` permet canviar el grup propietari d'un arxiu o directori al sistema GNU/Linux.

## Sintaxi

```bash
chgrp [OPCIONS] GRUP ARXIU...
```

## Opcions principals

- `-R, --recursive`: Canvia recursivament el grup de directoris i els seus continguts
- `-v, --verbose`: Mostra informació detallada sobre els canvis realitzats
- `-c, --changes`: Com `-v` però només informa quan es fa un canvi
- `-f, --silent`: No mostra la majoria d'errors
- `--reference=ARXIU_REF`: Utilitza el grup de l'ARXIU_REF en lloc d'especificar un valor de GRUP

## Exemples

### Canviar el grup d'un arxiu

```bash
chgrp estudiants document.txt
```

Aquest comandament canvia el grup propietari de `document.txt` a `estudiants`.

### Canviar el grup recursivament

```bash
chgrp -R professors projecte/
```

Canvia el grup propietari del directori `projecte/` i tots els seus arxius i subdirectoris al grup `professors`.

### Canviar el grup utilitzant un arxiu de referència

```bash
chgrp --reference=arxiu1.txt arxiu2.txt
```

Canvia el grup d'`arxiu2.txt` al mateix grup que té `arxiu1.txt`.

### Mostrar els canvis realitzats

```bash
chgrp -v estudiants *.pdf
```

Canvia el grup de tots els arxius PDF a `estudiants` i mostra els canvis realitzats.

## Notes importants

- Per canviar el grup d'un arxiu necessites ser el propietari de l'arxiu o tenir permisos de superusuari (root).
- El grup especificat ha d'existir al sistema.
- Pots utilitzar tant el nom del grup com l'ID numèric del grup.
- Si vols veure els grups existents al sistema, pots utilitzar el comandament `cat /etc/group`.
- Per veure el grup actual d'un arxiu, utilitza `ls -l`.
