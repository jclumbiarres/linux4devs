# chown - Canviar el propietari i grup d'un fitxer

## Descripció

El comandament `chown` (Change Owner) s'utilitza per canviar el propietari i/o el grup d'un fitxer o directori.

## Sintaxi

```
chown [opcions] propietari[:grup] fitxer...
```

## Opcions comunes

- `-R, --recursive`: Canvia recursivament els propietaris dels directoris i els seus continguts.
- `-v, --verbose`: Mostra un diagnòstic per a cada fitxer processat.
- `-c, --changes`: Com `--verbose` però només informa quan es fa un canvi.
- `--reference=FITXER_REF`: Utilitza el propietari i grup del FITXER_REF enlloc dels valors especificats.
- `-h, --no-dereference`: Afecta els enllaços simbòlics enlloc dels fitxers referenciats.

## Exemples

### Canviar el propietari d'un fitxer

```bash
chown joan fitxer.txt
```

Aquest comandament canvia el propietari del fitxer `fitxer.txt` a l'usuari `joan`.

### Canviar el propietari i el grup d'un fitxer

```bash
chown joan:desenvolupadors fitxer.txt
```

Canvia el propietari a `joan` i el grup a `desenvolupadors`.

### Canviar recursivament propietaris d'un directori

```bash
chown -R joan:desenvolupadors projecte/
```

Canvia el propietari i grup de `projecte/` i tots els fitxers i subdirectoris que conté.

### Canviar només el grup

```bash
chown :desenvolupadors fitxer.txt
```

Només canvia el grup del fitxer a `desenvolupadors`, deixant el propietari inalterat.

### Utilitzar un fitxer de referència

```bash
chown --reference=fitxer1.txt fitxer2.txt
```

Aplica el mateix propietari i grup de `fitxer1.txt` a `fitxer2.txt`.

## Notes importants

- Per utilitzar `chown` cal tenir privilegis d'administrador (root) o ser el propietari actual del fitxer.
- Els canvis de propietat poden afectar els permisos d'accés al fitxer.
- És important anar amb compte en utilitzar l'opció `-R` en directoris del sistema.
- Els noms d'usuari i grup poden ser especificats tant pel nom com pel seu ID numèric.
