# Comando `getent`

## Descripció

El comando `getent` és una eina de GNU/Linux que permet consultar les bases de dades dels serveis d'informació del sistema, com ara usuaris, grups, hosts, serveis, protocols i xarxes.

## Sintaxi

```bash
getent [opcions] base_de_dades [clau ...]
```

## Arguments principals

- `base_de_dades`: La base de dades que es vol consultar (passwd, group, hosts, services, protocols, networks, etc.).
- `clau`: Un o més valors específics a cercar dins la base de dades.

## Opcions comunes

- `-s, --service=SERVICE`: Especifica quin servei utilitzar per a la consulta.
- `-h, --help`: Mostra l'ajuda del comando.
- `-V, --version`: Mostra la versió del comando.

## Bases de dades disponibles

- `passwd`: Informació d'usuaris del sistema.
- `group`: Informació dels grups del sistema.
- `hosts`: Assignacions d'adreces IP a noms d'hosts.
- `services`: Serveis de xarxa disponibles.
- `protocols`: Protocols de xarxa suportats.
- `networks`: Xarxes conegudes.
- `shadow`: Informació de contrasenya dels usuaris (requereix permisos d'administrador).
- `gshadow`: Informació de contrasenya dels grups (requereix permisos d'administrador).

## Exemples d'ús

### Consultar informació d'un usuari específic

```bash
getent passwd usuari1
```

Retorna la informació de l'usuari "usuari1" en format: nom:x:UID:GID:informació:directori_home:shell

### Llistar tots els usuaris del sistema

```bash
getent passwd
```

### Consultar informació d'un grup

```bash
getent group desenvolupadors
```

### Consultar la informació IP d'un host

```bash
getent hosts exemple.com
```

Mostra l'adreça IP associada a exemple.com

### Consultar un servei específic

```bash
getent services http
```

Mostra la informació del port i protocol del servei HTTP

## Característiques destacables

- Consulta la informació independentment d'on estigui emmagatzemada (fitxers locals, bases de dades, LDAP, NIS, etc.).
- Segueix l'ordre especificat a `/etc/nsswitch.conf`.
- Format de sortida consistent i fàcil de processar.

## Notes

- Per algunes bases de dades com `shadow` i `gshadow` cal tenir permisos d'administrador.
- Si no s'especifica una clau, es mostren totes les entrades de la base de dades.
- És una eina molt útil per a scripts i l'automatització de tasques d'administració.
