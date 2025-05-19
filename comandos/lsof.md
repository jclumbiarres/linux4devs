# lsof

El comando `lsof` (List Open Files) és una eina potent que permet visualitzar els fitxers oberts en un sistema Linux.

## Sintaxi bàsica

```
lsof [opcions]
```

## Descripció

`lsof` mostra informació sobre els fitxers que estan sent utilitzats per processos en execució dins del sistema. A Linux, "tot és un fitxer", incloent dispositius, sockets, pipes i connexions de xarxa, per tant `lsof` resulta extremadament útil per diagnosticar problemes i entendre què està passant al sistema.

## Opcions principals

- `-u usuari`: Mostra els fitxers oberts per un usuari específic
- `-p PID`: Mostra els fitxers oberts per un procés específic
- `-i`: Mostra les connexions de xarxa
- `-c nom`: Mostra els fitxers oberts per processos que comencen amb "nom"
- `-t`: Mostra només els números de procés (PID)
- `+D directori`: Mostra tots els fitxers oberts dins del directori especificat

## Exemples d'ús

### Veure tots els fitxers oberts

```bash
lsof
```

Això mostra una gran quantitat d'informació sobre tots els fitxers oberts.

### Veure quins processos tenen obert un fitxer específic

```bash
lsof /path/al/fitxer
```

### Llistar els fitxers oberts per un usuari

```bash
lsof -u nom_usuari
```

### Veure connexions de xarxa actives

```bash
lsof -i
```

### Veure connexions a un port específic

```bash
lsof -i :80
```

Mostra processos que utilitzen el port 80 (HTTP).

### Veure fitxers oberts per un procés

```bash
lsof -p 1234
```

On 1234 és el PID (Process ID) del procés.

### Trobar qui està utilitzant un dispositiu

```bash
lsof /dev/sda1
```

## Columnes de sortida

Quan s'executa `lsof`, les columnes principals mostrades són:

- **COMMAND**: Nom del procés
- **PID**: ID del procés
- **USER**: Usuari que executa el procés
- **FD**: File Descriptor (descripció del tipus d'accés al fitxer)
- **TYPE**: Tipus de node (regular, directory, socket, etc.)
- **DEVICE**: Números de dispositiu
- **SIZE/OFF**: Mida del fitxer o offset
- **NODE**: Número d'inode
- **NAME**: Nom del fitxer o path

## Consells pràctics

- `lsof` requereix normalment privilegis d'administrador per veure tots els fitxers del sistema
- Combineu-lo amb `grep` per filtrar resultats específics
- Utilitzeu `lsof -i` per diagnosticar problemes de xarxa o trobar quines aplicacions estan utilitzant connexions de xarxa

`lsof` és una eina fonamental per a administradors de sistemes i desenvolupadors que necessiten entendre les relacions entre processos i recursos del sistema.
