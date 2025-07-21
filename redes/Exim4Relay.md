# Utilitzar Exim4 com a Relay de Gmail

Exim4 és un agent de transferència de correu (MTA) molt flexible i potent que es pot configurar per enviar correu electrònic a través d'un servidor SMTP extern, com ara Gmail. Aquesta configuració és útil si vols enviar correus des d'un servidor local però utilitzar la infraestructura de Gmail per a la lliurament.

## Requisits previs

- Un servidor amb Exim4 instal·lat (normalment en sistemes Debian/Ubuntu).
- Un compte de Gmail amb contrasenya o una contrasenya d'aplicació (recomanat per seguretat).
- Accés root o permisos d'administrador.

## Passos per configurar Exim4 com a relay de Gmail

### 1. Instal·lació d'Exim4

```bash
sudo apt update
sudo apt install exim4
```

### 2. Configuració bàsica d'Exim4

Executa la configuració interactiva:

```bash
sudo dpkg-reconfigure exim4-config
```

Respon les preguntes de la següent manera:

- **Mail sent by smarthost; received via SMTP or fetchmail**
- **System mail name:** El teu domini o hostname (ex: servidor.local)
- **IP addresses to listen on:** 127.0.0.1; ::1
- **Other destinations for which mail is accepted:** Deixa-ho en blanc o posa el teu domini.
- **Visible domain name for local users:** El teu domini.
- **Outgoing mail server (smarthost):** smtp.gmail.com::587
- **Hide local mail name in outgoing mail:** No
- **Keep number of DNS-queries minimal (Dial-on-Demand):** No
- **Split configuration into small files:** Sí (recomanat)

### 3. Configuració de l'autenticació SMTP

Edita el fitxer `/etc/exim4/passwd.client` i afegeix la següent línia:

```
smtp.gmail.com:TU_CORREU_GMAIL@gmail.com:CONTRASENYA_O_CONTRASENYA_APLICACIÓ
```

**Nota:** Si tens activada la verificació en dos passos a Gmail, has de crear una [contrasenya d'aplicació](https://support.google.com/accounts/answer/185833?hl=ca).

### 4. Configuració TLS/SSL

Assegura't que Exim4 utilitza TLS per connectar-se a Gmail. Edita (o crea) el fitxer `/etc/exim4/exim4.conf.localmacros` i afegeix:

```
MAIN_TLS_ENABLE = true
```

### 5. Actualitza la configuració

Després de fer els canvis, actualitza la configuració d'Exim4:

```bash
sudo update-exim4.conf
sudo systemctl restart exim4
```

### 6. Prova l'enviament de correu

Utilitza la comanda `mail` o `sendmail` per enviar un correu de prova:

```bash
echo "Prova d'Exim4 com a relay de Gmail" | mail -s "Test Exim4" destinatari@exemple.com
```

Revisa els logs a `/var/log/exim4/mainlog` per verificar que el correu s'ha enviat correctament.

## Consideracions de seguretat

- **Contrasenya d'aplicació:** No utilitzis la contrasenya principal del teu compte de Gmail. Utilitza sempre una contrasenya d'aplicació.
- **Protegeix el fitxer de contrasenyes:** Assegura't que `/etc/exim4/passwd.client` només sigui accessible per root:

```bash
sudo chmod 640 /etc/exim4/passwd.client
```

## Problemes comuns

- **Error d'autenticació:** Revisa la contrasenya i el nom d'usuari. Comprova que no hi ha espais extra.
- **Ports bloquejats:** Assegura't que el port 587 està obert al teu servidor.
- **TLS no activat:** Gmail requereix connexió segura. Comprova que `MAIN_TLS_ENABLE` està a `true`.

## Recursos addicionals

- [Documentació oficial d'Exim4](https://www.exim.org/docs.html)
- [Ajuda de Gmail SMTP](https://support.google.com/mail/answer/7126229?hl=ca)
- [Contrasenyes d'aplicació de Google](https://support.google.com/accounts/answer/185833?hl=ca)

---

Amb aquesta configuració, el teu servidor Exim4 podrà enviar correus electrònics utilitzant Gmail com a relay SMTP, aprofitant la seva infraestructura segura i fiable.
