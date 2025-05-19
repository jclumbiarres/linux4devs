# journalctl: Explorant els registres de systemd

## Introducció

El `journalctl` és una eina de línia de comandes que permet explorar i gestionar els registres (logs) del sistema gestionats per systemd. Aquests registres contenen informació detallada sobre el funcionament del sistema, serveis, aplicacions i esdeveniments diversos.

## Funcionament bàsic

Systemd utilitza un sistema centralitzat de registres anomenat "journal" que emmagatzema els missatges en format binari, oferint avantatges com ara indexació ràpida, metadades estructurades i millor rendiment respecte als logs tradicionals.

## Comandes bàsiques

### Visualitzar tots els registres

```bash
journalctl
```

Això mostrarà tots els missatges del journal des de l'inici del sistema, ordenats del més antic al més recent.

### Veure els últims missatges

```bash
journalctl -f
```

Mostra els últims registres i segueix mostrant-los en temps real (similar a `tail -f`).

### Filtrar per unitat (servei)

```bash
journalctl -u nom_servei
```

Per exemple, per veure els registres de SSH:

```bash
journalctl -u ssh
```

### Filtrar per temps

```bash
# Entrades des d'avui
journalctl --since="today"

# Entrades des d'una data específica
journalctl --since="2023-10-01"

# Interval de temps
journalctl --since="2023-10-01" --until="2023-10-02 12:00"
```

### Mostrar només els errors

```bash
journalctl -p err
```

Els nivells de prioritat disponibles són: emerg, alert, crit, err, warning, notice, info, debug.

## Opcions avançades

### Format de sortida

```bash
# Format JSON
journalctl -o json

# Format més compacte
journalctl -o short

# Format complet amb tots els camps
journalctl -o verbose
```

### Filtrar per executable o PID

```bash
# Per procés específic
journalctl _PID=1234

# Per executable
journalctl /usr/bin/firefox
```

### Veure l'ús del disc i manteniment

```bash
# Veure quant espai ocupen els registres
journalctl --disk-usage

# Netejar registres antics (mantenir només els últims 100MB)
sudo journalctl --vacuum-size=100M

# Netejar registres més antics de 2 dies
sudo journalctl --vacuum-time=2d
```

### Registres d'arrancada

```bash
# Registres de l'arrancada actual
journalctl -b

# Registres de l'arrancada anterior
journalctl -b -1
```

## Exemple de cas d'ús

Imaginem que tenim un problema amb el servei de xarxa i volem investigar què està passant:

```bash
# Mirem els errors de la xarxa de l'últim dia
journalctl -u NetworkManager --since="yesterday" -p err

# Seguim els registres en temps real mentre intentem solucionar el problema
journalctl -f -u NetworkManager
```

## Consells pràctics

1. Utilitzeu `-e` per situar-vos al final del registre automàticament: `journalctl -e`
2. Combineu filtres per obtenir resultats més precisos
3. Si el terminal no mostra colors, afegiu l'opció `--output=cat`
4. Els registres es poden exportar: `journalctl > registres.txt`

## Integració amb altres eines

El journal de systemd està integrat amb altres components del sistema, de manera que mostra informació del kernel, serveis, aplicacions i més, tot en un format unificat i fàcil de consultar.

Amb `journalctl` tens una eina potent per diagnosticar problemes, comprendre què està passant al teu sistema i fer un seguiment del comportament de les aplicacions i serveis.
