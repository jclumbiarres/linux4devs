# netstat

`netstat` és una eina de línia de comandes que mostra informació detallada sobre les connexions de xarxa del sistema, taules d'encaminament i estadístiques d'interfície.

## Descripció

`netstat` (network statistics) és una utilitat que permet supervisar les connexions de xarxa tant entrants com sortints, així com visualitzar taules d'encaminament, estadístiques d'interfícies i molt més. És una eina molt útil per a diagnòstic i monitoratge de xarxes.

## Sintaxi bàsica

```bash
netstat [opcions]
```

## Opcions principals

- `-a`: Mostra totes les connexions i ports en escolta.
- `-t`: Mostra només connexions TCP.
- `-u`: Mostra només connexions UDP.
- `-n`: Mostra adreces i ports en format numèric, sense resoldre noms.
- `-l`: Mostra només els sockets en estat d'escolta (listening).
- `-p`: Mostra el PID i nom del programa al qual pertany cada connexió.
- `-r`: Mostra la taula d'encaminament (equivalent a `route`).
- `-i`: Mostra la taula d'interfícies (similar a `ifconfig`).
- `-s`: Mostra estadístiques per protocol.
- `-c`: Actualitza la informació de manera contínua.

## Exemples d'ús

### Mostrar totes les connexions actives

```bash
netstat -a
```

### Mostrar les connexions TCP actives

```bash
netstat -at
```

### Mostrar els ports en escolta

```bash
netstat -tuln
```

### Mostrar connexions amb programes associats (requereix permisos root)

```bash
sudo netstat -tulnp
```

### Mostrar estadístiques de xarxa

```bash
netstat -s
```

### Mostrar la taula d'encaminament

```bash
netstat -r
```

### Actualitzar la informació cada 3 segons

```bash
netstat -c
```

### Mostrar connexions d'un port específic

```bash
netstat -an | grep 'PORT_NUMBER'
```

### Trobar quina aplicació utilitza un port específic

```bash
sudo netstat -tulnp | grep 'PORT_NUMBER'
```

## Sortida típica

La sortida de `netstat` normalment inclou:

- **Proto**: Protocol utilitzat (TCP, UDP, etc.)
- **Recv-Q**: Bytes rebuts en cua i encara no entregats a l'aplicació
- **Send-Q**: Bytes enviats sense confirmació
- **Local Address**: Adreça local i número de port
- **Foreign Address**: Adreça remota i número de port
- **State**: Estat de la connexió (ESTABLISHED, LISTEN, TIME_WAIT, etc.)
- **PID/Program name**: ID del procés i nom del programa (amb l'opció -p)

## Notes importants

- El comandament està considerat obsolet en algunes distribucions modernes de Linux.
- Es recomana utilitzar `ss` com a alternativa més moderna i eficient.
- Per veure tots els processos i connexions, cal executar el comandament amb privilegis d'administrador (sudo).

## Alternatives modernes

- `ss`: Substitueix a netstat amb més funcionalitats i millor rendiment.
- `ip`: Substitueix altres funcions de netstat com les taules d'encaminament.

## Recursos addicionals

- Podeu obtenir més informació amb `man netstat`.
- Per problemes específics de xarxa, pot ser útil combinar `netstat` amb altres eines com `tcpdump` o `wireshark`.
