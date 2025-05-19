# Permisos en GNU/Linux

## Introducció als Permisos

En els sistemes GNU/Linux, cada fitxer i directori té associat un conjunt de permisos que determinen qui pot llegir, escriure o executar el seu contingut. Els permisos són fonamentals per a la seguretat del sistema i el control d'accés als recursos.

## Tipus de Permisos Bàsics

Hi ha tres tipus de permisos bàsics:

- **r (read/lectura)**: Permet veure el contingut d'un fitxer o llistar el contingut d'un directori.
- **w (write/escriptura)**: Permet modificar el contingut d'un fitxer o crear, eliminar i canviar fitxers dins d'un directori.
- **x (execute/execució)**: Permet executar un fitxer o accedir a un directori.

## Categories d'Usuaris

Els permisos s'apliquen a tres categories d'usuaris:

- **Propietari (u/user)**: L'usuari que posseeix el fitxer o directori.
- **Grup (g/group)**: Els usuaris que pertanyen al grup assignat al fitxer o directori.
- **Altres (o/others)**: Tots els altres usuaris del sistema.

## Visualització de Permisos

Quan executem `ls -l`, podem veure els permisos d'un fitxer en el primer camp de la sortida:

```
-rwxr-xr-- 1 usuari grup 5432 oct 12 14:30 exemple.txt
```

La cadena de permisos es divideix així:

- El primer caràcter indica el tipus (`-` per fitxer, `d` per directori, `l` per enllaç simbòlic).
- Els tres següents (`rwx`) són els permisos del propietari.
- Els tres següents (`r-x`) són els permisos del grup.
- Els tres últims (`r--`) són els permisos per als altres usuaris.

## Modificació de Permisos amb `chmod`

La comanda `chmod` (change mode) permet modificar els permisos d'un fitxer o directori.

### Format Simbòlic

Sintaxi: `chmod [referències][operador][permisos] fitxer`

**Referències**:

- `u`: Propietari (user)
- `g`: Grup (group)
- `o`: Altres (others)
- `a`: Tots (all, equivalent a ugo)

**Operadors**:

- `+`: Afegeix permisos
- `-`: Elimina permisos
- `=`: Estableix permisos exactes

**Exemples**:

```bash
# Afegir permís d'execució al propietari
chmod u+x script.sh

# Eliminar permís d'escriptura per a altres
chmod o-w document.txt

# Establir permisos de lectura i escriptura per al grup
chmod g=rw informe.pdf

# Afegir permís de lectura per a tothom
chmod a+r manual.txt

# Eliminar tots els permisos per a altres
chmod o= confidencial.dat

# Establir permisos rwx per al propietari, rx per al grup, i només r per a altres
chmod u=rwx,g=rx,o=r programa
```

### Format Octal

En el format octal, cada permís té un valor numèric:

- `r` = 4
- `w` = 2
- `x` = 1

Per a cada categoria (propietari, grup, altres), sumem els valors dels permisos que volem concedir.

**Exemples**:

```bash
# 7 (rwx) per al propietari, 5 (rx) per al grup, 0 (---) per a altres
chmod 750 script.sh

# 6 (rw) per al propietari, 4 (r) per al grup, 4 (r) per a altres
chmod 644 document.txt

# 7 (rwx) per a tothom
chmod 777 programa

# 4 (r) per a tothom
chmod 444 readonly.txt

# 7 (rwx) per al propietari, 0 (---) per a la resta
chmod 700 privat.txt
```

## Combinacions Comunes en Format Octal

| Valor Octal | Permisos  | Descripció                                                           |
| ----------- | --------- | -------------------------------------------------------------------- |
| 777         | rwxrwxrwx | Accés total per a tothom (perillos)                                  |
| 755         | rwxr-xr-x | El propietari té control total; altres només poden llegir i executar |
| 700         | rwx------ | Només el propietari té accés                                         |
| 644         | rw-r--r-- | El propietari pot llegir i escriure; altres només poden llegir       |
| 600         | rw------- | El propietari pot llegir i escriure; ningú més té accés              |
| 555         | r-xr-xr-x | Tothom pot llegir i executar; ningú pot escriure                     |
| 444         | r--r--r-- | Tothom pot llegir; ningú pot escriure o executar                     |

## Canvi de Propietari i Grup amb `chown`

La comanda `chown` (change owner) permet canviar el propietari i/o el grup d'un fitxer o directori.

**Sintaxi**: `chown [opcions] propietari[:grup] fitxer`

**Exemples**:

```bash
# Canviar només el propietari
sudo chown nouusuari fitxer.txt

# Canviar el propietari i el grup
sudo chown nouusuari:nougrup document.pdf

# Canviar només el grup
sudo chown :nougrup informe.md

# Canviar recursivament el propietari i grup d'un directori i tot el seu contingut
sudo chown -R usuari:grup directori/
```

## Casos Pràctics

### Configuració d'un Script Executable

```bash
# Crear un script
echo '#!/bin/bash\necho "Hola, món!"' > script.sh

# Fer-lo executable per al propietari
chmod u+x script.sh
# O, alternativament:
chmod 744 script.sh

# Executar-lo
./script.sh
```

### Configuració d'un Directori Compartit

```bash
# Crear un directori compartit per a un grup
sudo mkdir /compartit

# Assignar propietat al grup "projecte"
sudo chown :projecte /compartit

# Establir permisos adequats (escriptura per al grup)
sudo chmod 775 /compartit

# Establir el bit SGID per mantenir el grup en els nous fitxers
sudo chmod g+s /compartit
```

### Protecció de Fitxers Confidencials

```bash
# Crear un fitxer confidencial
echo "Informació secreta" > confidencial.txt

# Assignar permisos estrictes (només el propietari pot llegir i escriure)
chmod 600 confidencial.txt
# O, alternativament:
chmod u=rw,g=,o= confidencial.txt
```

## Permisos Especials

A més dels permisos bàsics, Linux ofereix permisos especials:

### SUID (Set User ID) - 4000

Quan s'aplica a un fitxer executable, l'executa amb els permisos del propietari del fitxer.

```bash
# Establir el bit SUID
chmod u+s fitxer
# O, en format octal (4 davant dels permisos normals):
chmod 4755 fitxer
```

### SGID (Set Group ID) - 2000

Per a fitxers executables: executa amb els permisos del grup.
Per a directoris: els nous fitxers hereten el grup del directori.

```bash
# Establir el bit SGID
chmod g+s directori
# O, en format octal:
chmod 2755 directori
```

### Sticky Bit - 1000

Quan s'aplica a un directori, només el propietari d'un fitxer pot eliminar-lo, fins i tot si altres usuaris tenen permís d'escriptura al directori.

```bash
# Establir el sticky bit
chmod +t directori
# O, en format octal:
chmod 1755 directori
```

## Conclusions

Entendre i gestionar correctament els permisos és essencial per a la seguretat i la correcta administració d'un sistema GNU/Linux. Amb les comandes `chmod` i `chown`, podem controlar amb precisió qui pot accedir als nostres fitxers i directoris, i què poden fer amb ells.
