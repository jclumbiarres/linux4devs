# Què és el DNS?

El **DNS** (Domain Name System) és un sistema fonamental d'Internet que permet traduir noms de domini llegibles per humans (com ara `example.com`) en adreces IP numèriques (com `93.184.216.34`) que els ordinadors utilitzen per comunicar-se entre ells. Sense el DNS, hauríem de recordar les adreces IP de cada servei web, cosa que seria poc pràctica.

## Funcionament del DNS

El DNS funciona com una gran base de dades distribuïda i jeràrquica. Quan escrius una adreça web al navegador, el teu ordinador consulta un servidor DNS per obtenir l'adreça IP corresponent. El procés general és el següent:

1. **Consulta local:** El sistema operatiu consulta la seva memòria cau local.
2. **Consulta al servidor DNS configurat:** Si no troba la resposta, envia la consulta al servidor DNS configurat (normalment el del proveïdor d'Internet).
3. **Resolució recursiva:** Si el servidor DNS no té la resposta, consulta altres servidors DNS fins a trobar la informació.
4. **Resposta:** El servidor DNS retorna l'adreça IP corresponent al nom de domini.

## Tipus de servidors DNS

- **Servidors recursius:** Reben consultes dels clients i busquen la resposta, preguntant a altres servidors si cal.
- **Servidors autoritzats:** Contenen la informació definitiva sobre un domini concret.
- **Servidors de noms arrel:** Són el punt de partida de la jerarquia DNS.

## Components principals del DNS

- **Zones:** Una zona és una part de l'espai de noms DNS gestionada per un servidor autoritzat.
- **Registres:** Són entrades dins una zona, com ara:
    - `A`: Associa un nom de domini amb una adreça IPv4.
    - `AAAA`: Associa un nom de domini amb una adreça IPv6.
    - `MX`: Indica els servidors de correu electrònic.
    - `CNAME`: Alias d'un altre nom de domini.
    - `NS`: Indica els servidors de noms autoritzats per la zona.

# Configuració de DNS amb BIND9

**BIND9** és un dels servidors DNS més utilitzats en sistemes Linux. Permet configurar servidors autoritzats i recursius.

## Instal·lació de BIND9

```bash
sudo apt update
sudo apt install bind9 bind9utils bind9-doc
```

## Fitxers de configuració principals

- `/etc/bind/named.conf`: Fitxer principal de configuració.
- `/etc/bind/named.conf.local`: Per definir zones personalitzades.
- `/etc/bind/named.conf.options`: Opcions globals (com servidors recursius).
- `/etc/bind/db.*`: Fitxers de dades de les zones.

## Exemple de configuració d'una zona autoritzada

Suposem que volem gestionar el domini `exemple.local`.

### 1. Definir la zona a `named.conf.local`

```conf
zone "exemple.local" {
        type master;
        file "/etc/bind/db.exemple.local";
};
```

### 2. Crear el fitxer de zona `/etc/bind/db.exemple.local`

```text
$TTL    604800
@       IN      SOA     ns1.exemple.local. admin.exemple.local. (
                                                20240601        ; Serial
                                                604800          ; Refresh
                                                86400           ; Retry
                                                2419200         ; Expire
                                                604800 )        ; Negative Cache TTL
;
@       IN      NS      ns1.exemple.local.
ns1     IN      A       192.168.1.10
@       IN      A       192.168.1.20
www     IN      A       192.168.1.21
mail    IN      A       192.168.1.22
@       IN      MX      10 mail.exemple.local.
```

### 3. Comprovar la configuració

```bash
sudo named-checkconf
sudo named-checkzone exemple.local /etc/bind/db.exemple.local
```

### 4. Reiniciar BIND9

```bash
sudo systemctl restart bind9
```

## Configuració d'un servidor recursiu

Edita `/etc/bind/named.conf.options`:

```conf
options {
        directory "/var/cache/bind";
        recursion yes;
        allow-query { any; };
        forwarders {
                8.8.8.8;
                8.8.4.4;
        };
        dnssec-validation auto;
        listen-on { any; };
};
```

## Consultes DNS amb `dig`

Per provar el servidor DNS:

```bash
dig @192.168.1.10 exemple.local
dig @192.168.1.10 www.exemple.local
```

# Resum

El DNS és essencial per la navegació a Internet, traduint noms en adreces IP. Amb BIND9 pots crear servidors DNS autoritzats i recursius, gestionant zones i registres segons les teves necessitats. La configuració implica definir zones, crear fitxers de dades i assegurar-te que la sintaxi sigui correcta.
