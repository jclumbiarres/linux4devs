# GRUB2 - GRand Unified Bootloader, versió 2

## Descripció

GRUB2 és el carregador d'arrencada predeterminat utilitzat per la majoria de distribucions GNU/Linux. És l'encarregat d'iniciar el sistema operatiu quan engeguem l'ordinador.

## Estructura i fitxers principals

- `/boot/grub/` - Directori principal de GRUB2
- `/boot/grub/grub.cfg` - Fitxer de configuració principal (no s'hauria d'editar directament)
- `/etc/default/grub` - Fitxer de configuració d'usuari
- `/etc/grub.d/` - Scripts que generen la configuració

## Comandes bàsiques

### Actualitzar la configuració de GRUB2

```bash
sudo update-grub
```

o

```bash
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

### Instal·lar GRUB2 en un disc

```bash
sudo grub-install /dev/sdX  # On sdX és el dispositiu (per exemple, /dev/sda)
```

## Paràmetres de configuració comuns

En el fitxer `/etc/default/grub` pots modificar diferents opcions:

```bash
GRUB_DEFAULT=0                   # Entrada predeterminada a carregar
GRUB_TIMEOUT=5                   # Temps d'espera en segons
GRUB_CMDLINE_LINUX=""            # Paràmetres addicionals per al kernel
GRUB_TIMEOUT_STYLE="menu"        # Estil del menú (hidden, menu, countdown)
GRUB_DISABLE_OS_PROBER=false     # Habilita la detecció d'altres sistemes
```

## Personalització

### Canviar el tema

1. Instal·la un tema:

```bash
sudo apt install grub2-themes-ubuntu
```

2. Edita `/etc/default/grub`:

```bash
GRUB_THEME="/path/to/theme.txt"
```

3. Actualitza GRUB:

```bash
sudo update-grub
```

### Afegir entrada personalitzada

Crea un fitxer a `/etc/grub.d/40_custom` amb una estructura com aquesta:

```bash
menuentry "Nom personalitzat" {
    set root=(hdX,Y)
    linux /vmlinuz root=/dev/sdaZ
    initrd /initrd.img
}
```

## Recuperació en cas d'error

Si GRUB2 falla, pots iniciar en mode recuperació:

1. Reinicia l'ordinador
2. Prem ESC o Shift durant l'arrencada per mostrar el menú GRUB
3. Selecciona l'opció de recuperació o mode de rescat

Des del mode de recuperació pots reparar GRUB:

```bash
sudo grub-install /dev/sdX
sudo update-grub
```
