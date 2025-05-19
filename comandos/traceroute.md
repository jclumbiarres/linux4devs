# Traceroute

## Descripció

El comando `traceroute` és una eina de diagnòstic de xarxa que permet visualitzar el camí que segueix un paquet IP des del nostre ordinador fins a un destí específic, mostrant tots els salts (routers intermedis) pel camí.

## Sintaxi bàsica

```bash
traceroute [opcions] host
```

## Exemples d'ús

### Exemple bàsic

```bash
traceroute www.google.com
```

Aquest comando mostra la ruta completa que segueixen els paquets des del nostre ordinador fins al servidor de Google.

### Especificar el nombre màxim de salts

```bash
traceroute -m 10 www.example.com
```

Limita el traçat a un màxim de 10 salts (routers).

### Utilitzar paquets TCP en lloc d'UDP o ICMP

```bash
traceroute -T www.example.com
```

Utilitza paquets TCP per fer el traçat, útil quan els paquets UDP o ICMP estan bloquejats per firewalls.

### Mostrar adreces numèriques sense resoldre noms de domini

```bash
traceroute -n www.example.com
```

Mostra només les adreces IP numèriques, sense intentar resoldre els noms dels hosts.

## Opcions principals

- `-4`: Força l'ús d'IPv4.
- `-6`: Força l'ús d'IPv6.
- `-m max_ttl`: Estableix el nombre màxim de salts (valor TTL màxim).
- `-n`: No resol les adreces IP a noms de host.
- `-p port`: Especifica el port de destí per les proves.
- `-q nqueries`: Estableix el nombre de sondejos per cada salt.
- `-w waittime`: Estableix el temps d'espera en segons per a cada resposta.
- `-T`: Utilitza paquets TCP en lloc d'UDP.
- `-I`: Utilitza paquets ICMP ECHO en lloc d'UDP.

## Com funciona?

El comando `traceroute` funciona enviant paquets amb valors TTL (Time To Live) incrementals:

1. Comença enviant paquets amb TTL=1, que expiren en el primer router.
2. El router retorna un missatge d'error ICMP "Time Exceeded".
3. `traceroute` registra aquest router i augmenta el TTL a 2.
4. El procés es repeteix fins que s'arriba al destí o s'assoleix el nombre màxim de salts.

Per a cada salt, `traceroute` mostra:

- Número del salt
- Nom del host o adreça IP
- Temps de resposta (en mil·lisegons) per cada intent

## Notes importants

- Els asteriscs (`*`) indiquen que no s'ha rebut resposta dins del temps d'espera.
- Alguns routers poden estar configurats per no respondre a paquets de traçat.
- Diferents execucions de `traceroute` poden mostrar rutes diferents, ja que Internet és dinàmica.
- Es requereixen permisos d'administrador (sudo) en alguns sistemes per executar `traceroute`.

## Alternatives

- `tracepath`: Una alternativa que no requereix privilegis d'administrador.
- `mtr` (My Traceroute): Combinació de `traceroute` i `ping` que mostra estadístiques en temps real.
- `traceroute6`: Versió específica per a IPv6.

## Casos d'ús

- Diagnosticar problemes de connectivitat de xarxa.
- Identificar colls d'ampolla o punts de congestió a la xarxa.
- Entendre la topologia de la xarxa entre l'origen i el destí.
- Verificar que el tràfic segueix la ruta esperada.
