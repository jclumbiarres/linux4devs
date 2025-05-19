# Introducció a NFS (Network File System) a GNU/Linux

## Què és NFS?

NFS (Network File System) és un protocol que permet compartir fitxers i directoris entre diferents ordinadors a través d'una xarxa. És una eina molt útil per a entorns on diversos usuaris o sistemes necessiten accedir als mateixos recursos de manera remota, com si estiguessin en el seu propi ordinador.

NFS és especialment popular en sistemes GNU/Linux i UNIX, però també pot ser utilitzat en altres sistemes operatius. Aquest protocol permet que un ordinador actuï com a servidor, compartint fitxers, mentre que altres ordinadors actuen com a clients, accedint a aquests fitxers compartits.

---

## Per què utilitzar NFS?

### Avantatges:

1. **Facilitat d'ús**: Els fitxers compartits es poden muntar com si fossin part del sistema de fitxers local.
2. **Eficiència**: Permet compartir recursos sense necessitat de duplicar fitxers en diferents màquines.
3. **Integració**: Funciona de manera nativa en sistemes GNU/Linux i UNIX.
4. **Flexibilitat**: Es pot configurar per adaptar-se a diferents necessitats, com ara permisos d'accés i seguretat.

### Casos d'ús:

- Compartir directoris entre servidors en un centre de dades.
- Permetre que diversos usuaris accedeixin a fitxers comuns en una xarxa local.
- Crear còpies de seguretat centralitzades.

---

## Com funciona NFS?

NFS segueix un model client-servidor:

- **Servidor NFS**: És l'ordinador que comparteix els seus fitxers o directoris.
- **Client NFS**: És l'ordinador que accedeix als fitxers compartits pel servidor.

Els passos bàsics són:

1. El servidor exporta (comparteix) un directori.
2. El client munta aquest directori al seu sistema de fitxers local.
3. El client pot accedir als fitxers com si fossin locals.

---

## Configuració d'un servidor NFS

### 1. Instal·lació del programari necessari

En una distribució basada en Debian (com Ubuntu), pots instal·lar el servidor NFS amb:

```bash
sudo apt update
sudo apt install nfs-kernel-server
```

En distribucions basades en Red Hat (com CentOS o Fedora):

```bash
sudo dnf install nfs-utils
```

### 2. Configuració dels directoris a compartir

Edita el fitxer `/etc/exports` per definir els directoris que vols compartir. Per exemple:

```
/home/usuari/compartit 192.168.1.0/24(rw,sync,no_subtree_check)
```

- **`/home/usuari/compartit`**: És el directori que vols compartir.
- **`192.168.1.0/24`**: Indica la xarxa que pot accedir al directori.
- **`rw`**: Permet lectura i escriptura.
- **`sync`**: Garanteix que les dades s'escriguin immediatament al disc.
- **`no_subtree_check`**: Millora el rendiment en alguns casos.

Després de modificar aquest fitxer, aplica els canvis amb:

```bash
sudo exportfs -ra
```

### 3. Iniciar el servei NFS

Assegura't que el servei NFS està en funcionament:

```bash
sudo systemctl start nfs-server
sudo systemctl enable nfs-server
```

---

## Configuració d'un client NFS

### 1. Instal·lació del programari necessari

En sistemes basats en Debian:

```bash
sudo apt install nfs-common
```

En sistemes basats en Red Hat:

```bash
sudo dnf install nfs-utils
```

### 2. Muntar un directori NFS

Per muntar un directori compartit pel servidor, utilitza la comanda `mount`. Per exemple:

```bash
sudo mount 192.168.1.100:/home/usuari/compartit /mnt/nfs
```

- **`192.168.1.100`**: És l'adreça IP del servidor NFS.
- **`/home/usuari/compartit`**: És el directori compartit pel servidor.
- **`/mnt/nfs`**: És el punt de muntatge al client.

### 3. Muntatge automàtic

Per muntar automàticament el directori en reiniciar el sistema, afegeix una línia al fitxer `/etc/fstab`:

```
192.168.1.100:/home/usuari/compartit /mnt/nfs nfs defaults 0 0
```

---

## Seguretat en NFS

Tot i que NFS és molt útil, cal tenir en compte alguns aspectes de seguretat:

1. **Restricció d'accés**: Utilitza adreces IP o rangs de xarxa per limitar qui pot accedir als recursos compartits.
2. **Firewall**: Configura el tallafocs per permetre només el trànsit necessari per a NFS.
3. **Autenticació**: Considera utilitzar Kerberos per a una autenticació més segura.

---

## Resolució de problemes comuns

### 1. Error de muntatge

- Assegura't que el servidor NFS està en funcionament.
- Verifica que el directori està exportat correctament amb `exportfs -v`.

### 2. Problemes de permisos

- Comprova els permisos del directori compartit al servidor.
- Assegura't que els usuaris al client tenen els permisos adequats.

### 3. Rendiment lent

- Utilitza l'opció `async` en lloc de `sync` si el rendiment és una prioritat.
- Optimitza la configuració de la xarxa.
