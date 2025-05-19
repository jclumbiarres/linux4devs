# Runlevels en GNU/Linux

## Introducció

Els runlevels en GNU/Linux són estats del sistema que defineixen quins serveis estan actius i quins no. Cada runlevel té un propòsit específic i permet controlar quins programes i serveis s'inicien automàticament quan el sistema arrenca.

## Concepte bàsic

Un runlevel es pot entendre com un "mode d'operació" del sistema. Cada nivell té una configuració diferent que determina quins serveis s'executen. Per exemple, un runlevel pot estar configurat per a un entorn gràfic complet, mentre que un altre pot estar dissenyat només per a ús en mode text.

## Runlevels tradicionals

En sistemes GNU/Linux tradicionals (especialment els basats en SysVinit), hi ha 7 runlevels estàndard:

| Runlevel | Descripció                                                    |
| -------- | ------------------------------------------------------------- |
| 0        | Halt (aturada del sistema)                                    |
| 1        | Mode monousuari (només per a manteniment)                     |
| 2        | Mode multiusuari sense xarxa                                  |
| 3        | Mode multiusuari complet amb xarxa (sense interfície gràfica) |
| 4        | No utilitzat / Personalitzable                                |
| 5        | Mode multiusuari complet amb xarxa i interfície gràfica       |
| 6        | Reinici del sistema                                           |

## Comandes relacionades amb els runlevels

### Verificar el runlevel actual

```bash
runlevel
```

o

```bash
who -r
```

### Canviar el runlevel

Per canviar immediatament a un altre runlevel:

```bash
init [número_de_runlevel]
```

Per exemple, per passar al runlevel 3 (mode text):

```bash
sudo init 3
```

## Systemd i els Target Units

En sistemes moderns que utilitzen systemd (com Ubuntu, Fedora, Debian modern, etc.), els runlevels tradicionals han estat substituïts per "target units", encara que es manté compatibilitat amb els runlevels antics:

| Runlevel | Target Systemd    | Descripció            |
| -------- | ----------------- | --------------------- |
| 0        | poweroff.target   | Aturada del sistema   |
| 1        | rescue.target     | Mode monousuari       |
| 2, 3, 4  | multi-user.target | Mode text multiusuari |
| 5        | graphical.target  | Mode gràfic           |
| 6        | reboot.target     | Reinici del sistema   |

### Comandes amb systemd

Verificar el target actual:

```bash
systemctl get-default
```

Canviar el target per defecte:

```bash
sudo systemctl set-default multi-user.target  # Per a mode text
sudo systemctl set-default graphical.target   # Per a mode gràfic
```

Canviar temporalment de target:

```bash
sudo systemctl isolate multi-user.target  # Canvia al mode text
```

## Configuració dels serveis per runlevel

### En sistemes SysVinit tradicionals

En sistemes que utilitzen SysVinit, els serveis s'inicien o s'aturen en funció del runlevel mitjançant scripts ubicats a directoris específics:

```
/etc/rc[0-6].d/
```

Dins d'aquests directoris, els scripts comencen amb "S" per iniciar un servei i amb "K" per aturar-lo.

### En sistemes amb systemd

En systemd, els serveis es configuren mitjançant arxius .service i s'enllacen a targets específics:

```bash
sudo systemctl enable [servei]  # Habilita un servei per iniciar-se amb el sistema
sudo systemctl disable [servei] # Desactiva l'inici automàtic
```

## Exemples pràctics

### Reiniciar el sistema

```bash
sudo init 6
```

o amb systemd:

```bash
sudo systemctl isolate reboot.target
```

### Canviar a mode text (runlevel 3)

```bash
sudo init 3
```

o amb systemd:

```bash
sudo systemctl isolate multi-user.target
```

## Consells

- Utilitza `runlevel` o `systemctl get-default` per saber en quin nivell d'execució es troba el sistema actualment.
- El runlevel 1 (mode de recuperació) és útil quan tens problemes i necessites reparar el sistema.
- En sistemes moderns, és preferible utilitzar les comandes systemd en lloc de les tradicionals.
- Mai canviïs al runlevel 0 o 6 sense estar preparat per a una aturada o reinici del sistema.

Conèixer els runlevels és fonamental per gestionar serveis en GNU/Linux i per solucionar problemes quan el sistema no arrenca correctament.
