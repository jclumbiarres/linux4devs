# uname

El comandament `uname` (abreviació de "Unix Name") mostra informació bàsica sobre el sistema operatiu i el maquinari del teu ordinador.

## Sintaxi

```bash
uname [opcions]
```

## Descripció

El comandament `uname` t'ajuda a saber quin sistema operatiu estàs utilitzant i altres detalls sobre el teu ordinador. Sense cap opció, simplement mostra el nom del sistema operatiu.

## Opcions principals

- `-a`: Mostra tota la informació disponible
- `-s`: Mostra el nom del sistema operatiu (opció per defecte)
- `-n`: Mostra el nom de la xarxa de l'ordinador
- `-r`: Mostra la versió del nucli (kernel)
- `-v`: Mostra la data de la versió del nucli
- `-m`: Mostra el tipus de maquinari (arquitectura)
- `-p`: Mostra el tipus de processador
- `-o`: Mostra el nom del sistema operatiu

## Exemples

Mostrar tota la informació del sistema:

```bash
uname -a
```

Mostrar només el nom del sistema operatiu:

```bash
uname -s
```

Mostrar l'arquitectura del maquinari:

```bash
uname -m
```

## Consells

- Utilitza `uname -a` quan necessitis tota la informació del sistema per resoldre problemes.
- Aquest comandament és útil quan necessites comprovar si estàs utilitzant un sistema de 32 o 64 bits.
- És molt utilitzat en scripts per detectar el tipus de sistema operatiu i adaptar el comportament del script segons això.
