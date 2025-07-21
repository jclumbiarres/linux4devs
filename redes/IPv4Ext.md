# Protocol IPv4: ICMP, IGMP, GRE i Altres Paquets

## Introducció a IPv4

IPv4 (Internet Protocol version 4) és el protocol principal de la capa de xarxa, responsable d'encapsular i adreçar les dades entre dispositius. Les adreces IPv4 són de 32 bits, escrites en format decimal separat per punts (ex: `192.168.1.1`). IPv4 pot encapsular diversos protocols de la capa superior, cadascun amb funcions específiques.

### Estructura del paquet IPv4

Un paquet IPv4 consta de:

- **Capçalera IPv4**: Conté informació sobre la versió, longitud, identificador, fragmentació, TTL, protocol, checksum, adreça d'origen i destinació.
- **Dades (Payload)**: El contingut que es transmet, que pot ser un paquet ICMP, IGMP, GRE, TCP, UDP, etc.

#### Camps principals de la capçalera IPv4

| Camp                | Descripció                                                                 |
|---------------------|----------------------------------------------------------------------------|
| Versió              | Versió del protocol (4 per IPv4)                                           |
| IHL                 | Longitud de la capçalera                                                   |
| Type of Service     | Qualitat de servei                                                         |
| Total Length        | Longitud total del paquet                                                   |
| Identification      | Identificador de fragmentació                                               |
| Flags               | Control de fragmentació                                                     |
| Fragment Offset     | Posició del fragment                                                        |
| TTL                 | Temps de vida del paquet                                                    |
| Protocol            | Protocol de la capa superior (ex: 1=ICMP, 2=IGMP, 47=GRE, 6=TCP, 17=UDP)   |
| Header Checksum     | Comprovació d'errors de la capçalera                                        |
| Source Address      | Adreça IP d'origen                                                          |
| Destination Address | Adreça IP de destinació                                                     |

## Protocol ICMP (Internet Control Message Protocol)

ICMP és utilitzat per enviar missatges de control, diagnòstic i error dins de la xarxa. No transmet dades d'aplicació, sinó informació sobre l'estat de la xarxa.

### Tipus de paquets ICMP

Els paquets ICMP es classifiquen per tipus i codi. Alguns dels més rellevants són:

| Tipus | Nom                        | Descripció                                                                 |
|-------|----------------------------|----------------------------------------------------------------------------|
| 0     | Echo Reply                 | Resposta a una sol·licitud de ping                                         |
| 3     | Destination Unreachable    | Destinació inabastable (xarxa, host, protocol, port, etc.)                 |
| 4     | Source Quench              | Control de congestió (obsolet)                                             |
| 5     | Redirect                   | Redirecció de ruta                                                         |
| 8     | Echo Request               | Sol·licitud de ping                                                        |
| 11    | Time Exceeded              | Temps excedit (TTL esgotat)                                                |
| 12    | Parameter Problem          | Problema amb la capçalera IP                                               |
| 13    | Timestamp Request          | Sol·licitud de marca de temps                                              |
| 14    | Timestamp Reply            | Resposta de marca de temps                                                 |
| 17    | Address Mask Request       | Sol·licitud de màscara d'adreça                                            |
| 18    | Address Mask Reply         | Resposta de màscara d'adreça                                               |

#### Format d'un paquet ICMP

- **Tipus**: Identifica el tipus de missatge.
- **Codi**: Detalla el subtipus.
- **Checksum**: Comprovació d'errors.
- **Dades**: Informació específica (identificador, seqüència, payload).

#### Exemples d'ús d'ICMP

- **Ping**: Comprova la connectivitat entre dos hosts.
- **Traceroute**: Determina el camí fins a una destinació mitjançant missatges Time Exceeded.

#### Configuració i diagnòstic amb ICMP

```bash
ping 8.8.8.8
traceroute 8.8.8.8
```

#### Filtratge de paquets ICMP amb `iptables`

```bash
iptables -A INPUT -p icmp --icmp-type echo-request -j DROP
```

## Protocol IGMP (Internet Group Management Protocol)

IGMP és utilitzat per gestionar la pertinença a grups multicast en xarxes IPv4. Permet als hosts informar als routers si volen rebre tràfic multicast.

### Tipus de paquets IGMP

| Versió | Tipus de missatge           | Descripció                                              |
|--------|-----------------------------|---------------------------------------------------------|
| IGMPv1 | Membership Query            | El router pregunta quins hosts volen rebre multicast    |
| IGMPv1 | Membership Report           | El host informa que vol unir-se a un grup multicast     |
| IGMPv2 | Leave Group                 | El host informa que vol abandonar el grup multicast     |
| IGMPv3 | Membership Report           | Permet especificar fonts de multicast                   |

#### Format d'un paquet IGMP

- **Tipus**: Query, Report, Leave.
- **Checksum**: Comprovació d'errors.
- **Adreça de grup**: El grup multicast implicat.

#### Exemples de configuració IGMP

- **Activar IGMP snooping en un switch** (depèn del fabricant).
- **Configurar un router per suportar multicast**:

```bash
echo 0 > /proc/sys/net/ipv4/conf/all/force_igmp_version
```

- **Veure grups IGMP en Linux**:

```bash
ip maddr show
```

## Protocol GRE (Generic Routing Encapsulation)

GRE és un protocol d'encapsulació que permet crear túnels entre dos punts de la xarxa, encapsulant paquets de protocols diversos dins d'IPv4.

### Característiques de GRE

- Permet encapsular paquets de protocols diferents (IPv4, IPv6, etc.).
- Utilitzat per crear VPNs, túnels entre routers, etc.
- Protocol número 47 en la capçalera IPv4.

#### Format d'un paquet GRE

- **Capçalera GRE**: Inclou camps com flags, protocol type, checksum (opcional).
- **Payload**: El paquet encapsulat (pot ser IP, PPP, etc.).

#### Exemples de configuració GRE en Linux

- **Crear un túnel GRE**:

```bash
ip tunnel add gre1 mode gre remote 203.0.113.2 local 192.168.1.10 ttl 255
ip link set gre1 up
ip addr add 10.0.0.1/30 dev gre1
```

- **Eliminar el túnel GRE**:

```bash
ip tunnel del gre1
```

## Altres protocols encapsulats en IPv4

A més d'ICMP, IGMP i GRE, IPv4 pot encapsular altres protocols:

- **ESP (Encapsulating Security Payload)**: Utilitzat per IPsec per encriptar paquets.
- **AH (Authentication Header)**: Utilitzat per IPsec per autenticació.
- **OSPF (Open Shortest Path First)**: Protocol d'enrutament dinàmic.
- **EIGRP, RIP**: Altres protocols d'enrutament.

| Protocol | Número | Descripció                                      |
|----------|--------|-------------------------------------------------|
| ICMP     | 1      | Missatges de control i error                    |
| IGMP     | 2      | Gestió de grups multicast                       |
| GRE      | 47     | Encapsulació de paquets                         |
| ESP      | 50     | Encriptació IPsec                               |
| AH       | 51     | Autenticació IPsec                              |
| OSPF     | 89     | Enrutament dinàmic                              |

## Configuració d'adreces IPv4

En Linux, es pot configurar una adreça IP i ruta per defecte:

```bash
ip addr add 192.168.1.10/24 dev eth0
ip route add default via 192.168.1.1
```

## Resum

IPv4 és la base de la comunicació en xarxes IP, encapsulant protocols com ICMP (diagnòstic i control), IGMP (gestió de multicast), GRE (túnels), i molts altres. Cada protocol té una funció específica i una estructura de paquet pròpia. Entendre aquests protocols és essencial per configurar, diagnosticar i protegir xarxes, així com per implementar serveis avançats com multicast o VPNs.

