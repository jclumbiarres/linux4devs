### **Moviment del Cursor**

- **Ctrl + A** (`Principi de la línia`):  
    Mou el cursor al **inici** de la línia actual.  
    _Exemple_: Si tens `$ cd Documents/Projectes`, prem Ctrl+A per anar a la `$`.

- **Ctrl + E** (`Final de la línia`):  
    Mou el cursor al **final** de la línia actual.  
    _Exemple_: Després d’escriure `$ nano fitxer`, prem Ctrl+E per anar al final.

- **Alt + B** (`Enrera per paraules`):  
    Mou el cursor **enrera** una paraula (paraula = text sense espais).  
    _Exemple_: A `$ cp fitxer.txt /var/www/`, prem Alt+B per saltar entre carpetes.

- **Alt + F** (`Endavant per paraules`):  
    Mou el cursor **endavant** una paraula. Ideal per editar ràpidament.

---

### **Esborrar Text**

- **Ctrl + U** (`Esborrar fins al principi`):  
    **Esborra** tot des del cursor fins al **inici** de la línia.  
    _Exemple_: Si tens `$ sudo apt install nmap` i el cursor està a la `n`, esborrarà `nmap` i deixarà `$ sudo apt install` .

- **Ctrl + K** (`Esborrar fins al final`):  
    **Esborra** tot des del cursor fins al **final** de la línia.  
    _Exemple_: A `$ git commit -m "Missatge"`, si el cursor està abans de `"Missatge"`, esborrarà el missatge.

- **Ctrl + W** (`Esborrar paraula anterior`):  
    **Esborra** la paraula **anterior** al cursor.  
    _Exemple_: A `$ mv fitxer.txt /backup/`, si el cursor està després de `backup/`, esborrarà `backup`.

- **Alt + D** (`Esborrar paraula següent`):  
    **Esborra** la paraula **següent** al cursor.  
    _Exemple_: A `$ ls -l Documents/`, si el cursor està després de `ls`, esborrarà `-l`.

---

### **Historial i Comandes**

- **Ctrl + R** (`Cercar en l'historial`):  
    Obre una **cerca interactiva** a l’historial de comandes. Prem Ctrl+R i escriu part d’una comanda antiga per recuperar-la.  
    _Exemple_: Cerca `ssh` per trobar comandes de connexió anteriors.

- **Ctrl + G** (`Sortir de la cerca`):  
    **Tanca** la cerca d’historial sense seleccionar res.

- **Ctrl + P** (o **Fletxa Amunt**):  
    Mostra la comanda **anterior** en l’historial.

- **Ctrl + N** (o **Fletxa Avall**):  
    Mostra la comanda **següent** en l’historial.

---

### **Gestió de Processos**

- **Ctrl + C** (`Interrompre`):  
    **Atura** un procés en execució. Molt útil per cancel·lar comandes que s’han "penjat".  
    _Exemple_: Atura un bucle infinit o un servidor local.

- **Ctrl + Z** (`Pausar`):  
    **Pausa** un procés i el mou a segon pla. Pots reprendre'l amb `fg` (foreground) o `bg` (background).  
    _Exemple_: Pausar un editor nano i tornar al terminal.

- **Ctrl + D** (`Finalitzar entrada`):  
    **Tanca** la sessió actual o indica "fi d'entrada". Equivalent a escriure `exit`.  
    _Exemple_: En un terminal, Ctrl+D et desconnectarà.

---

### **Altres Shortcuts Útils**

- **Ctrl + L** (`Netejar pantalla`):  
    **Esborra** la pantalla del terminal, deixant-la com nova. Equivalent a `clear`.

- **Ctrl + T** (`Transposar caràcters`):  
    **Intercanvia** els dos caràcters anteriors al cursor.  
    _Exemple_: Si has escrit `sl` en lloc de `ls`, prem Ctrl+T per canviar-ho a `ls`.

- **Ctrl + Y** (`Enganxar text esborrat`):  
    **Recupera** l’últim text esborrat amb Ctrl+U, Ctrl+K, etc.  
    _Exemple_: Si vas esborrar accidentalment una ruta, prem Ctrl+Y per recuperar-la.

- **Tab** (`Autocompletar`):  
    **Completa** noms de fitxers, carpetes o comandes automàticament. Prem Tab dues vegades per veure opcions si n’hi ha múltiples.