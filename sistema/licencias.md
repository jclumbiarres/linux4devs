# Llicències Lliures

## Introducció

El programari lliure i de codi obert ha revolucionat el desenvolupament de software, però hi ha diferències conceptuals i pràctiques entre "Free Software" i "Open Source" que cal conèixer, així com les diverses llicències que defineixen com es pot utilitzar, modificar i distribuir el codi.

## Free Software vs Open Source

### Free Software (Programari Lliure)

El moviment del programari lliure, impulsat per Richard Stallman i la Free Software Foundation (FSF) el 1985, es basa en quatre llibertats fonamentals:

1. **Llibertat 0**: La llibertat d'utilitzar el programa per a qualsevol propòsit.
2. **Llibertat 1**: La llibertat d'estudiar com funciona el programa i adaptar-lo a les teves necessitats.
3. **Llibertat 2**: La llibertat de redistribuir còpies.
4. **Llibertat 3**: La llibertat de millorar el programa i fer públiques les millores.

Aquest moviment posa èmfasi en la llibertat com a valor ètic i social, no només en la qüestió tècnica o econòmica.

### Open Source (Codi Obert)

La iniciativa Open Source, fundada per Eric Raymond i altres el 1998, comparteix moltes característiques amb el programari lliure, però amb un enfocament diferent. Es centra més en els avantatges pràctics del desenvolupament col·laboratiu i l'accés al codi font, que en les qüestions ètiques sobre la llibertat dels usuaris.

### Principals diferències

- **Filosofia**: El programari lliure prioritza la llibertat dels usuaris com a valor social, mentre que l'open source emfatitza els beneficis pràctics i tècnics.
- **Compatibilitat amb programari propietari**: L'open source pot ser més permissiu en determinades circumstàncies.
- **Terminologia**: "Free" en anglès pot portar a confusió (lliure vs gratuït), mentre que "Open Source" és més clar en aquest aspecte.

## Principals Llicències Lliures

### Família GPL (GNU General Public License)

#### GPL versió 2 (GPLv2)

- **Publicada**: 1991
- **Característiques principals**:
  - És una llicència copyleft: obliga a què qualsevol obra derivada també sigui distribuïda sota la mateixa llicència.
  - Garanteix les quatre llibertats del programari lliure.
  - Qualsevol modificació distribuïda ha d'incloure el codi font.
- **Usos destacats**: Linux kernel (fins la versió 2.6), MySQL, GIMP

#### GPL versió 3 (GPLv3)

- **Publicada**: 2007
- **Característiques principals**:
  - Millora la GPLv2 abordant qüestions de patents de programari.
  - Prohibeix la "tivoització" (restriccions de hardware sobre el programari modificat).
  - És compatible amb més llicències que GPLv2.
  - Millor protecció contra les patents de programari.
- **Usos destacats**: GNU Bash, GCC, GNOME, Inkscape

#### AGPL (Affero General Public License) versió 2/3

- **Característiques principals**:
  - Similar a la GPL però afegeix l'obligació de proporcionar el codi font també quan el programari s'utilitza a través d'una xarxa.
  - AGPLv3 actualitza AGPLv2 similar a com GPLv3 actualitza GPLv2.
  - Dissenyada especialment per a serveis web i aplicacions al núvol.
- **Usos destacats**: MongoDB (abans del canvi de llicència), NextCloud, SugarCRM

#### LGPL (GNU Lesser General Public License)

- **Característiques principals**:
  - Versió més permissiva que la GPL.
  - Permet enllaçar el codi amb programari propietari.
  - Ideal per a biblioteques que volen ser àmpliament utilitzades.
- **Usos destacats**: LibreOffice (parcialment), GTK, Qt (en versions anteriors)

### Llicències Permissives

#### Llicència MIT

- **Característiques principals**:
  - Extremadament permissiva.
  - Permet l'ús, modificació i distribució sense restriccions significatives.
  - Només requereix incloure l'avís de copyright i la llicència.
  - Compatible amb llicències copyleft com la GPL.
- **Usos destacats**: jQuery, Node.js, Ruby on Rails, Angular.js

#### Llicència BSD (Berkeley Software Distribution)

- **2-clàusules BSD (BSD simplificada)**:
  - Només requereix mantenir l'avís de copyright i la renúncia de responsabilitat.
- **3-clàusules BSD**:
  - Afegeix la prohibició d'usar el nom dels autors per promocionar productes derivats.
- **4-clàusules BSD (original)**:
  - Actualment en desús, incloïa una clàusula publicitària problemàtica.
- **Usos destacats**: FreeBSD, NetBSD, aspectes del macOS i iOS

#### Llicència Apache 2.0

- **Característiques principals**:
  - Permet l'ús, modificació i distribució.
  - Exigeix conservar l'avís de copyright i les renúncies.
  - Proporciona una concessió expressa de drets de patent.
  - Requereix indicar canvis significatius.
- **Usos destacats**: Android, Hadoop, OpenOffice, Swift

### Altres Llicències Importants

#### Mozilla Public License (MPL)

- **Característiques principals**:
  - Copyleft moderat que s'aplica per fitxer.
  - Els fitxers sota MPL han de mantenir-se sota MPL si es modifiquen.
  - Permet combinar codi MPL amb codi propietari.
- **Usos destacats**: Firefox, Thunderbird

#### ISC License

- **Característiques principals**:
  - Funcionalment equivalent a la BSD de 2 clàusules.
  - Molt simple i permissiva.
  - Popular en els projectes OpenBSD.
- **Usos destacats**: OpenBSD, Node.js (alguns components)

#### Eclipse Public License (EPL)

- **Característiques principals**:
  - Copyleft feble amb protecció explícita de patents.
  - Ideal per a entorns empresarials.
- **Usos destacats**: Eclipse IDE, Jenkins

#### Creative Commons (CC)

- Tot i no ser específiques per a programari, aquestes llicències s'usen freqüentment per a documentació, art, imatges i altres continguts relacionats amb projectes de programari:
  - **CC0**: Dedicació al domini públic
  - **CC-BY**: Permet qualsevol ús citant l'autor
  - **CC-BY-SA**: Similar a la GPL, obliga a compartir amb la mateixa llicència

## Selecció de Llicències segons l'Objectiu

### Per a Màxima Llibertat de l'Usuari i Copyleft Fort

- GPLv3 o AGPLv3 (si és un servei web)

### Per a Compatibilitat amb Programari Propietari

- MIT, BSD, Apache 2.0

### Per a Protecció contra Patents

- GPLv3, Apache 2.0

### Per a Biblioteques que s'Utilitzaran Àmpliament

- LGPL, MIT, BSD

## Conclusions

La selecció d'una llicència té implicacions profundes en com es desenvoluparà, utilitzarà i distribuirà un projecte de programari. Mentre que les llicències permissives (MIT, BSD, Apache) ofereixen més flexibilitat per a la integració amb altres projectes, inclosos els propietaris, les llicències copyleft (GPL, AGPL) garanteixen que el programari i les seves derivacions romanguin lliures.

El debat entre "Free Software" i "Open Source" continua sent rellevant, no només com una qüestió de terminologia, sinó també com una reflexió sobre els valors i objectius que impulsen el desenvolupament de programari i com aquests afecten la societat en general.
