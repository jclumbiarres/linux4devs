# systemctl

## Descripció

El `systemctl` és una eina fonamental en sistemes GNU/Linux moderns que utilitzen systemd com a sistema d'inicialització i gestor de serveis. Permet controlar l'estat del sistema i gestionar els serveis del sistema operatiu.

## Sintaxi bàsica

```bash
systemctl [OPCIONS] ORDRE [NOM_UNITAT]
```

## Ordres principals

- `systemctl status [servei]`: Mostra l'estat d'un servei específic o del sistema en general.
- `systemctl start [servei]`: Inicia un servei.
- `systemctl stop [servei]`: Atura un servei.
- `systemctl restart [servei]`: Reinicia un servei.
- `systemctl enable [servei]`: Configura un servei perquè s'iniciï automàticament en arrencar el sistema.
- `systemctl disable [servei]`: Desactiva l'inici automàtic d'un servei.
- `systemctl reload [servei]`: Recarrega la configuració d'un servei sense aturar-lo.
- `systemctl list-units`: Llista totes les unitats (serveis, dispositius, muntatges, etc.) actives.
- `systemctl list-unit-files`: Mostra tots els fitxers d'unitat disponibles i el seu estat.

## Exemples d'ús

### Comprovar l'estat d'un servei

```bash
systemctl status nginx
```

Aquest comandament mostrarà si el servidor web Nginx està en funcionament, quan es va iniciar, els últims registres i altra informació útil.

### Iniciar un servei

```bash
systemctl start mariadb
```

Inicia el servei de base de dades MariaDB.

### Configurar un servei per iniciar-se amb el sistema

```bash
systemctl enable cups
```

Configura el servei d'impressió CUPS perquè s'iniciï automàticament quan s'engegui el sistema.

### Reiniciar un servei després de canviar la seva configuració

```bash
systemctl restart ssh
```

Atura i torna a iniciar el servei SSH, aplicant els canvis de configuració.

### Veure tots els serveis actius

```bash
systemctl list-units --type=service
```

Mostra una llista de tots els serveis que estan actualment en funcionament.

## Unitats de systemd

Systemd no només gestiona serveis, també controla:

- **Serveis** (`.service`): Programes que s'executen en segon pla
- **Punts de muntatge** (`.mount`): Sistemes de fitxers muntats
- **Dispositius** (`.device`): Maquinari del sistema
- **Sockets** (`.socket`): Comunicació entre processos
- **Temporitzadors** (`.timer`): Tasques programades (similar al cron)

## Opcions d'arrencada del sistema

- `systemctl poweroff`: Apaga el sistema
- `systemctl reboot`: Reinicia el sistema
- `systemctl suspend`: Posa el sistema en suspensió
- `systemctl hibernate`: Hiberna el sistema

## Notes importants

- Moltes ordres de `systemctl` requereixen privilegis d'administrador (root), per això s'han d'executar amb `sudo`.
- Els noms dels serveis són sensibles a majúscules i minúscules.
- Per veure més informació sobre qualsevol ordre, podeu utilitzar `man systemctl`.
