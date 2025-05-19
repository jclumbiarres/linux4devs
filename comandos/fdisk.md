# fdisk - Eina de gestió de particions del disc

## Introducció

`fdisk` és una eina de línia de comandes que permet gestionar les particions dels discs durs i altres dispositius d'emmagatzematge en sistemes GNU/Linux. Amb aquesta utilitat pots crear, eliminar, modificar i visualitzar les taules de particions dels teus dispositius.

## Sintaxi bàsica

```bash
fdisk [opcions] dispositiu
```

On `dispositiu` és la ruta al dispositiu d'emmagatzematge que vols gestionar (per exemple, `/dev/sda`).

## Opcions principals

| Opció | Descripció                                                          |
| ----- | ------------------------------------------------------------------- |
| `-l`  | Llista les taules de particions de tots els dispositius disponibles |
| `-s`  | Mostra la mida d'un dispositiu o partició específica                |
| `-b`  | Especifica la mida del sector (normalment 512 bytes)                |
| `-u`  | Mostra les unitats en sectors en lloc de cilindres                  |

## Comandes interactives

Quan executes `fdisk` amb un dispositiu, entres en un mode interactiu. Aquí tens les comandes més comunes:

| Comanda | Descripció                                                |
| ------- | --------------------------------------------------------- |
| `m`     | Mostra el menú d'ajuda amb totes les comandes disponibles |
| `p`     | Mostra la taula de particions actual                      |
| `n`     | Crea una nova partició                                    |
| `d`     | Elimina una partició                                      |
| `t`     | Canvia el tipus de partició                               |
| `w`     | Escriu els canvis al disc i surt                          |
| `q`     | Surt sense guardar els canvis                             |
| `l`     | Llista els tipus de particions coneguts                   |

## Exemples d'ús

### Mostrar informació de totes les particions

```bash
sudo fdisk -l
```

### Gestionar les particions d'un disc específic

```bash
sudo fdisk /dev/sda
```

### Crear una nova partició

```bash
sudo fdisk /dev/sda
# Dins del mode interactiu
Command (m for help): n
# Segueix les instruccions per definir el tipus de partició, número, mida, etc.
# Al finalitzar, guarda els canvis
Command (m for help): w
```

## Advertències

- **Cal tenir permisos de superusuari** (root) per executar `fdisk`.
- **Molt important**: Qualsevol error en modificar les particions pot ocasionar pèrdua de dades. És recomanable fer còpies de seguretat abans d'utilitzar aquesta eina.
- Els canvis no s'apliquen fins que s'utilitza la comanda `w` per escriure al disc.
- Si el disc està sent utilitzat pel sistema, pot ser necessari reiniciar perquè els canvis tinguin efecte.

## Exemples avançats

### Canviar el tipus d'una partició

```bash
sudo fdisk /dev/sda
Command (m for help): t
Partition number (1-4): 1
Hex code (type L to list all codes): 83
Changed type of partition 'Linux' to 'Linux'.
Command (m for help): w
```

### Eliminar una partició

```bash
sudo fdisk /dev/sda
Command (m for help): d
Partition number (1-4): 2
Partition 2 has been deleted.
Command (m for help): w
```
