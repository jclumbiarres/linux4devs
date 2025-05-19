# El Sistema de Fitxers Proc (ProcFS) a Linux

El sistema de fitxers `/proc` és una característica especial de Linux que proporciona una interfície per accedir a la informació del sistema i dels processos en execució. Tot i que sembla un directori normal, en realitat és un sistema de fitxers virtual que existeix només en memòria.

## Què és `/proc`?

`/proc` és un pseudo-sistema de fitxers que permet accedir a la informació del kernel i dels processos en forma de fitxers de text. No ocupa espai real al disc dur.

## Informació bàsica

Per veure el contingut de `/proc`:

```bash
ls /proc
```

Obtindràs una llista que inclou:

- Números: són directoris que representen els processos en execució (cada número és un PID)
- Directoris especials: ofereixen informació sobre diversos aspectes del sistema

## Fitxers i directoris importants

### Informació de processos

Cada procés té el seu propi directori amb el seu PID:

```bash
ls /proc/1234  # On 1234 és el PID d'un procés
```

Dins d'aquest directori trobaràs:

- `cmdline`: La línia de comandes amb què es va iniciar el procés
- `environ`: Les variables d'entorn del procés
- `status`: Estat del procés
- `fd/`: Directori amb els descriptors de fitxer oberts

### Informació del sistema

Alguns fitxers útils:

- `/proc/cpuinfo`: Informació sobre la CPU
- `/proc/meminfo`: Informació sobre la memòria
- `/proc/version`: Versió del kernel
- `/proc/uptime`: Temps d'execució del sistema
- `/proc/loadavg`: Càrrega mitjana del sistema

## Exemples pràctics

### Consultar informació de memòria:

```bash
cat /proc/meminfo
```

### Veure informació de la CPU:

```bash
cat /proc/cpuinfo
```

### Consultar el temps d'execució del sistema:

```bash
cat /proc/uptime
```

### Examinar un procés específic:

```bash
cat /proc/$(pidof firefox)/status
```

## Per què és útil?

- **Monitoratge del sistema**: Moltes eines com `top`, `htop` i `free` utilitzen `/proc`
- **Depuració**: Permet examinar l'estat dels processos
- **Administració del sistema**: Facilita l'accés a configuracions del kernel

## Consells addicionals

- És segur llegir de `/proc`, però cal anar amb compte en modificar els seus fitxers
- La majoria d'informació està en format text pla i es pot processar amb eines com `grep`, `awk`, etc.

Recorda que `/proc` és una finestra al funcionament intern del sistema operatiu i una eina valuosa per als administradors de sistemes i els desenvolupadors.
