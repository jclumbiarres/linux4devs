# Comanda `mount`

La comanda `mount` s'utilitza per muntar sistemes de fitxers. Muntar significa fer accessible un sistema de fitxers a través d'un directori específic (punt de muntatge) dins de l'estructura de directoris del sistema.

## Sintaxi bàsica

```bash
mount [opcions] dispositiu punt_de_muntatge
```

## Opcions comunes

- `-t tipus`: Especifica el tipus de sistema de fitxers (ext4, ntfs, vfat, etc.)
- `-o opcions`: Especifica opcions de muntatge addicionals
- `-a`: Munta tots els sistemes de fitxers definits al fitxer `/etc/fstab`
- `-r`: Munta el sistema de fitxers en mode només lectura
- `-w`: Munta el sistema de fitxers en mode lectura/escriptura (predeterminat)
- `-v`: Mode detallat (verbose)
- `-h`: Mostra l'ajuda

## Exemples d'ús

### Mostrar tots els sistemes de fitxers muntats

```bash
mount
```

### Muntar una unitat USB

```bash
sudo mount /dev/sdb1 /mnt/usb
```

### Muntar una imatge ISO

```bash
sudo mount -o loop imatge.iso /mnt/cdrom
```

### Muntar una partició NTFS amb suport complet

```bash
sudo mount -t ntfs-3g /dev/sda1 /mnt/windows
```

### Muntar amb opcions específiques

```bash
sudo mount -o remount,rw /
```

## Desmuntar sistemes de fitxers

Per desmuntar un sistema de fitxers, s'utilitza la comanda `umount`:

```bash
sudo umount /mnt/usb
```

## El fitxer `/etc/fstab`

Aquest fitxer conté informació sobre els sistemes de fitxers que s'han de muntar automàticament en iniciar el sistema. Cada línia representa un sistema de fitxers amb els següents camps:

```
dispositiu    punt_muntatge    tipus_sistema_fitxers    opcions    dump    pass
```

## Consideracions importants

- Cal tenir permisos d'administrador (sudo) per muntar la majoria de dispositius
- No es pot desmuntar un sistema de fitxers que està en ús
- Els sistemes de fitxers removibles (com USB) es munten automàticament en la majoria de distribucions modernes

## Consells per a principiants

- Abans de desconnectar qualsevol dispositiu, assegureu-vos de desmuntar-lo correctament amb `umount`
- Per veure quins dispositius estan disponibles per muntar, podeu utilitzar `lsblk` o `fdisk -l`
- Si rebeu errors de permisos, probablement necessitareu utilitzar `sudo`
