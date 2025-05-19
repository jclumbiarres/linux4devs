### **1. Terminal i Core Utils**

- **Aprèn les comandes bàsiques:** Domina `ls`, `grep`, `awk`, `sed`, `find`, i `rsync`. Combina-les amb pipes (`|`) per automatitzar tasques.
- **Documenta’t sempre:** Usa `man <comanda>` o `<comanda> --help` abans de preguntar. Exemple: `man grep`.
- **Evita permisos perillosos:** Mai facis `chmod 777`. Utilitza `chmod 755` per directoris i `644` per fitxers, si cal.

---

### **2. Gestió del Tallafocs (UFW)**

- **Activa sempre el tallafocs:**
```bash
sudo ufw enable
```

- **Sigues específic amb les regles:** Enlloc de permetre tot el trànsit (`sudo ufw allow 22/tcp`), limita per IP:
```bash
 sudo ufw allow from 192.168.1.10 to any port 22  
```

- **Revisa les regles regularment:**
```bash
sudo ufw status numbered  
```
 
---

### **3. Neovim (LazyVim)**

- **Personalitza el fitxer de configuració:** Edita `~/.config/nvim/lua/plugins` per adaptar-ho a les teves necessitats.

- **Versiona la teva configuració:** Fes un repositori Git per a la carpeta `~/.config/nvim`.
  

---

### **4. Gestió de Paquets (APT)**

- **Actualitza regularment:**
```bash
sudo apt update && sudo apt upgrade -y
```

- **Neteja el cache:**
```bash
sudo apt clean && sudo apt autoremove  
```
 
- **Evita trencar dependències:** No modifiquis el `/etc/apt/sources.list` sense fer una còpia abans:
```bash
sudo cp /etc/apt/sources.list /etc/apt/sources.list.backup  
```

---

### **5. Docker**

- **Executa com a usuari no-root:** Afegeix el teu usuari al grup `docker`:
```bash
sudo usermod -aG docker $USER 
```
 
- **Utilitza Docker Compose:** Organitza els serveis amb fitxers `docker-compose.yml`.
- **Neteja imatges inútils:**
```bash
docker system prune -a
```

---

### **6. Systemd**

- **Aprèn les comandes essencials:**
	- `systemctl start/stop/restart <servei>`
	- `systemctl enable/disable <servei>`

- **Revisa els logs:**
	* `journalctl -u <servei> -f` 

---

### **7. SSH**

- **Deshabilita l’accés root:** Modifica `/etc/ssh/sshd_config`:
	- `PermitRootLogin no`  
- **Usa claus SSH:** Genera-les amb `ssh-keygen` i copia-les amb `ssh-copy-id`.
- **Canvia el port per defecte (22):** Redueix els atacs automàtics.

---

### **Consells Generals**

- **Fes còpies de seguretat (backups):** Automatitza amb `cron` i `rsync`.
- **Prova en entorns aïllats:** Usa màquines virtuals o contenidors Docker per experiments.