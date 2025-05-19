# NTP (Network Time Protocol)

## Descripció

El protocol NTP (Network Time Protocol) és un sistema que permet la sincronització dels rellotges dels dispositius informàtics a través d'una xarxa. És fonamental per mantenir tots els sistemes d'una xarxa amb la mateixa hora exacta, cosa que resulta imprescindible per a moltes aplicacions i serveis.

## Sintaxi bàsica

```
ntpdate [opcions] servidor_ntp
```

o amb el servei systemd:

```
systemctl [acció] ntp
```

## Exemples d'ús comú

### Consultar l'hora d'un servidor NTP

```
ntpdate -q 0.pool.ntp.org
```

### Actualitzar l'hora del sistema amb un servidor NTP

```
sudo ntpdate 0.pool.ntp.org
```

### Iniciar el servei NTP (en sistemes amb systemd)

```
sudo systemctl start ntp
```

### Activar NTP perquè s'iniciï en arrencar el sistema

```
sudo systemctl enable ntp
```

### Comprovar l'estat del servei NTP

```
systemctl status ntp
```

## Opcions importants

- `-q`: Mode consulta (query). Només mostra l'hora del servidor sense modificar l'hora local.
- `-d`: Mode depuració (debug). Mostra informació més detallada.
- `-v`: Mode detallat (verbose). Mostra més informació sobre el procés.
- `-u`: Utilitza el protocol UDP (predeterminat).
- `-b`: Mode emisió (broadcast). El client escolta paquets de difusió.

## Configuració

El fitxer principal de configuració és `/etc/ntp.conf`. Aquí es poden definir:

- Servidors NTP de referència
- Permisos d'accés
- Intervals de sincronització
- Registres (logs)

## Consells pràctics

- Utilitzeu diversos servidors NTP per garantir precisió i redundància
- Els servidors del pool.ntp.org són una bona opció per a ús general
- La sincronització regular és important per a serveis que depenen de timestamps precisos
- En sistemes crítics, considereu utilitzar fonts de temps locals com a reserva

## Resolució de problemes comuns

- Si la sincronització falla, verifiqueu la connectivitat de xarxa amb els servidors NTP
- Consulteu els registres amb `journalctl -u ntp` per veure possibles errors
- Assegureu-vos que el port UDP 123 no estigui bloquejat pel tallafoc
