# Protocol UDP (User Datagram Protocol)

El **UDP** (User Datagram Protocol) és un protocol de comunicació de la capa de transport del model OSI i TCP/IP. És conegut per ser simple, ràpid i no orientat a connexió.

## Característiques principals

- **No orientat a connexió:** No estableix una connexió prèvia entre l'emissor i el receptor.
- **Sense control d'errors ni confirmació:** No garanteix la recepció ni l'ordre dels paquets. Si es perden, no es retransmeten.
- **Baixa latència:** Ideal per aplicacions que requereixen rapidesa, com videoconferències, streaming o jocs en línia.
- **Trames petites:** El missatge s'envia en datagrames independents.

## Funcionament

1. L'aplicació genera dades i les envia a la capa de transport.
2. UDP encapsula les dades en datagrames, afegint una capçalera amb la informació mínima (ports d'origen i destinació, longitud i checksum).
3. Els datagrames es transmeten directament a la capa de xarxa (IP).
4. El receptor rep els datagrames i els passa a l'aplicació corresponent segons el port de destinació.

## Estructura de la capçalera UDP

| Camp         | Mida (bits) | Descripció                       |
|--------------|-------------|-----------------------------------|
| Port origen  | 16          | Port de l'emissor                 |
| Port destí   | 16          | Port del receptor                 |
| Longitud     | 16          | Longitud total del datagrama      |
| Checksum     | 16          | Verificació d'errors bàsica       |

## Avantatges

- **Simplicitat:** Implementació senzilla.
- **Eficiència:** Menys sobrecàrrega que TCP.
- **Rapidesa:** Transmissió immediata de dades.

## Inconvenients

- **No fiable:** Possibilitat de pèrdua o duplicació de paquets.
- **No ordenat:** Els datagrames poden arribar desordenats.
- **Sense gestió de congestió:** No adapta la velocitat d'enviament.

## Usos habituals

- DNS (Domain Name System)
- Streaming de vídeo i àudio
- Jocs en línia
- Protocols de veu (VoIP)
- SNMP (Simple Network Management Protocol)

## Comparació amb TCP

| Característica | UDP                  | TCP                       |
|----------------|----------------------|---------------------------|
| Connexió       | No                   | Sí                        |
| Fiabilitat     | No                   | Sí                        |
| Ordenació      | No                   | Sí                        |
| Velocitat      | Alta                 | Mitjana                   |
| Sobrecarrega   | Baixa                | Alta                      |

## Exemple d'ús en codi (Python)

```python
import socket

# Crear socket UDP
sock = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)

# Enviar missatge
sock.sendto(b'Hola UDP!', ('localhost', 12345))
```

## Resum

UDP és un protocol senzill i ràpid, adequat per aplicacions on la velocitat és més important que la fiabilitat. No garanteix la recepció ni l'ordre dels missatges, però és ideal per escenaris on la pèrdua d'algun paquet no afecta significativament el servei.
