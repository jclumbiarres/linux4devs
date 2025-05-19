## Què és Ulimit?

Ulimit és una eina integrada als sistemes basats en Unix, com Ubuntu, que permet controlar els recursos disponibles per als processos i usuaris del sistema. Mitjançant ulimit, els administradors poden establir límits en diversos aspectes del sistema, com ara el nombre de fitxers oberts, l'ús de CPU, la mida de la memòria i més.

## Conceptes Bàsics

Ulimit opera amb dos tipus de límits:

- **Límits tous (soft limits)**: Són els límits actuals aplicats als processos. Es poden augmentar pel propi usuari fins al límit dur corresponent.
- **Límits durs (hard limits)**: Són els valors màxims fins als quals es poden augmentar els límits tous. Només l'usuari root pot modificar aquests límits.

## Comandes Bàsiques d'Ulimit

### Visualitzar Límits Actuals

Per veure tots els límits actuals de l'usuari:

```bash
ulimit -a
```

Sortida típica:

```
core file size          (blocks, -c) 0
data seg size           (kbytes, -d) unlimited
scheduling priority             (-e) 0
file size               (blocks, -f) unlimited
pending signals                 (-i) 15615
max locked memory       (kbytes, -l) 16384
max memory size         (kbytes, -m) unlimited
open files                      (-n) 1024
pipe size            (512 bytes, -p) 8
POSIX message queues     (bytes, -q) 819200
real-time priority              (-r) 0
stack size              (kbytes, -s) 8192
cpu time               (seconds, -t) unlimited
max user processes              (-u) 15615
virtual memory          (kbytes, -v) unlimited
file locks                      (-x) unlimited
```

### Tipus de Límits i Paràmetres

Els paràmetres més comuns són:

- `-n`: Nombre màxim de fitxers oberts (open files)
- `-u`: Nombre màxim de processos per usuari (max user processes)
- `-f`: Mida màxima de fitxer en blocs (file size)
- `-t`: Temps màxim de CPU en segons (cpu time)
- `-m`: Mida màxima de memòria en kilobytes (max memory size)
- `-v`: Mida màxima de memòria virtual en kilobytes (virtual memory)
- `-s`: Mida màxima de la pila en kilobytes (stack size)
- `-c`: Mida màxima dels fitxers core en blocs (core file size)
- `-l`: Memòria màxima bloquejada en kilobytes (max locked memory)

### Modificar Límits Temporalment

Per canviar el nombre màxim de fitxers oberts per a la sessió actual:

```bash
# Establir límit tou
ulimit -n 4096

# Establir límit dur (necessita privilegis de root)
sudo ulimit -Hn 4096
```

On:

- `-n`: Especifica que volem modificar el límit de fitxers oberts
- `-H`: Indica que volem canviar el límit dur (sense aquesta opció, canviem el límit tou)

## Configuració Permanent de Límits

Els canvis realitzats amb la comanda `ulimit` només són vàlids durant la sessió actual. Per establir límits permanents, cal modificar els fitxers de configuració del sistema.

### Límits per a Tots els Usuaris

Per establir límits globals que afectin tots els usuaris, modifica el fitxer `/etc/security/limits.conf`:

```bash
sudo nano /etc/security/limits.conf
```

Format del fitxer:

```
domain type item value
```

On:

- `domain`: Pot ser un nom d'usuari, un grup (prefixat amb @) o * per a tots els usuaris
- `type`: `soft` per a límits tous o `hard` per a límits durs
- `item`: El recurs a limitar (nofile, nproc, etc.)
- `value`: El valor del límit

Exemple:

```
# Augmentar el nombre de fitxers oberts per a tots els usuaris
*       soft    nofile  4096
*       hard    nofile  10240

# Límits específics per a l'usuari "ubuntu"
ubuntu  soft    nproc   2048
ubuntu  hard    nproc   4096

# Límits per al grup "desenvolupadors"
@desenvolupadors soft    nofile  8192
@desenvolupadors hard    nofile  16384
```

### Límits per a Serveis Systemd

Per als serveis gestionats per systemd, pots establir límits en el fitxer de configuració del servei:

```bash
sudo systemctl edit nom_del_servei
```

I afegir:

```ini
[Service]
LimitNOFILE=65535
LimitNPROC=4096
```

O editar directament el fitxer del servei:

```bash
sudo nano /etc/systemd/system/nom_del_servei.service
```

Després de modificar el fitxer de servei, cal recarregar systemd i reiniciar el servei:

```bash
sudo systemctl daemon-reload
sudo systemctl restart nom_del_servei
```

## Comprovació de Límits

### Per a un Procés en Execució

Per comprovar els límits d'un procés en execució, utilitza:

```bash
cat /proc/PID/limits
```

On `PID` és l'identificador del procés. Per exemple:

```bash
cat /proc/1234/limits
```

### Per a l'Usuari Actual

Per verificar els límits aplicats a l'usuari actual:

```bash
ulimit -a
```

## Paràmetres del Sistema Relacionats

Alguns límits del sistema estan controlats pel kernel de Linux i no per ulimit. Aquests es poden consultar i modificar a través de `sysctl`:

```bash
# Consultar el nombre màxim de fitxers oberts a nivell de sistema
sysctl fs.file-max

# Modificar temporalment
sudo sysctl -w fs.file-max=100000

# Fer el canvi permanent
echo "fs.file-max = 100000" | sudo tee -a /etc/sysctl.conf
sudo sysctl -p
```

## Configuracions Recomanades per a Casos d'Ús Comuns

### Servidor Web (Nginx/Apache)

```
# A /etc/security/limits.conf
www-data soft nofile 16384
www-data hard nofile 32768
```

### Servidor de Base de Dades (MySQL/PostgreSQL)

```
# A /etc/security/limits.conf
mysql soft nofile 65536
mysql hard nofile 65536
mysql soft nproc  4096
mysql hard nproc  4096
```

### Entorn de Desenvolupament

```
# A /etc/security/limits.conf
dev_user soft nofile 8192
dev_user hard nofile 16384
dev_user soft nproc  2048
dev_user hard nproc  4096
```

## Solució de Problemes Comuns

### "Too many open files"

Aquest error apareix quan un procés intenta obrir més fitxers dels permesos pel límit `nofile`:

1. Identifica quin procés està tenint el problema
2. Comprova els seus límits actuals:
    
    ```bash
    cat /proc/PID/limits | grep "open files"
    ```
    
3. Augmenta el límit a `/etc/security/limits.conf`
4. Si és un servei de systemd, afegeix `LimitNOFILE=65535` a la seva configuració

### "Cannot allocate memory" o "Out of memory"

Aquest problema pot aparèixer quan els processos excedeixen els límits de memòria:

1. Comprova els límits de memòria:
    
    ```bash
    ulimit -a | grep memory
    ```
    
2. Augmenta els límits si és necessari, tant a `limits.conf` com potencialment els paràmetres del kernel

### "Cannot fork: Resource temporarily unavailable"

Aquest error indica que s'ha arribat al límit de processos (`nproc`):

1. Verifica el límit actual:
    
    ```bash
    ulimit -u
    ```
    
2. Augmenta el límit a `/etc/security/limits.conf`:
    
    ```
    usuari soft nproc 4096usuari hard nproc 8192
    ```
    

## Exemples Pràctics

### Exemple 1: Configurar un Entorn per a Desenvolupament Web

```bash
# Afegir a /etc/security/limits.conf
developer soft nofile 8192
developer hard nofile 16384
developer soft nproc  4096
developer hard nproc  8192

# Reiniciar la sessió per aplicar els canvis
```

### Exemple 2: Preparar un Servidor per a Alta Càrrega

```bash
# Editar /etc/sysctl.conf
fs.file-max = 2097152
net.core.somaxconn = 65535

# Editar /etc/security/limits.conf
*       soft    nofile  1048576
*       hard    nofile  1048576
*       soft    nproc   262144
*       hard    nproc   262144

# Aplicar canvis
sudo sysctl -p
```

### Exemple 3: Limitar els Recursos d'un Usuari Específic

```bash
# Afegir a /etc/security/limits.conf
usuari_limitat soft cpu    60
usuari_limitat hard cpu    120
usuari_limitat soft nproc  100
usuari_limitat hard nproc  150
```

## Consideracions Importants

1. **Reinici de Sessió**: Els canvis a `limits.conf` només s'apliquen quan l'usuari inicia una nova sessió.
    
2. **Jerarquia de Configuració**: Els límits es carreguen en aquest ordre:
    
    - `/etc/security/limits.conf`
    - Fitxers a `/etc/security/limits.d/`
    - Configuració específica de PAM
3. **Comptabilitat de Recursos**: Alguns paràmetres requereixen que el kernel tingui activada la comptabilitat de recursos corresponent.
    
4. **Serveis Systemd**: Els serveis gestionats per systemd ignoren la configuració a `limits.conf` si no s'especifica als fitxers de servei.
    

## Comandaments Útils de Referència Ràpida

```bash
# Veure tots els límits
ulimit -a

# Establir límit de fitxers oberts
ulimit -n 4096

# Veure límit dur de fitxers oberts
ulimit -Hn

# Veure límit tou de fitxers oberts
ulimit -Sn

# Veure límit de processos
ulimit -u

# Eliminar límit (establir a il·limitat)
ulimit -s unlimited
```

## Conclusió

Ulimit és una eina essencial per a l'administració de sistemes Linux com Ubuntu, ja que permet un control precís sobre l'ús de recursos del sistema. Configurar adequadament els límits de recursos pot millorar significativament l'estabilitat i el rendiment del sistema, especialment en entorns amb alta càrrega o múltiples usuaris.

Recorda que alguns canvis requereixen privilegis de superusuari i que la configuració òptima dependrà del maquinari disponible i dels requisits específics de les aplicacions que s'executin al sistema.