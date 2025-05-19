# Comandament `sysctl`

## Introducció

El comandament `sysctl` és una eina de gestió de sistema que permet visualitzar, establir i modificar els paràmetres del nucli (kernel) de Linux en temps d'execució. Aquests paràmetres es troben al sistema de fitxers virtual `/proc/sys/` i controlen diversos aspectes del comportament del sistema operatiu.

## Sintaxi bàsica

```bash
sysctl [opcions] [variable[=valor]] [...]
```

## Principals opcions

| Opció            | Descripció                                                            |
| ---------------- | --------------------------------------------------------------------- |
| `-a`, `--all`    | Mostra tots els paràmetres disponibles                                |
| `-e`, `--ignore` | Ignora els errors en cas que una variable no existeixi                |
| `-n`, `--values` | Mostra només els valors (sense els noms de variables)                 |
| `-w`, `--write`  | Estableix un nou valor per a una variable                             |
| `-p[FITXER]`     | Carrega els paràmetres des d'un fitxer (per defecte /etc/sysctl.conf) |
| `-q`, `--quiet`  | No mostra els valors establerts                                       |
| `-f`             | Alias per l'opció -p                                                  |
| `-h`, `--help`   | Mostra l'ajuda                                                        |

## Fitxers de configuració

Els paràmetres permanents del sistema es configuren en els següents fitxers:

- `/etc/sysctl.conf`: Fitxer de configuració tradicional
- `/etc/sysctl.d/*.conf`: Directori amb fitxers de configuració addicionals

## Estructura dels paràmetres

Els paràmetres s'estructuren en grups jeràrquics com:

- `kernel`: Paràmetres del nucli
- `net`: Paràmetres de xarxa
- `fs`: Paràmetres del sistema de fitxers
- `vm`: Paràmetres de la memòria virtual

## Exemples d'ús

### Mostrar tots els paràmetres

```bash
sysctl -a
```

### Consultar un paràmetre específic

```bash
sysctl net.ipv4.ip_forward
```

### Modificar un paràmetre temporalment

```bash
sysctl -w net.ipv4.ip_forward=1
```

### Aplicar canvis des d'un fitxer de configuració

```bash
sysctl -p /etc/sysctl.conf
```

## Paràmetres comuns i la seva utilitat

### Paràmetres de xarxa

| Paràmetre                       | Descripció                                           |
| ------------------------------- | ---------------------------------------------------- |
| `net.ipv4.ip_forward`           | Activa/desactiva l'encaminament IP                   |
| `net.ipv4.icmp_echo_ignore_all` | Ignora tots els pings ICMP                           |
| `net.ipv4.tcp_syncookies`       | Activa/desactiva la protecció contra atacs SYN flood |

### Paràmetres de memòria

| Paràmetre               | Descripció                                                                                     |
| ----------------------- | ---------------------------------------------------------------------------------------------- |
| `vm.swappiness`         | Controla la tendència del sistema a utilitzar l'swap                                           |
| `vm.dirty_ratio`        | Percentatge màxim de memòria amb pàgines brutes abans de sincronitzar                          |
| `vm.vfs_cache_pressure` | Controla la tendència del kernel a recuperar memòria utilitzada per la caché d'inodes/dentries |

### Paràmetres del kernel

| Paràmetre         | Descripció                                                |
| ----------------- | --------------------------------------------------------- |
| `kernel.hostname` | Nom de l'equip                                            |
| `kernel.panic`    | Temps en segons abans de reiniciar en cas de kernel panic |
| `kernel.pid_max`  | Valor màxim d'ID de processos                             |

## Canvis permanents

Per fer canvis permanents, cal editar els fitxers de configuració:

```bash
echo "net.ipv4.ip_forward=1" >> /etc/sysctl.conf
```

I aplicar els canvis:

```bash
sysctl -p
```

O, millor encara, crear un fitxer nou al directori de configuració:

```bash
echo "net.ipv4.ip_forward=1" > /etc/sysctl.d/99-custom.conf
sysctl --system
```

## Consideracions de seguretat

Cal tenir precaució en modificar paràmetres del kernel, ja que alguns canvis poden:

- Comprometre la seguretat del sistema
- Afectar l'estabilitat i rendiment
- Causar un comportament impredictible

És recomanable documentar-se sobre cada paràmetre abans de modificar-lo i provar els canvis en entorns no productius.
