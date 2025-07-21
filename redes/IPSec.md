# IPSec: Explicació Exhaustiva

## Què és IPSec?

**IPSec** (Internet Protocol Security) és un conjunt de protocols desenvolupats per protegir les comunicacions a nivell de xarxa IP. Permet la transmissió segura de dades entre dos punts mitjançant autenticació, integritat i xifratge. IPSec s'utilitza principalment per crear VPNs (Virtual Private Networks), protegint la informació que viatja per xarxes públiques com Internet.

## Objectius Principals d'IPSec

- **Confidencialitat:** Xifra les dades perquè només el destinatari les pugui llegir.
- **Integritat:** Garanteix que les dades no han estat modificades durant la transmissió.
- **Autenticació:** Verifica la identitat dels participants en la comunicació.
- **No-repudiació:** Evita que una de les parts negui haver enviat o rebut dades.

## Components d'IPSec

### Protocols Principals

1. **AH (Authentication Header):**
    - Proporciona autenticació i integritat, però no xifra les dades.
    - S'utilitza quan la confidencialitat no és necessària.

2. **ESP (Encapsulating Security Payload):**
    - Proporciona xifratge, autenticació i integritat.
    - És el protocol més utilitzat en VPNs.

### Modes de Funcionament

- **Mode Transport:** Protegeix només la càrrega útil del paquet IP. S'utilitza entre dos hosts.
- **Mode Tunnel:** Protegeix tot el paquet IP original encapsulant-lo en un nou paquet IP. S'utilitza entre dos routers o gateways.

## Arquitectura d'IPSec

IPSec funciona a la capa de xarxa (capa 3 del model OSI). Utilitza dos protocols per establir i gestionar les connexions segures:

- **IKE (Internet Key Exchange):** Protocol per negociar i establir les claus de seguretat.
- **SA (Security Association):** Conjunt de paràmetres de seguretat acordats entre dos punts.

## Funcionament d'IPSec

1. **Negociació de la connexió:** Els dos punts negocien els paràmetres de seguretat (algoritmes de xifratge, claus, etc.) mitjançant IKE.
2. **Establiment de la SA:** Es crea una associació de seguretat amb els paràmetres acordats.
3. **Transmissió de dades:** Les dades es xifren i s'envien a través de la connexió segura.
4. **Finalització:** Quan la comunicació acaba, es destrueix la SA.

## Algoritmes Utilitzats

- **Xifratge:** AES, 3DES, etc.
- **Integritat:** SHA-1, SHA-2, MD5.
- **Autenticació:** Certificats digitals, pre-shared keys (PSK).

## Exemples de Configuració

### Exemple Bàsic amb `ipsec-tools` (Linux)

#### Instal·lació

```bash
sudo apt-get install racoon ipsec-tools
```

#### Configuració de `/etc/ipsec.conf`

```conf
config setup
     charondebug="ike 2, knl 2, cfg 2, net 2, esp 2, dmn 2,  mgr 2"

conn %default
     keyexchange=ikev2
     ike=aes256-sha256-modp2048!
     esp=aes256-sha256!
     dpdaction=clear
     dpddelay=300s
     rekey=no

conn myvpn
     left=192.168.1.1
     leftsubnet=192.168.1.0/24
     leftauth=psk
     leftid=@myvpn
     right=192.168.2.1
     rightsubnet=192.168.2.0/24
     rightauth=psk
     rightid=@myvpn
     auto=start
```

#### Configuració de la clau pre-compartida `/etc/ipsec.secrets`

```
@myvpn : PSK "clau_secreta"
```

### Exemple amb `strongSwan`

#### Instal·lació

```bash
sudo apt-get install strongswan
```

#### Configuració de `/etc/ipsec.conf`

```conf
config setup
     charondebug="ike 2, knl 2, cfg 2, net 2, esp 2, dmn 2,  mgr 2"

conn home-office
     left=192.168.1.1
     leftsubnet=192.168.1.0/24
     leftauth=psk
     right=203.0.113.1
     rightsubnet=10.0.0.0/24
     rightauth=psk
     ike=aes256-sha256-modp2048!
     esp=aes256-sha256!
     auto=start
```

#### Configuració de la clau pre-compartida `/etc/ipsec.secrets`

```
192.168.1.1 203.0.113.1 : PSK "clau_secreta"
```

## Avantatges i Desavantatges d'IPSec

### Avantatges

- Seguretat robusta a nivell de xarxa.
- Compatible amb la majoria de sistemes operatius i dispositius.
- Flexible (pot utilitzar diversos algoritmes i mètodes d'autenticació).

### Desavantatges

- Pot ser complex de configurar.
- Pot introduir latència degut al xifratge/desxifratge.
- Algunes aplicacions poden tenir problemes amb NAT (Network Address Translation).

## Casos d'Ús

- Connexió segura entre oficines (site-to-site VPN).
- Accés remot segur per a empleats (remote access VPN).
- Protecció de tràfic entre servidors.

## Recursos Addicionals

- [Documentació oficial de strongSwan](https://wiki.strongswan.org/)
- [RFC 4301 - Security Architecture for the Internet Protocol](https://tools.ietf.org/html/rfc4301)
- [Guia de VPN amb IPSec a Linux](https://www.linux.com/training-tutorials/ipsec-vpn-linux/)

---

Amb aquesta informació tens una base sòlida per entendre i configurar IPSec en entorns Linux. Si necessites exemples més específics o detallats, pots consultar la documentació oficial dels paquets o RFCs corresponents.