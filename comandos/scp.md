`scp` (Secure Copy Protocol)
#### **Què és?**

`scp` permet **copiar fitxers o directoris** entre:
- Un sistema local i un remot.
- Dos sistemes remots (passant pel teu ordinador).

**Avantatges**:
- Senzill i ràpid per a transferències puntuals.
- Usa **SSH** per a xifratge i autenticació (mateixa seguretat que `ssh`).

#### **Sintaxi bàsica**

```bash
scp [OPCIONS] ORIGEN DESTÍ  
```

**Estructura d'origen/destí**:

- **Local**: `fitxer.txt` o `/ruta/local/fitxer.txt`
- **Remot**: `usuari@servidor:/ruta/remota/fitxer.txt`

---

#### **Opcions principals**

- **`-P`**: Port SSH del servidor (per defecte: 22).
 ```bash
scp -P 2222 fitxer.txt usuari@servidor:/ruta
```
- **`-r`**: Copia directoris de manera **recursiva**.
```bash
scp -r directori/ usuari@servidor:/backups
```
- **`-C`**: Activa compressió de dades durant la transferència.
- **`-v`**: Mode **verbose** (mostra detalls de la connexió).

---

#### **Exemples pràctics**

1. **Local → Remot**:
```bash
scp foto.jpg usuari@example.com:/home/usuari/imatges/
```

- **Remot → Local**:
```bash
scp usuari@example.com:/var/log/syslog .
```

- **Entre dos servidors remots**:
```bash
scp usuari@servidor1:/fitxer.txt usuari@servidor2:/backups/
```


