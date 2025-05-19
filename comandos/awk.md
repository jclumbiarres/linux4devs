
`awk` és una potent eina de processament de text i llenguatge de programació interpretat disponible a sistemes Unix i Linux. S'utilitza principalment per escanejar fitxers línia per línia, dividir cada línia en camps i realitzar accions sobre aquests camps o línies que compleixen certs patrons.

## Sintaxi Bàsica

La sintaxi més comuna d'`awk` és:

```bash
awk 'patró { acció }' nom_fitxer
```

- **`patró`**: Una condició que determina si l'acció s'ha d'executar en la línia actual. Si s'omet, l'acció s'aplica a totes les línies.
- **`{ acció }`**: El codi que s'executa quan una línia compleix el patró. Normalment implica imprimir o manipular camps. Si s'omet, l'acció per defecte és imprimir tota la línia (`print $0`).
- **`nom_fitxer`**: El fitxer d'entrada que `awk` processarà. Si s'omet, `awk` llegeix de l'entrada estàndard (stdin).

## Camps i Variables Especials

`awk` divideix cada línia d'entrada en camps, utilitzant espais o tabuladors com a separadors per defecte. Aquests camps es poden referenciar amb `$1`, `$2`, `$3`, etc.

- `$0`: Representa tota la línia actual.
- `$1`: Representa el primer camp.
- `$2`: Representa el segon camp, i així successivament.
- `NR` (Number of Record): El número de la línia actual.
- `NF` (Number of Fields): El nombre de camps en la línia actual.
- `FS` (Field Separator): El caràcter o expressió regular utilitzada per separar els camps (per defecte, espai o tabulador). Es pot canviar amb l'opció `-F`.

## Exemples per a Novells

Suposem que tenim un fitxer anomenat `dades.txt` amb el següent contingut:

```
nom cognom edat ciutat
anna martinez 25 barcelona
pere soler 30 girona
laia vidal 22 tarragona
jordi puig 35 lleida
```

**1. Imprimir totes les línies del fitxer:**

```bash
awk '{ print $0 }' dades.txt
```

O simplement (acció per defecte):

```bash
awk '1' dades.txt
```

**2. Imprimir només la primera columna (noms):**

```bash
awk '{ print $1 }' dades.txt
```

**Sortida:**

```
nom
anna
pere
laia
jordi
```

**3. Imprimir el nom i la ciutat (columnes 1 i 4):**

```bash
awk '{ print $1, $4 }' dades.txt
```

**Sortida:**

```
nom ciutat
anna barcelona
pere girona
laia tarragona
jordi lleida
```

**4. Imprimir les línies on l'edat (columna 3) sigui major de 25:**

```bash
# Ometem la capçalera amb NR > 1
awk 'NR > 1 && $3 > 25 { print $0 }' dades.txt
```

**Sortida:**

```
pere soler 30 girona
jordi puig 35 lleida
```

**5. Imprimir el número de línia i la línia completa:**

```bash
awk '{ print NR, $0 }' dades.txt
```

**Sortida:**

```
1 nom cognom edat ciutat
2 anna martinez 25 barcelona
3 pere soler 30 girona
4 laia vidal 22 tarragona
5 jordi puig 35 lleida
```

**6. Utilitzar un separador de camps diferent:**

Suposem un fitxer `usuaris.csv`:

```
usuari;id;grup
root;0;root
daemon;1;daemon
bin;2;bin
```

Per imprimir l'usuari i l'ID, utilitzant `;` com a separador:

```bash
awk -F';' '{ print "Usuari:", $1, "ID:", $2 }' usuaris.csv
```

**Sortida:**

```
Usuari: usuari ID: id
Usuari: root ID: 0
Usuari: daemon ID: 1
Usuari: bin ID: 2
```

`awk` és molt més potent i ofereix moltes més funcionalitats (variables, funcions, control de flux), però aquests exemples bàsics són un bon punt de partida per començar a utilitzar-lo per a tasques senzilles de processament de text.
