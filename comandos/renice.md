# Comanda renice

## Descripció

La comanda `renice` permet modificar la prioritat d'un procés que ja està en execució. A Linux, cada procés té un valor de prioritat anomenat "niceness" que va de -20 (màxima prioritat) a 19 (mínima prioritat). Com més baix sigui el valor, més CPU utilitzarà el procés.

## Sintaxi

```bash
renice prioritat [-p] ID_PROCÉS [-g] ID_GRUP [-u] USUARI
```

## Opcions principals

- `-p`: Especifica un ID de procés (PID)
- `-g`: Especifica un ID de grup
- `-u`: Especifica un nom d'usuari

## Exemples

### Canviar la prioritat d'un procés específic

```bash
# Canviar la prioritat d'un procés amb PID 1234 a 10 (prioritat baixa)
renice 10 -p 1234
```

### Canviar la prioritat de tots els processos d'un usuari

```bash
# Canviar la prioritat de tots els processos de l'usuari "joan" a 5
renice 5 -u joan
```

### Augmentar la prioritat d'un procés (requereix drets d'administrador)

```bash
# Augmentar la prioritat d'un procés amb PID 5678 (valor negatiu)
sudo renice -10 -p 5678
```

## Detalls importants

- Només l'usuari root (o amb sudo) pot assignar valors de prioritat negatius o reduir el "niceness" d'un procés.
- Un usuari normal només pot augmentar el valor de "niceness" (reduir la prioritat) dels seus propis processos.
- Els valors de "niceness" no són garanties absolutes d'assignació de CPU, només són suggeriments per al planificador del sistema.

## Casos d'ús comuns

- Reduir la prioritat de processos que consumeixen molts recursos però no són urgents
- Augmentar la prioritat de processos crítics que necessiten respondre ràpidament
- Gestionar millor els recursos del sistema quan hi ha múltiples aplicacions en execució

## Exemples pràctics

### Trobar un procés que consumeix molta CPU i reduir la seva prioritat

```bash
# Primer identifiquem el procés amb top
top

# Un cop trobat el PID (per exemple 3145), reduïm la seva prioritat
renice 15 -p 3145
```

### Comprovar el valor de "nice" d'un procés

```bash
ps -o pid,nice,comm -p PID
```
