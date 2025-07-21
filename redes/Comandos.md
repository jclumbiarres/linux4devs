# Comandes de Xarxes a Linux

A continuació trobaràs una explicació exhaustiva dels principals comandaments de xarxa a Linux, amb exemples i detalls per entendre el seu funcionament.

## 1. `ip`

Permet gestionar interfícies de xarxa, adreces IP, rutes i més.

- **Mostrar informació de les interfícies:**
    ```bash
    ip addr
    ip link
    ```
- **Assignar una IP:**
    ```bash
    sudo ip addr add 192.168.1.100/24 dev eth0
    ```
- **Activar/desactivar interfície:**
    ```bash
    sudo ip link set eth0 up
    sudo ip link set eth0 down
    ```
- **Mostrar rutes:**
    ```bash
    ip route
    ```

## 2. `iptables`

Permet configurar el tallafoc del sistema.

- **Llistar regles:**
    ```bash
    sudo iptables -L
    ```
- **Permetre connexió a un port:**
    ```bash
    sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
    ```
- **Bloquejar una IP:**
    ```bash
    sudo iptables -A INPUT -s 192.168.1.50 -j DROP
    ```
- **Guardar regles:**
    ```bash
    sudo iptables-save > /etc/iptables/rules.v4
    ```

## 3. `curl`

Eina per fer peticions HTTP/HTTPS.

- **Descarregar una pàgina web:**
    ```bash
    curl https://exemple.com
    ```
- **Descarregar un fitxer:**
    ```bash
    curl -O https://exemple.com/fitxer.zip
    ```
- **Enviar dades POST:**
    ```bash
    curl -X POST -d "usuari=joan&clau=1234" https://exemple.com/login
    ```

## 4. `dig`

Consulta DNS.

- **Consultar una adreça:**
    ```bash
    dig exemple.com
    ```
- **Consultar només l'IP:**
    ```bash
    dig +short exemple.com
    ```
- **Consultar un tipus de registre:**
    ```bash
    dig exemple.com MX
    ```

## 5. `ping`

Comprova la connectivitat amb una altra màquina.

- **Ping a una IP o domini:**
    ```bash
    ping 8.8.8.8
    ping exemple.com
    ```

## 6. `netstat` / `ss`

Mostra connexions de xarxa, ports oberts, etc.

- **Llistar connexions:**
    ```bash
    netstat -tuln
    ss -tuln
    ```

## 7. `nmap`

Escaneja ports i serveis.

- **Escanejar una IP:**
    ```bash
    nmap 192.168.1.1
    ```
- **Escanejar un rang de ports:**
    ```bash
    nmap -p 1-1000 exemple.com
    ```

## 8. `traceroute`

Mostra el camí que segueix un paquet fins a la destinació.

- **Utilitzar traceroute:**
    ```bash
    traceroute exemple.com
    ```

## 9. `hostname`

Gestiona el nom de la màquina.

- **Mostrar hostname:**
    ```bash
    hostname
    ```
- **Canviar hostname:**
    ```bash
    sudo hostname nou_nom
    ```

## 10. `ifconfig` (obsolet, però encara usat)

Mostra i configura interfícies de xarxa.

- **Mostrar interfícies:**
    ```bash
    ifconfig
    ```
- **Assignar IP:**
    ```bash
    sudo ifconfig eth0 192.168.1.100 netmask 255.255.255.0 up
    ```

---

### Recursos addicionals

- [Documentació oficial de iptables](https://netfilter.org/documentation/index.html)
- [Manual de curl](https://curl.se/docs/manpage.html)
- [Guia de comandes de xarxa a Linux](https://wiki.archlinux.org/title/Network_configuration)
