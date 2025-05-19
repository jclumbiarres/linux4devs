# lsblk

## Descripció

El comandament `lsblk` (list block devices) s'utilitza per a mostrar informació sobre tots els dispositius de bloc disponibles en el sistema. Els dispositius de bloc són components d'emmagatzematge com discos durs, SSD, unitats USB i particions.

## Sintaxi

```bash
lsblk [opcions]
```

## Opcions principals

- `-a`, `--all`: Mostra tots els dispositius, inclosos els buits.
- `-b`, `--bytes`: Mostra la mida en bytes en lloc d'en format humanament llegible.
- `-d`, `--nodeps`: No mostra les particions d'un dispositiu (només mostra el dispositiu principal).
- `-f`, `--fs`: Mostra informació sobre sistemes de fitxers.
- `-m`, `--perms`: Mostra els permisos dels dispositius.
- `-o`, `--output LIST`: Especifica quines columnes mostrar.
- `-p`, `--paths`: Mostra els noms complets dels dispositius.
- `-S`, `--scsi`: Mostra només dispositius SCSI.

## Exemples d'ús

### Mostrar tots els dispositius de bloc

```bash
lsblk
```

Aquest comandament mostrarà una llista estructurada en forma d'arbre de tots els dispositius de bloc, indicant la seva mida, tipus, punt de muntatge i altres informacions bàsiques.

### Mostrar informació detallada sobre sistemes de fitxers

```bash
lsblk -f
```

Mostra informació addicional com ara el tipus de sistema de fitxers, l'UUID i el punt de muntatge.

### Mostrar la mida en bytes

```bash
lsblk -b
```

Mostra la mida dels dispositius en bytes en lloc del format humanament llegible (com GB o MB).

### Mostrar columnes específiques

```bash
lsblk -o NAME,SIZE,TYPE,MOUNTPOINT
```

Aquest comandament mostra només les columnes especificades: nom, mida, tipus i punt de muntatge.

### Mostrar tots els dispositius amb rutes completes

```bash
lsblk -p
```

Mostra els noms dels dispositius amb rutes completes (ex: `/dev/sda` en lloc de `sda`).

## Sortida típica

La sortida de `lsblk` normalment s'organitza en columnes que mostren:

- **NAME**: Nom del dispositiu
- **MAJ:MIN**: Números major i menor del dispositiu
- **RM**: Si el dispositiu és extraïble (1) o no (0)
- **SIZE**: Mida total del dispositiu
- **RO**: Si el dispositiu és només de lectura (1) o no (0)
- **TYPE**: Tipus de dispositiu (disk, part, rom, etc.)
- **MOUNTPOINT**: El punt de muntatge del dispositiu

## Consells pràctics

- Utilitzeu `lsblk` abans de manipular particions per verificar quins dispositius i particions existeixen en el vostre sistema.
- Combineu-lo amb `sudo fdisk -l` per obtenir més detalls sobre les taules de particions.
- Per veure la utilització d'espai dels dispositius muntats, utilitzeu `df -h` en comptes d'aquest comandament.

## Exemple de sortida

```
NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
sda      8:0    0 119.2G  0 disk
├─sda1   8:1    0   512M  0 part /boot/efi
└─sda2   8:2    0 118.8G  0 part /
sdb      8:16   1   7.5G  0 disk
└─sdb1   8:17   1   7.5G  0 part /media/usb
```

En aquest exemple, es mostra un disc dur principal (`sda`) amb dues particions i una unitat USB (`sdb`) amb una partició.
