# Sistema de Fitxers ext4

**ext4** (Fourth Extended Filesystem) és un sistema de fitxers amb _journaling_ àmpliament utilitzat per a sistemes operatius Linux. És el successor d'ext3 i va ser dissenyat per superar algunes de les seves limitacions i millorar el rendiment i la fiabilitat.

## Origen

- Desenvolupat com una evolució d'ext3.
- Va ser inclòs per primera vegada de forma estable al kernel Linux 2.6.28 (desembre de 2008).

## Característiques Principals

- **Suport per a volums i fitxers grans:**
  - Pot gestionar volums de fins a 1 exbibyte (EiB).
  - Pot gestionar fitxers individuals de fins a 16 tebibytes (TiB).
- **Extents:**
  - Substitueix el tradicional mapeig de blocs d'ext2/ext3 per _extents_. Un _extent_ és un rang contigu de blocs físics.
  - Millora el rendiment, especialment amb fitxers grans, i redueix la fragmentació.
- **Compatibilitat:**
  - Ofereix retrocompatibilitat amb ext3 i ext2. És possible muntar un sistema de fitxers ext3 com a ext4 (i viceversa en alguns casos, si no s'utilitzen característiques noves com els _extents_).
- **Journaling:**
  - Com ext3, utilitza _journaling_ per garantir la integritat del sistema de fitxers en cas de fallades (p. ex., talls de llum).
  - El _journaling_ registra les operacions de metadades abans d'executar-les, permetent una recuperació ràpida.
  - Modes de _journaling_: `journal` (dades i metadades), `ordered` (només metadades, per defecte), `writeback` (només metadades, menys segur però més ràpid).
- **Assignació Retardada (Delayed Allocation):**
  - Retarda l'assignació de blocs fins que les dades s'escriuen al disc.
  - Permet al sistema de fitxers prendre millors decisions sobre l'assignació, millorant el rendiment i reduint la fragmentació.
- **Assignació Multiblock (Multiblock Allocator):**
  - Assigna múltiples blocs en una sola operació, reduint la sobrecàrrega i millorant el rendiment d'escriptura.
- **Sumes de Verificació (Checksums) per al Journal:**
  - Millora la fiabilitat detectant corrupcions al _journal_.
  - Opcionalment, es poden habilitar checksums per a les metadades dels grups de blocs.
- **Marques de Temps en Nanosegons:**
  - Ofereix una major precisió en les marques de temps dels fitxers (creació, modificació, accés).
- **Preassignació Persistent (Persistent Preallocation):**
  - Permet a les aplicacions reservar espai al disc per a un fitxer abans d'escriure-hi les dades. Útil per a bases de dades o màquines virtuals.

## Avantatges

- **Maduresa i Estabilitat:** Ha estat provat extensament i és considerat molt estable.
- **Bon Rendiment:** Ofereix millores significatives respecte a ext3.
- **Àmplia Adopció:** És el sistema de fitxers per defecte en moltes distribucions Linux.
- **Eines de Gestió:** Disposa d'un conjunt complet i madur d'eines per a la seva creació, verificació i reparació (`mkfs.ext4`, `fsck.ext4`, `tune2fs`, etc.).

## Desavantatges

- **Manca de Funcionalitats Avançades:** No inclou característiques presents en sistemes de fitxers més moderns com Btrfs o ZFS (p. ex., instantànies (snapshots) integrades, compressió transparent a nivell de sistema de fitxers, gestió de volums integrada, checksums de dades).
- **Verificació Lenta:** `fsck` pot ser lent en volums molt grans.

## Ús Típic

ext4 és una opció sòlida i fiable per a la majoria d'usos en sistemes Linux, des d'escriptoris fins a servidors, especialment quan la prioritat és l'estabilitat i la compatibilitat per sobre de les funcionalitats més avançades.
