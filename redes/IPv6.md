# IPv6: Explicació Exhaustiva

## Què és IPv6?

IPv6 (Internet Protocol version 6) és la versió més recent del protocol IP, dissenyada per substituir IPv4 a causa de l'esgotament d'adreces.

### Característiques d'IPv6

- **Adreces de 128 bits** (en comparació amb els 32 bits d'IPv4).
- **Notació hexadecimal**: Ex. `2001:0db8:85a3:0000:0000:8a2e:0370:7334`
- **Més adreces disponibles**.
- **Simplificació del processament de paquets**.
- **Autoconfiguració** i millora de la seguretat.

## Tipus d'adreces IPv6

- **Unicast**: Identifica un únic dispositiu.
- **Multicast**: Envia dades a múltiples dispositius.
- **Anycast**: Envia dades al dispositiu més proper d'un grup.

## Estructura d'una adreça IPv6

- 8 grups de 4 dígits hexadecimals separats per dos punts.
- Exemples de simplificació:
    - Omissió de zeros inicials: `2001:db8::1`
    - Substitució de grups de zeros per `::` (només una vegada per adreça).

## Subxarxes en IPv6

### Prefix i CIDR

- El prefix indica la part de l'adreça que identifica la xarxa.
- S'especifica amb la notació CIDR: `2001:db8:abcd:0012::/64`
- `/64` indica que els primers 64 bits són el prefix de xarxa.

### Càlcul de subxarxes

1. **Determina el prefix de xarxa**: Ex. `/64`
2. **Divideix el prefix per crear subxarxes**: Ex. `/68`, `/72`, etc.
3. **Cada subxarxa té un rang d'adreces únic**.

#### Exemple

- Xarxa principal: `2001:db8:abcd:0012::/64`
- Primera subxarxa: `2001:db8:abcd:0012:0000::/68`
- Segona subxarxa: `2001:db8:abcd:0012:0001::/68`

### Com calcular subxarxes

1. **Escull el prefix de subxarxa** (més gran que el prefix de xarxa).
2. **Calcula el nombre de subxarxes**: Cada bit afegit al prefix duplica el nombre de subxarxes.
     - Ex. `/64` a `/68` = 2⁴ = 16 subxarxes.

## Informació addicional

- **Adreça link-local**: `fe80::/10` (per comunicació dins la mateixa xarxa local).
- **Adreça global unicast**: Utilitzada per comunicació a Internet.
- **Adreça loopback**: `::1`

## Recursos útils

- [Documentació oficial IPv6](https://datatracker.ietf.org/doc/html/rfc8200)
- [Calculadora de subxarxes IPv6](https://www.ultratools.com/tools/ipv6SubnetCalculator)
