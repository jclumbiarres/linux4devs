# `kill` - Enviar senyals a processos

## Descripció

El comandament `kill` s'utilitza per enviar senyals a processos en execució. Malgrat el seu nom, que literalment significa "matar", no només serveix per finalitzar processos, sinó que pot enviar diferents tipus de senyals que permeten comunicar-se amb els programes en execució.

## Sintaxi

```bash
kill [opcions] PID...
```

## Arguments

- `PID`: Identificador del procés al qual es vol enviar el senyal.

## Opcions principals

- `-l`: Mostra una llista de tots els senyals disponibles.
- `-s SENYAL` o `-SENYAL`: Especifica el senyal a enviar (per nom o número).
- `-9`: Envia el senyal SIGKILL, que força el tancament immediat del procés.
- `-15`: Envia el senyal SIGTERM (per defecte), que sol·licita el tancament normal del procés.

## Senyals comuns

- `1` (SIGHUP): Demana que el procés es reiniciï.
- `9` (SIGKILL): Força la finalització immediata del procés (no es pot ignorar).
- `15` (SIGTERM): Demana el tancament normal del procés (pot ser tractat pel programa).
- `19` (SIGSTOP): Pausa l'execució del procés (no es pot ignorar).
- `18` (SIGCONT): Reprèn un procés prèviament pausat.

## Exemples

### Finalitzar un procés normalment

```bash
kill 1234
```

Envia el senyal SIGTERM (15) al procés amb PID 1234 per sol·licitar que es tanqui correctament.

### Forçar la finalització d'un procés

```bash
kill -9 1234
```

Força el tancament immediat del procés 1234 sense permetre que faci operacions de neteja.

### Reiniciar un procés

```bash
kill -HUP 1234
```

Envia el senyal SIGHUP al procés 1234, generalment utilitzat per demanar-li que es reiniciï.

### Mostrar tots els senyals disponibles

```bash
kill -l
```

## Consells pràctics

- Per trobar el PID d'un procés, pots utilitzar els comandaments `ps` o `pgrep`.
- El senyal SIGKILL (-9) és molt potent i s'ha d'utilitzar només quan un procés no respon a SIGTERM.
- Alguns processos poden requerir privilegis d'administrador per ser finalitzats.
- Combinat amb `pkill` o `killall` permet matar processos pel seu nom en comptes del PID.

## Observacions

- Els processos poden programar-se per capturar i gestionar la majoria de senyals, excepte SIGKILL i SIGSTOP.
- L'ús incorrecte del senyal SIGKILL pot provocar problemes, com ara arxius temporals no eliminats o dades no guardades.
- Els administradors de sistema haurien d'entendre bé els diferents senyals abans d'utilitzar-los.
