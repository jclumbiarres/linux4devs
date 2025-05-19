# Comanda `blkid`

## Descripció

`blkid` és una comanda d'utilitat a GNU/Linux que serveix per identificar i mostrar informació sobre dispositius de bloc, com ara discs durs, particions, dispositius USB i altres suports d'emmagatzematge.

## Sintaxi

```bash
blkid [opcions] [dispositiu...]
```

## Opcions principals

- `-c fitxer`: Utilitza un fitxer de cache alternatiu.
- `-g`: Desactiva l'ús de la cache.
- `-o format`: Especifica el format de sortida (`value`, `device`, `list`, `udev`, `export`).
- `-s etiqueta`: Només mostra els dispositius que tenen l'etiqueta especificada.
- `-t nom=valor`: Cerca dispositius amb propietats específiques.
- `-L etiqueta`: Cerca un dispositiu amb l'etiqueta especificada.
- `-U uuid`: Cerca un dispositiu amb l'UUID especificat.
- `-p`: Mostra els resultats en un format llegible per a programes.

## Exemples d'ús

### Mostrar informació de tots els dispositius de bloc

```bash
blkid
```

### Mostrar informació d'un dispositiu específic

```bash
blkid /dev/sda1
```

### Cercar un dispositiu per UUID

```bash
blkid -U "5678-1234-abcd-ef01"
```

### Cercar un dispositiu per etiqueta

```bash
blkid -L "DADES"
```

### Mostrar només els tipus de sistema de fitxers

```bash
blkid -s TYPE
```

### Format llegible per a scripts

```bash
blkid -o export
```

## Explicació detallada

La comanda `blkid` forma part del paquet `util-linux` i actua com una interfície per a la biblioteca libblkid, que permet identificar i accedir a propietats dels dispositius de bloc. Això és especialment útil per:

1. **Identificació automàtica**: Determinar quin tipus de sistema de fitxers hi ha en una partició.
2. **Configuració de sistemes**: Facilitar la configuració del fitxer `/etc/fstab` utilitzant UUIDs o etiquetes en lloc de noms de dispositius que poden canviar.
3. **Scripts**: Els administradors de sistemes poden utilitzar aquesta eina en scripts per automatitzar tasques relacionades amb dispositius d'emmagatzematge.
4. **Resolució de problemes**: Identificar ràpidament particions i els seus formats.

La informació que mostra `blkid` inclou:

- **UUID**: Identificador únic universal del dispositiu.
- **LABEL**: Etiqueta del sistema de fitxers (si s'ha configurat).
- **TYPE**: Tipus de sistema de fitxers (ext4, ntfs, vfat, etc.).
- **PARTUUID**: Identificador de la partició.
- **PARTLABEL**: Etiqueta de la partició.

## Notes importants

- Per executar `blkid` amb totes les funcionalitats, normalment necessiteu permisos de superusuari (sudo).
- Els UUIDs són molt útils per identificar dispositius de forma consistent, ja que el nom del dispositiu (/dev/sdX) pot canviar segons l'ordre de connexió o arrencada.
- És una eina fonamental per configurar correctament el fitxer `/etc/fstab`.
