El comandament `ln` s'utilitza per **crear enllaços** entre fitxers. Hi ha dos tipus: _hard links_ (enllaços durs) i _soft links_ o _symbolic links_ (enllaços simbòlics).

**Sintaxi bàsica**:

```bash
ln [OPCIONS] ORIGEN DESTÍ
```

**Opcions clau**:
- **`-s`**: Crea un **enllaç simbòlic** (sense aquesta opció, crea un _hard link_).
- **`-f`**: Força la creació (sobreescriu si el destí ja existeix).
- **`-i`**: Pregunta abans de sobreescriure.

## Hard link vs Soft Link

#### **Hard Link (Enllaç dur)**

- **Què és?**: Una **còpia directa** del fitxer original. Tots els _hard links_ comparteixen el mateix **inode** (identificador únic del fitxer al sistema).

- **Característiques**:
    - Funcionen **només dins del mateix sistema de fitxers** (no poden enllaçar entre particions o dispositius).
    - Si s'esborra l'original, **els _hard links_ segueixen funcionant** (el contingut roman fins que tots els _hard links_ s'esborrin).
    - No poden enllaçar **directoris**, només fitxers.
    - Els canvis en un _hard link_ es reflecteixen a tots els altres.

```bash
ls -li  
# Mostrarà el mateix inode per a tots els hard links
```

#### **Soft Link (Enllaç simbòlic)**

- **Què és?**: Un **accés directe** que apunta al **nom del fitxer original** (com una porta que redirigeix).
    
- **Característiques**:
    
    - Poden enllaçar **entre sistemes de fitxers** (ex: d'un USB a una carpeta local).
    - Si s'esborra l'original, **l'enllaç es torna "orphe"** (no funciona).
    - Poden enllaçar **directoris**.
    - Mostren la ruta absoluta o relativa de l'original.

```bash
ls -l  
# Mostrarà alguna cosa com: "softlink_fitxer -> fitxer.txt"
```

### **Resum de diferències**

|Característica|Hard Link|Soft Link|
|---|---|---|
|**Inode**|Mateix que l'original|Propi (apunta al nom)|
|**Sistemes de fitxers**|Només el mateix|Qualsevol|
|**Esborrar original**|No afecta l'enllaç|Enllaç inútil|
|**Directoris**|No permès|Permès|
|**Grandària**|No ocupa espai addicional|Ocupa espai (només la ruta)|