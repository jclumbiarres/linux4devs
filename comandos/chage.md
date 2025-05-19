# chage - Gestió de l'expiració de contrasenyes d'usuari

## Descripció

El comando `chage` (Change Age) permet gestionar i configurar la informació d'expiració de contrasenyes dels comptes d'usuari en sistemes GNU/Linux.

## Sintaxi

```
chage [opcions] LOGIN
```

## Opcions principals

- `-d, --lastday DARRER_DIA`: Estableix l'últim dia que es va canviar la contrasenya
- `-E, --expiredate DATA_EXPIRACIÓ`: Estableix la data d'expiració del compte
- `-I, --inactive DIES`: Estableix el període d'inactivitat després del qual el compte es bloqueja
- `-l, --list`: Mostra la configuració actual de l'expiració
- `-m, --mindays DIES_MÍNIMS`: Estableix el mínim de dies entre canvis de contrasenya
- `-M, --maxdays DIES_MÀXIMS`: Estableix el màxim de dies que una contrasenya és vàlida
- `-W, --warndays DIES_AVÍS`: Estableix els dies d'avís abans de l'expiració

## Exemples

### Mostrar la configuració d'expiració d'un usuari

```bash
chage -l usuari
```

### Establir una data d'expiració concreta per a un compte

```bash
chage -E 2024-12-31 usuari
```

### Configurar que la contrasenya expiri en 90 dies

```bash
chage -M 90 usuari
```

### Forçar a un usuari a canviar la contrasenya al proper inici de sessió

```bash
chage -d 0 usuari
```

### Establir l'avís d'expiració 7 dies abans

```bash
chage -W 7 usuari
```

## Notes importants

- Cal tenir permisos d'administrador (root) per executar aquest comando.
- Les dates es poden especificar en diferents formats (AAAA-MM-DD és recomanat).
- El valor `-1` en qualsevol opció indica "mai" (sense límit).
- Configurat correctament, ajuda a mantenir una política de seguretat robusta al sistema.
