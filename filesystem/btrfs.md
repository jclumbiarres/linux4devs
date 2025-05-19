# Btrfs (B-tree File System)

Btrfs és un sistema de fitxers modern per a Linux que implementa la tècnica de **còpia en escriptura (Copy-on-Write o CoW)**. Està dissenyat per abordar limitacions de sistemes de fitxers anteriors, centrant-se en la tolerància a fallades, la reparació i la facilitat d'administració.

## Característiques Principals

- **Copy-on-Write (CoW):** En lloc de sobreescriure les dades directament, Btrfs escriu les dades modificades en una nova ubicació. Això millora la resistència a fallades durant les escriptures i permet funcionalitats com les instantànies.
- **Instantànies (Snapshots):** Permet crear còpies quasi instantànies i eficients en espai de l'estat del sistema de fitxers (o d'un subvolum) en un moment donat. Les instantànies poden ser de només lectura o escriptura.
- **Subvolums:** Btrfs pot dividir un únic sistema de fitxers en múltiples subvolums. Cada subvolum pot ser muntat i gestionat de forma independent, actuant com un sistema de fitxers separat però compartint l'espai subjacent.
- **RAID Integrat:** Suporta nivells RAID 0, 1, 10, 5 i 6 directament dins del sistema de fitxers, sense necessitat de `mdadm`.
- **Compressió Transparent:** Pot comprimir dades automàticament usant algoritmes com zlib, LZO o Zstandard (zstd), estalviant espai i potencialment millorant el rendiment en alguns casos.
- **Suma de Verificació (Checksums):** Emmagatzema sumes de verificació per a les dades i metadades per detectar corrupció (silent data corruption). Pot intentar reparar automàticament la corrupció si hi ha redundància (RAID 1/10/5/6).
- **Gestió d'Espai Flexible:** Permet afegir i eliminar dispositius d'un sistema de fitxers muntat, així com redimensionar-lo.

## Avantatges

- **Integritat de Dades:** Gràcies a CoW i checksums.
- **Flexibilitat:** Subvolums i gestió dinàmica de dispositius.
- **Eficiència d'Espai:** Instantànies i compressió.
- **Administració Simplificada:** Funcionalitats avançades integrades.

## Consideracions

- **Maduresa:** Encara que estable per a molts usos, algunes característiques (com RAID 5/6) han tingut problemes de fiabilitat en el passat (tot i que han millorat significativament).
- **Rendiment:** El CoW pot introduir certa sobrecàrrega i fragmentació en càrregues de treball específiques (p. ex., bases de dades, màquines virtuals sense configuració adequada).
- **Complexitat:** Pot ser més complex d'entendre i gestionar que sistemes de fitxers tradicionals com ext4.

## Comandes Bàsiques (Exemples)

```bash
# Formatar una partició com a Btrfs
sudo mkfs.btrfs /dev/sdXN

# Muntar el sistema de fitxers
sudo mount /dev/sdXN /mnt/btrfs_pool

# Crear un subvolum
sudo btrfs subvolume create /mnt/btrfs_pool/my_subvolume

# Crear una instantània (snapshot)
sudo btrfs subvolume snapshot /mnt/btrfs_pool/my_subvolume /mnt/btrfs_pool/my_snapshot

# Llistar subvolums
sudo btrfs subvolume list /mnt/btrfs_pool
```

Btrfs és una opció potent per a usuaris que busquen característiques avançades de gestió de dades i protecció contra la corrupció.
