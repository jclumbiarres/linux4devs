`rsync`

- **Remote Synchronization**\_) és una eina **potent i eficient** per a:
- **Sincronitzar fitxers i directoris** (local o remotament).
- **Fer còpies de seguretat** incrementals (només transfereix els canvis).
- **Transferir dades** amb compressió i opcions de seguretat.

### **Sintaxi Bàsica**

```bash
rsync [OPCIONS] ORIGEN DESTÍ
```

**Exemples d'origen/destí**:

- **Local**: `/ruta/local/`
- **Remot**: `usuari@servidor:/ruta/remota/`
- **Protocols suportats**: SSH (`rsync://`, `ssh` per defecte).

### **Opcions Clau**

#### **Opcions generals**:

- **`-a` (archive mode)**: Activa opcions per a **mantenir** metadades (permisos, propietari, timestamps).  
   Inclou: `-r` (recursiu), `-l` (copiar enllaços simbòlics), `-p` (permisos), `-t` (timestamps), `-g` (grup).
- **`-v` (verbose)**: Mostra detalls de la transferència.
- **`-z` (compressió)**: Comprimeix dades durant la transferència (ideal per a xarxes lentes).
- **`-P`**: Combina `--progress` (mostra progrés) i `--partial` (resumeix transferències interrompudes).
- **`-n` (dry run)**: Simula la sincronització **sense fer canvis reals** (ideal per provar).
- **`--delete`**: **Esborra fitxers al destí** que ja no existeixen a l'origen (_**ús amb cura!**_).

#### **Opcions per a exclusions**:

- **`--exclude="PATRÓ"`**: Exclou fitxers/directoris que coincideixin amb el patró (ex: `*.log`).
- **`--include="PATRÓ"`**: Inclou fitxers/directoris específic després d'exclusions.
- **`--exclude-from=FILE`**: Llegeix patrons d'exclusió des d'un fitxer.

#### **Opcions per a transferències remotes**:

- **`-e "ssh"`**: Especifica el protocol (per defecte és SSH).
- **`-avz`**: Combinació habitual per a sincronització remota segura i comprimida.

#### **Sincronització local**

```bash
rsync -av /ruta/origen/ /ruta/destí/
```

**Nota**: La **barra final (`/`)** a l'origen importa:

- **Amb `/`**: Sincronitza el _**contingut**_ del directori origen al destí.
- **Sense `/`**: Crea una _**còpia del directori**_ dins del destí.

#### **2. Sincronització remota (local → servidor)**

```bash
rsync -avz -P /ruta/local/ usuari@servidor:/ruta/remota/
```

#### **3. Sincronització remota (servidor → local)**

```bash
rsync -avz -P usuari@servidor:/ruta/remota/ /ruta/local/
```

#### **4. Excloure fitxers/directoris**

```bash
rsync -av --exclude="*.tmp" --exclude="/backups/" /origen/ /destí/
```

#### **5. Sincronització bidireccional (mirroring)**

```bash
rsync -av --delete /origen/ /destí/  # Elimina al destí el que no hi és a l'origen
```

#### **6. Transferir amb compressió (xarxes lentes)**

```bash
rsync -avz -e "ssh -p 2222" /origen/ usuari@servidor:/destí/
```
