# Ordre `passwd`: Gestió de contrasenyes d'usuari

## Descripció

L'ordre `passwd` permet gestionar les contrasenyes dels usuaris en un sistema GNU/Linux. Amb aquesta eina, els usuaris poden canviar les seves contrasenyes, i els administradors del sistema poden gestionar les contrasenyes de tots els usuaris.

## Sintaxi bàsica

```
passwd [opcions] [usuari]
```

## Ús comú

- `passwd`: Canvia la contrasenya de l'usuari actual.
- `passwd usuari`: Canvia la contrasenya de l'usuari especificat (requereix permisos d'administrador).

## Opcions principals

- `-l`: Bloqueja el compte d'un usuari.
- `-u`: Desbloqueja el compte d'un usuari.
- `-d`: Elimina la contrasenya d'un usuari (no recomanat).
- `-e`: Fa que la contrasenya caduqui immediatament, obligant a l'usuari a canviar-la en el pròxim inici de sessió.
- `-S`: Mostra l'estat de la contrasenya d'un usuari.

## Exemples

### Canviar la pròpia contrasenya

```
$ passwd
Contrasenya actual:
Nova contrasenya:
Torna a escriure la nova contrasenya:
passwd: s'ha actualitzat correctament la contrasenya
```

### Canviar la contrasenya d'un altre usuari (com a administrador)

```
$ sudo passwd maria
Nova contrasenya:
Torna a escriure la nova contrasenya:
passwd: s'ha actualitzat correctament la contrasenya
```

### Fer que una contrasenya caduqui

```
$ sudo passwd -e joan
passwd: s'ha actualitzat correctament la contrasenya
```

### Consultar l'estat d'una contrasenya

```
$ sudo passwd -S joan
joan P 2023-11-10 0 99999 7 -1
```

Aquest resultat mostra: nom d'usuari, estat (P=contrasenya vàlida), data del darrer canvi, dies mínims abans de poder canviar-la, dies màxims de validesa, dies d'avís abans de caducitat i dies després de caducitat.

## Fitxers relacionats

- `/etc/passwd`: Conté informació bàsica dels comptes d'usuari.
- `/etc/shadow`: Conté les contrasenyes encriptades i informació sobre la seva caducitat.

## Consells de seguretat

- Utilitzeu contrasenyes fortes que combinin lletres majúscules i minúscules, números i símbols.
- Eviteu utilitzar informació personal o paraules del diccionari.
- Canvieu les contrasenyes periòdicament.
- No compartiu mai les vostres contrasenyes amb altres persones.

## Notes

- Els usuaris normals només poden canviar la seva pròpia contrasenya.
- L'usuari root (administrador) pot canviar la contrasenya de qualsevol usuari.
- L'eina `passwd` verificarà la complexitat de la contrasenya segons les polítiques del sistema.
