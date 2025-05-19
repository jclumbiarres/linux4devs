## Índex de tasques

1. Gestió d'usuaris i permisos (20 min)
2. Instal·lació i configuració de Docker (25 min)
3. Configuració de Distrobox amb Arch Linux (20 min)
4. Instal·lació i configuració de tmux amb TPM (20 min)
5. Instal·lació d'asdf-vm 0.16.7 (20 min)
6. Instal·lació de Neovim des de Distrobox (15 min)
7. Instal·lació d'eines de desenvolupament (15 min)
8. Configuració de LazyVim (15 min)
9. Instal·lació de llenguatges amb asdf-vm (20 min)
10. Creació d'script de backup amb rsync (15 min)
11. Configuració d'UFW (10 min)
12. Creació de servei d'usuari i configuració de crontab (15 min)

## 1. Gestió d'usuaris i permisos (20 min)

### Creació d'un nou usuari

```bash
sudo adduser alumne
sudo useradd -m alumne && sudo passwd alumne
```

### Afegir l'usuari als grups sudo i docker

```bash
sudo usermod -aG sudo alumne
sudo usermod -aG docker alumne
```

### Verificar els grups de l'usuari

```bash
groups alumne
```

### Canviar a l'usuari nou

```bash
su - alumne
```

## 2. Instal·lació i configuració de Docker (25 min)

### Actualitzar els paquets

```bash
sudo apt update
sudo apt upgrade -y
```

### Instal·lar paquets necessaris

```bash
sudo apt install -y apt-transport-https ca-certificates curl software-properties-common gnupg
```

### Afegir la clau GPG oficial de Docker

```bash
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

### Afegir el repositori de Docker

```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

### Instal·lar Docker CE

```bash
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io
```

### Verificar que Docker s'ha instal·lat correctament

```bash
sudo docker run hello-world
```

### Comprovar que l'usuari pot executar Docker sense sudo

```bash
docker run hello-world
```

## 3. Configuració de Distrobox amb Arch Linux (20 min)

### Instal·lar Distrobox

```bash
curl -s https://raw.githubusercontent.com/89luca89/distrobox/main/install | sudo sh
```


```

### Afegir Distrobox al PATH

```bash
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

### Crear un contenidor amb Arch Linux

```bash
distrobox-create --name archlinux --image archlinux:latest
```

### Entrar al contenidor d'Arch Linux

```bash
distrobox enter archlinux
```

### Actualitzar el sistema Arch Linux

```bash
sudo pacman -Syu --noconfirm
```

### Sortir del contenidor

```bash
exit
```

## 4. Instal·lació i configuració de tmux amb TPM (20 min)

### Instal·lar tmux

```bash
sudo apt install -y tmux
```

### Instal·lar TPM (Tmux Plugin Manager)

```bash
git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
```

### Crear configuració de tmux

```bash
cat > ~/.tmux.conf << 'EOF'
# Canviar prefix a Ctrl+a
unbind C-b
set -g prefix C-a
bind C-a send-prefix

# Millores en la navegació
set -g mouse on
set -g mode-keys vi
set -g history-limit 10000

# Indexar des de 1 (més intuïtiu)
set -g base-index 1
setw -g pane-base-index 1

# Recarregar configuració amb prefix + r
bind r source-file ~/.tmux.conf \; display "Configuració recarregada!"

# Dividir panells amb v i h
bind v split-window -h
bind h split-window -v

# Tema i colors
set -g status-style 'bg=#333333 fg=#5eacd3'
set -g status-right '#[fg=green]#H | %d/%m/%Y %H:%M'

# Plugins
set -g @plugin 'tmux-plugins/tpm'
set -g @plugin 'tmux-plugins/tmux-sensible'
set -g @plugin 'tmux-plugins/tmux-resurrect'
set -g @plugin 'tmux-plugins/tmux-continuum'
set -g @plugin 'tmux-plugins/tmux-yank'

# Inicialitzar TPM (ha d'estar al final)
run '~/.tmux/plugins/tpm/tpm'
EOF
```

### Instal·lar els plugins

```bash
# Iniciar tmux si no està obert
tmux

# Instal·lar plugins (dins de tmux)
# Pressionar Ctrl+a i després Shift+i
```

### Sortir i tornar a entrar a tmux per verificar

```bash
# Sortir de tmux
# Ctrl+a + d

# Tornar a entrar
tmux
```

## 5. Instal·lació d'asdf-vm 0.16.7 (20 min)

### Descarregar asdf-vm 0.16.7 (ara en golang)

```bash
mkdir -p ~/.local/bin
cd /tmp

# Descarregar el binari per a l'arquitectura corresponent
curl -LO https://github.com/asdf-vm/asdf/releases/download/v0.16.7/asdf-v0.16.7-linux-amd64.tar.gz
```

### Verificar el checksum

```bash
curl -LO https://github.com/asdf-vm/asdf/releases/download/v0.16.7/asdf-v0.16.7-linux-amd64.tar.gz.md5
md5sum asdf-v0.16.7-linux-amd64.tar.gz && cat asdf-v0.16.7-linux-amd64.tar.gz.md5
```

### Instal·lar el binari

```bash
tar -xzf asdf-v0.16.7-linux-amd64.tar.gz
mv asdf ~/.local/bin/
chmod +x ~/.local/bin/asdf
```

### Configurar asdf al .bashrc

```bash
# si no existeix el condicional amb $HOME/.local/bin al bashrc:
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
echo 'source <(asdf completion bash)' >> ~/.bashrc
source ~/.bashrc
```

### Verificar la instal·lació

```bash
asdf --version
```

## 6. Instal·lació de Neovim des de Distrobox (15 min)

### Entrar al contenidor d'Arch

```bash
distrobox enter archlinux
```

### Instal·lar Neovim en Arch

```bash
sudo pacman -S --noconfirm neovim
```

### Exportar el binari al sistema host

```bash
distrobox-export --bin /usr/bin/nvim --export-path ~/.local/bin
```

### Sortir del contenidor

```bash
exit
```

### Verificar que Neovim funciona al sistema host

```bash
nvim --version
```

## 7. Instal·lació d'eines de desenvolupament (15 min)

### Instal·lar build-essential i altres eines

```bash
sudo apt install -y build-essential
```

### Instal·lar FZF (Fuzzy Finder)

```bash
sudo apt install -y fzf
```

### Instal·lar fd-find

```bash
sudo apt install -y fd-find
ln -s $(which fdfind) ~/.local/bin/fd
```

### Instal·lar ripgrep

```bash
sudo apt install -y ripgrep
```

### Verificar les instal·lacions

```bash
gcc --version
fzf --version
fd --version
rg --version
```

## 8. Configuració de LazyVim (15 min)

### Crear directoris necessaris

```bash
mkdir -p ~/.config/nvim
```

### Instal·lar LazyVim

```bash
git clone https://github.com/LazyVim/starter ~/.config/nvim
rm -rf ~/.config/nvim/.git
```

### Iniciar Neovim per instal·lar plugins

```bash
nvim
```

### Verificar que LazyVim s'ha instal·lat correctament

```bash
# Després de tancar nvim, tornar a obrir-lo
nvim
```

## 9. Instal·lació de llenguatges amb asdf-vm (20 min)

### Instal·lar plugins per als llenguatges

```bash
asdf plugin add java
asdf plugin add golang
asdf plugin add python
asdf plugin add nodejs
```

### Instal·lar Java i configurar-lo com a versió global

```bash
asdf install java latest
asdf set -u java XXXX 
```

### Instal·lar Go i configurar-lo com a versió global

```bash
asdf install golang latest
asdf set -u golang XXXX
```

### Instal·lar Python i configurar-lo com a versió global

```bash
asdf install python latest
asdf set -u python XXXX
```

### Instal·lar Node.js i configurar-lo com a versió global

```bash
asdf install nodejs latest
asdf set -u nodejs XXXX
```

### Verificar les instal·lacions

```bash
java -version
go version
python --version
node --version
```

## 10. Creació d'script de backup amb rsync (15 min)

### Crear directori per a backups

```bash
mkdir -p ~/backups
```

### Crear directori per a scripts

```bash
mkdir -p ~/.local/bin
```

### Crear l'script de backup amb Neovim

```bash
nvim ~/.local/bin/backup.sh
```

### Contingut de l'script de backup

```bash
#!/bin/bash

# Script de còpia de seguretat amb rsync
# Crea una còpia de seguretat del directori principal de l'usuari

# Definir origen i destí
ORIGEN="$HOME/Documents"
DESTI="$HOME/backups/backup-$(date +%Y%m%d-%H%M%S)"

# Crear missatge al log
echo "Iniciant còpia de seguretat a $(date)" >> "$HOME/backups/backup.log"

# Executar rsync
rsync -av --exclude=".*" --exclude="node_modules" --exclude=".git" "$ORIGEN" "$DESTI"

# Registrar finalització
echo "Còpia de seguretat completada a $(date)" >> "$HOME/backups/backup.log"
echo "S'ha desat a: $DESTI" >> "$HOME/backups/backup.log"
echo "----------------------------------------" >> "$HOME/backups/backup.log"
```

### Fer executable l'script

```bash
chmod +x ~/.local/bin/backup.sh
```

### Provar l'script

```bash
~/.local/bin/backup.sh
```

## 11. Configuració d'UFW (10 min)

### Instal·lar UFW si no està instal·lat

```bash
sudo apt install -y ufw
```

### Configurar regles per defecte

```bash
# Denegar tot el tràfic entrant per defecte
sudo ufw default deny incoming

# Permetre tot el tràfic sortint per defecte
sudo ufw default allow outgoing
```

### Afegir regles per permetre connexions als ports específics

```bash
# Permetre SSH (port 22)
sudo ufw allow 22/tcp

# Permetre HTTP (port 80)
sudo ufw allow 80/tcp

# Permetre HTTPS (port 443)
sudo ufw allow 443/tcp
```

### Habilitar UFW

```bash
sudo ufw enable
```

### Verificar l'estat d'UFW

```bash
sudo ufw status verbose
```

## 12. Creació de servei d'usuari i configuració de crontab (15 min)

### Crear directori per als serveis d'usuari

```bash
mkdir -p ~/.config/systemd/user
```

### Crear el fitxer de servei de backup

```bash
nvim ~/.config/systemd/user/backup.service
```

### Contingut del fitxer de servei

```ini
[Unit]
Description=Backup personal amb rsync
After=network.target

[Service]
Type=oneshot
ExecStart=%h/.local/bin/backup.sh
StandardOutput=journal

[Install]
WantedBy=default.target
```

### Habilitar i iniciar el servei

```bash
systemctl --user daemon-reload
systemctl --user enable backup.service
systemctl --user start backup.service
```

### Crear un temporitzador (timer) per a execucions periòdiques

```bash
nvim ~/.config/systemd/user/backup.timer
```

### Contingut del fitxer del temporitzador

```ini
[Unit]
Description=Executa backup cada 12 hores

[Timer]
OnBootSec=5min
OnUnitActiveSec=12h
Persistent=true

[Install]
WantedBy=timers.target
```

### Habilitar i iniciar el temporitzador

```bash
systemctl --user enable backup.timer
systemctl --user start backup.timer
```

### Configurar crontab per a execucions cada 12 hores

```bash
crontab -e
```

### Afegir la següent línia al crontab

```
0 */12 * * * ~/.local/bin/backup.sh &
```

### Verificar l'estat del servei i temporitzador

```bash
systemctl --user status backup.service
systemctl --user status backup.timer
systemctl --user list-timers
```

---

## Verificació final (10 min)

Verifica tot el que s'ha instal·lat i configurat:

```bash
# Comprovar usuari i grups
id alumne

# Comprovar Docker
docker --version

# Comprovar Distrobox
distrobox list

# Comprovar tmux
tmux -V

# Comprovar asdf
asdf --version

# Comprovar Neovim
nvim --version

# Comprovar eines de desenvolupament
gcc --version
fzf --version
fd --version
rg --version

# Comprovar els llenguatges
java -version
go version
python --version
node --version

# Comprovar l'script de backup
ls -la ~/.local/bin/backup.sh
cat ~/backups/backup.log

# Comprovar UFW
sudo ufw status verbose

# Comprovar serveis d'usuari
systemctl --user status backup.service
systemctl --user status backup.timer
```