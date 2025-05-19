# Comanda `ip`

El comanda `ip` és una eina avançada i versàtil utilitzada en sistemes GNU/Linux per configurar i gestionar xarxes. Substitueix eines més antigues com `ifconfig`, `route` i `arp`, proporcionant més funcionalitats en una única interfície.

## Sintaxi bàsica

```bash
ip [opcions] OBJECTE [comanda]
```

On:

- **OBJECTE**: Pot ser `address`, `link`, `route`, `neigh` (veí), etc.
- **comanda**: Acció a realitzar, com `show`, `add`, `del`, etc.

## Objectes principals

| Objecte   | Descripció                                      |
| --------- | ----------------------------------------------- |
| `link`    | Dispositius de xarxa                            |
| `address` | Adreces IPv4 o IPv6                             |
| `route`   | Entrades de la taula d'enrutament               |
| `neigh`   | Entrades de la taula ARP/NDISC (veïns de xarxa) |
| `rule`    | Regles d'enrutament                             |
| `tunnel`  | Túnels IP sobre IP                              |

## Exemples d'ús comú

### Mostrar informació de xarxa

Veure tots els dispositius de xarxa:

```bash
ip link show
# o simplement
ip link
```

Mostrar adreces IP assignades:

```bash
ip address show
# o simplement
ip addr
```

### Gestionar adreces IP

Afegir una adreça IP a una interfície:

```bash
ip address add 192.168.1.10/24 dev eth0
```

Eliminar una adreça IP:

```bash
ip address del 192.168.1.10/24 dev eth0
```

### Manipular interfícies de xarxa

Activar una interfície:

```bash
ip link set eth0 up
```

Desactivar una interfície:

```bash
ip link set eth0 down
```

### Gestionar rutes

Mostrar taula d'enrutament:

```bash
ip route show
# o simplement
ip route
```

Afegir una ruta:

```bash
ip route add 192.168.2.0/24 via 192.168.1.1
```

Establir una ruta per defecte (gateway):

```bash
ip route add default via 192.168.1.1
```

### Gestionar la taula ARP

Mostrar entrades de la taula ARP:

```bash
ip neigh show
```

## Opcions útils

| Opció                    | Descripció                                    |
| ------------------------ | --------------------------------------------- |
| `-s`, `--stats`          | Mostra més estadístiques                      |
| `-c`, `--color`          | Utilitza colors per a la sortida              |
| `-h`, `--human-readable` | Mostra les mides de forma llegible per humans |
| `-4`, `-6`               | Utilitza IPv4 o IPv6                          |

## Avantatges sobre les eines antigues

- Unificada: una sola eina per a múltiples funcions
- Més flexible i extensible
- Suporta característiques avançades de xarxa
- Millor suport per IPv6
- Sintaxi més coherent

## Observacions

- Requereix privilegis de superusuari (`sudo`) per a la majoria de les operacions de canvi
- Les configuracions fetes amb `ip` no són permanents per defecte (es perden en reiniciar)
- Per a canvis permanents, caldrà configurar els arxius corresponents del sistema (varia segons la distribució)

Aquest comandament és essencial per als administradors de sistemes i útil per a qualsevol usuari que necessiti diagnosticar o configurar connexions de xarxa en un sistema GNU/Linux.
