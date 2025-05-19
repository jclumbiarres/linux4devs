
## Introducció

UFW (Uncomplicated Firewall) és una interfície simplificada per a iptables que facilita la configuració i gestió d'un tallafocs en sistemes Linux. Com el seu nom indica, UFW està dissenyat per ser fàcil d'utilitzar i configurar, sense necessitat de conèixer les complexitats d'iptables.

## Instal·lació

En la majoria de distribucions basades en Ubuntu, UFW ve preinstal·lat. Si no és el cas, pots instal·lar-lo amb:

```bash
sudo apt update
sudo apt install ufw
```

Per a distribucions basades en Fedora/RHEL:

```bash
sudo dnf install ufw
```

Per a Arch Linux:

```bash
sudo pacman -S ufw
```

## Comandes bàsiques

### Comprovar l'estat d'UFW

```bash
sudo ufw status
```

Per obtenir informació més detallada:

```bash
sudo ufw status verbose
```

Per veure les regles numerades:

```bash
sudo ufw status numbered
```

### Activar i desactivar UFW

Activar UFW:

```bash
sudo ufw enable
```

Desactivar UFW:

```bash
sudo ufw disable
```

Reiniciar UFW:

```bash
sudo ufw reload
```

### Configurar regles predeterminades

Denegar tot el tràfic entrant:

```bash
sudo ufw default deny incoming
```

Permetre tot el tràfic sortint:

```bash
sudo ufw default allow outgoing
```

## Gestió de regles

### Permetre o denegar serveis

Permetre SSH:

```bash
sudo ufw allow ssh
```

O utilitzant el número de port:

```bash
sudo ufw allow 22
```

Permetre el tràfic HTTP i HTTPS:

```bash
sudo ufw allow http
sudo ufw allow https
```

O utilitzant els números de port:

```bash
sudo ufw allow 80
sudo ufw allow 443
```

### Especificar el protocol (TCP/UDP)

Permetre el port 53 només per a tràfic UDP (DNS):

```bash
sudo ufw allow 53/udp
```

Permetre el port 53 només per a tràfic TCP:

```bash
sudo ufw allow 53/tcp
```

### Gestió de rangs de ports

Permetre un rang de ports:

```bash
sudo ufw allow 6000:6007/tcp
```

### Denegar serveis

Denegar el tràfic SSH:

```bash
sudo ufw deny ssh
```

O utilitzant el número de port:

```bash
sudo ufw deny 22
```

### Regles per a adreces IP específiques

Permetre connexions des d'una adreça IP específica:

```bash
sudo ufw allow from 192.168.1.100
```

Permetre connexions des d'una adreça IP específica a un port específic:

```bash
sudo ufw allow from 192.168.1.100 to any port 22
```

### Regles per a subxarxes

Permetre connexions des d'una subxarxa específica:

```bash
sudo ufw allow from 192.168.1.0/24
```

Permetre connexions des d'una subxarxa a un port específic:

```bash
sudo ufw allow from 192.168.1.0/24 to any port 3306
```

### Eliminar regles

Eliminar una regla específica (primer llistar-les amb números):

```bash
sudo ufw status numbered
sudo ufw delete [número]
```

Per exemple, per eliminar la regla número 3:

```bash
sudo ufw delete 3
```

O eliminar una regla específica pel seu contingut:

```bash
sudo ufw delete allow 80
```

## Configuració avançada

### Especificar la interfície

Permetre SSH només en una interfície específica:

```bash
sudo ufw allow in on eth0 to any port 22
```

### Limitar intents de connexió

Limitar els intents de connexió SSH (útil per evitar atacs de força bruta):

```bash
sudo ufw limit ssh
```

### Regles per a connexions establertes

Permetre connexions establertes i relacionades:

```bash
sudo ufw allow established
```

## Registres (Logs)

### Activar el registre

```bash
sudo ufw logging on
```

Establir el nivell de registre (low, medium, high, full):

```bash
sudo ufw logging medium
```

### Desactivar el registre

```bash
sudo ufw logging off
```

### Visualitzar els registres

```bash
sudo less /var/log/ufw.log
```

## Aplicacions

UFW inclou perfils d'aplicacions que faciliten la gestió de regles.

### Llistar les aplicacions disponibles

```bash
sudo ufw app list
```

### Obtenir informació d'una aplicació específica

```bash
sudo ufw app info "Nginx Full"
```

### Permetre o denegar una aplicació

```bash
sudo ufw allow "Nginx Full"
sudo ufw deny "Nginx Full"
```

## Configuracions d'exemple

### Configuració bàsica d'un servidor web

```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow ssh
sudo ufw allow http
sudo ufw allow https
sudo ufw enable
```

### Configuració d'un servidor de desenvolupament local

```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow ssh
sudo ufw allow from 192.168.1.0/24 to any port 3000
sudo ufw allow from 192.168.1.0/24 to any port 8080
sudo ufw enable
```

### Configuració d'un servidor de base de dades

```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow ssh
sudo ufw allow from 192.168.1.0/24 to any port 3306
sudo ufw enable
```

## Resolució de problemes

### Reiniciar UFW

Si trobes problemes amb les regles o la configuració, prova de reiniciar UFW:

```bash
sudo ufw reset
```

Això eliminarà totes les regles i et permetrà començar de nou.

### Verificar configuració

Per verificar la configuració d'UFW sense activar-lo:

```bash
sudo ufw show raw
```

### Problemes comuns

#### No es pot accedir al servidor després d'activar UFW

Assegura't d'haver permès les connexions SSH abans d'activar UFW:

```bash
sudo ufw allow ssh
sudo ufw enable
```

#### Errors en les regles

Si una regla no funciona com s'espera, comprova els registres:

```bash
sudo grep UFW /var/log/syslog
```

## Consells de seguretat

1. **Principi de mínims privilegis**: Permet només els serveis i ports necessaris.
2. **Actualitza regularment**: Mantén el sistema i UFW actualitzats.
3. **Monitoritza els registres**: Revisa els registres per detectar possibles intents d'intrusió.
4. **Utilitza limitacions de connexions**: Utilitza la comanda `ufw limit` per evitar atacs de força bruta.
5. **Configura les regles predeterminades**: Estableix una política predeterminada "deny incoming" i "allow outgoing".

## Conclusió

UFW és una eina potent i senzilla que et permet protegir el teu sistema Linux. Amb les comandes i configuracions que hem vist en aquesta guia, pots configurar un tallafocs efectiu per al teu sistema o servidor.

Recorda que la seguretat és un procés continu, i és recomanable revisar i actualitzar regularment les regles del tallafocs segons les necessitats canviants del teu sistema.