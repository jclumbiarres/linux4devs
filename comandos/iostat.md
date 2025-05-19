# Comando iostat

El `iostat` és una eina útil per monitoritzar l'activitat del sistema d'entrada/sortida (I/O) i estadístiques de la CPU a GNU/Linux.

## Descripció

El comando `iostat` mostra estadístiques per dispositius d'emmagatzematge i les seves particions, així com dades generals de l'ús de la CPU. És molt útil per identificar problemes de rendiment relacionats amb els discos o per analitzar el comportament del sistema.

## Instal·lació

El `iostat` forma part del paquet `sysstat`, que pot instal·lar-se amb:

```bash
sudo apt install sysstat    # En distribucions basades en Debian/Ubuntu
```

## Ús bàsic

La sintaxi bàsica del comando és:

```bash
iostat [opcions] [interval [recompte]]
```

On:

- **interval**: és el temps (en segons) entre cada actualització de les estadístiques.
- **recompte**: el nombre de vegades que s'executarà l'informe.

## Exemples d'ús

### Mostrar estadístiques bàsiques

```bash
iostat
```

Aquest comando mostra les estadístiques bàsiques de la CPU i dels dispositius d'I/O.

### Actualitzar estadístiques cada 2 segons, 5 vegades

```bash
iostat 2 5
```

### Mostrar només estadístiques de dispositius

```bash
iostat -d
```

### Mostrar estadístiques amb unitats llegibles per humans

```bash
iostat -h
```

### Mostrar estadístiques esteses sobre els dispositius

```bash
iostat -x
```

### Mostrar estadístiques d'un dispositiu específic

```bash
iostat -p sda
```

## Explicació de la sortida

Quan s'executa `iostat`, es mostren dues seccions principals:

### Estadístiques de la CPU

- **%user**: Percentatge d'ús de CPU en l'espai d'usuari.
- **%nice**: Percentatge d'ús de CPU per processos amb prioritat "nice".
- **%system**: Percentatge d'ús de CPU en mode sistema (kernel).
- **%iowait**: Percentatge de temps que la CPU està inactiva a causa d'operacions d'I/O.
- **%steal**: Percentatge de temps d'espera involuntari en entorns virtualitzats.
- **%idle**: Percentatge de temps que la CPU està inactiva.

### Estadístiques de dispositius

- **Device**: Nom del dispositiu.
- **tps**: Transferències per segon.
- **kB_read/s**: Kilobytes llegits per segon.
- **kB_wrtn/s**: Kilobytes escrits per segon.
- **kB_read**: Total de kilobytes llegits.
- **kB_wrtn**: Total de kilobytes escrits.

En el mode estès (`-x`), es mostren més estadístiques com:

- **r/s, w/s**: Lectures/escriptures per segon.
- **await**: Temps mitjà d'espera (en ms) per a sol·licituds d'I/O.
- **svctm**: Temps mitjà de servei (en ms) per a sol·licituds d'I/O.
- **%util**: Percentatge d'utilització del dispositiu.

## Consells pràctics

- Utilitzeu `iostat -xz 1` per veure estadístiques detallades actualitzades cada segon.
- Un valor alt en **%iowait** pot indicar que el sistema està limitat pel rendiment del disc.
- Un **%util** proper al 100% indica que el dispositiu està saturat.
- Combineu `iostat` amb altres eines com `top` i `vmstat` per tenir una visió més completa del rendiment del sistema.
