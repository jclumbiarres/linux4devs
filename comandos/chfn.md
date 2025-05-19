# Comanda `chfn` (Change Finger Information)

## Descripció

La comanda `chfn` (Change Finger Information) permet modificar la informació de l'usuari que es mostra quan s'utilitza la comanda `finger`. Aquesta informació inclou el nom real, número de telèfon, oficina i altres dades personals de l'usuari.

## Sintaxi

```
chfn [opcions] [usuari]
```

## Opcions principals

- `-f, --full-name NOM`: Canvia el nom real de l'usuari
- `-r, --room HABITACIÓ`: Canvia el número d'habitació o oficina
- `-w, --work-phone TELÈFON`: Canvia el número de telèfon de la feina
- `-h, --home-phone TELÈFON`: Canvia el número de telèfon de casa
- `-o, --other INFO`: Canvia informació addicional de l'usuari
- `-u, --help`: Mostra l'ajuda de la comanda

## Exemples

### Canviar la informació personal de l'usuari actual

```bash
chfn
```

Quan s'executa sense arguments, la comanda demana interactivament la nova informació personal de l'usuari actual.

### Canviar el nom complet de l'usuari

```bash
chfn -f "Joan Garcia Puig"
```

### Canviar el número de telèfon de la feina

```bash
chfn -w "93 123 45 67"
```

### Canviar múltiples camps alhora

```bash
chfn -f "Joan Garcia" -r "Despatx 42" -w "93 123 45 67"
```

### Canviar la informació d'un altre usuari (requereix privilegis de superusuari)

```bash
sudo chfn anna
```

## Notes

- Cal tenir drets d'administrador (sudo) per modificar la informació d'altres usuaris.
- La informació es guarda al fitxer `/etc/passwd`.
- No tots els camps són obligatoris i es poden deixar en blanc prement Enter quan es demanen interactivament.
- Aquesta comanda no està disponible en tots els sistemes Unix/Linux.

## Compatibilitat

La comanda `chfn` forma part del paquet `util-linux` en la majoria de distribucions GNU/Linux.
