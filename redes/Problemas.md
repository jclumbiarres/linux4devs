# Problemes bàsics en xarxes Linux i com resoldre'ls

Les xarxes en sistemes Linux poden presentar diversos problemes que dificulten la comunicació entre dispositius o l'accés a Internet. A continuació, s'explica de manera exhaustiva els problemes més comuns, les seves causes i les possibles solucions, incloent exemples de configuració.

## 1. Problema de connexió física

### Causes
- Cable de xarxa desconnectat o mal connectat.
- Targeta de xarxa (NIC) defectuosa.
- Port de switch o router avariat.

### Solució
- Comprova que el cable estigui ben connectat.
- Utilitza la comanda `ethtool` per verificar l'estat de la interfície:
    ```bash
    sudo ethtool eth0
    ```
- Reemplaça el cable o prova amb un altre port.

## 2. Problemes d'adreçament IP

### Causes
- Configuració incorrecta de l'adreça IP.
- Absència de configuració DHCP.
- Conflicte d'adreces IP.

### Solució
- Verifica la configuració amb:
    ```bash
    ip addr show
    ```
- Assigna una IP manualment:
    ```bash
    sudo ip addr add 192.168.1.100/24 dev eth0
    sudo ip link set eth0 up
    ```
- Si utilitzes DHCP:
    ```bash
    sudo dhclient eth0
    ```
- Comprova que no hi hagi duplicats amb:
    ```bash
    arp-scan --interface=eth0 --localnet
    ```

## 3. Problemes de resolució de noms (DNS)

### Causes
- Servidor DNS incorrecte o inexistent.
- Fitxer `/etc/resolv.conf` mal configurat.

### Solució
- Edita `/etc/resolv.conf` i afegeix:
    ```
    nameserver 8.8.8.8
    nameserver 1.1.1.1
    ```
- Prova la resolució amb:
    ```bash
    dig www.google.com
    nslookup www.google.com
    ```

## 4. Problemes de passarel·la (Gateway)

### Causes
- Passarel·la predeterminada no configurada.
- Passarel·la fora de la subxarxa.

### Solució
- Comprova la passarel·la amb:
    ```bash
    ip route show
    ```
- Configura la passarel·la:
    ```bash
    sudo ip route add default via 192.168.1.1
    ```

## 5. Problemes de tallafocs (Firewall)

### Causes
- Regles restrictives a `iptables` o `firewalld`.
- Ports bloquejats.

### Solució
- Llista les regles:
    ```bash
    sudo iptables -L -n
    ```
- Permet el tràfic:
    ```bash
    sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
    ```
- Desactiva temporalment el tallafocs (només per proves):
    ```bash
    sudo systemctl stop firewalld
    ```

## 6. Problemes de rutes

### Causes
- Rutes incorrectes o inexistents.
- Xarxes no accessibles.

### Solució
- Comprova les rutes:
    ```bash
    ip route
    ```
- Afegeix una ruta:
    ```bash
    sudo ip route add 10.0.0.0/24 via 192.168.1.254
    ```

## 7. Problemes de configuració de serveis de xarxa

### Causes
- Serveis com SSH, HTTP, FTP no funcionen.
- Ports tancats o bloquejats.

### Solució
- Comprova que el servei estigui actiu:
    ```bash
    sudo systemctl status ssh
    ```
- Obre el port al tallafocs:
    ```bash
    sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT
    ```

## 8. Problemes de drivers de la targeta de xarxa

### Causes
- Driver no instal·lat o incompatible.

### Solució
- Comprova el driver:
    ```bash
    lspci -k | grep -A 3 Ethernet
    ```
- Instal·la el driver adequat segons el fabricant.

## 9. Problemes de configuració automàtica (NetworkManager)

### Causes
- NetworkManager no gestiona la interfície.
- Configuració manual en conflicte amb NetworkManager.

### Solució
- Comprova l'estat:
    ```bash
    nmcli device status
    ```
- Configura la connexió amb NetworkManager:
    ```bash
    nmcli con add type ethernet con-name connexio1 ifname eth0 autoconnect yes ip4 192.168.1.100/24 gw4 192.168.1.1
    ```

## 10. Problemes de connectivitat sense fils (Wi-Fi)

### Causes
- SSID incorrecte.
- Clau de seguretat errònia.
- Driver Wi-Fi no instal·lat.

### Solució
- Llista xarxes disponibles:
    ```bash
    nmcli device wifi list
    ```
- Connecta't a una xarxa:
    ```bash
    nmcli device wifi connect SSID password CONTRASENYA
    ```

## 11. Diagnòstic general

### Comandes útils
- `ping` per comprovar la connectivitat:
    ```bash
    ping 8.8.8.8
    ```
- `traceroute` per seguir el camí de paquets:
    ```bash
    traceroute www.google.com
    ```
- `netstat` per veure connexions actives:
    ```bash
    netstat -tuln
    ```

## 12. Logs i depuració

- Consulta els logs de sistema:
    ```bash
    dmesg | grep eth
    journalctl -u NetworkManager
    ```

---

Amb aquesta informació, pots identificar, diagnosticar i resoldre la majoria de problemes bàsics de xarxa en sistemes Linux. Recorda sempre fer còpies de seguretat de la configuració abans de fer canvis importants.
