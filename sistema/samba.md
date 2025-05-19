# Introducció a Samba en GNU/Linux

Samba és una implementació lliure del protocol SMB/CIFS que permet la interoperabilitat entre sistemes operatius GNU/Linux i Windows. És una eina essencial per compartir fitxers i impressores en xarxes mixtes, i és àmpliament utilitzada tant en entorns domèstics com empresarials.

## Què és Samba?

Samba és un programari que permet que un sistema GNU/Linux actuï com un servidor o client en una xarxa Windows. Això significa que pots compartir carpetes, fitxers i impressores entre ordinadors amb diferents sistemes operatius. Samba utilitza el protocol SMB (Server Message Block), que és el mateix que utilitza Windows per a la compartició de recursos.

### Característiques principals:

- Compartició de fitxers i impressores.
- Autenticació d'usuaris i gestió de permisos.
- Integració amb dominis Windows (Active Directory).
- Capacitat per actuar com un controlador de domini.

---

## Instal·lació de Samba

### Requisits previs

Abans d'instal·lar Samba, assegura't que el teu sistema està actualitzat. Pots fer-ho amb les següents comandes:

```bash
sudo apt update
sudo apt upgrade
```

### Instal·lació

Per instal·lar Samba en una distribució basada en Debian (com Ubuntu), executa:

```bash
sudo apt install samba
```

Per verificar que Samba s'ha instal·lat correctament, pots comprovar la seva versió:

```bash
smbd --version
```

---

## Configuració bàsica de Samba

El fitxer principal de configuració de Samba és `/etc/samba/smb.conf`. Aquest fitxer conté totes les opcions necessàries per personalitzar el comportament de Samba.

### Exemple de configuració

A continuació, es mostra un exemple bàsic per compartir una carpeta:

1. Obre el fitxer de configuració amb un editor de text:

   ```bash
   sudo nano /etc/samba/smb.conf
   ```

2. Afegeix la següent configuració al final del fitxer:

   ```ini
   [Compartida]
   path = /home/usuari/compartida
   browseable = yes
   read only = no
   guest ok = yes
   ```

3. Crea la carpeta que vols compartir:

   ```bash
   mkdir -p /home/usuari/compartida
   ```

4. Assigna els permisos adequats:

   ```bash
   chmod 777 /home/usuari/compartida
   ```

5. Reinicia el servei de Samba perquè els canvis tinguin efecte:
   ```bash
   sudo systemctl restart smbd
   ```

---

## Prova de la configuració

Per comprovar que la carpeta compartida està disponible, pots utilitzar un ordinador amb Windows i accedir-hi mitjançant l'explorador de fitxers. Escriu l'adreça IP del servidor GNU/Linux seguit de la carpeta compartida, per exemple:

```
\\192.168.1.100\Compartida
```

---

## Gestió d'usuaris

Samba permet gestionar usuaris específics per accedir als recursos compartits. A continuació, es mostra com afegir un usuari:

1. Crea un usuari al sistema:

   ```bash
   sudo adduser nom_usuari
   ```

2. Afegeix l'usuari a Samba:

   ```bash
   sudo smbpasswd -a nom_usuari
   ```

3. Activa l'usuari:
   ```bash
   sudo smbpasswd -e nom_usuari
   ```

---

## Integració amb Active Directory

Samba també pot actuar com un membre d'un domini Active Directory o fins i tot com un controlador de domini. Aquesta funcionalitat és útil en entorns empresarials.

### Configuració avançada

Per integrar Samba amb Active Directory, necessitaràs instal·lar paquets addicionals com `winbind` i configurar el fitxer `/etc/samba/smb.conf` amb les opcions adequades.

---

## Resolució de problemes

### Comprovar l'estat del servei

Si Samba no funciona correctament, pots comprovar l'estat del servei amb:

```bash
sudo systemctl status smbd
```

### Registres

Els registres de Samba es troben normalment a `/var/log/samba/`. Revisa aquests fitxers per obtenir informació detallada sobre errors.
