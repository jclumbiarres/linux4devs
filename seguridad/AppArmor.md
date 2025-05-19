
## Introducció

AppArmor és un sistema de seguretat integrat al kernel de Linux que limita els programes a un conjunt de recursos definits per l'administrador. Forma part del sistema de seguretat de Ubuntu per defecte i ofereix una protecció addicional contra vulnerabilitats i exploits en aplicacions.

A diferència d'altres solucions de seguretat com SELinux, AppArmor se centra en els camins dels fitxers (path-based) en lloc d'etiquetes, el que fa que sigui més fàcil d'entendre i configurar, especialment per a administradors que s'inicien en sistemes de control d'accés obligatori.

## Conceptes Bàsics

### Perfils

Els perfils són fitxers que defineixen quins recursos pot utilitzar un programa. Cada perfil pot estar en un dels següents modes:

- **Mode d'aplicació (enforce)**: Les restriccions s'apliquen i les violacions es registren i es bloquegen.
- **Mode de queixa (complain)**: Les violacions es registren però no es bloquegen.
- **Desactivat**: El perfil existeix però no està en ús.

### Espai de Noms (Namespaces)

AppArmor utilitza espais de noms per organitzar els perfils. Els principals són:

- **/usr/share/apparmor/extra-profiles/**: Perfils addicionals.
- **/etc/apparmor.d/**: Perfils locals instal·lats.
- **/var/lib/apparmor/profiles/**: Perfils generats per eines.

## Instal·lació i Configuració Bàsica

AppArmor ve instal·lat per defecte a Ubuntu, però pots verificar el seu estat amb:

```bash
sudo systemctl status apparmor
```

Si no està instal·lat o ha estat desactivat, pots instal·lar-lo i activar-lo amb:

```bash
sudo apt update
sudo apt install apparmor apparmor-utils apparmor-profiles
sudo systemctl enable apparmor
sudo systemctl start apparmor
```

## Comandes Bàsiques

### Verificar l'Estat d'AppArmor

```bash
# Veure l'estat del servei
sudo systemctl status apparmor

# Comprovar que està carregat al kernel
sudo aa-status
```

### Gestionar Perfils

```bash
# Llistar tots els perfils i els seus estats
sudo aa-status

# Canviar un perfil a mode d'aplicació
sudo aa-enforce /path/to/profile

# Canviar un perfil a mode de queixa
sudo aa-complain /path/to/profile

# Desactivar un perfil
sudo ln -s /etc/apparmor.d/profile /etc/apparmor.d/disable/
sudo apparmor_parser -R /etc/apparmor.d/profile

# Reactivar un perfil desactivat
sudo rm /etc/apparmor.d/disable/profile
sudo apparmor_parser -r /etc/apparmor.d/profile
```

### Recarregar Perfils

```bash
# Recarregar tots els perfils
sudo systemctl reload apparmor

# Recarregar un perfil específic
sudo apparmor_parser -r /etc/apparmor.d/profile
```

## Creació i Modificació de Perfils

### Generar un Perfil Nou

AppArmor ofereix eines per generar perfils basats en les activitats d'una aplicació:

```bash
# Començar a generar un perfil per a una aplicació
sudo aa-genprof /ruta/a/la/aplicacio

# Executar l'aplicació en una altra terminal per generar esdeveniments
# Tornar a aa-genprof i seguir les instruccions
```

### Actualitzar un Perfil Existent

```bash
# Actualitzar un perfil basant-se en registres de queixa
sudo aa-logprof
```

### Editar Manualment un Perfil

Pots editar directament els fitxers de perfil amb un editor de text:

```bash
sudo nano /etc/apparmor.d/nom_del_perfil
```

## Estructura d'un Perfil

Un perfil d'AppArmor té la següent estructura bàsica:

```
#include <tunables/global>

profile nom_del_perfil /camí/a/l'executable {
  #include <abstractions/base>
  
  # Permisos de fitxers
  /camí/a/fitxer rw,
  /un/altre/camí r,
  
  # Capacitats
  capability net_bind_service,
  capability setuid,
  
  # Variables
  @{HOME}/fitxer rw,
}
```

### Permisos de Fitxers

Els permisos bàsics inclouen:

- `r`: Lectura
- `w`: Escriptura
- `a`: Annexió (append)
- `m`: Memmap
- `k`: Bloqueig (lock)
- `l`: Enllaç
- `x`: Execució

### Directives Comunes

- `#include <abstractions/nom>`: Inclou conjunts predefinits de regles.
- `capability nom_capacitat`: Permet l'ús d'una capacitat específica.
- `network`: Controla l'accés a la xarxa.
- `signal`: Controla l'enviament de senyals entre processos.

## Exemple de Perfil Complet

Aquí teniu un exemple d'un perfil per a un servidor web simple:

```
#include <tunables/global>

profile servidor_web /usr/bin/servidor_web {
  #include <abstractions/base>
  #include <abstractions/nameservice>
  #include <abstractions/apache2-common>
  
  # Directori d'aplicació
  /usr/bin/servidor_web mr,
  
  # Fitxers de configuració
  /etc/servidor_web/** r,
  
  # Fitxers servits
  /var/www/** r,
  
  # Registres
  /var/log/servidor_web/* w,
  
  # Capacitats
  capability net_bind_service,
  
  # Xarxa
  network inet stream,
  network inet6 stream,
}
```

## Casos d'Ús Comuns

### Protegir Serveis de Sistema

```bash
# Aplicar mode d'aplicació a un servei
sudo aa-enforce /etc/apparmor.d/usr.sbin.mysqld

# Verificar el seu estat
sudo aa-status | grep mysqld
```

### Protegir Aplicacions d'Usuari

```bash
# Crear un perfil per a una aplicació d'usuari
sudo aa-genprof /usr/bin/firefox

# Després d'utilitzar l'aplicació, finalitzar la generació del perfil
```

### Depurar Problemes de Perfil

Quan una aplicació no funciona correctament sota AppArmor:

```bash
# Canviar temporalment a mode de queixa
sudo aa-complain /path/to/profile

# Revisar els registres per veure les violacions
sudo cat /var/log/syslog | grep DENIED

# Actualitzar el perfil basant-se en les violacions
sudo aa-logprof
```

## Registres i Depuració

### On Trobar els Registres

Els registres d'AppArmor es troben principalment a:

```bash
/var/log/syslog
/var/log/audit/audit.log  # Si auditd està instal·lat
```

### Filtrar Registres d'AppArmor

```bash
# Veure només entrades d'AppArmor
sudo grep "apparmor" /var/log/syslog

# Veure denegacions d'accés
sudo grep "DENIED" /var/log/syslog
```

### Eines de Depuració

```bash
# Mostrar informació detallada d'un procés sota AppArmor
sudo aa-status --verbose

# Provar un perfil contra una comanda sense aplicar-lo
sudo aa-exec -p perfil_a_provar -- comanda_a_executar
```

## Integració amb Systemd

Pots configurar serveis systemd per utilitzar perfils específics d'AppArmor:

```ini
[Service]
AppArmorProfile=/etc/apparmor.d/nom_del_perfil
```

O per generar un perfil automàticament:

```ini
[Service]
AppArmorProfile=:name:
```

## Exemples Pràctics

### Protegir un Servidor NGINX

1. Instal·lar NGINX si encara no està instal·lat:
    
    ```bash
    sudo apt install nginx
    ```
    
2. Generar un perfil per a NGINX:
    
    ```bash
    sudo aa-genprof /usr/sbin/nginx
    ```
    
3. En una altra terminal, realitzar accions comunes amb NGINX:
    
    ```bash
    sudo systemctl restart nginx
    curl http://localhost
    ```
    
4. Tornar a aa-genprof i acabar la configuració.
    

### Protegir una Aplicació de Base de Dades

1. Per a MySQL/MariaDB (ja té un perfil predefinit):
    
    ```bash
    sudo aa-enforce /etc/apparmor.d/usr.sbin.mysqld
    sudo systemctl restart mysql
    ```
    
2. Verificar que tot funciona correctament:
    
    ```bash
    mysql -u root -p
    ```
    
3. Si hi ha problemes, revisar els registres:
    
    ```bash
    sudo grep "mysqld" /var/log/syslog
    ```
    

## Resolució de Problemes

### L'Aplicació No S'Inicia

1. Canviar temporalment a mode de queixa:
    
    ```bash
    sudo aa-complain /etc/apparmor.d/perfil.problema
    ```
    
2. Revisar els registres:
    
    ```bash
    sudo grep DENIED /var/log/syslog
    ```
    
3. Actualitzar el perfil:
    
    ```bash
    sudo aa-logprof
    ```
    

### Permisos Denegats Inesperats

Si una aplicació que funcionava correctament comença a tenir problemes després d'una actualització:

1. Revisar els registres de denegació:
    
    ```bash
    sudo grep "apparmor=\"DENIED\"" /var/log/syslog
    ```
    
2. Actualitzar el perfil:
    
    ```bash
    sudo aa-logprof
    ```
    
3. Recarregar el perfil:
    
    ```bash
    sudo apparmor_parser -r /etc/apparmor.d/perfil.actualitzat
    ```
    

## Consells Avançats

### Utilitzar Variables en els Perfils

AppArmor permet utilitzar variables per fer perfils més flexibles:

```
@{HOME}/documents/** r,
@{PROC}/@{pid}/status r,
```

### Crear Abstraccions Personalitzades

Pots crear abstraccions personalitzades per reutilitzar regles comunes:

```bash
sudo nano /etc/apparmor.d/abstractions/meva-abstraccio
```

I després incloure-la en els perfils:

```
#include <abstractions/meva-abstraccio>
```

### Perfils per a Containers

AppArmor es pot utilitzar per protegir containers:

```bash
# Per a LXC/LXD
sudo aa-genprof /usr/bin/lxc-start

# Per a Docker
sudo aa-genprof /usr/bin/dockerd
```

## Manteniment i Bones Pràctiques

1. **Revisa regularment els registres** per detectar problemes.
2. **Actualitza els perfils** després d'actualitzacions de sistema o aplicacions.
3. **Comença amb mode de queixa** i passa a mode d'aplicació quan estiguis segur que tot funciona correctament.
4. **Fes còpies de seguretat dels perfils** abans de modificar-los.
5. **Utilitza abstraccions** per mantenir els perfils nets i reutilitzables.

## Recursos Addicionals

- [Documentació oficial d'Ubuntu sobre AppArmor](https://wiki.ubuntu.com/AppArmor)
- [Wiki d'AppArmor](https://gitlab.com/apparmor/apparmor/-/wikis/home)
- [Manual de perfils d'AppArmor](https://manpages.ubuntu.com/manpages/focal/man5/apparmor.d.5.html)

## Conclusió

AppArmor és una eina potent per millorar la seguretat del teu sistema Ubuntu, limitant el que les aplicacions poden fer i mitigant l'impacte potencial de vulnerabilitats. Amb aquesta guia, hauries de poder implementar i gestionar AppArmor en el teu sistema Ubuntu per protegir els serveis i aplicacions més sensibles.