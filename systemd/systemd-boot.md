# Guía de SystemD-Boot

El SystemD-Boot (anteriorment anomenat gummiboot) és un gestor d'arrencada simple dissenyat per a sistemes amb UEFI. A diferència de GRUB2, SystemD-Boot està específicament orientat a sistemes moderns amb UEFI i està integrat amb el sistema systemd.

## Què és SystemD-Boot?

SystemD-Boot és un gestor d'arrencada minimalista que permet escollir entre diferents sistemes operatius o kernels durant l'inici del sistema. Algunes característiques destacades:

- Només funciona en sistemes amb UEFI
- És molt més lleuger i ràpid que GRUB2
- Està dissenyat per ser simple i fàcil de configurar
- Forma part del projecte systemd

## Instal·lació

Per instal·lar SystemD-Boot en una distribució basada en systemd:

```bash
# Primer, confirmar que estem en mode UEFI
ls /sys/firmware/efi/efivars

# Instal·lar systemd-boot a la partició EFI
bootctl install
```

## Configuració bàsica

La configuració es troba a `/boot/loader/`:

1. **loader.conf**: Configuració general del carregador
2. **entries/**: Directori amb les entrades d'arrencada

### Exemple de loader.conf

```
default arch.conf
timeout 3
editor 0
```

### Exemple d'entrada d'arrencada (arch.conf)

```
title Arch Linux
linux /vmlinuz-linux
initrd /initramfs-linux.img
options root=PARTUUID=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx rw
```

## Comandes útils

```bash
# Instal·lar systemd-boot
bootctl install

# Actualitzar systemd-boot
bootctl update

# Mostrar l'estat actual
bootctl status

# Mostrar les entrades disponibles
bootctl list
```

## Avantatges respecte a GRUB2

- **Més ràpid**: Inicia el sistema més ràpidament
- **Més simple**: Configuració molt més senzilla d'entendre
- **Millor integració**: S'integra perfectament amb systemd
- **Menys problemes**: En ser més simple, té menys possibilitats de fallar

## Limitacions

- Només funciona en sistemes UEFI
- No suporta sistemes amb Legacy BIOS
- Té menys opcions i flexibilitat que GRUB2

Si utilitzes un sistema modern amb UEFI, SystemD-Boot és una excel·lent alternativa a GRUB2, especialment si prefereixes un gestor d'arrencada simple, ràpid i amb una configuració mínima.
