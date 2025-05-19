# LVM (Logical Volume Manager) a GNU/Linux

El Gestor de Volums Lògics (LVM) és una capa d'abstracció que permet una gestió més flexible de l'emmagatzematge en sistemes GNU/Linux. LVM permet redimensionar, moure i gestionar els volums d'emmagatzematge de manera dinàmica sense interrompre el servei del sistema.

## Conceptes bàsics

- **Volums físics (PV)**: Particions de disc o discos sencers que s'utilitzen en LVM.
- **Grups de volums (VG)**: Agrupació de volums físics que formen un "dipòsit" d'espai.
- **Volums lògics (LV)**: "Particions virtuals" creades dins d'un grup de volums, que poden ser redimensionades dinàmicament.

## Comandes bàsiques per gestionar LVM

### Gestió de volums físics

```bash
# Crear un volum físic a partir d'una partició o disc
pvcreate /dev/sdb1

# Mostrar informació dels volums físics
pvdisplay

# Llistar volums físics
pvs
```

### Gestió de grups de volums

```bash
# Crear un grup de volums
vgcreate nom_del_grup /dev/sdb1 /dev/sdc1

# Estendre un grup de volums
vgextend nom_del_grup /dev/sdd1

# Mostrar informació dels grups de volums
vgdisplay

# Llistar grups de volums
vgs
```

### Gestió de volums lògics

```bash
# Crear un volum lògic
lvcreate -L 10G -n nom_del_volum nom_del_grup

# Redimensionar un volum lògic (augmentar)
lvextend -L +5G /dev/nom_del_grup/nom_del_volum

# Redimensionar un volum lògic (reduir) - cal desconnectar-lo primer
lvreduce -L -5G /dev/nom_del_grup/nom_del_volum

# Mostrar informació dels volums lògics
lvdisplay

# Llistar volums lògics
lvs
```

### Formateig i muntatge

```bash
# Formatar un volum lògic
mkfs.ext4 /dev/nom_del_grup/nom_del_volum

# Muntar un volum lògic
mount /dev/nom_del_grup/nom_del_volum /punt_de_muntatge
```

## Aplicacions pràctiques

### Avantatges d'utilitzar LVM

1. **Flexibilitat**: Permet canviar la mida dels volums sense haver de reiniciar el sistema.
2. **Escalabilitat**: Es poden afegir nous discs i estendre els volums existents.
3. **Instantànies (snapshots)**: Permet crear còpies de seguretat consistents.
4. **Agregació de discs**: Es poden combinar múltiples discs per crear un únic espai d'emmagatzematge.

### Exemple d'ús comú

```bash
# 1. Crear volums físics
pvcreate /dev/sdb1 /dev/sdc1

# 2. Crear un grup de volums
vgcreate grup_dades /dev/sdb1 /dev/sdc1

# 3. Crear volums lògics
lvcreate -L 50G -n vol_home grup_dades
lvcreate -L 100G -n vol_var grup_dades

# 4. Formatar els volums lògics
mkfs.ext4 /dev/grup_dades/vol_home
mkfs.ext4 /dev/grup_dades/vol_var

# 5. Muntar els volums
mount /dev/grup_dades/vol_home /home
mount /dev/grup_dades/vol_var /var
```

## Consideracions addicionals

- **Còpies de seguretat**: Sempre feu còpies de seguretat abans de fer canvis importants a l'estructura LVM.
- **Espai lliure**: Deixeu sempre un marge d'espai lliure per facilitar la gestió i l'expansió.
- **Instantànies**: Les instantànies són útils, però consumeixen espai del grup de volums.
- **Redimensionar sistemes de fitxers**: Després d'ampliar un volum lògic, cal també ampliar el sistema de fitxers:
  ```bash
  resize2fs /dev/nom_del_grup/nom_del_volum
  ```

LVM és una eina potent que proporciona gran flexibilitat en la gestió d'emmagatzematge en sistemes GNU/Linux. Si bé requereix una mica més de configuració inicial, els avantatges a llarg termini en termes d'administració i flexibilitat són considerables.
