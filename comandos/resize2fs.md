# resize2fs

## Què és?

`resize2fs` és una eina de línia de comandes que permet redimensionar sistemes de fitxers ext2, ext3 i ext4 sense pèrdua de dades. Aquest comandament és molt útil quan necessites augmentar o reduir la mida d'un sistema de fitxers, especialment després de modificar la mida d'una partició.

## Sintaxi bàsica

```bash
resize2fs [opcions] dispositiu [mida]
```

On:

- **dispositiu**: és el sistema de fitxers que vols redimensionar (per exemple, `/dev/sda1`)
- **mida**: és la mida final desitjada (opcional)

## Opcions més comunes

- `-f`: Força el redimensionament encara que el sistema de fitxers sembli no estar net
- `-p`: Mostra una barra de progrés durant el procés
- `-M`: Redueix el sistema de fitxers al mínim possible

## Exemples d'ús

### Exemple 1: Ampliar un sistema de fitxers per ocupar tot l'espai disponible

```bash
sudo resize2fs /dev/sda1
```

En aquest cas, quan no especifiquem mida, el sistema de fitxers s'expandirà per ocupar tot l'espai disponible a la partició.

### Exemple 2: Redimensionar a una mida específica

```bash
sudo resize2fs /dev/sda1 10G
```

Aquest comandament redimensionarà el sistema de fitxers a 10 gigabytes.

### Exemple 3: Redimensionar al mínim possible

```bash
sudo resize2fs -M /dev/sda1
```

Reduirà el sistema de fitxers a la mida mínima necessària per contenir les dades actuals.

## Consideracions importants

- **El sistema de fitxers ha d'estar desmuntat** o **en mode només lectura** (excepte en alguns casos amb ext4 que permet redimensionament en línia)
- Abans d'utilitzar `resize2fs` per reduir un sistema de fitxers, primer has de reduir la partició amb eines com `fdisk`, `parted` o `gparted`
- És **molt recomanable fer una còpia de seguretat** de les teves dades abans de realitzar aquesta operació
- Si el sistema de fitxers no està net (ha tingut un tancament inadequat), primer s'ha d'executar `e2fsck`

## Exemple de flux de treball complet

Per ampliar un sistema de fitxers:

1. Primer redimensiona la partició:

   ```bash
   sudo fdisk /dev/sda  # o utilitza parted/gparted
   ```

2. Comprova la integritat del sistema de fitxers:

   ```bash
   sudo e2fsck -f /dev/sda1
   ```

3. Redimensiona el sistema de fitxers:
   ```bash
   sudo resize2fs /dev/sda1
   ```

## Errors comuns

- **"El sistema de fitxers està muntat"**: Intenta desmuntar-lo abans o utilitza eines alternatives per a redimensionament en línia si és possible
- **"No hi ha prou espai"**: Comprova que la partició s'ha ampliat correctament abans d'utilitzar resize2fs
- **"Sistema de fitxers no net"**: Executa `e2fsck` en el dispositiu abans de redimensionar
