# Tipus de cables per a xarxes: UTP, fibra òptica i altres

En una xarxa de comunicacions, el tipus de cable utilitzat és fonamental per garantir la qualitat, velocitat i fiabilitat de la transmissió de dades. A continuació es detallen els principals tipus de cables utilitzats en xarxes, amb una explicació exhaustiva de les seves característiques, usos i exemples de configuració.

## 1. Cables UTP (Unshielded Twisted Pair)

Els cables UTP són els més comuns en xarxes Ethernet. Estan formats per parells de fils de coure trenats sense blindatge.

### Categories de cables UTP

- **Cat 3:** Utilitzat antigament per xarxes 10BASE-T (10 Mbps). Actualment en desús.
- **Cat 5:** Suporta fins a 100 Mbps (Fast Ethernet). Ja no es recomana per noves instal·lacions.
- **Cat 5e:** Millora del Cat 5, suporta fins a 1 Gbps (Gigabit Ethernet). Molt utilitzat.
- **Cat 6:** Suporta fins a 10 Gbps a distàncies curtes (fins a 55 m). Millor blindatge contra interferències.
- **Cat 6a:** Suporta 10 Gbps fins a 100 m. Ideal per entorns amb alta demanda de velocitat.
- **Cat 7:** Blindatge addicional, fins a 10 Gbps, millor resistència a interferències electromagnètiques.
- **Cat 8:** Fins a 40 Gbps, utilitzat en centres de dades.

### Característiques

- **Connector:** RJ-45.
- **Distància màxima recomanada:** 100 metres per Cat 5e/6/6a.
- **Aplicacions:** Xarxes d’oficina, domèstiques, centres de dades.

### Avantatges i inconvenients

- **Avantatges:** Econòmic, fàcil d’instal·lar, compatible amb la majoria d’equipaments.
- **Inconvenients:** Sensible a interferències electromagnètiques, limitació de distància i velocitat segons la categoria.

## 2. Fibra òptica

La fibra òptica utilitza fils de vidre o plàstic per transmetre dades mitjançant polsos de llum. Permet velocitats molt altes i grans distàncies.

### Tipus de fibra òptica

- **Monomode (SMF):** Un sol feix de llum, distàncies molt llargues (fins a 40 km o més), utilitzat en xarxes WAN i backbone.
- **Multimode (MMF):** Diversos feixos de llum, distàncies més curtes (fins a 2 km), utilitzat en xarxes LAN i centres de dades.

### Connectors habituals

- **LC:** Petit, molt utilitzat en equips moderns.
- **SC:** Més gran, tradicional.
- **ST:** Rodó, antigament molt comú.

### Avantatges i inconvenients

- **Avantatges:** Immunitat a interferències electromagnètiques, gran amplada de banda, distàncies llargues.
- **Inconvenients:** Cost més elevat, instal·lació més complexa, fragilitat del cable.

## 3. Altres tipus de cables

### Coaxial

- **Característiques:** Utilitzat antigament en xarxes 10BASE2 i 10BASE5. Format per un conductor central, aïllament, blindatge i coberta externa.
- **Aplicacions:** Televisió per cable, xarxes antigues.

### Cables blindats (STP/FTP)

- **STP (Shielded Twisted Pair):** Similar a UTP però amb blindatge per reduir interferències.
- **FTP (Foiled Twisted Pair):** Cada parell de fils té una capa de foil per a més protecció.

## 4. Consideracions per a la configuració

- **Distància:** Escull el cable segons la distància entre dispositius.
- **Velocitat:** La categoria del cable determina la velocitat màxima suportada.
- **Entorn:** En entorns amb molta interferència, utilitza cables blindats o fibra òptica.
- **Compatibilitat:** Assegura’t que els connectors i equips siguin compatibles amb el tipus de cable.

## 5. Exemples d’ús

- **Oficina petita:** Cat 5e o Cat 6 UTP per a ordinadors i switches.
- **Centre de dades:** Cat 6a/7/8 per a racks, fibra òptica per a backbone.
- **Connexió entre edificis:** Fibra òptica monomode per a grans distàncies.

## 6. Resum

La selecció del cable adequat depèn de les necessitats de la xarxa: distància, velocitat, entorn i pressupost. Els cables UTP són ideals per a la majoria de xarxes LAN, mentre que la fibra òptica és imprescindible per a connexions d’alta velocitat i llargues distàncies.

---

**Referències:**
- [Wikipedia: Twisted pair](https://ca.wikipedia.org/wiki/Parell_trenat)
- [Wikipedia: Fibra òptica](https://ca.wikipedia.org/wiki/Fibra_%C3%B2ptica)
- [Ethernet standards](https://en.wikipedia.org/wiki/Ethernet_physical_layer)
