# findfs

## Resum

El comandament `findfs` s'utilitza per a trobar un sistema de fitxers per la seva etiqueta o UUID (Identificador Únic Universal). És especialment útil quan necessitem identificar particions sense conèixer la seva ubicació exacta al dispositiu.

## Sintaxi

```bash
findfs ETIQUETA=valor
findfs UUID=valor
```

## Descripció

`findfs` és una eina que permet localitzar un sistema de fitxers mitjançant la seva etiqueta o UUID, en lloc d'utilitzar el nom del dispositiu (com `/dev/sda1`). Això resulta molt útil, ja que els noms dels dispositius poden canviar depenent de l'ordre en què es detecten els dispositius d'emmagatzematge durant l'arrencada, mentre que les etiquetes i UUIDs romanen constants.

## Opcions

Aquest comandament no té moltes opcions, ja que la seva funció és molt específica:

- `LABEL=etiqueta` - Cerca un sistema de fitxers amb l'etiqueta especificada
- `UUID=uuid` - Cerca un sistema de fitxers amb l'UUID especificat

## Exemples

### Trobar un sistema de fitxers per la seva etiqueta

```bash
findfs LABEL=DADES
```

Aquest comandament mostrarà la ruta al dispositiu (p. ex., `/dev/sda2`) que té l'etiqueta "DADES".

### Trobar un sistema de fitxers pel seu UUID

```bash
findfs UUID=5db9-a2c1
```

Retorna la ruta al dispositiu amb l'UUID especificat.

## Avantatges de fer servir findfs

- Identificació consistent de les particions independentment de l'ordre de detecció dels dispositius
- Útil per a scripts d'arrencada i muntatge automàtic
- Permet referenciar particions de manera més robusta que els noms de dispositius tradicionals

## Informació addicional

- Els UUIDs són cadenes llargues úniques generades quan es formata un sistema de fitxers
- Les etiquetes són més curtes i fàcils de recordar, però cal assegurar-se que siguin úniques en el sistema
- Per veure les etiquetes i UUIDs disponibles al sistema, es pot utilitzar `blkid`
