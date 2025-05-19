# Comanda `groups`

La comanda `groups` a GNU/Linux ens permet veure els grups als quals pertany un usuari del sistema. Els grups són una forma d'organitzar els usuaris i gestionar els seus permisos d'accés als recursos del sistema.

## Sintaxi

```bash
groups [OPCIÓ]... [USUARI]...
```

## Descripció

Quan s'executa sense cap argument, `groups` mostra els grups als quals pertany l'usuari actual. Si s'especifica un nom d'usuari, mostra els grups als quals pertany aquest usuari.

## Opcions

La comanda `groups` té poques opcions:

- `--help`: Mostra l'ajuda de la comanda i finalitza.
- `--version`: Mostra la informació de versió i finalitza.

## Exemples d'ús

### Veure els grups de l'usuari actual

```bash
groups
```

Resultat (exemple):

```
usuari wheel audio video
```

### Veure els grups d'un usuari específic

```bash
groups joan
```

Resultat (exemple):

```
joan : joan administradors docker
```

### Veure els grups de múltiples usuaris

```bash
groups joan maria pere
```

Resultat (exemple):

```
joan : joan administradors docker
maria : maria usuaris
pere : pere usuaris docker
```

## Consells pràctics

- Els grups són essencials per a la gestió de permisos a Linux.
- Un usuari pot pertànyer a múltiples grups.
- El primer grup que apareix a la sortida de la comanda `groups` és el grup primari de l'usuari.
- Per afegir un usuari a un grup, es pot utilitzar la comanda: `sudo usermod -aG grup usuari`
