# TCP/IP IPv4: Explicació Exhaustiva

## Què és TCP/IP?

TCP/IP (Transmission Control Protocol/Internet Protocol) és el conjunt de protocols utilitzats per la comunicació a Internet i xarxes privades. Permet la transmissió de dades entre dispositius de diferents xarxes.

## IPv4

IPv4 (Internet Protocol version 4) és la quarta versió del protocol IP. Utilitza adreces de 32 bits, escrites habitualment en format decimal separat per punts (ex: `192.168.1.1`).

### Estructura d'una adreça IPv4

- **Adreça IP:** 32 bits dividits en 4 octets (8 bits cadascun).
- **Exemple:** `192.168.0.1`
- **Classes d'adreces:**
    - Classe A: `1.0.0.0` a `126.255.255.255`
    - Classe B: `128.0.0.0` a `191.255.255.255`
    - Classe C: `192.0.0.0` a `223.255.255.255`
    - Classe D: Multicast
    - Classe E: Experimental

### Components de TCP/IP

- **TCP:** Protocol orientat a connexió, garanteix la transmissió fiable de dades.
- **IP:** Protocol sense connexió, s'encarrega de l'adreçament i encaminament dels paquets.

## Subxarxes IPv4

### Què és una subxarxa?

Una subxarxa és una divisió lògica d'una xarxa IP. Permet segmentar una xarxa gran en xarxes més petites per millorar la gestió i la seguretat.

### Màscara de subxarxa

La màscara de subxarxa determina quina part de l'adreça IP correspon a la xarxa i quina als hosts.

- **Exemple:** `255.255.255.0` (o `/24` en notació CIDR)
- **Notació CIDR:** Indica el nombre de bits dedicats a la xarxa (ex: `192.168.1.0/24`)

### Càlcul de subxarxes

1. **Determina la màscara de subxarxa:** Decideix quants hosts necessites per subxarxa.
2. **Calcula el nombre de subxarxes i hosts:**
     - Nombre de subxarxes = 2^(nombre de bits de subxarxa afegits)
     - Nombre d'hosts per subxarxa = 2^(nombre de bits d'host) - 2
3. **Divideix l'adreça IP segons la màscara:**
     - Xarxa: part comuna per a tots els hosts
     - Host: part variable per a cada dispositiu

#### Exemple pràctic

- Xarxa: `192.168.1.0/24`
- Volem 4 subxarxes:
    - Necessitem 2 bits addicionals per subxarxa (`2^2 = 4`)
    - Nova màscara: `/26` (`255.255.255.192`)
    - Cada subxarxa tindrà 62 hosts (`2^6 - 2 = 62`)

| Subxarxa         | Rang d'IPs           | Broadcast      |
|------------------|---------------------|---------------|
| 192.168.1.0/26   | 192.168.1.1-62      | 192.168.1.63  |
| 192.168.1.64/26  | 192.168.1.65-126    | 192.168.1.127 |
| 192.168.1.128/26 | 192.168.1.129-190   | 192.168.1.191 |
| 192.168.1.192/26 | 192.168.1.193-254   | 192.168.1.255 |

## Informació addicional

- **Adreça de xarxa:** Primera adreça de la subxarxa (no assignable a hosts)
- **Adreça de broadcast:** Última adreça de la subxarxa (utilitzada per enviar a tots els hosts)
- **Adreces privades:** Rangs reservats per xarxes internes (`10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16`)
- **Gateway:** Dispositiu que connecta la subxarxa amb altres xarxes

## Resum

TCP/IP i IPv4 són fonamentals per la comunicació en xarxes. Entendre el funcionament de les adreces IP, les màscares de subxarxa i el càlcul de subxarxes és essencial per administrar xarxes eficientment.
