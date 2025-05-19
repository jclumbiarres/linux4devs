# Llistes de Control d'Accés (ACL) a GNU/Linux

## Introducció a les ACL

Les Llistes de Control d'Accés (ACL) són un mecanisme de seguretat avançat al sistema operatiu GNU/Linux que permet definir permisos més granulars que els permisos tradicionals d'Unix (lectura, escriptura, execució).

Mentre que els permisos estàndard només permeten definir accés per a propietari, grup i altres, les ACL proporcionen un control més precís, permetent assignar permisos específics a usuaris o grups concrets.

## Permisos tradicionals vs ACL

### Sistema tradicional de permisos

Abans d'entrar en detall amb les ACL, recordem com funciona el sistema de permisos tradicional:

- Cada arxiu o directori té assignats tres conjunts de permisos:
  - Per al propietari (u)
  - Per al grup propietari (g)
  - Per a altres usuaris (o)
- Cada conjunt pot tenir tres tipus de permisos:
  - Lectura (r): valor 4
  - Escriptura (w): valor 2
  - Execució (x): valor 1

Per exemple, quan veiem `-rw-r--r--`, significa:

- El propietari pot llegir i escriure
- El grup i altres només poden llegir

### Limitacions del sistema tradicional

Aquest sistema, tot i ser simple, presenta limitacions importants:

1. No es poden assignar permisos a més d'un grup
2. No es poden donar permisos a usuaris específics (diferents del propietari)
3. La gestió es complica en entorns multiusuari

Aquí és on entren les ACL, per superar aquestes limitacions.

## Instal·lació dels paquets ACL

Abans de començar a treballar amb ACL, cal assegurar-se que els paquets necessaris estiguin instal·lats:

### Per a distribucions basades en Debian (Ubuntu, Linux Mint, etc.):

```bash
sudo apt-get update
sudo apt-get install acl
```

### Per a distribucions basades en RedHat (Fedora, CentOS, etc.):

```bash
sudo yum install acl
```

### Verificació de suport ACL al sistema de fitxers

Cal assegurar-se que el sistema de fitxers suporta ACL. La majoria de sistemes moderns (ext4, xfs, btrfs) ho fan per defecte, però podem verificar-ho:

```bash
mount | grep "acl"
```

Si no es mostra l'opció "acl", podem activar-la:

1. Editar el fitxer /etc/fstab:

   ```bash
   sudo nano /etc/fstab
   ```

2. Afegir l'opció "acl" a la partició desitjada:

   ```
   UUID=xxxxx-xxxx-xxxx-xxxx-xxxxx / ext4 defaults,acl 0 1
   ```

3. Tornar a muntar el sistema de fitxers:
   ```bash
   sudo mount -o remount /
   ```

## Comandes bàsiques per a la gestió d'ACL

Les ACL s'administren principalment mitjançant dues comandes:

- `getfacl`: Mostra les ACL d'un fitxer o directori
- `setfacl`: Estableix o modifica les ACL d'un fitxer o directori

### Visualització d'ACL amb getfacl

Per veure les ACL d'un fitxer:

```bash
getfacl nom_fitxer
```

Exemple de sortida:

```
# file: nom_fitxer
# owner: usuari
# group: grup
user::rw-
group::r--
other::r--
```

### Establiment d'ACL amb setfacl

La sintaxi bàsica és:

```bash
setfacl [opcions] regla_acl nom_fitxer
```

On les regles ACL tenen el format:

```
[d:]tipus:nom:permisos
```

- `d:`: Opcional, per defecte indica que l'ACL és per defecte (s'aplicarà als nous elements creats dins d'un directori)
- `tipus`: pot ser `user` (u), `group` (g), `other` (o) o `mask` (m)
- `nom`: identificador de l'usuari o grup
- `permisos`: combinació de r (read), w (write) i x (execute)

## Exemples pràctics d'ús d'ACL

### Afegir permisos per a un usuari específic

```bash
# Donar permisos de lectura i escriptura a l'usuari 'maria'
setfacl -m u:maria:rw- fitxer.txt
```

### Afegir permisos per a un grup específic

```bash
# Donar permisos de lectura al grup 'desenvolupadors'
setfacl -m g:desenvolupadors:r-- fitxer.txt
```

### Revocar permisos

```bash
# Eliminar l'entrada ACL per a l'usuari 'maria'
setfacl -x u:maria fitxer.txt
```

### Eliminar totes les ACL

```bash
# Eliminar totes les ACL d'un fitxer
setfacl -b fitxer.txt
```

## ACL per defecte per a directoris

Les ACL per defecte només s'apliquen a directoris i determinen les ACL inicials dels fitxers creats dins d'aquests directoris:

```bash
# Establir ACL per defecte per a un directori
setfacl -d -m u:maria:rwx /projecte/documents
```

Amb aquesta configuració, tots els nous fitxers creats a `/projecte/documents` heretaran aquesta ACL.

## Opcions avançades de setfacl

### Aplicació recursiva

```bash
# Aplicar ACL recursivament a tots els fitxers i directoris
setfacl -R -m u:maria:rx /projecte
```

### Preservació de les ACL en copiar fitxers

Cal utilitzar l'opció `-p` amb la comanda `cp`:

```bash
cp -p fitxer_amb_acl.txt destinacio/
```

O millor encara, usar l'opció `--preserve=all`:

```bash
cp --preserve=all fitxer_amb_acl.txt destinacio/
```

## ACL en màscares

La màscara ACL defineix els permisos màxims que poden tenir les entrades d'usuari i grup en una ACL.

```bash
# Establir una màscara ACL
setfacl -m m::rx fitxer.txt
```

Aquesta màscara limita els permisos efectius a només lectura i execució, independentment del que s'hagi configurat per als usuaris i grups.

## Exemples de casos d'ús reals

### Cas 1: Gestió d'un projecte compartit

Imaginem un directori `/projecte` on volem:

- L'administrador (admin) té control total
- L'equip de desenvolupament pot llegir i executar
- El cap de projecte (maria) pot llegir, escriure i executar
- El dissenyador (joan) només pot llegir els fitxers de disseny

```bash
# Crear estructura
mkdir -p /projecte/{codi,disseny,docs}

# Establir propietari i grup
chown -R admin:desenvolupadors /projecte

# Permisos base
chmod -R 750 /projecte

# ACL pel cap de projecte
setfacl -R -m u:maria:rwx /projecte

# ACL pel dissenyador (només a la carpeta de disseny)
setfacl -R -m u:joan:r-x /projecte/disseny

# ACL per defecte que s'heretaran
setfacl -d -m u:maria:rwx /projecte
setfacl -d -m g:desenvolupadors:r-x /projecte
setfacl -d -m u:joan:r-x /projecte/disseny
```

### Cas 2: Compartir fitxers entre usuaris

Suposem que tenim un directori `/compartit` on diversos usuaris han de poder col·laborar:

```bash
# Crear directori compartit
mkdir /compartit

# Establir permisos base
chmod 770 /compartit

# Donar accés a diferents usuaris
setfacl -m u:usuari1:rwx /compartit
setfacl -m u:usuari2:rwx /compartit
setfacl -m u:usuari3:r-x /compartit

# Fer que els nous fitxers mantinguin aquests permisos
setfacl -d -m u:usuari1:rwx /compartit
setfacl -d -m u:usuari2:rwx /compartit
setfacl -d -m u:usuari3:r-x /compartit
```

## Interpretació de les ACL en 'ls -l'

Quan un fitxer té ACL configurades, la comanda `ls -l` mostrarà un signe `+` després dels permisos estàndard:

```
-rw-r--r--+ 1 usuari grup 4096 oct 10 12:45 fitxer.txt
```

Aquest `+` indica que cal utilitzar `getfacl` per veure els permisos detallats.

## Backup i restauració d'ACL

És important considerar les ACL al fer còpies de seguretat:

### Guardar les ACL d'un directori

```bash
getfacl -R /directori > permisos_acl.txt
```

### Restaurar les ACL

```bash
setfacl --restore=permisos_acl.txt
```

## Problemes comuns amb les ACL

### ACL no funcionen després de copiar

Solució: utilitzar `cp` amb l'opció `-p` o `--preserve=all`:

```bash
cp -p fitxer_original.txt fitxer_nou.txt
```

### ACL no s'apliquen a nous fitxers

Solució: assegurar-se d'haver configurat ACL per defecte:

```bash
setfacl -d -m u:usuari:rwx directori
```

### Permisos efectius diferents dels configurats

Causa: la màscara ACL limita els permisos.
Solució: verificar i ajustar la màscara:

```bash
getfacl fitxer.txt  # Per veure la màscara actual
setfacl -m m::rwx fitxer.txt  # Per ajustar-la
```

## Les ACL i el seu impacte en el rendiment

Les ACL afegeixen una capa addicional de processament quan es comproven els permisos, cosa que pot afectar lleugerament el rendiment, especialment en sistemes amb molts accessos a fitxers. Tot i així, en la majoria de casos pràctics, aquesta sobrecàrrega és mínima i els beneficis en flexibilitat superen aquest petit cost.

## Integració d'ACL amb altres mecanismes de seguretat

### ACL i SELinux/AppArmor

Les ACL treballen a un nivell diferent que SELinux o AppArmor:

- Les ACL controlen l'accés basat en usuaris i grups
- SELinux/AppArmor s'enfoquen en confinar aplicacions

Quan s'utilitzen junts, es poden obtenir múltiples capes de protecció:

1. Les ACL determinen si un usuari pot accedir al fitxer
2. SELinux/AppArmor determinen si una aplicació pot accedir al fitxer

### ACL i atributs de fitxers

Les ACL funcionen independentment dels atributs de fitxers (com els que es configuren amb `chattr`). Per exemple, un fitxer pot tenir:

- ACL que permeten l'escriptura a diversos usuaris
- L'atribut immutable (`chattr +i`) que impedeix qualsevol modificació

En aquest cas, l'atribut té precedència sobre les ACL.

## Exercicis pràctics amb ACL

### Exercici 1: Configuració bàsica d'ACL

1. Crear un directori i un fitxer:

   ```bash
   mkdir ~/prova_acl
   echo "Contingut de prova" > ~/prova_acl/document.txt
   ```

2. Comprovar els permisos actuals:

   ```bash
   ls -l ~/prova_acl
   getfacl ~/prova_acl/document.txt
   ```

3. Afegir permisos per a un altre usuari:

   ```bash
   # Suposant que existeix un usuari 'company'
   setfacl -m u:company:rw- ~/prova_acl/document.txt
   ```

4. Verificar els canvis:
   ```bash
   getfacl ~/prova_acl/document.txt
   ```

### Exercici 2: ACL per defecte i herència

1. Configurar ACL per defecte en un directori:

   ```bash
   mkdir ~/projecte_equip
   setfacl -d -m u:company:rwx ~/projecte_equip
   ```

2. Crear nous fitxers i verificar l'herència:

   ```bash
   touch ~/projecte_equip/fitxer1.txt
   mkdir ~/projecte_equip/subdir
   touch ~/projecte_equip/subdir/fitxer2.txt
   ```

3. Comprovar les ACL:
   ```bash
   getfacl ~/projecte_equip/fitxer1.txt
   getfacl ~/projecte_equip/subdir
   getfacl ~/projecte_equip/subdir/fitxer2.txt
   ```

### Exercici 3: Simulació d'un entorn col·laboratiu

1. Crear una estructura de directoris per a un projecte:

   ```bash
   mkdir -p ~/col·laboracio/{documents,codi,recursos}
   ```

2. Configurar diferents nivells d'accés:

   ```bash
   # Suposant que existeixen els usuaris 'programador' i 'redactor'

   # El programador pot accedir i modificar tot el codi
   setfacl -R -m u:programador:rwx ~/col·laboracio/codi

   # El redactor pot accedir i modificar tots els documents
   setfacl -R -m u:redactor:rwx ~/col·laboracio/documents

   # Ambdós poden llegir els recursos, però no modificar-los
   setfacl -R -m u:programador:r-x ~/col·laboracio/recursos
   setfacl -R -m u:redactor:r-x ~/col·laboracio/recursos

   # Configurar herència
   setfacl -d -m u:programador:rwx ~/col·laboracio/codi
   setfacl -d -m u:redactor:rwx ~/col·laboracio/documents
   setfacl -d -m u:programador:r-x ~/col·laboracio/recursos
   setfacl -d -m u:redactor:r-x ~/col·laboracio/recursos
   ```

3. Verificar la configuració:
   ```bash
   getfacl -R ~/col·laboracio
   ```

## Les ACL en entorns empresarials

En entorns empresarials, les ACL són especialment útils per a:

### Compliment normatiu

Les regulacions com GDPR, PCI DSS o HIPAA sovint requereixen controls d'accés granulars. Les ACL permeten:

- Limitar l'accés a dades sensibles a personal específic
- Proporcionar proves d'auditoria sobre qui té accés a quina informació
- Implementar el principi de privilegi mínim

### Gestió de projectes complexos

En projectes amb diferents equips i rols:

- Cada equip pot tenir nivells d'accés específics a diferents parts del projecte
- Es poden assignar permisos especials a coordinadors o supervisors
- Els nous membres poden heretar els permisos del seu rol automàticament

### Servidors compartits

En servidors utilitzats per diferents departaments o clients:

- Cada client pot tenir el seu propi espai amb accessos personalitzats
- El personal de suport pot tenir accés limitat per a tasques específiques
- Els administradors mantenen accés complet per a gestió del sistema

## Automatització de la gestió d'ACL

Per a sistemes grans, la gestió manual d'ACL pot ser complicada. Algunes opcions d'automatització:

### Scripts Bash

```bash
#!/bin/bash
# Script per a configurar ACL per a un nou projecte

PROJECTE=$1
PROPIETARI=$2
EQUIP=$3

# Crear estructura
mkdir -p /projectes/$PROJECTE/{docs,codi,recursos}

# Establir propietari
chown -R $PROPIETARI:$EQUIP /projectes/$PROJECTE

# Configurar ACL
setfacl -R -m g:$EQUIP:rwx /projectes/$PROJECTE
setfacl -d -m g:$EQUIP:rwx /projectes/$PROJECTE

# Afegir permisos per al departament de QA
setfacl -R -m g:qa:r-x /projectes/$PROJECTE
setfacl -d -m g:qa:r-x /projectes/$PROJECTE

echo "Projecte $PROJECTE configurat amb èxit"
```

### Ansible

Per a una gestió centralitzada més avançada, podem utilitzar eines com Ansible:

```yaml
---
- name: Configurar ACL per a projectes
    hosts: servidors_projectes
    become: yes
    tasks:
        - name: Crear estructura de directoris
            file:
                path: "/projectes/{{ projecte }}/{{ item }}"
                state: directory
                owner: "{{ propietari }}"
                group: "{{ equip }}"
                mode: "0770"
            loop:
                - docs
                - codi
                - recursos

        - name: Configurar ACL per a l'equip
            acl:
                path: "/projectes/{{ projecte }}"
                entity: "{{ equip }}"
                etype: group
                permissions: rwx
                recursive: yes
                default: yes
                state: present

        - name: Configurar ACL per a QA
            acl:
                path: "/projectes/{{ projecte }}"
                entity: "qa"
                etype: group
                permissions: rx
                recursive: yes
                default: yes
                state: present
```

## Millors pràctiques per a ACL

1. **Planificar abans d'implementar**: Dissenyar l'estructura d'accés abans de començar a aplicar ACL.

2. **Seguir el principi de privilegi mínim**: Concedir només els permisos estrictament necessaris.

3. **Utilitzar grups quan sigui possible**: En lloc d'assignar permisos a múltiples usuaris individuals, crear grups i assignar permisos als grups.

4. **Documentar la configuració**: Mantenir un registre de quines ACL s'apliquen i perquè.

5. **Revisar periòdicament**: Auditar regularment les ACL per eliminar permisos innecessaris.

6. **Utilitzar ACL per defecte amb cura**: Assegurar-se que els permisos heretats són apropriats per a tots els casos.

7. **Tenir en compte les màscares**: Recordar que la màscara pot limitar els permisos efectius.

8. **Incloure les ACL en els backup**: Assegurar-se que les còpies de seguretat preserven les ACL.

## Eines gràfiques per a la gestió d'ACL

Per als usuaris que prefereixen interfícies gràfiques, existeixen diverses opcions:

### Nautilus (GNOME)

El gestor de fitxers de GNOME permet gestionar ACL:

1. Clic dret sobre un fitxer → Propietats
2. Pestanya "Permisos"
3. Clic a "Accés a fitxers: Gestionar accés"

### Dolphin (KDE)

El gestor de fitxers de KDE també ho permet:

1. Clic dret sobre un fitxer → Propietats
2. Pestanya "Permisos"
3. Secció "Permisos avançats"

### eiciel

Una eina específica per a la gestió gràfica de les ACL:

```bash
# Instal·lació en distribucions basades en Debian
sudo apt-get install eiciel

# En distribucions basades en RedHat
sudo yum install eiciel
```

Es pot iniciar des de la línia de comandes o integrar-se amb Nautilus.

## Consideracions de seguretat avançades

### Interacció entre permisos tradicionals i ACL

És important entendre que:

1. Els permisos tradicionals i les ACL coexisteixen
2. Per tal que un usuari accedeixi a un fitxer, **ambdós** sistemes han de permetre-ho
3. Si els permisos tradicionals deneguen l'accés, les ACL no poden concedir-lo

Exemple: Si un fitxer té permisos `chmod 600` (només el propietari pot llegir/escriure), una ACL que doni permisos a un altre usuari no tindrà efecte fins que es canviïn els permisos tradicionals.

### Implicacions de seguretat

Les ACL afegeixen complexitat, cosa que pot tenir conseqüències no intencionades:

- Més difícil detectar configuracions incorrectes
- Problemes de permisos més difícils de diagnosticar
- Possibilitat d'oblidar entrades ACL antigues

Recomanacions:

- Utilitzar eines com `getfacl -R` per auditar regularment
- Mantenir una documentació clara de l'esquema d'ACL
- Implementar processos per revisar les ACL quan els usuaris canvien de rol

## Casos d'estudi: Resolució de problemes amb ACL

### Cas 1: "No puc modificar els fitxers tot i tenir permisos"

**Problema**: Un usuari té permisos d'escriptura segons `getfacl`, però no pot modificar els fitxers.

**Diagnòstic**:

```bash
ls -la /projecte/fitxer.txt
# Mostra: -rw-r--r-- 1 propietari grup 123 Oct 10 12:00 fitxer.txt

getfacl /projecte/fitxer.txt
# Mostra:
# file: projecte/fitxer.txt
# owner: propietari
# group: grup
user::rw-
user:usuari:rw-     #effective:r--
group::r--
mask::r--
other::r--
```

**Causa**: La màscara ACL està limitant els permisos efectius a només lectura.

**Solució**:

```bash
setfacl -m m::rwx /projecte/fitxer.txt
```

### Cas 2: "Les ACL no s'apliquen als nous fitxers"

**Problema**: S'han configurat ACL en un directori, però els nous fitxers creats no hereten els permisos.

**Diagnòstic**:

```bash
getfacl /projecte
# No es mostren ACL per defecte
```

**Causa**: No s'han configurat ACL per defecte, només ACL normals.

**Solució**:

```bash
# Afegir ACL per defecte (amb l'opció -d)
setfacl -d -m u:usuari:rwx /projecte
```

### Cas 3: "Les ACL es perden després de moure fitxers"

**Problema**: Després de moure fitxers d'un directori a un altre, les ACL desapareixen.

**Diagnòstic**: Verificar com s'estan movent els fitxers. Si s'utilitza `mv` entre sistemes de fitxers diferents, es fa una còpia i eliminació en lloc d'un simple reanomenament.

**Solució**:

```bash
# Opció 1: Copiar preservant atributs i després eliminar
cp -a fitxer.txt /destí/
rm fitxer.txt

# Opció 2: Utilitzar eines que preservin les ACL
rsync -a fitxer.txt /destí/
```

## Les ACL en sistemes de fitxers diferents

Les ACL es comporten de manera similar en els principals sistemes de fitxers de Linux, però hi ha diferències a tenir en compte:

### ext4

- Suport complet per a ACL
- Activat per defecte en la majoria de distribucions modernes
- Molt estable i ben provat

### XFS

- Suport natiu per a ACL
- Especialment bon rendiment amb ACL
- Gestió excel·lent en sistemes amb molts fitxers

### Btrfs

- Suport complet per a ACL
- Les instantànies (snapshots) preserven les ACL
- Capacitats addicionals com compressió i deduplicació

### NTFS (muntats a Linux)

- Suport limitat per a ACL
- Les ACL natives de Windows no es tradueixen directament a ACL de Linux
- Cal precaució en entorns mixtos Windows/Linux

## Migració i compatibilitat

### Migració de sistemes sense ACL a sistemes amb ACL

Quan es migra d'un sistema que no utilitzava ACL a un que sí:

1. Definir l'esquema d'ACL desitjat
2. Aplicar ACL als directoris principals
3. Utilitzar l'opció recursiva per aplicar-les:
   ```bash
   setfacl -R -m u:usuari:rwx /directori
   ```
4. Configurar ACL per defecte per a nous fitxers:
   ```bash
   setfacl -R -d -m u:usuari:rwx /directori
   ```

### Compatibilitat amb altres sistemes

Les ACL POSIX són un estàndard, però cal tenir en compte:

- **NFS**: Verificar que el servidor i el client tenen activades les ACL
- **Samba**: Per compartir amb Windows, configurar `vfs objects = acl_xattr` al smb.conf
- **Backup**: Assegurar-se que el sistema de còpies de seguretat preserva les ACL

## Conclusions i Resum

Les Llistes de Control d'Accés (ACL) són una extensió valuosa del sistema tradicional de permisos de Linux que proporcionen:

1. **Major granularitat**: Permisos específics per a usuaris i grups concrets
2. **Flexibilitat**: Superació de les limitacions del model clàssic propietari/grup/altres
3. **Control avançat**: Especialment útil en entorns multiusuari i col·laboratius

Les ACL són essencials en entorns empresarials, acadèmics o col·laboratius on es requereix un control precís de l'accés als fitxers i directoris.

### Resum de comandes principals

- `getfacl fitxer`: Visualitzar les ACL
- `setfacl -m u:usuari:rwx fitxer`: Afegir o modificar ACL
- `setfacl -x u:usuari fitxer`: Eliminar una entrada ACL
- `setfacl -b fitxer`: Eliminar totes les ACL
- `setfacl -d -m u:usuari:rwx directori`: Establir ACL per defecte
- `setfacl -R -m u:usuari:rwx directori`: Aplicar ACL recursivament

### Recomanacions finals

1. Començar amb un disseny simple i anar afegint complexitat quan sigui necessari
2. Documentar l'esquema d'ACL utilitzat
3. Incloure les ACL en els plans de backup i restauració
4. Auditar periòdicament els permisos ACL
5. Formar als administradors i usuaris sobre com gestionar i interpretar les ACL

## Referències i recursos addicionals

Per aprofundir més en l'ús de les ACL a GNU/Linux:

1. Pàgines del manual:

   ```bash
   man acl
   man getfacl
   man setfacl
   ```

2. Documentació de sistemes de fitxers:

   ```bash
   man mount  # Cercar l'opció "acl"
   man ext4
   man xfs
   ```
