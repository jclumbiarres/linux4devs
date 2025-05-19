# El Comando `dig` (GNU/Linux)

## Descripció

El comando `dig` (Domain Information Groper) és una eina utilitzada per a consultar els servidors DNS (Domain Name System) i obtenir informació sobre diversos registres de DNS. És molt útil per solucionar problemes relacionats amb el DNS, comprovar la configuració de dominis i entendre com funciona la resolució de noms a Internet.

## Sintaxi bàsica

```bash
dig [@servidor] [domini] [tipus]
```

## Paràmetres principals

- **@servidor**: El servidor DNS que s'utilitzarà per a la consulta. Si no s'especifica, s'utilitzarà el servidor configurat al sistema.
- **domini**: El nom de domini que es vol consultar.
- **tipus**: El tipus de registre DNS que es vol consultar (A, MX, NS, etc.).

## Exemples pràctics

### Consultar les adreces IP d'un domini

```bash
dig example.com
```

Això mostrarà els registres A (adreces IPv4) del domini example.com.

### Consultar un tipus de registre específic

```bash
dig example.com MX
```

Aquesta comanda mostrarà els registres MX (servidors de correu) del domini example.com.

### Utilitzar un servidor DNS específic

```bash
dig @8.8.8.8 example.com
```

Consulta el domini example.com utilitzant el servidor DNS públic de Google (8.8.8.8).

### Obtenir una resposta més curta i concisa

```bash
dig example.com +short
```

Aquesta opció mostra només les adreces IP, sense tota la informació addicional.

### Consultar registres NS (Name Servers)

```bash
dig example.com NS
```

Mostra els servidors de noms autoritatius per al domini.

## Seccions de la sortida

La sortida del comando `dig` normalment està dividida en diverses seccions:

1. **Capçalera**: Mostra la versió de `dig` i la consulta realitzada.
2. **Secció QUESTION**: Detalla la consulta que s'ha fet.
3. **Secció ANSWER**: Conté la resposta a la consulta.
4. **Secció AUTHORITY**: Mostra els servidors autoritatius per al domini.
5. **Secció ADDITIONAL**: Proporciona informació addicional.
6. **Estadístiques**: Mostra el temps que ha trigat la consulta i quan s'ha realitzat.

## Opcions comunes

- `+short`: Mostra només la resposta sense informació addicional.
- `+nocomments`: Omet els comentaris a la sortida.
- `+noall`: Desactiva tota la visualització.
- `+answer`: Mostra només la secció de resposta.
- `+nocmd`: No mostra la línia de comanda a la sortida.
- `+time=N`: Estableix el temps d'espera a N segons.

## Ús avançat

### Traçar el camí de resolució d'un domini

```bash
dig example.com +trace
```

Aquesta comanda mostra el procés complet de resolució del domini, començant pels servidors arrel.

### Realitzar una consulta inversa

```bash
dig -x 192.0.2.1
```

Consulta el nom de domini associat a una adreça IP específica.

## Consells pràctics

- `dig` és més potent i detallat que altres eines com `nslookup` o `host`.
- És molt útil per diagnosticar problemes de DNS o verificar canvis en la configuració del DNS.
- Podeu utilitzar `dig` per comprovar si els servidors DNS estan propagant correctament els vostres registres.

## Conclusió

El comando `dig` és una eina essencial per a administradors de sistemes i xarxes, però també és útil per a qualsevol persona que vulgui entendre com funciona la resolució de dominis a Internet. Amb pràctica, podràs interpretar fàcilment la sortida i utilitzar-la per resoldre problemes relacionats amb el DNS.
