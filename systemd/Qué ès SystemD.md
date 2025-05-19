Systemd és un sistema init modern, creat el 2010, que substitueix SysVinit en moltes distribucions (com Ubuntu, Fedora o Debian). No només gestiona l’inici del sistema, sinó que també ofereix eines per administrar processos, registres (logs), dispositius, i més. Els seus objectius principals són:​

- Velocitat: Iniciar serveis en paral·lel (no seqüencialment).​
- Estandardització: Unificar la configuració de serveis amb fitxers declaratius.​
- Integració: Gestionar totes les parts del sistema (no només serveis).​

Systemd organitza tot amb unitats (units), que són entitats configurades mitjançant fitxers amb extensió .service, .socket, .target, etc. Cada unitat defineix com gestionar un recurs. Vegem-ne els tipus principals:​

​
Tipus d’unitats​
- .service: Defineix un servei (per exemple, un servidor web).​
- .socket: Gestiona una connexió de xarxa o socket (activa un servei quan rep una petició).​
- .target: Grups d’unitats (similar als "runlevels" de SysVinit).​
- .mount: Configura muntatges de discos.​
- .timer: Executa tasques programades (com el cron).​
- .device: Gestiona dispositius hardware.​