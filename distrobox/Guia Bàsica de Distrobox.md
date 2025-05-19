
## Què és Distrobox?

Distrobox és una eina que permet utilitzar qualsevol distribució de Linux dins del vostre sistema Ubuntu existent. Utilitza contenidors (amb Docker o Podman) per crear entorns aïllats on podeu instal·lar i executar aplicacions d'altres distribucions sense modificar el vostre sistema amfitrió.

## Avantatges de Distrobox

- Utilitzar eines i versions de programari d'altres distribucions
- Provar diferents distribucions sense necessitat de màquines virtuals pesades
- Mantenir un sistema base net i estable mentre es treballa amb configuracions experimentals
- Migrar gradualment entre distribucions
- Executar versions específiques de programari sense afectar el sistema principal

## Instal·lació de Distrobox a Ubuntu

### Requisits previs

Primer, cal tenir instal·lat Docker o Podman. Per a aquesta guia, utilitzarem Docker:

```bash
# Actualitzar els repositoris
sudo apt update

# Instal·lar dependències necessàries
sudo apt install -y ca-certificates curl gnupg lsb-release

# Afegir la clau GPG oficial de Docker
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

# Configurar el repositori de Docker
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# Actualitzar els repositoris
sudo apt update

# Instal·lar Docker
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-compose-plugin

# Afegir l'usuari al grup docker per evitar utilitzar sudo
sudo usermod -aG docker $USER
```

Després de l'últim comandament, haureu de tancar la sessió i tornar a iniciar-la (o reiniciar) perquè els canvis del grup tinguin efecte.

### Instal·lació de Distrobox

Hi ha diverses maneres d'instal·lar Distrobox:

#### Mètode 1: Instal·lació des dels repositoris (Ubuntu 22.10+)

```bash
sudo apt install distrobox
```

#### Mètode 2: Instal·lació manual

```bash
# Baixar l'script d'instal·lació
curl -s https://raw.githubusercontent.com/89luca89/distrobox/main/install | sudo sh
```

#### Mètode 3: Instal·lació només per a l'usuari actual (sense privilegis de root)

```bash
curl -s https://raw.githubusercontent.com/89luca89/distrobox/main/install | sh -s -- --prefix ~/.local
```

## Ús bàsic de Distrobox

### Crear un nou contenidor

```bash
# Sintaxi: distrobox create -n [nom] -i [imatge]
distrobox-create -n fedora -i fedora:latest
distrobox-create -n arch -i archlinux:latest
distrobox-create -n debian -i debian:latest
```

### Entrar al contenidor

```bash
# Entrar al contenidor "fedora"
distrobox enter fedora
```

### Llistar els contenidors existents

```bash
distrobox list
```

### Executar comandes directament dins del contenidor

```bash
# Sintaxi: distrobox-enter -n [nom] -- [comanda]
distrobox enter -n fedora -- dnf search vim
```

### Aturar i iniciar contenidors

```bash
# Aturar un contenidor
distrobox stop fedora

# Iniciar un contenidor aturat
distrobox start fedora
```

### Eliminar un contenidor

```bash
distrobox rm fedora
```

## Funcionalitats avançades

### Exportar aplicacions del contenidor al sistema amfitrió

Podeu instal·lar aplicacions dins del contenidor i després exportar-les per utilitzar-les com si fossin aplicacions natives:

```bash
# Instal·lar una aplicació dins del contenidor
distrobox enter -n fedora -- sudo dnf install -y vlc

# Exportar l'aplicació al sistema amfitrió
distrobox enter -n fedora -- distrobox-export --app vlc
```

Ara trobareu l'aplicació al vostre menú d'aplicacions d'Ubuntu.

### Exportar binaris

També podeu exportar binaris específics:

```bash
distrobox enter -n fedora -- distrobox-export --bin /usr/bin/htop
```

### Compartir directoris amb el contenidor

Per defecte, el vostre directori personal ja està compartit. Per compartir directoris addicionals:

```bash
distrobox create -n fedora -i fedora:latest -V /ruta/al/directori/a/compartir:/destí/al/contenidor
```

## Resolució de problemes comuns

### El contenidor no s'inicia

Comproveu que Docker estigui en funcionament:

```bash
sudo systemctl status docker
```

### Errors de permisos

Assegureu-vos que l'usuari formi part del grup docker:

```bash
groups $USER
```

Si no hi apareix "docker", executeu:

```bash
sudo usermod -aG docker $USER
```

i reinicieu la sessió.

## Exemples d'ús pràctic

1. **Provar programari més recent**: Utilitzeu una distribució rolling release com Arch Linux per accedir a les versions més recents.
    
    ```bash
    distrobox-create -n arch -i archlinux:latest
    distrobox enter arch
    sudo pacman -Syu firefox
    ```
    
2. **Desenvolupament amb entorns específics**: Crear un contenidor dedicat a un projecte.
    
    ```bash
    distrobox-create -n dev-python -i fedora:latest
    distrobox enter dev-python
    sudo dnf install -y python3-devel gcc
    ```
    
3. **Utilitzar eines exclusives d'altres distribucions**:
    
    ```bash
    distrobox-create -n opensuse -i opensuse/tumbleweed:latest
    distrobox enter opensuse
    sudo zypper install yast2
    ```