# chsh - Canviar la Shell de l'Usuari

## Sinopsi

```bash
chsh [opcions] [nom_usuari]
```

## Descripció

El comandament `chsh` (change shell) permet canviar la shell d'inici de sessió d'un usuari. La shell és el programa d'intèrpret de comandaments que s'inicia automàticament quan un usuari inicia sessió al sistema. Els canvis realitzats amb `chsh` es registren al fitxer `/etc/passwd`.

## Opcions principals

- `-s, --shell SHELL`: Especifica la nova shell d'inici de sessió.
- `-l, --list-shells`: Mostra la llista de shells disponibles al sistema.
- `-h, --help`: Mostra l'ajuda del comandament.
- `-v, --version`: Mostra la versió del programa.

## Exemples

### Canviar la teva pròpia shell

```bash
chsh -s /bin/bash
```

Aquest comandament canvia la teva shell actual a bash.

### Veure quines shells estan disponibles

```bash
chsh -l
```

Mostra una llista de totes les shells disponibles al sistema definides a `/etc/shells`.

### Canviar la shell d'un altre usuari (requereix permisos d'administrador)

```bash
sudo chsh -s /bin/zsh usuari
```

Canvia la shell de l'usuari especificat a zsh.

## Notes importants

- Per canviar la teva pròpia shell, no necessites privilegis especials.
- Per canviar la shell d'un altre usuari, necessites permisos d'administrador (root).
- La nova shell ha d'estar llistada al fitxer `/etc/shells` o el comandament fallarà.
- Els canvis tindran efecte a partir del proper inici de sessió de l'usuari.
- La shell per defecte en molts sistemes GNU/Linux és `/bin/bash`.
