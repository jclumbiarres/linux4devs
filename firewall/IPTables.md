## Introducció

Iptables és una eina de configuració del tallafocs integrada al kernel de Linux que permet a l'administrador del sistema configurar les taules proporcionades pel tallafocs del kernel de Linux i les cadenes i regles que emmagatzema. És una eina potent i flexible, però també pot ser complexa d'aprendre i utilitzar.

## Conceptes Bàsics

### Taules i Cadenes

Iptables organitza les seves regles en **taules** i **cadenes**:

- **Taules**: Contenen cadenes i s'utilitzen per organitzar regles segons el tipus de decisions.
    
    - `filter`: Taula per defecte, s'utilitza per filtrar paquets.
    - `nat`: S'utilitza per la traducció d'adreces de xarxa (NAT).
    - `mangle`: Per a modificacions especialitzades de paquets.
    - `raw`: S'utilitza principalment per configurar exempcions del seguiment de connexions.

- **Cadenes**: Contenen conjunts de regles dins de cada taula.
    
    - `INPUT`: Per a paquets destinats al sistema local.
    - `OUTPUT`: Per a paquets generats localment.
    - `FORWARD`: Per a paquets que passen a través del sistema.
    - `PREROUTING`: Per a modificacions de paquets just quan arriben.
    - `POSTROUTING`: Per a modificacions de paquets just abans que surtin.

### Polítiques per Defecte

Cada cadena té una política per defecte que s'aplica quan un paquet no coincideix amb cap regla:

```bash
# Establir política per defecte per rebutjar tot el tràfic entrant
sudo iptables -P INPUT DROP

# Establir política per defecte per permetre tot el tràfic sortint
sudo iptables -P OUTPUT ACCEPT

# Establir política per defecte per rebutjar tot el tràfic de reenviament
sudo iptables -P FORWARD DROP
```

## Instal·lació

En la majoria de distribucions Linux, iptables ve preinstal·lat. En cas contrari, pots instal·lar-lo amb:

### Debian/Ubuntu:

```bash
sudo apt update
sudo apt install iptables
```

### CentOS/RHEL:

```bash
sudo yum install iptables-services
```

### Arch Linux:

```bash
sudo pacman -S iptables
```

## Comandes Bàsiques

### Visualitzar Regles Actuals

```bash
# Visualitzar regles de la taula filter (per defecte)
sudo iptables -L

# Amb números de línia i sense resolució de noms
sudo iptables -L -n --line-numbers

# Visualitzar regles de la taula nat
sudo iptables -t nat -L

# Visualitzar regles amb estadístiques de paquets i bytes
sudo iptables -L -v
```

### Afegir Regles

```bash
# Sintaxi general
sudo iptables -t [taula] -A [cadena] [coincidència] -j [acció]
```

Exemples comuns:

```bash
# Permetre SSH (port 22)
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT

# Permetre HTTP (port 80)
sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT

# Permetre HTTPS (port 443)
sudo iptables -A INPUT -p tcp --dport 443 -j ACCEPT

# Permetre DNS
sudo iptables -A INPUT -p udp --dport 53 -j ACCEPT
sudo iptables -A INPUT -p tcp --dport 53 -j ACCEPT
```

### Eliminar Regles

```bash
# Eliminar per número de línia
sudo iptables -D INPUT [número]

# Eliminar una regla específica
sudo iptables -D INPUT -p tcp --dport 80 -j ACCEPT

# Buidar una cadena específica
sudo iptables -F INPUT

# Buidar totes les cadenes
sudo iptables -F
```

### Modificar Regles

```bash
# Substituir una regla
sudo iptables -R INPUT [número] -p tcp --dport 8080 -j ACCEPT
```

### Inserir Regles

```bash
# Inserir una regla en la posició específica
sudo iptables -I INPUT [número] -p tcp --dport 8080 -j ACCEPT
```

## Accions Comunes

- `ACCEPT`: Permet el paquet.
- `DROP`: Descarta el paquet sense notificar l'emissor.
- `REJECT`: Rebutja el paquet i notifica l'emissor.
- `LOG`: Registra el paquet als logs del sistema.
- `REDIRECT`: Redirigeix el paquet a un altre port.
- `MASQUERADE`: Emmascarar una IP (utilitzada per a NAT).
- `DNAT`: Traducció d'adreça de destinació.
- `SNAT`: Traducció d'adreça d'origen.

## Regles Avançades

### Filtrar per Adreça IP o Subxarxa

```bash
# Permetre tràfic d'una IP específica
sudo iptables -A INPUT -s 192.168.1.100 -j ACCEPT

# Permetre tràfic d'una subxarxa
sudo iptables -A INPUT -s 192.168.1.0/24 -j ACCEPT

# Bloquejar una IP específica
sudo iptables -A INPUT -s 10.0.0.5 -j DROP
```

### Filtrar per Interfície

```bash
# Permetre tràfic entrant en l'interfície eth0
sudo iptables -A INPUT -i eth0 -j ACCEPT

# Permetre tràfic sortint per l'interfície eth0
sudo iptables -A OUTPUT -o eth0 -j ACCEPT
```

### Filtrar per Estat de Connexió

```bash
# Permetre tràfic relacionat amb connexions establertes
sudo iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT

# Permetre noves connexions sortints
sudo iptables -A OUTPUT -m state --state NEW -j ACCEPT
```

### Limitar Connexions

```bash
# Limitar connexions SSH a 3 per minut
sudo iptables -A INPUT -p tcp --dport 22 -m state --state NEW -m recent --set
sudo iptables -A INPUT -p tcp --dport 22 -m state --state NEW -m recent --update --seconds 60 --hitcount 4 -j DROP
```

### Redirecció de Ports

```bash
# Redirigir el tràfic del port 80 al port 8080
sudo iptables -t nat -A PREROUTING -p tcp --dport 80 -j REDIRECT --to-port 8080
```

## Configuracions d'Exemple

### Tallafocs Bàsic per a Servidor Web

```bash
# Buidar totes les regles
sudo iptables -F

# Establir polítiques per defecte
sudo iptables -P INPUT DROP
sudo iptables -P FORWARD DROP
sudo iptables -P OUTPUT ACCEPT

# Permetre connexions establertes i relacionades
sudo iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT

# Permetre loopback
sudo iptables -A INPUT -i lo -j ACCEPT

# Permetre SSH, HTTP i HTTPS
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT
sudo iptables -A INPUT -p tcp --dport 443 -j ACCEPT

# Permetre ping (opcional)
sudo iptables -A INPUT -p icmp --icmp-type echo-request -j ACCEPT

# Registrar els paquets rebutjats
sudo iptables -A INPUT -j LOG --log-prefix "IPTables-Dropped: "
```

### Router/NAT Bàsic

```bash
# Habilitar IP forwarding
echo 1 > /proc/sys/net/ipv4/ip_forward

# Configurar NAT per a una xarxa interna (suposant que eth0 és l'interfície externa)
sudo iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE

# Permetre tràfic de reenviament
sudo iptables -A FORWARD -i eth1 -o eth0 -j ACCEPT
sudo iptables -A FORWARD -i eth0 -o eth1 -m state --state ESTABLISHED,RELATED -j ACCEPT
```

## Persistència de Regles

Les regles d'iptables no persisteixen després de reiniciar el sistema a menys que es configurin explícitament.

### Debian/Ubuntu

```bash
# Instal·lar el paquet de persistència
sudo apt install iptables-persistent

# Guardar les regles actuals
sudo netfilter-persistent save

# Recarregar les regles
sudo netfilter-persistent reload
```

### CentOS/RHEL

```bash
# Guardar les regles actuals
sudo service iptables save

# Assegurar-se que el servei s'inicia amb el sistema
sudo systemctl enable iptables
```

### Script Manual

Alternativament, pots crear un script que s'executi a l'inici del sistema:

```bash
#!/bin/bash
# Guardar en /etc/network/if-pre-up.d/iptables

# Restaurar regles des d'un fitxer
iptables-restore < /etc/iptables.rules

exit 0
```

I fer-lo executable:

```bash
sudo chmod +x /etc/network/if-pre-up.d/iptables
```

## Guardar i Restaurar Regles

```bash
# Guardar regles a un fitxer
sudo iptables-save > /etc/iptables.rules

# Restaurar regles des d'un fitxer
sudo iptables-restore < /etc/iptables.rules
```

## Resolució de Problemes

### Registres del Sistema

Els registres d'iptables es poden trobar normalment a `/var/log/syslog` o `/var/log/messages`:

```bash
sudo grep "IPTables" /var/log/syslog
```

### Depuració

```bash
# Utilitzar l'opció -v per a més informació
sudo iptables -v -L

# Registrar paquets que coincideixen amb una regla específica
sudo iptables -A INPUT -p tcp --dport 80 -j LOG --log-prefix "HTTP Request: "
```

### Problemes Comuns

1. **Has bloquejat la teva connexió SSH**: Si t'has bloquejat a tu mateix, hauràs d'accedir físicament al servidor per corregir les regles d'iptables.
    
2. **No es pot accedir a serveis web**: Comprova que has permès els ports HTTP (80) i HTTPS (443).
    
3. **Les regles no es carreguen després de reiniciar**: Has d'utilitzar un dels mètodes de persistència descrits anteriorment.
    

## Consells de Seguretat

1. **Començar amb Polítiques Restrictives**: Estableix polítiques per defecte de DROP i afegeix regles específiques per permetre només el tràfic necessari.
    
2. **Utilitzar l'Estat de Connexió**: Utilitza sempre el mòdul state per permetre tràfic relacionat amb connexions establertes.
    
3. **Protegir el Servei SSH**: Limita les connexions SSH per evitar atacs de força bruta.
    
4. **Mantenir les Regles Simples**: Evita configuracions massa complexes que puguin tenir conseqüències no desitjades.
    
5. **Provar les Regles**: Sempre prova les teves regles abans d'aplicar-les en un entorn de producció.
    

## Comandes Útils de Referència Ràpida

```bash
# Visualitzar totes les regles
sudo iptables -L -v -n --line-numbers

# Buidar totes les regles
sudo iptables -F

# Permetre localhost
sudo iptables -A INPUT -i lo -j ACCEPT

# Permetre SSH
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT

# Permetre connexions establertes
sudo iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT

# Bloquejar una IP
sudo iptables -A INPUT -s 123.456.789.0 -j DROP

# Registrar i després eliminar tràfic
sudo iptables -A INPUT -j LOG --log-prefix "IPTables-Dropped: " --log-level 7
sudo iptables -A INPUT -j DROP
```

## Conclusió

Iptables és una eina potent per gestionar el tallafocs a Linux, però requereix una comprensió clara dels conceptes i la sintaxi. Amb aquesta guia, hauries de poder configurar un tallafocs bàsic o avançat segons les teves necessitats. Recorda sempre fer còpies de seguretat de les teves regles i provar-les abans d'aplicar-les en entorns crítics.