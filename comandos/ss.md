# Comanda `ss` (Socket Statistics)

`ss` és una eina poderosa per a mostrar informació detallada sobre els sockets de xarxa en un sistema GNU/Linux. Substitueix la comanda tradicional `netstat` i ofereix més funcionalitats i un rendiment millor.

## Descripció General

La comanda `ss` mostra estadístiques dels sockets, permetent als usuaris veure les connexions de xarxa actives, els ports en escolta, i altres detalls relacionats amb els sockets del sistema. És especialment útil per a:

- Diagnosticar problemes de connectivitat de xarxa
- Monitoritzar connexions actives
- Verificar quins ports estan en ús o en escolta
- Analitzar l'estat de les connexions TCP/IP

## Sintaxi Bàsica

```
ss [opcions] [filtre]
```

## Opcions Principals

| Opció | Descripció                                           |
| ----- | ---------------------------------------------------- |
| `-a`  | Mostra tots els sockets (en escolta i no en escolta) |
| `-l`  | Mostra només els sockets en escolta                  |
| `-t`  | Mostra només els sockets TCP                         |
| `-u`  | Mostra només els sockets UDP                         |
| `-x`  | Mostra només els sockets Unix                        |
| `-n`  | No resol noms de serveis o hosts                     |
| `-p`  | Mostra el procés que utilitza el socket              |
| `-s`  | Mostra estadístiques resumides                       |
| `-4`  | Mostra només els sockets IPv4                        |
| `-6`  | Mostra només els sockets IPv6                        |

## Exemples d'Ús

### Mostrar tots els sockets TCP

```bash
ss -t
```

### Mostrar sockets TCP en estat d'escolta amb detalls del procés

```bash
ss -tlp
```

### Mostrar totes les connexions establertes

```bash
ss -ta state established
```

### Filtrar per port específic

```bash
ss -t dst :80
```

### Veure estadístiques resumides

```bash
ss -s
```

### Mostrar connexions a una adreça IP específica

```bash
ss dst 192.168.1.100
```

## Filtres Avançats

`ss` permet utilitzar filtres complexos per mostrar només la informació que necessitem:

```bash
ss state time-wait
ss "(sport = :http or sport = :https)"
ss '(dport = :ssh or sport = :ssh)'
```

## Diferències amb `netstat`

- `ss` és més ràpid i eficient
- Mostra més informació sobre els estats dels sockets
- Té millors capacitats de filtrat
- Utilitza recursos del sistema més eficientment amb grans volums de connexions

## Consells

- Utilitzeu `-n` per millorar el rendiment quan no necessiteu resolució de noms
- Combineu `-p` amb altres opcions per veure quins programes utilitzen cada connexió
- Per problemes de xarxa, combineu amb `grep` per filtrar connexions específiques

## Conclusió

La comanda `ss` és una eina essencial per administradors de sistemes i desenvolupadors que necessiten informació detallada sobre l'estat de la xarxa i les connexions al sistema. A mesura que `netstat` es considera obsolet en moltes distribucions modernes de Linux, `ss` s'ha convertit en l'estàndard per a l'anàlisi de sockets de xarxa.
