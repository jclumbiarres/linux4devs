# Comanda pgrep

## Visió General

La comanda `pgrep` s'utilitza en entorns GNU/Linux per buscar processos en execució que coincideixin amb un patró específic. És una eina molt útil per identificar i gestionar processos al sistema.

## Sintaxi Bàsica

```bash
pgrep [opcions] patró
```

## Descripció

La comanda `pgrep` cerca entre la llista de processos actius i retorna els IDs dels processos que compleixen amb el patró especificat. Això permet als usuaris identificar ràpidament processos sense haver de filtrar la sortida de comandes com `ps`.

## Opcions Principals

| Opció          | Descripció                                                           |
| -------------- | -------------------------------------------------------------------- |
| `-a`           | Mostra els noms complets dels processos a més dels seus PIDs         |
| `-d delimiter` | Especifica el delimitador entre els PIDs (per defecte és nova línia) |
| `-f`           | Cerca al nom complet de la comanda, no només al nom del procés       |
| `-g`           | Cerca processos que pertanyen a un grup específic                    |
| `-l`           | Mostra el nom del procés juntament amb el PID                        |
| `-n`           | Selecciona només el procés més recent que coincideix                 |
| `-o`           | Selecciona només el procés més antic que coincideix                  |
| `-u usuari`    | Cerca processos que pertanyen a un usuari específic                  |
| `-x`           | Requereix una coincidència exacta amb el nom del procés              |
| `-P ppid`      | Cerca processos amb un pare específic                                |

## Exemples d'Ús

### Exemple 1: Trobar tots els processos per nom

```bash
pgrep firefox
```

Això retornarà els PIDs de tots els processos amb "firefox" al nom.

### Exemple 2: Mostrar els noms dels processos amb els seus PIDs

```bash
pgrep -l bash
```

Mostrarà els PIDs i noms dels processos "bash" en execució.

### Exemple 3: Buscar processos per usuari

```bash
pgrep -u root
```

Retornarà els PIDs de tots els processos executats per l'usuari "root".

### Exemple 4: Buscar processos amb nom complet

```bash
pgrep -f "python script.py"
```

Cerca processos que continguin "python script.py" al nom complet de la comanda.

## Casos d'Ús Comuns

- Trobar ràpidament el PID d'un procés per nom
- Verificar si un servei concret està en execució
- Identificar processos per un usuari específic
- Obtenir una llista de processos per interactuar amb ells (aturar, reiniciar, etc.)

## Combinació amb altres Comandes

La comanda `pgrep` sovint es combina amb altres comandes per gestionar processos:

```bash
# Aturar tots els processos Firefox
kill $(pgrep firefox)

# Veure informació detallada dels processos de Firefox
ps -fp $(pgrep firefox)
```

## Consells i Trucs

- Utilitza l'opció `-f` quan necessitis cercar al nom complet de la comanda.
- Combina `pgrep` amb `xargs` per executar comandes en els processos trobats.
- Per obtenir més detalls sobre un procés, combina `pgrep` amb la comanda `ps`.

## Comanda Relacionada

La comanda `pkill` funciona de manera similar a `pgrep` però en comptes de mostrar els PIDs, envia senyals als processos coincidents per defecte.
