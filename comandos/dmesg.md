# Comanda `dmesg` a GNU/Linux

## Descripció

La comanda `dmesg` (diagnostic message) mostra els missatges del nucli (kernel) del sistema operatiu que es generen durant el procés d'arrencada i durant el funcionament del sistema. Aquests missatges inclouen informació sobre el maquinari detectat, errors, advertències i altres esdeveniments importants del sistema.

## Sintaxi bàsica

```bash
dmesg [opcions]
```

## Opcions principals

- `-c, --clear`: Neteja el buffer de missatges del kernel després de mostrar-los.
- `-f, --facility=LLISTA`: Restringeix la sortida a les instal·lacions especificades.
- `-H, --human`: Format de sortida llegible per a humans.
- `-k, --kernel`: Mostra missatges del kernel (comportament predeterminat).
- `-l, --level=LLISTA`: Restringeix la sortida als nivells especificats.
- `-n, --console-level=NIVELL`: Estableix el nivell dels missatges impresos a la consola.
- `-r, --raw`: Imprimeix el buffer de missatges en brut.
- `-s, --buffer-size=MIDA`: Mida del buffer a utilitzar.
- `-T, --ctime`: Mostra timestamps llegibles per humans.
- `-w, --follow`: Espera nous missatges (similar a `tail -f`).
- `-x, --decode`: Descodifica les instal·lacions i els nivells en text llegible.

## Exemples d'ús

### Visualitzar els missatges del kernel

```bash
dmesg
```

### Mostrar els missatges amb timestamps llegibles

```bash
dmesg -T
```

### Mostrar els missatges en format llegible per humans

```bash
dmesg -H
```

### Filtrar missatges per nivell (per exemple, errors)

```bash
dmesg --level=err
```

### Seguir els nous missatges en temps real

```bash
dmesg -w
```

### Mostrar només els missatges relacionats amb USB

```bash
dmesg | grep USB
```

## Nivells de prioritat

Els missatges de `dmesg` es classifiquen en diferents nivells de prioritat:

- `emerg` (0): El sistema està inutilitzable
- `alert` (1): Cal actuar immediatament
- `crit` (2): Condicions crítiques
- `err` (3): Condicions d'error
- `warn` (4): Condicions d'advertència
- `notice` (5): Normal però significatiu
- `info` (6): Informatiu
- `debug` (7): Missatges de depuració

## Casos d'ús habituals

- Diagnòstic de problemes de maquinari
- Identificació d'errors durant l'arrencada del sistema
- Detecció de problemes amb controladors de dispositius
- Seguiment dels missatges del sistema en temps real
- Inspecció d'errors de sistema relacionats amb la memòria, CPU o dispositius perifèrics

## Observacions

- El buffer de `dmesg` té una mida limitada, per la qual cosa els missatges antics poden ser sobreescrits.
- És necessari tenir permisos de superusuari (root) per executar algunes opcions de `dmesg`.
- Els missatges de `dmesg` es guarden també al directori `/var/log/`, especialment a `/var/log/kern.log`.
- Des de la versió del kernel 3.5.0, cal tenir permisos administratius o el capability `CAP_SYSLOG` per veure tots els missatges.

## Comparació amb altres eines

A diferència d'altres eines de registre com `journalctl`, `dmesg` es centra específicament en els missatges del nucli, mentre que `journalctl` proporciona accés a logs de tot el sistema, inclosos serveis i aplicacions.
