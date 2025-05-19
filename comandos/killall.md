# El Comando `killall` a GNU/Linux

## Descripció General

El comando `killall` s'utilitza per matar processos pel seu nom en lloc del seu ID de procés (PID). Això és especialment útil quan vols finalitzar tots els processos amb el mateix nom simultàniament.

## Sintaxi Bàsica

```bash
killall [opcions] nom_del_procés
```

## Opcions Comunes

- `-e, --exact`: Requereix una coincidència exacta pel nom del procés.
- `-I, --ignore-case`: Ignora les majúscules i minúscules quan busca processos.
- `-i, --interactive`: Demana confirmació abans de matar cada procés.
- `-s, --signal señal`: Envia una senyal específica en lloc de SIGTERM.
- `-u, --user usuari`: Mata només els processos que pertanyen a l'usuari especificat.
- `-v, --verbose`: Informa sobre si la senyal s'ha enviat correctament.
- `-w, --wait`: Espera fins que els processos hagin mort.
- `-9`: Envia un SIGKILL, que és una senyal que no es pot ignorar i força la terminació del procés.

## Exemples d'Ús

### Finalitzar Tots els Processos d'un Programa

```bash
killall firefox
```

Aquest comando finalitzarà tots els processos anomenats "firefox".

### Finalitzar Processos amb Confirmació

```bash
killall -i chrome
```

Demanarà confirmació abans de matar cada procés de Chrome.

### Enviar una Senyal Específica

```bash
killall -s SIGTERM vlc
```

Envia la senyal SIGTERM a tots els processos de VLC.

### Finalitzar Processos d'un Usuari Específic

```bash
killall -u jordi nginx
```

Finalitza només els processos nginx que pertanyen a l'usuari "jordi".

### Forçar la Finalització de Processos

```bash
killall -9 process_bloquejat
```

Envia un SIGKILL per forçar la terminació dels processos anomenats "process_bloquejat".

## Notes Importants

- Cal tenir en compte que `killall` pot ser perillós si no es fa servir amb cura, ja que pots finalitzar processos crítics del sistema.
- En alguns sistemes (com Solaris), `killall` pot matar TOTS els processos, així que s'ha d'utilitzar amb precaució.
- És recomanable utilitzar l'opció `-i` (interactiva) quan no estàs segur de quins processos s'acabaran.
- Si tens permisos d'administrador (root), pots matar processos d'altres usuaris.

## Consell per a Principiants

Si ets nou en l'ús de `killall`, és recomanable primer utilitzar el comando `ps aux | grep nom_del_procés` per identificar els processos que vols finalitzar abans d'utilitzar `killall`.
