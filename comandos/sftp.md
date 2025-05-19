#### **Què és?**

`sftp` és un **client interactiu** per a transferir fitxers, similar a l'antic `ftp`, però amb xifratge SSH. Permet:

- Navegar per directoris locals i remots.
- Pujar, baixar, eliminar o renombrar fitxers.

**Avantatges**:
- Ideal per a **sessions interactives** amb múltiples operacions.
- Suporta comandes similars a les d'un terminal (ex: `ls`, `cd`, `mkdir`).

#### **Iniciar una connexió**

```bash
sftp usuari@servidor  
```

Si el servidor usa un port diferent a 22:
```bash
sftp -oPort=2222 usuari@servidor  
```

---

#### **Comandes bàsiques dins de `sftp`**

| **Comanda**       | **Descripció**                        |
| ----------------- | ------------------------------------- |
| `ls`              | Llista fitxers/directoris **remots**. |
| `lls`             | Llista fitxers/directoris **locals**. |
| `cd`              | Canvia de directori **remot**.        |
| `lcd`             | Canvia de directori **local**.        |
| `put fitxer`      | Puja un fitxer **local → remot**.     |
| `get fitxer`      | Baixa un fitxer **remot → local**.    |
| `mkdir directori` | Crea un directori **remot**.          |
| `rm fitxer`       | Elimina un fitxer **remot**.          |
| `exit` o `bye`    | Tanca la connexió.                    |

---

#### **Exemple d'ús interactiu**

```bash
sftp usuari@example.com  
sftp> cd /var/www  
sftp> lcd ~/Downloads  
sftp> put index.html  
sftp> get error.log  
sftp> bye  
```
---

### **4. Comparativa `scp` vs `sftp`**

| **Característica**         | **`scp`**                              | **`sftp`**                           |
| -------------------------- | -------------------------------------- | ------------------------------------ |
| **Interactivitat**         | No (execució única)                    | Sí (sessió interactiva)              |
| **Transferències**         | Ràpid per a fitxers grans o únics      | Millor per a múltiples operacions    |
| **Navegació**              | No permet navegar directoris           | Permet navegar tant local com remot  |
| **Resumir transferències** | No suporta reprendre transferències    | Sí (amb clients avançats)            |
| **Casos d'ús**             | Còpies puntuals, scripts automatitzats | Gestió de fitxers remots interactiva |
