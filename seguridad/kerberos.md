# Introducció a Kerberos en GNU/Linux

Kerberos és un protocol d'autenticació de xarxa dissenyat per proporcionar una comunicació segura entre clients i servidors en una xarxa no segura. En aquest document, explorarem els conceptes bàsics de Kerberos, com funciona, i com es pot implementar en un sistema GNU/Linux. Aquesta explicació està pensada per a persones amb pocs coneixements tècnics, així que anirem pas a pas.

---

## Què és Kerberos?

Kerberos és un sistema d'autenticació que utilitza un model de "tercer de confiança". Això significa que un servidor centralitzat, conegut com a **Key Distribution Center (KDC)**, gestiona les credencials d'autenticació dels usuaris i serveis. El protocol es basa en la criptografia de clau simètrica i utilitza "tickets" per autenticar els usuaris sense necessitat d'enviar contrasenyes a través de la xarxa.

### Per què utilitzar Kerberos?

1. **Seguretat**: Les contrasenyes no es transmeten mai per la xarxa, reduint el risc d'intercepció.
2. **Autenticació única (Single Sign-On)**: Els usuaris només han d'iniciar sessió una vegada per accedir a múltiples serveis.
3. **Escalabilitat**: És adequat per a xarxes grans amb molts usuaris i serveis.

---

## Components principals de Kerberos

Kerberos es compon de tres elements principals:

1. **Key Distribution Center (KDC)**:

   - És el cor del sistema Kerberos.
   - Conté dues parts:
     - **Authentication Server (AS)**: Autentica els usuaris i emet un "Ticket Granting Ticket (TGT)".
     - **Ticket Granting Server (TGS)**: Proporciona tickets per accedir a serveis específics.

2. **Client**:

   - És l'usuari o aplicació que vol accedir a un servei.

3. **Servidor de serveis**:
   - És el servei al qual el client vol accedir (per exemple, un servidor de fitxers o una base de dades).

---

## Com funciona Kerberos?

El procés d'autenticació de Kerberos es divideix en tres passos principals:

### 1. Autenticació inicial

- L'usuari introdueix el seu nom d'usuari i contrasenya.
- El client envia una sol·licitud al **Authentication Server (AS)** del KDC.
- Si les credencials són correctes, l'AS emet un **Ticket Granting Ticket (TGT)**, que està xifrat amb la clau del KDC.

### 2. Sol·licitud de servei

- Quan l'usuari vol accedir a un servei, el client utilitza el TGT per sol·licitar un ticket específic al **Ticket Granting Server (TGS)**.
- El TGS verifica el TGT i emet un ticket per al servei sol·licitat.

### 3. Accés al servei

- El client presenta el ticket al servidor de serveis.
- El servidor verifica el ticket i permet l'accés.

---

## Implementació de Kerberos en GNU/Linux

### Requisits previs

1. Un sistema GNU/Linux amb accés a la xarxa.
2. Paquets de Kerberos instal·lats (normalment `krb5-*`).
3. Un domini configurat per a Kerberos.

### Instal·lació dels paquets necessaris

```bash
sudo apt update
sudo apt install krb5-user krb5-kdc krb5-admin-server
```

Durant la instal·lació, se't demanarà que configuris el domini Kerberos. Introdueix el nom del domini (per exemple, `EXEMPLE.COM`).

### Configuració del KDC

Edita el fitxer de configuració principal de Kerberos:

```bash
sudo nano /etc/krb5.conf
```

Assegura't que el fitxer inclogui el domini i el realm:

```ini
[libdefaults]
     default_realm = EXEMPLE.COM

[realms]
     EXEMPLE.COM = {
          kdc = kdc.exemple.com
          admin_server = kdc.exemple.com
     }

[domain_realm]
     .exemple.com = EXEMPLE.COM
     exemple.com = EXEMPLE.COM
```

### Creació de la base de dades Kerberos

Inicialitza la base de dades del KDC:

```bash
sudo krb5_newrealm
```

### Creació de principals

Un "principal" és una identitat en Kerberos (pot ser un usuari o un servei). Per crear un principal:

```bash
sudo kadmin.local
addprinc usuari@EXEMPLE.COM
```

### Configuració del client

Edita el fitxer `/etc/krb5.conf` al client per apuntar al KDC.

Prova l'autenticació:

```bash
kinit usuari@EXEMPLE.COM
klist
```

---

## Avantatges i desavantatges de Kerberos

### Avantatges

- Alta seguretat.
- Reducció de la necessitat de múltiples contrasenyes.
- Compatible amb molts sistemes i serveis.

### Desavantatges

- Complexitat en la configuració.
- Dependència d'un servidor centralitzat (KDC).
- Pot ser difícil de diagnosticar problemes.
