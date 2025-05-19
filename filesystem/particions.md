# Particions en GNU/Linux

## Què és una Partició?

Una partició és una divisió lògica d'un disc dur físic. Permet tractar un únic disc físic com si fossin múltiples discs independents. Cada partició pot contenir el seu propi sistema de fitxers.

## Per què particionar?

Particionar un disc ofereix diversos avantatges:

1.  **Organització:** Separar el sistema operatiu, les aplicacions i les dades d'usuari (`/home`). Això facilita les còpies de seguretat i les reinstal·lacions del sistema sense afectar les dades personals.
2.  **Sistemes de Fitxers Diferents:** Permet utilitzar diferents sistemes de fitxers (com ext4, XFS, Btrfs, FAT32, NTFS) en diferents particions segons les necessitats.
3.  **Instal·lació de Múltiples Sistemes Operatius:** Cada sistema operatiu pot residir a la seva pròpia partició.
4.  **Seguretat i Aïllament:** Si una partició es corromp, les altres particions generalment no es veuen afectades.
5.  **Rendiment:** Separar la partició d'intercanvi (`swap`) o directoris amb molta E/S pot millorar el rendiment en certs escenaris.

## Tipus de Taules de Particions

Hi ha dos estàndards principals per a les taules de particions:

1.  **MBR (Master Boot Record):**
    - Més antic i tradicional.
    - Limitat a 4 particions primàries, o 3 primàries i 1 estesa (que pot contenir múltiples particions lògiques).
    - Limitat a discs de fins a 2TB.
2.  **GPT (GUID Partition Table):**
    - Més modern i flexible, associat amb UEFI.
    - Suporta fins a 128 particions per defecte (configurable).
    - Suporta discs de mida molt més gran (> 2TB).
    - Inclou redundància (còpia de la taula de particions al final del disc).

## Particions Comunes en Linux

Encara que la disposició pot variar, algunes particions típiques en una instal·lació de Linux són:

- `/` (**Arrel**): Conté el nucli del sistema operatiu i els fitxers essencials del sistema. És obligatòria.
- `/home` (**Inici**): Emmagatzema els directoris personals dels usuaris, incloent documents, configuracions, etc. És molt recomanable separar-la per facilitar actualitzacions i reinstal·lacions.
- `swap` (**Intercanvi**): Espai de disc utilitzat com a memòria virtual quan la RAM física s'esgota. Pot ser una partició dedicada o un fitxer d'intercanvi (`swap file`).
- `/boot` (**Arrencada**): Conté els fitxers necessaris per iniciar el sistema, incloent el gestor d'arrencada (GRUB) i el nucli (kernel). De vegades necessari en configuracions específiques (encriptació, LVM, RAID).
- `/boot/efi` o **EFI System Partition (ESP)**: Necessària en sistemes amb UEFI. Conté els carregadors d'arrencada. Formatada normalment com a FAT32.

## Eines de Particionament

- **`fdisk`**: Eina clàssica de línia de comandes per a taules MBR.
- **`gdisk`**: Eina de línia de comandes similar a `fdisk`, però per a taules GPT.
- **`parted`**: Eina de línia de comandes més avançada que suporta MBR i GPT, i permet redimensionar particions.
- **GParted**: Eina gràfica (GUI) molt popular i potent, basada en `parted`. Permet crear, eliminar, redimensionar, moure, comprovar i copiar particions i sistemes de fitxers.
- **KDE Partition Manager**: Eina gràfica similar a GParted per a l'entorn d'escriptori KDE.

Gestionar particions és una tasca fonamental en l'administració de sistemes Linux, permetent una organització eficient i segura de l'emmagatzematge.
