# Conectivitat de Xarxes: DHCP, Gateway i Més

## Què és la Conectivitat de Xarxa?

La conectivitat de xarxa fa referència a la capacitat dels dispositius per comunicar-se entre ells dins d’una xarxa local (LAN) o amb xarxes externes (com Internet). Aquesta comunicació depèn de diversos protocols i dispositius que gestionen la transmissió de dades.

---

## DHCP (Dynamic Host Configuration Protocol)

### Definició

DHCP és un protocol de xarxa que permet als dispositius obtenir automàticament una configuració IP (adreça IP, màscara de subxarxa, gateway, DNS, etc.) quan es connecten a una xarxa. Això evita la configuració manual de cada dispositiu.

### Funcionament

1. **Discover:** El dispositiu client envia un missatge DHCP Discover per trobar servidors DHCP disponibles.
2. **Offer:** El servidor DHCP respon amb una oferta d’adreça IP i altres paràmetres de xarxa.
3. **Request:** El client sol·licita formalment l’adreça IP ofertada.
4. **Acknowledge:** El servidor confirma la concessió de l’adreça IP.

### Avantatges

- Configuració automàtica i centralitzada.
- Evita conflictes d’adreces IP.
- Fàcil gestió de dispositius mòbils o temporals.

---

## Gateway

### Definició

El gateway (porta d’enllaç) és el dispositiu que connecta la xarxa local amb altres xarxes, normalment amb Internet. S’acostuma a ser un router.

### Funcionament

- El gateway rep paquets destinats a xarxes externes i els redirigeix cap a la destinació adequada.
- Permet la comunicació entre dispositius de diferents subxarxes.

### Exemple

Si tens una xarxa amb adreces IP 192.168.1.x, el gateway podria ser 192.168.1.1.

---

## Exemple de Configuració (General)

```bash
# Configuració manual d’una IP a Linux
sudo ip addr add 192.168.1.10/24 dev eth0
sudo ip route add default via 192.168.1.1

# Configuració automàtica amb DHCP
sudo dhclient eth0
```
