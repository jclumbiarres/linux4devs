# Pi-hole: Explicació Exhaustiva

## Què és Pi-hole?

**Pi-hole** és un programari de codi obert que actua com a bloquejador de publicitat a nivell de xarxa. S’instal·la habitualment en una Raspberry Pi, però també pot funcionar en altres dispositius Linux. Pi-hole intercepta les sol·licituds DNS de tots els dispositius connectats a la xarxa i bloqueja aquelles que corresponen a dominis de publicitat, rastreig o malware.

## Característiques Principals

- **Bloqueig de publicitat a nivell de xarxa:** Tots els dispositius connectats a la xarxa es beneficien del bloqueig, sense necessitat d’instal·lar extensions als navegadors.
- **Interfície web:** Permet monitoritzar l’activitat DNS, veure estadístiques i gestionar llistes de bloqueig.
- **Llistes de bloqueig personalitzables:** Es poden afegir o eliminar llistes de dominis bloquejats segons les necessitats.
- **Integració amb DHCP:** Pi-hole pot actuar com a servidor DHCP, gestionant les IPs de la xarxa.
- **Protecció contra malware i rastrejadors:** Bloqueja dominis coneguts per distribuir malware o rastrejar l’activitat dels usuaris.

## Funcionament

Pi-hole funciona com un servidor DNS local. Quan un dispositiu de la xarxa fa una consulta DNS (per exemple, per carregar una pàgina web), Pi-hole comprova si el domini està a la llista de bloqueig. Si és així, la consulta es bloqueja i el contingut no es carrega. Si no, Pi-hole resol la consulta normalment.

## Instal·lació

### Requisits

- Una Raspberry Pi (o qualsevol dispositiu Linux)
- Connexió a Internet
- Accés SSH o físic al dispositiu

### Passos d’instal·lació

1. **Actualitza el sistema:**
    ```bash
    sudo apt update && sudo apt upgrade
    ```
2. **Instal·la Pi-hole:**
    ```bash
    curl -sSL https://install.pi-hole.net | bash
    ```
3. **Segueix l’assistent d’instal·lació:** Selecciona la interfície de xarxa, el servidor DNS extern (Google, Cloudflare, etc.), i configura les llistes de bloqueig.

## Configuració

### Configuració bàsica

- **Accés a la interfície web:** Normalment a `http://<IP_de_la_Raspberry_Pi>/admin`
- **Usuari i contrasenya:** Es genera una contrasenya durant la instal·lació. Pots canviar-la amb:
  ```bash
  pihole -a -p
  ```

### Afegir llistes de bloqueig

A la interfície web, ves a *Group Management > Adlists* i afegeix URLs de llistes de bloqueig, com per exemple:
- https://raw.githubusercontent.com/StevenBlack/hosts/master/hosts
- https://mirror1.malwaredomains.com/files/justdomains

### Configuració del router

Perquè Pi-hole bloquegi la publicitat a tota la xarxa, configura el router perquè utilitzi la IP de Pi-hole com a servidor DNS principal.

### DHCP

Si vols que Pi-hole gestioni les IPs de la xarxa, activa el servidor DHCP des de la interfície web (*Settings > DHCP*).

## Exemples de configuració

### Exemple de configuració de DNS en un dispositiu

A Windows:
1. Ves a *Configuració de xarxa*.
2. Edita les propietats de la connexió.
3. Introdueix la IP de Pi-hole com a servidor DNS.

A Linux:
Edita `/etc/resolv.conf`:
```
nameserver <IP_de_Pi-hole>
```

### Exemple d’afegir una llista de bloqueig

A la interfície web:
1. Ves a *Group Management > Adlists*.
2. Fes clic a *Add a new adlist*.
3. Introdueix la URL i guarda.

## Monitorització i Estadístiques

Pi-hole mostra estadístiques en temps real:
- Nombre de consultes bloquejades
- Dominis més sol·licitats
- Dispositius més actius

## Avantatges i Limitacions

### Avantatges

- Reducció de publicitat i rastreig
- Millora de la velocitat de navegació
- Protecció contra malware

### Limitacions

- No bloqueja publicitat incrustada en vídeos (YouTube, etc.)
- Algunes webs poden no funcionar correctament si es bloquegen dominis essencials

## Recursos Addicionals

- [Documentació oficial de Pi-hole](https://docs.pi-hole.net/)
- [Llistes de bloqueig recomanades](https://firebog.net/)
- [Comunitat Pi-hole](https://discourse.pi-hole.net/)

---

Pi-hole és una eina potent per millorar la privacitat i la seguretat a la teva xarxa domèstica. Amb una configuració adequada, pots controlar la publicitat i el rastreig de manera centralitzada i eficient.