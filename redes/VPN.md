# Xarxes Privades Virtuals (VPN) amb WireGuard, OpenVPN i Altres

## Què és una VPN?

Una **VPN (Xarxa Privada Virtual)** és una tecnologia que permet crear una connexió segura i xifrada entre dos punts a través d'una xarxa pública, com Internet. Això permet als usuaris accedir a recursos remots com si estiguessin a la mateixa xarxa local, protegint la privacitat i la integritat de les dades.

## Avantatges d'utilitzar una VPN

- **Seguretat:** Xifra el tràfic de dades, protegint-lo de tercers.
- **Privacitat:** Amaga la teva adreça IP real.
- **Accés remot:** Permet connectar-se a xarxes privades des de qualsevol lloc.
- **Evita restriccions geogràfiques:** Permet accedir a serveis restringits per ubicació.

---

## WireGuard

### Què és WireGuard?

**WireGuard** és un protocol VPN modern, simple i extremadament ràpid. Està integrat al nucli de Linux i destaca per la seva facilitat de configuració, rendiment i seguretat.

### Característiques principals

- **Codi font petit i auditable**
- **Configuració senzilla**
- **Alt rendiment**
- **Utilitza criptografia moderna**

### Instal·lació

#### Ubuntu/Debian

```bash
sudo apt update
sudo apt install wireguard
```

#### CentOS/Fedora

```bash
sudo dnf install wireguard-tools
```

### Configuració bàsica

#### Generar claus

```bash
wg genkey | tee privatekey | wg pubkey > publickey
```

#### Exemple de configuració del servidor (`/etc/wireguard/wg0.conf`)

```ini
[Interface]
Address = 10.0.0.1/24
PrivateKey = <clau_privada_del_servidor>
ListenPort = 51820

[Peer]
PublicKey = <clau_pública_del_client>
AllowedIPs = 10.0.0.2/32
```

#### Exemple de configuració del client

```ini
[Interface]
Address = 10.0.0.2/24
PrivateKey = <clau_privada_del_client>

[Peer]
PublicKey = <clau_pública_del_servidor>
Endpoint = <ip_del_servidor>:51820
AllowedIPs = 0.0.0.0/0
```

#### Iniciar WireGuard

```bash
sudo wg-quick up wg0
```

---

## OpenVPN

### Què és OpenVPN?

**OpenVPN** és un protocol VPN molt utilitzat, flexible i compatible amb molts sistemes operatius. Utilitza SSL/TLS per a l'autenticació i xifratge.

### Característiques principals

- **Molt configurable**
- **Suporta múltiples protocols de xifratge**
- **Compatible amb molts dispositius**

### Instal·lació

#### Ubuntu/Debian

```bash
sudo apt update
sudo apt install openvpn easy-rsa
```

### Configuració bàsica

#### Crear infraestructura de claus amb Easy-RSA

```bash
make-cadir ~/openvpn-ca
cd ~/openvpn-ca
source vars
./clean-all
./build-ca
./build-key-server server
./build-key client1
./build-dh
openvpn --genkey --secret keys/ta.key
```

#### Exemple de configuració del servidor (`server.conf`)

```ini
port 1194
proto udp
dev tun
ca ca.crt
cert server.crt
key server.key
dh dh2048.pem
server 10.8.0.0 255.255.255.0
ifconfig-pool-persist ipp.txt
push "redirect-gateway def1 bypass-dhcp"
push "dhcp-option DNS 8.8.8.8"
keepalive 10 120
tls-auth ta.key 0
cipher AES-256-CBC
persist-key
persist-tun
status openvpn-status.log
verb 3
```

#### Exemple de configuració del client (`client.ovpn`)

```ini
client
dev tun
proto udp
remote <ip_del_servidor> 1194
resolv-retry infinite
nobind
persist-key
persist-tun
ca ca.crt
cert client1.crt
key client1.key
tls-auth ta.key 1
cipher AES-256-CBC
verb 3
```

#### Iniciar OpenVPN

```bash
sudo systemctl start openvpn@server
```

---

## Altres protocols VPN

- **IPsec:** Utilitzat per a VPNs corporatives, integrat en molts routers i sistemes operatius.
- **L2TP/IPsec:** Combinació de Layer 2 Tunneling Protocol amb IPsec per a xifratge.
- **PPTP:** Protocol antic, menys segur, però fàcil de configurar.

---

## Consideracions de seguretat

- Utilitza claus fortes i actualitza-les regularment.
- Mantingues el programari actualitzat.
- Limita els accessos amb regles de firewall.
- Monitoritza els logs de connexió.

---

## Recursos addicionals

- [Documentació oficial de WireGuard](https://www.wireguard.com/)
- [Documentació oficial d'OpenVPN](https://openvpn.net/)
- [Guia de VPN a la Wikipedia](https://ca.wikipedia.org/wiki/Xarxa_privada_virtual)

---

## Conclusions

Les VPN són eines fonamentals per a la seguretat i privacitat a Internet. WireGuard destaca per la seva simplicitat i rendiment, mentre que OpenVPN ofereix una gran flexibilitat. La configuració pot variar segons les necessitats, però amb els exemples anteriors es pot començar a desplegar una VPN segura i funcional.
