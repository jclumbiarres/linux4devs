### **Què és `ssh`?**

El comandament `ssh` (_**Secure Shell**_) és una eina **imprescindible** per a:
- **Connectar-se de manera segura** a servidors o dispositius remots.
- **Executar comandes** en un sistema remot des del teu terminal local.
- **Transferir dades** de forma xifrada (evitant espionatge o manipulació).

**Avantatges respecte a protocols insegurs (ex: Telnet)**:
- **Xifratge**: Tota la comunicació es xifra (usuari, contrasenya, dades).
- **Autenticació flexible**: Mitjançant contrasenya o claus SSH (més segur).
- **Túnelització**: Redirigir ports locals/remots de forma segura.

---

### **2. Sintaxi Bàsica**

```bash
ssh [OPCIONS] USUARI@SERVIDOR  
```

**Exemples**:

```bash
# Connexió bàsica  
ssh root@192.168.1.10  

# Especificant port  
ssh -p 2222 usuari@example.com  
```
---

### **3. Opcions Clau**

#### **Opcions generals**:

- **`-p`**: Port del servidor SSH (per defecte: **22**).
```bash
ssh -p 2222 usuari@servidor
```
- **`-i`**: Ruta a una **clau privada** per a autenticació (sense contrasenya).
```bash
ssh -i ~/.ssh/clau_privada usuari@servidor
```
- **`-v`**: Mode **verbose** (mostra detalls de la connexió, útil per depurar errors).
```bash
ssh -v usuari@servidor
```
- **`-X`**: Habilita **X11 forwarding** (per executar aplicacions gràfiques remotes).
```bash
ssh -X usuari@servidor
```

#### **Opcions avançades**:

- **`-L`**: **Redirigir un port local** al remot (_Local Forwarding_).
```bash
# Accedeix al port 3306 del servidor remot via localhost:3306  
ssh -L 3306:localhost:3306 usuari@servidor      
```
- **`-R`**: **Redirigir un port remot** al local (_Remote Forwarding_).
```bash
ssh -R 8080:localhost:80 usuari@servidor 
```
- **`-t`**: Força l'ús d'una **pseudo-terminal** (necessari per a comandes interactives com `sudo`).
```bash
ssh -t usuari@servidor "sudo apt update"
```

---

### **4. Casos d'Ús Comuns**

#### **1. Connexió bàsica a un servidor**

```bash
ssh usuari@servidor  
```

**Nota**: Si és la primera vegada que et connectes, demana confirmar l'empremta del servidor (tecleja `yes`).

#### **2. Executar una comanda directa sense entrar al shell remot**

```bash
ssh usuari@servidor "ls -l /var/log"  
```

#### **3. Transferir fitxers usant `ssh` + `cat` (alternativa ràpida)**

```bash
# Local → Remot  
cat local.txt | ssh usuari@servidor "cat > remot.txt"  

# Remot → Local  
ssh usuari@servidor "cat remot.txt" > local.txt  
```

#### **4. Túnel segur per a accedir a un servei remot**

```bash
# Accedeix a un servidor web remot (port 80) via localhost:8888  
ssh -L 8888:localhost:80 usuari@servidor  
```

Obre el navegador i visita `http://localhost:8888`.

---

### **5. Configuració avançada amb `~/.ssh/config`**

Evita repetir opcions creant un fitxer de configuració:

```bash
nvim ~/.ssh/config  
```
**Exemple**:

```bash
Host servidor_web  
    HostName 192.168.1.20  
    User root  
    Port 2222  
    IdentityFile ~/.ssh/clau_web  
```

**Ús**:

```bash
ssh servidor_web  # Equival a ssh -p 2222 -i ~/.ssh/clau_web root@192.168.1.20  
```


---

### **6. Consells de Seguretat**

1. **Usa claus SSH en lloc de contrasenyes**:

```bash
ssh-keygen -t ed25519  # Genera un parell de claus  
ssh-copy-id usuari@servidor  # Copia la clau pública al servidor  
```

- **Deshabilita l'accés root per contrasenya**:  
    Modifica `/etc/ssh/sshd_config` al servidor:
```
PermitRootLogin no  
    PasswordAuthentication no
```

- **Canvia el port per defecte (22)**:

```
Port 2222
```

---

### **7. Resolució de Problemes**

- **Error "Connection refused"**:
    - Verifica que el servidor escolta el port correcte.
    - Assegura't que el firewall permet el trànsit.

- **Error "Permission denied"**:
    - Revisa els permisos dels fitxers `~/.ssh` (haurien de ser `700`).
    - Comprova que la clau pública estigui afegida a `~/.ssh/authorized_keys` al servidor.

---

### **8. Comparativa amb Alternatives**

| **Eina**    | **Avantatges**                    | **Inconvenients**               |
| ----------- | --------------------------------- | ------------------------------- |
| **`ssh`**   | Xifratge, versatilitat, claus SSH | Requerix configuració inicial   |
| **Telnet**  | Senzill                           | **Insegur** (dades en clar)     |
| **VNC/RDP** | Interfície gràfica                | Menys eficient en xarxes lentes |

---

### **9. Exemple Pràctic**

1. **Genera una clau SSH**:

```bash
ssh-keygen -t ed25519 -C "clau@meuportatil"
```

- **Copia la clau al teu servidor**:

```bash
ssh-copy-id -i ~/.ssh/id_ed25519.pub usuari@servidor
```  

- **Connecta't sense contrasenya**:

```bash
ssh usuari@servidor  
```

- **Executa una comanda remota**:

```bash
ssh usuari@servidor "df -h | grep /dev/sda1"
```
