# Comando usermod

## Descripció

El comandament `usermod` (user modify) permet modificar diversos paràmetres dels comptes d'usuari existents en el sistema GNU/Linux. És una eina essencial per a l'administració dels usuaris dins del sistema operatiu.

## Sintaxi bàsica

```bash
usermod [opcions] usuari
```

## Opcions principals

- `-a, --append`: Afegir l'usuari a grups suplementaris. S'ha d'utilitzar juntament amb `-G`.
- `-c, --comment`: Modificar el camp de comentari (normalment el nom complet de l'usuari).
- `-d, --home DIRECTORI`: Establir un nou directori personal per a l'usuari.
- `-e, --expiredate DATA`: Establir la data d'expiració del compte (format AAAA-MM-DD).
- `-g, --gid GRUP`: Canviar el grup principal de l'usuari.
- `-G, --groups GRUPS`: Llista de grups suplementaris als quals pertany l'usuari (separats per comes).
- `-l, --login NOM`: Canviar el nom d'usuari.
- `-L, --lock`: Bloquejar el compte d'usuari.
- `-m, --move-home`: Moure el contingut del directori personal quan es canvia la ubicació.
- `-s, --shell SHELL`: Canviar l'intèrpret de comandes predeterminat de l'usuari.
- `-U, --unlock`: Desbloquejar el compte d'usuari.

## Exemples d'ús

### Canviar el directori personal d'un usuari

```bash
sudo usermod -d /home/nou_directori -m usuari
```

Aquest comandament canvia el directori personal de l'usuari a `/home/nou_directori` i mou tot el contingut del directori antic al nou.

### Afegir un usuari a més grups

```bash
sudo usermod -aG docker,developers usuari
```

Afegeix l'usuari als grups "docker" i "developers" sense eliminar-lo dels grups als quals ja pertanyia (gràcies a l'opció `-a`).

### Canviar el shell predeterminat

```bash
sudo usermod -s /bin/bash usuari
```

Aquest comandament canvia l'intèrpret de comandes de l'usuari a bash.

### Bloquejar i desbloquejar un compte

```bash
# Bloquejar
sudo usermod -L usuari

# Desbloquejar
sudo usermod -U usuari
```

### Canviar el nom d'un usuari

```bash
sudo usermod -l nou_nom antic_nom
```

Canvia el nom d'usuari d'"antic_nom" a "nou_nom".

## Notes importants

- Per executar `usermod` es necessiten permisos d'administrador (normalment amb `sudo`).
- Algunes modificacions no tenen efecte fins que l'usuari tanqui sessió i torni a iniciar-la.
- Si es canvia el nom d'usuari amb `-l`, els permisos dels fitxers no es modifiquen automàticament.
- És recomanable fer una còpia de seguretat abans de fer canvis significatius en els comptes d'usuari.
- No es pot modificar un usuari que està actualment amb sessió iniciada al sistema.
