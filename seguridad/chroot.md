# Chroot: Aïllament i Seguretat en GNU/Linux

## Introducció a Chroot

Chroot (Change Root) és una operació en sistemes GNU/Linux que canvia el directori arrel aparent per un procés i els seus fills. Aquesta tècnica permet crear un entorn aïllat dins del sistema operatiu, limitat a una part específica del sistema de fitxers.

## Conceptes Bàsics

### Què significa "canviar el directori arrel"?

En GNU/Linux, tot comença des del directori arrel `/`. Quan s'executa un chroot, es modifica aquesta referència perquè el procés i tots els seus fills vegin com a directori arrel un subdirectori del sistema real.

### Diferències amb una màquina virtual

- **Chroot**: Comparteix el mateix kernel, només aïlla el sistema de fitxers.
- **Màquina Virtual**: Emula hardware complet amb el seu propi kernel.

## Usos Principals de Chroot

### 1. Recuperació del Sistema

Quan un sistema no arrenca correctament, podem usar chroot per accedir al sistema des d'un Live CD/USB i reparar-lo.

### 2. Entorns de Desenvolupament

Crear entorns aïllats per desenvolupar i provar aplicacions sense afectar el sistema principal.

### 3. Seguretat

Limitar el que un servei o aplicació pot accedir dins del sistema de fitxers.

### 4. Actualitzacions i Manteniment

Realitzar actualitzacions o manteniment en un sistema sense necessitat d'arrencar-lo completament.

## Crear un Entorn Chroot Pas a Pas

### Preparació de l'Entorn

1. Crear el directori que servirà com a nova arrel:

```bash
mkdir -p /ruta/al/meu_chroot
```

2. Instal·lar els paquets bàsics necessaris (exemple per a distribucions basades en Debian):

```bash
debootstrap --arch=amd64 bullseye /ruta/al/meu_chroot http://deb.debian.org/debian
```

### Muntar Sistemes de Fitxers Virtuals

Abans d'entrar al chroot, cal muntar alguns sistemes de fitxers virtuals:

```bash
mount -t proc proc /ruta/al/meu_chroot/proc
mount -t sysfs sys /ruta/al/meu_chroot/sys
mount -o bind /dev /ruta/al/meu_chroot/dev
mount -o bind /dev/pts /ruta/al/meu_chroot/dev/pts
```

### Entrar a l'Entorn Chroot

```bash
chroot /ruta/al/meu_chroot /bin/bash
```

### Configurar l'Entorn Básic

Un cop dins de l'entorn chroot, cal configurar alguns elements bàsics:

1. Configurar xarxa (còpia del fitxer resolv.conf):

```bash
cp /etc/resolv.conf /ruta/al/meu_chroot/etc/resolv.conf
```

2. Actualitzar repositoris:

```bash
apt update
```

## Limitacions de Seguretat de Chroot

### El que Chroot NO fa

- **No limita l'accés a recursos del sistema**: CPU, memòria, dispositius.
- **No impedeix l'accés a dispositius**: Encara es pot accedir als dispositius del sistema.
- **No protegeix contra usuaris amb privilegis**: Un usuari root dins d'un chroot pot escapar-se.

### Escapar d'un Chroot (per què cal ser cautelós)

Un usuari amb privilegis de root podria escapar-se d'un chroot utilitzant diverses tècniques, per exemple:

- Creant dispositius especials dins del chroot
- Utilitzant crides al sistema específiques
- Explotant vulnerabilitats del kernel

## Millores de Seguretat per a Chroot

### Combinació amb altres tecnologies

- **Capabilities**: Limitar els privilegis dins del chroot.
- **Namespaces**: Aïllar més recursos que només el sistema de fitxers.
- **Seccomp**: Restringir les crides al sistema disponibles.

## Pràctica: Casos d'Ús Detallats

### Cas 1: Reparació d'un Sistema que no Arrenca

1. Arrencar des d'un Live CD/USB
2. Identificar les particions del sistema:

```bash
lsblk
fdisk -l
```

3. Muntar la partició arrel del sistema:

```bash
mount /dev/sdaX /mnt
```

4. Muntar altres particions necessàries (/boot, /home, etc.):

```bash
mount /dev/sdaY /mnt/boot
mount /dev/sdaZ /mnt/home
```

5. Muntar sistemes de fitxers virtuals:

```bash
mount -t proc proc /mnt/proc
mount -t sysfs sys /mnt/sys
mount -o bind /dev /mnt/dev
mount -o bind /dev/pts /mnt/dev/pts
```

6. Entrar al chroot:

```bash
chroot /mnt /bin/bash
```

7. Realitzar reparacions (per exemple, reconfigurando GRUB):

```bash
grub-install /dev/sda
update-grub
```

8. Sortir i desmuntar:

```bash
exit
umount -R /mnt
```

### Cas 2: Creació d'un Entorn de Desenvolupament Aïllat

1. Crear el directori base:

```bash
mkdir -p ~/chroot_dev
```

2. Instal·lar sistema base:

```bash
debootstrap --arch=amd64 bullseye ~/chroot_dev http://deb.debian.org/debian
```

3. Configurar l'entorn de desenvolupament:

```bash
chroot ~/chroot_dev /bin/bash
apt update
apt install build-essential git cmake python3 python3-pip
```

4. Configurar carpetes compartides:

```bash
mkdir -p ~/chroot_dev/projectes
mount -o bind ~/projectes ~/chroot_dev/projectes
```

### Cas 3: Executar Aplicacions en Sandbox

1. Crear un chroot mínim:

```bash
mkdir -p ~/sandbox
debootstrap --variant=minbase --arch=amd64 bullseye ~/sandbox http://deb.debian.org/debian
```

2. Instal·lar només els paquets necessaris:

```bash
chroot ~/sandbox /bin/bash
apt update
apt install firefox-esr dbus-x11
```

3. Executar aplicacions gràfiques des del chroot:

```bash
xhost +local:
chroot ~/sandbox /bin/bash -c "export DISPLAY=:0 && firefox-esr"
```

## Alternatives Modernes a Chroot

### 1. Contenidors (Docker, LXC)

Els contenidors ofereixen un aïllament més complet que chroot, incloent:

- Aïllament de xarxa
- Control de recursos (CPU, memòria)
- Millor seguretat

Exemple bàsic de Docker:

```bash
docker run -it debian:bullseye bash
```

### 2. Namespaces de Linux

Els namespaces permeten aïllar diferents aspectes del sistema:

- Espai de noms PID
- Espai de noms de xarxa
- Espai de noms de muntatge

Exemple amb `unshare`:

```bash
unshare --fork --pid --mount-proc bash
```

### 3. Firejail

Eina específica per executar aplicacions en un entorn sandbox:

```bash
firejail firefox
```

## Administració Avançada de Chroot

### Gestió de Múltiples Entorns Chroot

Crear un script per gestionar diferents entorns chroot:

```bash
#!/bin/bash
CHROOT_BASE="/var/chroots"

case "$1" in
    create)
        mkdir -p "$CHROOT_BASE/$2"
        debootstrap --arch=amd64 bullseye "$CHROOT_BASE/$2" http://deb.debian.org/debian
        ;;
    enter)
        mount -t proc proc "$CHROOT_BASE/$2/proc"
        mount -t sysfs sys "$CHROOT_BASE/$2/sys"
        mount -o bind /dev "$CHROOT_BASE/$2/dev"
        mount -o bind /dev/pts "$CHROOT_BASE/$2/dev/pts"
        chroot "$CHROOT_BASE/$2" /bin/bash
        ;;
    exit)
        umount -R "$CHROOT_BASE/$2/proc"
        umount -R "$CHROOT_BASE/$2/sys"
        umount -R "$CHROOT_BASE/$2/dev/pts"
        umount -R "$CHROOT_BASE/$2/dev"
        ;;
    list)
        ls -la "$CHROOT_BASE"
        ;;
    *)
        echo "Ús: $0 {create|enter|exit|list} [nom_chroot]"
        exit 1
        ;;
esac
```

### Automatització amb Systemd

Crear serveis systemd per gestionar entorns chroot:

```
[Unit]
Description=Servei Chroot per a %i
After=network.target

[Service]
Type=forking
ExecStart=/usr/local/bin/chroot_manager enter %i
ExecStop=/usr/local/bin/chroot_manager exit %i
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target
```

## Solució de Problemes Comuns

### Problema 1: "Command not found" dins del chroot

Assegurar-se que els paquets essencials estiguin instal·lats:

```bash
apt install coreutils bash
```

### Problema 2: Problemes de DNS

Copiar la configuració DNS:

```bash
cp /etc/resolv.conf /ruta/al/meu_chroot/etc/resolv.conf
```

### Problema 3: No es poden muntar sistemes de fitxers

Assegurar-se de tenir els privilegis adequats i que els directoris de muntatge existeixen:

```bash
mkdir -p /ruta/al/meu_chroot/{proc,dev,sys}
```

### Problema 4: Errors de localització (locale)

Generar i configurar locales:

```bash
apt install locales
dpkg-reconfigure locales
```

## Projectes Pràctics amb Chroot

### Projecte 1: Servidor Web Aïllat

1. Crear un chroot per a Apache:

```bash
mkdir -p /var/chroot/apache
debootstrap --arch=amd64 bullseye /var/chroot/apache http://deb.debian.org/debian
```

2. Instal·lar Apache dins del chroot:

```bash
chroot /var/chroot/apache /bin/bash
apt update
apt install apache2
```

3. Configurar Apache perquè s'executi dins del chroot amb un usuari no privilegiat:

```bash
# Configuració del servei systemd per executar Apache en chroot
```

### Projecte 2: Entorn Multi-Distribució

Crear diferents entorns chroot per a diverses distribucions:

```bash
# Debian
debootstrap bullseye /var/chroot/debian http://deb.debian.org/debian

# Ubuntu
debootstrap focal /var/chroot/ubuntu http://archive.ubuntu.com/ubuntu

# Arch Linux (requereix arch-bootstrap)
arch-bootstrap /var/chroot/arch
```

### Projecte 3: Entorn de Compilació Creuat

Crear un entorn chroot per compilar per a arquitectures diferents:

```bash
# Instal·lar eina per a compilació creuada
apt install qemu-user-static binfmt-support

# Crear chroot per a ARM
debootstrap --arch=arm64 --foreign bullseye /var/chroot/arm64 http://deb.debian.org/debian

# Copiar qemu-arm-static
cp /usr/bin/qemu-aarch64-static /var/chroot/arm64/usr/bin/

# Completar instal·lació
chroot /var/chroot/arm64 /usr/bin/qemu-aarch64-static /bin/bash -c "/debootstrap/debootstrap --second-stage"
```

## Implicacions Legals i Ètiques

### Consideracions de Llicències

Quan creem entorns chroot amb diferents distribucions, cal respectar les llicències:

- Distribucions amb llicències lliures (GPL, etc.)
- Software propietari dins del chroot

### Aspectes de Seguretat i Privacitat

- No utilitzar chroot com a única mesura de seguretat
- Considerar les implicacions de privacitat a l'aïllar aplicacions

## Optimització i Rendiment

### Minimitzar l'Espai en Disc

```bash
# Instal·lar només el necessari
debootstrap --variant=minbase --include=apt bullseye /chroot http://deb.debian.org/debian

# Netejar cache d'APT després d'instal·lar paquets
apt clean
```

### Compartir Recursos entre Entorns Chroot

```bash
# Muntar directoris compartits en mode de només lectura
mount -o bind,ro /usr/share/common-licenses /chroot/usr/share/common-licenses
```

## Chroot en el Context d'Administració de Sistemes

### Integració amb Estratègies de Backup

Consideracions per fer backups d'entorns chroot:

```bash
# Exemple de backup amb tar
tar -czf /backup/chroot_backup.tar.gz -C /ruta/al/meu_chroot .
```

### Monitoratge d'Entorns Chroot

Eines i tècniques per supervisar processos dins d'un chroot:

```bash
# Identificar processos dins d'un chroot
ps auxf | grep /ruta/al/meu_chroot
```
