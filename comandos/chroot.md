# `chroot`

## Descripció

El comando `chroot` (Change Root) permet canviar el directori arrel aparent per al procés actual i els seus fills. Això crea un entorn aïllat on el directori especificat esdevé la nova arrel del sistema (`/`), impedint l'accés als fitxers fora d'aquest entorn.

## Sintaxi

```bash
chroot [OPCIONS] DIRECTORI_NOU_ARREL [COMANDA [ARGS]...]
```

## Opcions principals

- `--userspec=USUARI:GRUP`: Especifica l'usuari i grup per executar la comanda
- `--groups=GRUPS`: Especifica grups suplementaris
- `--skip-chdir`: No canvia el directori de treball a `/`

## Exemples

### Exemple bàsic

```bash
sudo chroot /mnt/sistema_reparacio /bin/bash
```

Aquest comando canvia l'arrel al directori `/mnt/sistema_reparacio` i executa una shell bash dins d'aquest entorn.

### Reparar un sistema que no arrenca

```bash
sudo mount /dev/sda1 /mnt/sistema
sudo chroot /mnt/sistema
```

Per reparar un sistema, podem muntar la seva partició i fer chroot per treballar-hi com si haguéssim arrencat des d'ella.

### Crear un entorn de desenvolupament aïllat

```bash
sudo chroot /home/entorn_dev /usr/bin/make
```

Executa la comanda `make` dins d'un entorn aïllat.

## Importància per a administradors de sistemes

`chroot` és una eina fonamental per a sysadmins per diverses raons:

1. **Recuperació de sistemes**: Permet reparar sistemes que no arrenquen correctament accedint-hi des d'un Live CD/USB.
2. **Seguretat**: Pot aïllar processos en un entorn restringit per limitar el dany potencial.
3. **Proves**: Facilita provar aplicacions en entorns diferents sense afectar el sistema principal.
4. **Virtualització lleugera**: Ofereix una forma simple de virtualització a nivell de sistema de fitxers.

## Preparació d'un entorn chroot

Un entorn chroot necessita tots els fitxers essencials per funcionar:

```bash
# Crear directori pel chroot
mkdir -p /mnt/entorn_chroot

# Copiar o instal·lar eines bàsiques
cp -a /bin /lib /lib64 /usr /mnt/entorn_chroot/

# Muntar sistemes virtuals necessaris
mount --bind /proc /mnt/entorn_chroot/proc
mount --bind /sys /mnt/entorn_chroot/sys
mount --bind /dev /mnt/entorn_chroot/dev

# Entrar al chroot
chroot /mnt/entorn_chroot
```

## Notes importants

- Requereix permisos de superusuari (root)
- No és una mesura de seguretat completa per si sola
- Cal tenir tots els fitxers i directoris necessaris dins l'entorn chroot
- És la base de moltes tecnologies modernes de contenidors
