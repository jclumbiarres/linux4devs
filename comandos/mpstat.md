# mpstat - Estadístiques del processador

El comandament `mpstat` és una eina de monitoratge que proporciona estadístiques detallades sobre el rendiment dels processadors en sistemes GNU/Linux. Aquest comandament forma part del paquet `sysstat` i resulta molt útil per analitzar l'ús de la CPU i identificar possibles colls d'ampolla en el sistema.

## Instal·lació

Si el comandament no està disponible al sistema, es pot instal·lar amb:

```bash
# En sistemes basats en Debian (Ubuntu, Mint...)
sudo apt install sysstat
```

## Sintaxi bàsica

```bash
mpstat [opcions] [interval [nombre]]
```

On:

- `interval`: especifica el temps (en segons) entre actualitzacions de les dades
- `nombre`: indica quantes vegades es mostraran les estadístiques abans de finalitzar

## Exemples d'ús

### Mostrar estadístiques de tots els processadors

```bash
mpstat
```

Aquest comandament mostra un resum de l'ús de la CPU des de l'arrencada del sistema.

### Mostrar estadístiques actualitzades cada 2 segons, 5 vegades

```bash
mpstat 2 5
```

### Mostrar estadístiques per a cada processador individualment

```bash
mpstat -P ALL
```

### Mostrar estadístiques amb timestamp

```bash
mpstat -P ALL 1 3 -o JSON
```

## Interpretació de la sortida

La sortida del comandament `mpstat` inclou diverses columnes:

- `%usr`: percentatge d'utilització de la CPU en mode usuari
- `%sys`: percentatge d'utilització de la CPU en mode sistema
- `%idle`: percentatge de temps que la CPU està inactiva
- `%iowait`: percentatge de temps que la CPU està esperant operacions d'E/S
- `%irq`: percentatge de temps dedicat a interrupcions de maquinari
- `%soft`: percentatge de temps dedicat a interrupcions de programari

## Consells pràctics

- Utilitza `mpstat -P ALL` per identificar si una aplicació està saturant un nucli específic
- Valors alts a `%iowait` indiquen possibles problemes de rendiment en el disc
- Valors baixos a `%idle` indiquen que el processador està treballant a prop de la seva capacitat màxima

Aquest comandament és especialment útil per a administradors de sistemes i desenvolupadors que necessiten optimitzar el rendiment de les seves aplicacions o diagnosticar problemes relacionats amb l'ús de la CPU.
