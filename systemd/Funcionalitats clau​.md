
## Inici en paral·lel​
- Systemd inicia serveis simultàniament si no tenen dependències entre ells, accelerant l’engegada del sistema.

## Gestió de dependències​
- Defineix relacions entre unitats (per exemple, que un servei necessiti la xarxa activa abans d’iniciar-se).​

## Journald: Registre centralitzat​
- Systemd inclou journald, un sistema de registres que recopila totes les sortides dels serveis (logs). Pots consultar-los amb:​
```
journalctl -u nginx.service # Mostra logs del servei NGINX​
```
## Supervisió de processos​
- Systemd monitoritza els serveis i pot reiniciar-los automàticament si fallen.​