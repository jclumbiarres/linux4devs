# Introducció a OpenLDAP en GNU/Linux

OpenLDAP és una implementació de codi obert del protocol LDAP (Lightweight Directory Access Protocol). LDAP és un protocol utilitzat per accedir i gestionar serveis d'informació distribuïts, com ara directoris d'usuaris, grups, permisos i altres dades.

---

## Què és LDAP i per a què serveix?

LDAP és un protocol que permet accedir a un directori jeràrquic d'informació. Un directori és com una base de dades, però optimitzada per a lectures ràpides i consultes. Alguns exemples d'ús d'LDAP són:

- Gestionar usuaris i contrasenyes en una xarxa.
- Centralitzar l'autenticació d'usuaris en diversos sistemes.
- Emmagatzemar informació sobre recursos, com ara impressores o dispositius.

OpenLDAP és una eina que implementa aquest protocol i permet crear i gestionar aquests directoris.

---

## Components principals d'OpenLDAP

Abans de començar a treballar amb OpenLDAP, és important entendre els seus components bàsics:

1. **Servidor LDAP**: És el servei que emmagatzema i proporciona accés al directori.
2. **Base de dades LDAP**: Conté la informació organitzada en una estructura jeràrquica.
3. **Client LDAP**: És l'aplicació que interactua amb el servidor per consultar o modificar dades.
4. **Schema**: Defineix l'estructura de les dades, com ara quins tipus d'atributs i objectes es poden emmagatzemar.

---

## Instal·lació d'OpenLDAP en GNU/Linux

### Requisits previs

Abans d'instal·lar OpenLDAP, assegura't de tenir accés a un sistema GNU/Linux amb permisos d'administrador. També és recomanable tenir coneixements bàsics sobre la línia de comandes.

### Instal·lació

1. **Actualitza els repositoris del sistema**:

   ```bash
   sudo apt update
   ```

2. **Instal·la el paquet d'OpenLDAP**:

   ```bash
   sudo apt install slapd ldap-utils
   ```

3. **Configura el servidor LDAP**:
   Durant la instal·lació, se't demanarà que configuris una contrasenya d'administrador per al directori LDAP. Aquesta contrasenya serà necessària per gestionar el servidor.

4. **Verifica la instal·lació**:
   Pots comprovar que el servei està funcionant amb:
   ```bash
   sudo systemctl status slapd
   ```

---

## Configuració bàsica d'OpenLDAP

### Configuració inicial

Després d'instal·lar OpenLDAP, és necessari configurar-lo per adaptar-lo a les teves necessitats. Això inclou definir el domini, afegir usuaris i establir permisos.

1. **Reconfigura el servidor si cal**:
   Si necessites canviar la configuració inicial, pots executar:

   ```bash
   sudo dpkg-reconfigure slapd
   ```

2. **Defineix el domini**:
   Durant la configuració, se't demanarà que introdueixis el nom del domini. Per exemple, si el teu domini és `exemple.com`, el directori LDAP utilitzarà `dc=exemple,dc=com`.

3. **Afegir un esquema**:
   Els esquemes defineixen quins tipus de dades es poden emmagatzemar. Per exemple, pots carregar l'esquema `inetorgperson` per gestionar usuaris.

   ```bash
   ldapadd -Y EXTERNAL -H ldapi:/// -f /etc/ldap/schema/inetorgperson.ldif
   ```

---

## Estructura del directori LDAP

L'estructura d'un directori LDAP és jeràrquica, similar a un arbre. Els elements principals són:

- **Entrades**: Cada element del directori, com un usuari o un grup.
- **DN (Distinguished Name)**: Identificador únic per a cada entrada.
- **Atributs**: Informació associada a una entrada, com ara el nom, correu electrònic, etc.

Exemple d'estructura:

```
dc=exemple,dc=com
├── ou=usuaris
│   ├── cn=Joan
│   ├── cn=Maria
├── ou=grups
     ├── cn=admins
     ├── cn=usuaris
```

---

## Com afegir usuaris al directori LDAP

1. **Crea un fitxer LDIF**:
   Un fitxer LDIF (LDAP Data Interchange Format) conté les dades que vols afegir al directori. Per exemple, per afegir un usuari:

   ```ldif
   dn: cn=Joan,ou=usuaris,dc=exemple,dc=com
   objectClass: inetOrgPerson
   cn: Joan
   sn: Garcia
   mail: joan@exemple.com
   userPassword: contrasenya123
   ```

2. **Afegeix l'usuari al directori**:
   Utilitza la comanda `ldapadd` per afegir l'usuari:

   ```bash
   ldapadd -x -D "cn=admin,dc=exemple,dc=com" -W -f usuari.ldif
   ```

3. **Verifica l'entrada**:
   Pots comprovar que l'usuari s'ha afegit correctament amb:
   ```bash
   ldapsearch -x -LLL -b "dc=exemple,dc=com" "cn=Joan"
   ```

---

## Autenticació amb OpenLDAP

Un dels usos més comuns d'OpenLDAP és centralitzar l'autenticació d'usuaris. Això permet que els usuaris iniciïn sessió en diversos sistemes utilitzant les mateixes credencials.

### Configuració del client LDAP

1. **Instal·la els paquets necessaris**:

   ```bash
   sudo apt install libnss-ldap libpam-ldap ldap-utils
   ```

2. **Configura el client**:
   Durant la instal·lació, se't demanarà que introdueixis el domini LDAP i la contrasenya d'administrador.

3. **Habilita l'autenticació LDAP**:
   Edita el fitxer `/etc/nsswitch.conf` i assegura't que les línies següents inclouen `ldap`:

   ```
   passwd:         files ldap
   group:          files ldap
   shadow:         files ldap
   ```

4. **Prova l'autenticació**:
   Intenta iniciar sessió amb un usuari definit al directori LDAP.

---

## Resolució de problemes comuns

1. **El servei slapd no arrenca**:

   - Comprova els registres del sistema:
     ```bash
     sudo journalctl -u slapd
     ```

2. **Error d'autenticació**:

   - Assegura't que la contrasenya d'administrador és correcta.
   - Verifica que el fitxer LDIF està ben format.

3. **No es poden afegir usuaris**:
   - Comprova els permisos del directori.
   - Revisa l'esquema utilitzat.
