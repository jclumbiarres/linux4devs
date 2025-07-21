# Què és una Honeypot?

Una **honeypot** és un sistema de seguretat informàtica dissenyat per atraure, detectar, analitzar i contrarestar atacs cibernètics. S’instal·la de manera deliberada en una xarxa per simular vulnerabilitats o serveis atractius per als atacants, amb l’objectiu d’observar el seu comportament i obtenir informació valuosa sobre les seves tècniques, eines i motivacions.

## Funcionament d’una Honeypot

### 1. Simulació de vulnerabilitats
La honeypot es configura per semblar un sistema real vulnerable, com ara un servidor web, una base de dades o un dispositiu IoT. Pot contenir dades fictícies o serveis aparentment reals, però no té cap funció productiva dins de l’organització.

### 2. Captura d’activitat maliciosa
Quan un atacant accedeix a la honeypot, totes les seves accions són registrades: com accedeix, quines eines utilitza, quins fitxers intenta modificar, etc. Aquesta informació permet als administradors entendre millor les amenaces i preparar defenses més efectives.

### 3. Aïllament
La honeypot està aïllada de la resta de la xarxa per evitar que un atacant pugui utilitzar-la com a trampolí per comprometre sistemes reals.

### 4. Anàlisi i resposta
Les dades recopilades s’analitzen per identificar noves vulnerabilitats, tècniques d’atac i signatures de malware. Això ajuda a millorar la seguretat global de la xarxa.

## Tipus de Honeypots

- **Honeypots de producció:** S’utilitzen en entorns reals per protegir xarxes empresarials i detectar intrusions.
- **Honeypots de recerca:** S’utilitzen principalment per estudiar el comportament dels atacants i desenvolupar noves estratègies de defensa.

## Avantatges

- **Detecció primerenca d’amenaces:** Permet identificar atacs abans que afectin sistemes reals.
- **Anàlisi detallada:** Proporciona informació sobre tècniques i eines utilitzades pels atacants.
- **Millora de la seguretat:** Ajuda a reforçar les defenses i a corregir vulnerabilitats.

## Inconvenients

- **Risc de compromís:** Si no està ben aïllada, pot ser utilitzada per atacar altres sistemes.
- **Gestió complexa:** Requereix manteniment i monitorització constant.
- **Falsos positius:** Pot captar activitat legítima que no és maliciosa.

## Casos d’ús

- **Educació i formació:** Per ensenyar tècniques de seguretat i resposta a incidents.
- **Investigació:** Per analitzar malware i comportament d’atacants.
- **Protecció d’infraestructures:** Com a part d’una estratègia de defensa en profunditat.

## Conclusió

Les honeypots són eines poderoses per millorar la seguretat informàtica, permetent detectar, analitzar i contrarestar amenaces de manera proactiva. Tot i els riscos associats, el seu ús adequat pot aportar un gran valor a qualsevol infraestructura tecnològica.
