# APT - Advanced Package Tool

`apt` és una eina de línia de comandes per gestionar paquets a distribucions GNU/Linux basades en Debian, com Ubuntu, Linux Mint i el mateix Debian.

## Què és APT?

APT (Advanced Package Tool) és un gestor de paquets que simplifica el procés d'instal·lació, actualització i eliminació de programari al sistema operatiu. Funciona com una capa sobre el sistema de paquets `dpkg` i facilita la resolució de dependències de forma automàtica.

## Comandes bàsiques

### Actualitzar la llista de paquets

```bash
apt update
```

Aquesta comanda actualitza la informació dels repositoris configurats al sistema sense instal·lar res.

### Actualitzar els paquets instal·lats

```bash
apt upgrade
```

Actualitza tots els paquets instal·lats a les seves versions més recents.

### Actualització completa del sistema

```bash
apt full-upgrade
```

Actualitza tot el sistema, podent eliminar paquets obsolets si és necessari (anteriorment conegut com `dist-upgrade`).

### Instal·lar un paquet

```bash
apt install nom_del_paquet
```

Instal·la un paquet i totes les seves dependències.

### Eliminar un paquet

```bash
apt remove nom_del_paquet
```

Elimina el paquet però manté els fitxers de configuració.

### Eliminar completament un paquet

```bash
apt purge nom_del_paquet
```

Elimina el paquet i els seus fitxers de configuració.

### Eliminar dependències innecessàries

```bash
apt autoremove
```

Elimina paquets que es van instal·lar automàticament com a dependències i que ja no són necessaris.

### Cercar paquets

```bash
apt search terme_de_cerca
```

Cerca paquets que coincideixin amb el terme de cerca.

### Mostrar informació d'un paquet

```bash
apt show nom_del_paquet
```

Mostra informació detallada sobre el paquet.

### Netejar la memòria cau

```bash
apt clean
```

Elimina tots els fitxers .deb descarregats a la memòria cau.

### Netejar parcialment la memòria cau

```bash
apt autoclean
```

Elimina només els fitxers .deb obsolets de la memòria cau.

## Opcions comunes

- `-y` o `--yes`: Respon automàticament "sí" a totes les preguntes
- `-q` o `--quiet`: Mode silenciós
- `--no-upgrade`: No actualitzar paquets ja instal·lats
- `--only-upgrade`: Només actualitzar paquets ja instal·lats

## Fitxers de configuració

- `/etc/apt/sources.list`: Defineix els repositoris principals de paquets
- `/etc/apt/sources.list.d/`: Directori que conté fitxers addicionals de fonts de paquets
- `/etc/apt/preferences`: Configuració de preferències de paquets

## Diferències amb altres comandes

- `apt`: Interfície moderna i simplificada per a usuaris finals
- `apt-get`: Eina tradicional més orientada a scripts
- `aptitude`: Interfície més avançada amb funcions addicionals

## Exemples d'ús

### Instal·lar i actualitzar en un sol pas

```bash
apt update && apt install nom_del_paquet
```

### Instal·lar diversos paquets alhora

```bash
apt install paquet1 paquet2 paquet3
```

### Descarregar un paquet sense instal·lar-lo

```bash
apt download nom_del_paquet
```

### Simular una instal·lació sense fer canvis

```bash
apt --simulate install nom_del_paquet
```

### Instal·lar una versió específica d'un paquet

```bash
apt install nom_del_paquet=versió
```

## Consells pràctics

1. Sempre executa `apt update` abans d'instal·lar o actualitzar paquets
2. Utilitza `apt list --upgradable` per veure quins paquets poden ser actualitzats
3. Necessites permisos d'administrador (sudo) per utilitzar la majoria de comandes apt
4. Els problemes de dependències poden resoldre's sovint amb `apt --fix-broken install`

`apt` és una eina poderosa que fa que el manteniment del sistema sigui molt més senzill que instal·lar programari manualment. La seva gestió automàtica de dependències és un dels avantatges més importants dels sistemes basats en Debian.
