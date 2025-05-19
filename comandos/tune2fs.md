# El comando `tune2fs`

## Què és?

`tune2fs` és una eina del sistema GNU/Linux que permet ajustar i modificar els paràmetres dels sistemes de fitxers ext2, ext3 i ext4. Aquests paràmetres controlen aspectes importants del comportament del sistema de fitxers.

## Sintaxi bàsica

```
tune2fs [opcions] dispositiu
```

## Opcions principals

- `-l`: Mostra el contingut del superbloc del sistema de fitxers.
- `-c [nombre]`: Estableix el nombre màxim de muntatges abans d'una comprovació forçada.
- `-i [interval]`: Estableix l'interval màxim entre comprovacions (per exemple, "1m" per un mes).
- `-j`: Afegeix un journal per convertir ext2 a ext3.
- `-L [etiqueta]`: Estableix l'etiqueta del volum.
- `-m [percentatge]`: Ajusta el percentatge d'espai reservat per l'usuari root.
- `-U [UUID]`: Estableix l'UUID del sistema de fitxers.

## Exemples d'ús

**Mostrar informació del sistema de fitxers:**

```bash
sudo tune2fs -l /dev/sda1
```

**Establir l'etiqueta d'un sistema de fitxers:**

```bash
sudo tune2fs -L "DADES" /dev/sda1
```

**Modificar l'interval de comprovació a 3 mesos:**

```bash
sudo tune2fs -i 3m /dev/sda1
```

**Canviar l'espai reservat per a root al 3%:**

```bash
sudo tune2fs -m 3 /dev/sda1
```

## Precaucions

- Sempre fes servir `tune2fs` amb precaució, ja que modifica aspectes fonamentals del sistema de fitxers.
- És recomanable fer una còpia de seguretat abans de modificar paràmetres crítics.
- Cal tenir privilegis d'administrador (root) per executar aquest comandament.
- El sistema de fitxers no hauria d'estar muntat quan es modifiquen alguns paràmetres.

## Casos d'ús comuns

- Ajustar la freqüència de les comprovacions del sistema de fitxers.
- Afegir un journal a particions ext2 per convertir-les a ext3.
- Modificar l'espai reservat per a l'usuari root en discs grans.
- Canviar l'etiqueta o UUID d'un sistema de fitxers per facilitar-ne la identificació.
