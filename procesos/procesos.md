# Processos a GNU/Linux

Aquesta guia explica què són els processos en sistemes operatius GNU/Linux, com funcionen i com gestionar-los des de la línia de comandes.

## Què és un Procés?

En termes senzills, un **procés** és una instància d'un programa en execució. Quan executes una aplicació (com el teu navegador web, un editor de text o una comanda a la terminal), el sistema operatiu crea un o més processos per dur a terme aquesta tasca.

Cada procés té el seu propi espai de memòria aïllat, recursos assignats (com temps de CPU) i un identificador únic.

## Identificadors de Procés: PID i PPID

Cada procés a Linux té un identificador numèric únic anomenat **PID** (Process ID). Aquest número permet al sistema operatiu i a l'usuari referenciar processos específics.

A més del PID, cada procés (excepte el primer procés iniciat pel sistema) té un **PPID** (Parent Process ID), que és el PID del procés que el va crear. Això crea una jerarquia de processos.

El primer procés que s'inicia quan arrenca el sistema (sovint anomenat `init` o `systemd`) té el PID 1 i és l'avantpassat de tots els altres processos.

## Creació de Processos: `fork` i `exec`

Els nous processos a Linux es creen generalment mitjançant una crida al sistema anomenada `fork`.

1.  **`fork`**: Quan un procés existent crida `fork`, crea una còpia quasi exacta d'ell mateix. Aquesta còpia és el **procés fill**, i l'original és el **procés pare**. El procés fill hereta moltes propietats del pare però obté el seu propi PID i té el PPID del pare.
2.  **`exec`**: Sovint, després d'un `fork`, el procés fill vol executar un programa diferent del pare. Per fer-ho, utilitza una crida al sistema de la família `exec`. Aquesta crida reemplaça el codi i les dades del procés fill amb els del nou programa, però el PID es manté.

## Estats d'un Procés

Un procés pot passar per diferents estats durant la seva vida:

- **Running (R)**: El procés s'està executant a la CPU o està a la cua llest per executar-se.
- **Sleeping (S)**: El procés està esperant que passi alguna cosa (per exemple, una entrada de l'usuari, dades del disc, una pausa temporal). La majoria dels processos passen gran part del temps en aquest estat. Hi ha dos tipus:
  - _Interruptible Sleep_: Pot ser despertat per senyals.
  - _Uninterruptible Sleep (D)_: Esperant una operació d'entrada/sortida (I/O) que no pot ser interrompuda. Sovint vist quan s'espera accés a disc.
- **Stopped (T)**: El procés ha estat aturat, normalment per un senyal (com quan prems `Ctrl+Z` a la terminal). Pot ser reprès més tard.
- **Zombie (Z)**: El procés ha acabat la seva execució, però encara té una entrada a la taula de processos perquè el seu procés pare encara no ha recollit el seu estat de sortida (mitjançant la crida `wait`). Els processos zombis no consumeixen recursos significatius (només una entrada a la taula), però un gran nombre pot indicar un problema amb el procés pare.

## Comandes per Gestionar Processos

La línia de comandes ofereix eines potents per visualitzar i gestionar processos.

### `top` i `htop`: Monitorització de processos en temps real

- `top`: Eina clàssica que mostra una llista actualitzada dinàmicament dels processos que més recursos consumeixen. Permet ordenar per CPU, memòria, etc., i enviar senyals als processos.
- `htop`: Una alternativa millorada a `top` (sovint s'ha d'instal·lar: `sudo apt install htop` o `sudo dnf install htop`). Ofereix una interfície més visual, amb colors, desplaçament fàcil, i gestió de processos més intuïtiva amb les tecles de funció.

### `kill`: Envia senyals als processos

La comanda `kill` s'utilitza per enviar senyals a un procés, normalment per aturar-lo. Es necessita el PID del procés.

- `kill <PID>`: Envia el senyal per defecte, **SIGTERM** (número 15). Aquest senyal demana educadament al procés que acabi. El procés pot intentar tancar fitxers i netejar abans de sortir.
- `kill -9 <PID>` o `kill -SIGKILL <PID>`: Envia el senyal **SIGKILL** (número 9). Aquest senyal força l'aturada immediata del procés pel sistema operatiu. S'ha d'utilitzar com a últim recurs, ja que el procés no té oportunitat de netejar i pot deixar dades corruptes.
- `kill -l`: Mostra una llista de tots els senyals disponibles.

### `pkill` i `killall`: Atura processos pel nom

De vegades no coneixes el PID, però sí el nom del programa.

- `pkill <nom_proces>`: Envia SIGTERM als processos que coincideixen amb el nom.
  - `pkill -9 <nom_proces>`: Envia SIGKILL.
- `killall <nom_exacte_proces>`: Similar a `pkill`, però sovint requereix el nom exacte de l'executable i pot ser més estricte en la coincidència.
  - `killall -9 <nom_exacte_proces>`: Envia SIGKILL.

**Precaució:** Utilitza `pkill` i `killall` amb cura, especialment amb `-9`, ja que podries aturar processos importants si el nom no és prou específic.

### `pgrep`: Troba PIDs pel nom

- `pgrep <nom_proces>`: Mostra els PIDs dels processos que coincideixen amb el nom. Útil per verificar quins processos afectaria un `pkill` o per obtenir el PID per a `kill`.
  - `pgrep -u <usuari> <nom_proces>`: Busca processos d'un usuari específic.
  - `pgrep -l <nom_proces>`: Mostra el PID i el nom del procés.

## Processos en Primer Pla (Foreground) i Segon Pla (Background)

Quan executes una comanda a la terminal, normalment s'executa en **primer pla (foreground)**. Això significa que la terminal espera que la comanda acabi abans de mostrar-te el prompt de nou. No pots introduir noves comandes mentre s'executa.

Pots executar una comanda en **segon pla (background)** afegint un `&` al final:

```bash
comanda_llarga &
```


La terminal et mostrarà el PID del nou procés en segon pla i et tornarà el prompt immediatament, permetent-te continuar treballant.

- `jobs`: Mostra els processos que s'estan executant en segon pla des de la terminal actual.
- `fg %<numero_job>`: Porta un procés del segon pla (%1, %2, etc., segons `jobs`) al primer pla.
- `bg %<numero_job>`: Reprèn l'execució d'un procés aturat (`Ctrl+Z`) en segon pla.
- `Ctrl+Z`: Atura (Suspèn, estat T) el procés que s'està executant en primer pla i el posa en segon pla. Pots reprendre'l amb `fg` o `bg`.

## Prioritat de Processos: `nice` i `renice`

El sistema operatiu assigna temps de CPU als processos segons la seva prioritat. Pots influir en aquesta prioritat.

- **Valor `nice`**: Un número que va de -20 (màxima prioritat) a 19 (mínima prioritat). Per defecte, els processos comencen amb `nice` 0.
- `nice -n <valor> <comanda>`: Executa una comanda amb un valor `nice` específic (només usuaris normals poden augmentar el valor, és a dir, disminuir la prioritat; `root` pot assignar valors negatius).
  - `nice -n 10 comanda_pesada &` # Executa amb menys prioritat
- `renice <valor> -p <PID>`: Canvia la prioritat d'un procés ja en execució.
  - `renice 15 -p 1234` # Baixa la prioritat del procés amb PID 1234
  - `sudo renice -5 -p 5678` # Augmenta la prioritat (requereix `sudo`)