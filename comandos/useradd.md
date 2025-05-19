# useradd

## Introducció

El comando `useradd` es una eina que permet crear nous usuaris al sistema GNU/Linux. Aquesta eina és essencial per a l'administració de sistemes i la gestió de permisos d'usuaris.

## Sintaxi

```
useradd [opcions] nom_usuari
```

## Descripció

`useradd` crea un nou compte d'usuari al sistema utilitzant els valors especificats a la línia de comandes i els valors predeterminats del sistema. Segons la configuració, també crea el directori personal de l'usuari, copia els fitxers inicials i configura la contrasenya inicial.

## Opcions més comunes

- `-c, --comment COMENTARI`: Informació addicional sobre l'usuari (normalment el nom complet).
- `-d, --home DIRECTORI`: Directori personal del nou usuari. Si no s'especifica, s'utilitza el valor predeterminat.
- `-g, --gid GRUP`: Nom o ID del grup principal de l'usuari.
- `-G, --groups GRUPS`: Llista de grups complementaris als quals l'usuari també pertany.
- `-m, --create-home`: Crea el directori personal de l'usuari si no existeix.
- `-s, --shell SHELL`: Nom de la shell d'inici de sessió de l'usuari.
- `-u, --uid UID`: Valor numèric de l'ID d'usuari.
- `-e, --expiredate DATA`: Data en què el compte caducarà (format YYYY-MM-DD).
- `-p, --password CONTRASENYA`: Contrasenya encriptada per l'usuari (no és recomanable utilitzar aquesta opció).
- `-r, --system`: Crea un compte de sistema (amb UID baix).

## Exemples

1. Crear un usuari bàsic:

   ```bash
   sudo useradd joan
   ```

2. Crear un usuari amb informació addicional i directori personal:

   ```bash
   sudo useradd -m -c "Joan Garcia" -s /bin/bash joan
   ```

3. Crear un usuari i afegir-lo a grups addicionals:

   ```bash
   sudo useradd -m -G sudo,docker,developers joan
   ```

4. Crear un usuari de sistema:
   ```bash
   sudo useradd -r servei_web
   ```

## Notes importants

- Després de crear un usuari amb `useradd`, normalment cal establir una contrasenya utilitzant el comando `passwd`:

  ```bash
  sudo passwd joan
  ```

- La configuració predeterminada per als nous usuaris es troba a `/etc/default/useradd` i `/etc/login.defs`.

- En alguns sistemes, es recomana utilitzar `adduser` en lloc de `useradd`, ja que `adduser` és més interactiu i fàcil d'usar.

- Els fitxers per defecte que es copien al nou directori personal de l'usuari es troben a `/etc/skel/`.

- Per modificar un usuari existent, es pot utilitzar el comando `usermod`.
