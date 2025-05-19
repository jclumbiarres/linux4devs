### **Què és Nushell?**

Nushell és una **shell alternativa** a Bash/Zsh/Fish, escrita en Rust, dissenyada per treballar amb **dades estructurades** (com taules, llistes, etc.) en lloc de text pla. És **multiplataforma** (Windows, Linux, macOS) i ideal per a qui vol una experiència més intuïtiva.

**Per què és especial?**

- **Dades estructurades**: Tracta fitxers, processos, etc., com **taules** amb columnes i registres.
- **Pipelines poderosos**: Filtra, transforma o visualitza dades com si fossis un expert.
- **Sintaxi senzilla**: Combina el millor de les shells tradicionals amb funcions de programació moderna.

---

### **Conceptes Clau**

#### 1. **Dades com Taules**

A Bash, tot és text. En **Nushell**, tot són taules amb camps definits.  
_Exemple_:

`ls  # Mostra fitxers com una taula amb nom, mida, data, etc.`

Sortida:
```

───┬──────────────┬──────┬───────────  
 # │ nom          │ mida │ data  
───┼──────────────┼──────┼───────────  
 0 │ document.txt │ 1 KB │ 2023-10-05  
```

#### 2. **Pipelines (Canalitzacions)**

En Nushell, pots **encadenar** comandes amb el símbol `|` per transformar dades.  
_Exemple_:

`ls | where mida > 1KB | sort-by data`

_Això llista fitxers de més d’1KB i els ordena per data_.

#### 3. **Tipus de Dades Forts**

Tot té un tipus: **strings**, **números**, **dates**, **booleans**, etc. Això evita errors comuns.

---

### **Comandes Bàsiques**

#### **1. `ls` (Llistar)**

Mostra fitxers com una taula. Filtra amb `where`:

`ls | where nom =~ "*.txt"  # Mostra només fitxers .txt`

#### **2. `select` (Seleccionar Columnes)**

`ls | select nom mida  # Mostra només les columnes "nom" i "mida"`

#### **3. `get` (Accedir a Valors)**

`git --version | get stdout  # Captura la sortida de "git --version"`

#### **4. `sort-by` (Ordenar)**

`ps | sort-by cpu  # Ordena processos per ús de CPU`

#### **5. `open` i `save` (Treballar amb Fitxers)**

`open dades.csv | save dades.json  # Converteix CSV a JSON`

---

### **Exemple Pràctic**

Imagina que vols **trobar els 5 fitxers més grans al directori actual**:

```nushell
ls  
| where type == "file"  
| sort-by mida --reverse  
| first 5  
| select name size  
```
_Explicació_:

1. Llista fitxers.
2. Filtra només fitxers (no carpetes).
3. Ordena de major a menor mida.
4. Agafa els 5 primers.
5. Mostra nom i mida.

---

### **Comparació amb Bash**

| **Acció**       | **Bash**               | **Nushell**                 |
| --------------- | ---------------------- | --------------------------- |
| Llistar fitxers | `ls -l` (text)         | `ls` (taula interactiva)    |
| Filtrar         | `grep "pattern"`       | `where nom =~ "pattern"`    |
| Processar dades | `awk`, `cut` complexos | `select`, `sort-by` simples |
