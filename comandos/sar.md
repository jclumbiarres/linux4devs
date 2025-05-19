# Comanda `sar`

La comanda `sar` (System Activity Reporter) és una eina molt útil per a monitoritzar el rendiment del sistema en temps real i per a recollir i generar informes sobre l'activitat del sistema.

## Descripció

`sar` forma part del paquet `sysstat` i permet visualitzar estadístiques de rendiment del sistema, com l'ús de CPU, memòria, dispositius d'entrada/sortida, xarxa i més. És especialment útil per a diagnosticar problemes de rendiment i per a fer un seguiment del comportament del sistema al llarg del temps.

## Sintaxi bàsica

```bash
sar [opcions] [interval] [comptador]
```

- **interval**: temps en segons entre cada mostra (per defecte, 1 segon)
- **comptador**: nombre de mostres a prendre (per defecte, infinit)

## Opcions principals

- `-u`: Mostra l'ús de la CPU
- `-r`: Mostra l'ús de la memòria
- `-b`: Mostra estadístiques d'entrada/sortida
- `-n`: Mostra estadístiques de xarxa (utilitzar amb DEV, EDEV, TCP, etc.)
- `-d`: Mostra estadístiques dels dispositius d'emmagatzematge
- `-A`: Mostra totes les estadístiques disponibles
- `-o fitxer`: Guarda les estadístiques en un fitxer per a una anàlisi posterior
- `-f fitxer`: Llegeix les dades d'un fitxer ja creat

## Exemples d'ús

### 1. Monitoritzar l'ús de CPU cada 2 segons durant 5 mostres

```bash
sar -u 2 5
```

Aquest comandament mostrarà l'ús de la CPU (percentatge d'ús en mode usuari, sistema, en espera d'E/S, etc.) cada 2 segons, un total de 5 vegades.

### 2. Monitoritzar l'ús de la memòria

```bash
sar -r 1 3
```

Aquest comandament mostrarà l'ús de memòria cada segon durant 3 mostres.

### 3. Monitoritzar el trànsit de xarxa

```bash
sar -n DEV 1 3
```

Aquest comandament mostrarà les estadístiques de xarxa per cada interfície de xarxa cada segon durant 3 mostres.

### 4. Consultar dades històriques

```bash
sar -f /var/log/sysstat/sa20
```

Aquest comandament mostrarà les dades recollides automàticament pel servei sysstat el dia 20 del mes actual.

### 5. Mostra totes les estadístiques

```bash
sar -A
```

Aquest comandament mostrarà totes les estadístiques disponibles.

## Informació addicional

- El servei `sysstat` pot configurar-se per recollir dades periòdicament (generalment cada 10 minuts).
- Les dades històriques es guarden per defecte a `/var/log/sysstat/`.
- És necessari tenir instal·lat el paquet `sysstat` per utilitzar `sar`.

## Consell pràctic

Per instal·lar el paquet `sysstat` si no està disponible:

```bash
# En distribucions basades en Debian (Ubuntu, Mint...)
sudo apt install sysstat

```

Un cop instal·lat, pot ser necessari habilitar la recopilació automàtica de dades editant el fitxer `/etc/default/sysstat` i establint `ENABLED="true"`.

## Conclusió

La comanda `sar` és una eina molt potent per a la monitorització del rendiment del sistema. És especialment útil per a la detecció de colls d'ampolla en el sistema i per a la planificació de la capacitat a llarg termini.
