# Comanda `ping`

## Descripció

La comanda `ping` és una eina bàsica de diagnòstic de xarxes que permet verificar la connectivitat entre el teu ordinador i un altre dispositiu a través d'una xarxa IP. El nom "ping" és una analogia al sonar dels submarins que envia un senyal i escolta el seu eco.

## Sintaxi

```
ping [opcions] destí
```

## Arguments

- `destí`: L'adreça IP o el nom de domini del dispositiu remot al qual vols enviar paquets.

## Opcions principals

- `-c nombre`: Especifica el nombre de paquets a enviar abans d'aturar-se.
- `-i segons`: Estableix l'interval entre l'enviament de paquets (per defecte és 1 segon).
- `-s mida`: Modifica la mida dels paquets en bytes (per defecte és 56).
- `-t ttl`: Estableix el valor del "Time To Live" (temps de vida) dels paquets.
- `-w segons`: Especifica el temps màxim d'espera per a tots els paquets.
- `-q`: Mode silenciós, només mostra el resum final.
- `-v`: Mode detallat (verbose), mostra més informació.
- `-4`: Força l'ús de IPv4.
- `-6`: Força l'ús de IPv6.

## Exemples

### Comprovar la connectivitat bàsica

```bash
ping www.google.com
```

Aquest exemple envia paquets ICMP a Google i mostra el temps de resposta de cadascun. S'executarà indefinidament fins que l'usuari ho aturi amb Ctrl+C.

### Enviar un nombre específic de paquets

```bash
ping -c 5 192.168.1.1
```

Envia 5 paquets a l'adreça IP 192.168.1.1 (generalment el router) i després s'atura.

### Canviar l'interval entre paquets

```bash
ping -i 2 -c 4 8.8.8.8
```

Envia 4 paquets al servidor DNS de Google (8.8.8.8) amb un interval de 2 segons entre cadascun.

### Modificar la mida dels paquets

```bash
ping -s 1000 -c 3 www.example.com
```

Envia 3 paquets amb una mida de 1000 bytes a example.com.

### Obtenir només un resum de resultats

```bash
ping -q -c 10 192.168.0.10
```

Envia 10 paquets de manera silenciosa i només mostra l'estadística final.

## Interpretació de la sortida

```
64 bytes from 142.250.184.68: icmp_seq=1 ttl=115 time=12.2 ms
```

- `64 bytes`: Mida del paquet rebut
- `142.250.184.68`: Adreça IP que respon
- `icmp_seq=1`: Número de seqüència del paquet
- `ttl=115`: Temps de vida restant del paquet
- `time=12.2 ms`: Temps de resposta en mil·lisegons

Al final de l'execució, es mostra una estadística amb:

- Nombre de paquets transmesos
- Nombre de paquets rebuts
- Percentatge de pèrdua de paquets
- Temps mínim, mitjà, màxim i desviació estàndard (mdev)

## Usos habituals

- Comprovar si un ordinador remot està actiu i accessible
- Mesurar la latència (temps de resposta) d'una connexió de xarxa
- Diagnosticar problemes de connectivitat a internet o xarxes locals
- Verificar la configuració del DNS (usant noms de domini)
- Detectar pèrdua de paquets, que pot indicar problemes de xarxa

## Observacions

- Si el ping no rep resposta, pot ser degut a:
  1. El dispositiu remot està apagat o inaccessible.
  2. Hi ha un tallafoc (firewall) bloquejant les peticions ICMP.
  3. La xarxa està congestionada o té problemes.
- Molts servidors tenen desactivada la resposta a ping per seguretat.
- La comanda requereix privilegis d'administrador en alguns sistemes per funcionar correctament.
- Per aturar l'execució, sempre pots utilitzar la combinació de tecles Ctrl+C.
