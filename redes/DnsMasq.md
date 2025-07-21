# Dnsmasq: Explicació Exhaustiva

Dnsmasq és una eina lleugera i potent que proporciona serveis de DNS, DHCP, TFTP i PXE, especialment dissenyada per a xarxes petites i mitjanes. S'utilitza àmpliament en entorns domèstics, petites oficines, laboratoris i dispositius embarcats per la seva facilitat de configuració i baix consum de recursos.

## Característiques Principals

- **Servidor DNS**: Proporciona resolució de noms local i cache de consultes DNS, millorant la velocitat i reduint el tràfic extern.
- **Servidor DHCP**: Assigna automàticament adreces IP als dispositius de la xarxa, amb opcions avançades com la reserva d'IP per MAC.
- **Servidor TFTP/PXE**: Permet l'arrencada remota de dispositius mitjançant xarxa.
- **Integració amb fitxers hosts**: Pot utilitzar `/etc/hosts` per resoldre noms locals.
- **Configuració senzilla**: La configuració es fa principalment a través del fitxer `/etc/dnsmasq.conf` o línia de comandes.

## Funcionament

Dnsmasq actua com a intermediari entre els clients de la xarxa i els servidors DNS/DHCP externs. Quan un client fa una consulta DNS, Dnsmasq pot respondre des de la seva cache, utilitzar entrades locals o reenviar la consulta a servidors externs. Per DHCP, gestiona el pool d'adreces IP i opcions com la passarel·la, DNS, etc.

## Instal·lació

A la majoria de distribucions Linux, es pot instal·lar amb:

```bash
sudo apt install dnsmasq
```

## Configuració Bàsica

El fitxer principal de configuració és `/etc/dnsmasq.conf`. Algunes opcions habituals:

```ini
# Activar el servidor DHCP en la xarxa 192.168.1.0/24
dhcp-range=192.168.1.50,192.168.1.150,12h

# Assignar IP fixa a un dispositiu per MAC
dhcp-host=00:11:22:33:44:55,192.168.1.60

# Utilitzar servidors DNS externs
server=8.8.8.8
server=1.1.1.1

# Utilitzar el fitxer hosts local
addn-hosts=/etc/dnsmasq.hosts

# Limitar el nombre de consultes simultànies
dns-forward-max=150
```

## Exemples de Configuració

### 1. DNS Local amb Cache

Permet resoldre noms locals i cachejar consultes externes:

```ini
domain-needed
bogus-priv
no-resolv
server=8.8.8.8
local=/lan/
```

### 2. DHCP amb Reserva d'IP

Assigna IPs dinàmiques i reserva IPs per dispositius concrets:

```ini
dhcp-range=192.168.0.100,192.168.0.200,24h
dhcp-host=AA:BB:CC:DD:EE:FF,192.168.0.150
```

### 3. Integració amb fitxer hosts

Permet definir noms personalitzats:

```
addn-hosts=/etc/dnsmasq.hosts
```

Al fitxer `/etc/dnsmasq.hosts`:

```
192.168.0.10    servidor.lan
192.168.0.11    impressora.lan
```

### 4. TFTP/PXE

Per arrencada remota:

```ini
enable-tftp
tftp-root=/srv/tftp
dhcp-boot=pxelinux.0
```

## Seguretat

- **Restringir interfícies**: Utilitza `interface=eth0` per limitar el servei a una interfície.
- **Bloquejar dominis**: Amb `address=/domini-bloquejat/0.0.0.0`.
- **Logs**: Activa `log-queries` per monitoritzar consultes.

## Integració amb Sistemes

Dnsmasq pot funcionar com a servidor principal o complementari amb altres serveis (com NetworkManager). En entorns embarcats, sovint s'utilitza per la seva lleugeresa.

## Avantatges

- Fàcil de configurar i mantenir.
- Baix consum de recursos.
- Suport per múltiples protocols.
- Gran flexibilitat per a xarxes petites.

## Recursos Addicionals

- [Documentació oficial](http://www.thekelleys.org.uk/dnsmasq/doc.html)
- Pàgina de manual: `man dnsmasq`
- Comunitats Linux i fòrums de xarxes

---

Dnsmasq és una solució robusta i versàtil per gestionar serveis de xarxa essencials en entorns petits i mitjans, amb una corba d'aprenentatge suau i gran capacitat d'adaptació.