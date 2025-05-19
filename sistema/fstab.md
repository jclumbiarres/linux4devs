# Fitxer `/etc/fstab`

El fitxer `/etc/fstab` (file system table) és un fitxer de configuració que controla com els sistemes de fitxers es munten al sistema Linux. És crucial per al correcte funcionament del sistema operatiu.

## Descripció Bàsica

Aquest fitxer conté la informació necessària per muntar automàticament els diferents sistemes de fitxers durant l'arrencada del sistema. També permet als usuaris especificar opcions de muntatge per a cada sistema de fitxers.

## Format del Fitxer

Cada línia del fitxer `/etc/fstab` representa una entrada de sistema de fitxers amb sis camps separats per espais o tabulacions:

```
<dispositiu>  <punt_de_muntatge>  <tipus_sistema_fitxers>  <opcions>  <dump>  <pass>
```

### Explicació dels Camps

1. **Dispositiu**: Pot ser:

   - Un dispositiu físic (p.ex., `/dev/sda1`)
   - Un UUID (`UUID=xxxx-xxxx-xxxx-xxxx`)
   - Una etiqueta (`LABEL=etiquetalliure`)

2. **Punt de muntatge**: Directori on es muntarà el sistema de fitxers (p.ex., `/`, `/home`, `/media/usb`).

3. **Tipus de sistema de fitxers**: El format del sistema (p.ex., ext4, ntfs, vfat, swap).

4. **Opcions**: Paràmetres de muntatge separats per comes (p.ex., `defaults`, `noauto`, `user`, `ro`).

5. **Dump**: Indica si el sistema s'ha d'incloure en còpies de seguretat (0=no, 1=sí).

6. **Pass**: Ordre de comprovació d'errors durant l'arrencada (0=no comprovar, 1=root, 2=altres).

## Exemple Pràctic

```
# Partició root
UUID=1234-5678-90ab-cdef  /  ext4  defaults,errors=remount-ro  0  1

# Partició home
/dev/sda2  /home  ext4  defaults  0  2

# Unitat DVD
/dev/sr0  /media/cdrom  udf,iso9660  noauto,user,ro  0  0

# Partició d'intercanvi (swap)
/dev/sda3  none  swap  sw  0  0

# Compartit Windows
//192.168.1.100/Compartit  /mnt/compartit  cifs  username=user,password=pass  0  0
```

## Com Modificar-lo Amb Seguretat

És molt important tenir cura quan es modifica aquest fitxer:

1. **Fes una còpia de seguretat**: `sudo cp /etc/fstab /etc/fstab.bak`
2. **Edita el fitxer**: `sudo nano /etc/fstab`
3. **Comprova la validesa**: Després d'editar-lo, pots verificar amb `sudo mount -a`

Si hi ha errors en aquest fitxer, el sistema pot no arrencar correctament i necessitaràs entrar en mode de rescat.

## Consells

- Usa UUID en lloc de noms de dispositiu per més fiabilitat
- Comprova sempre amb `mount -a` abans de reiniciar
- No eliminis mai entrades que no entenguis
