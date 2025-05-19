# `sudo`: Executar Comandes com a Superusuari

## Descripció

El comandament `sudo` (Super User DO) permet executar programes amb els privilegis de seguretat d'un altre usuari, normalment l'administrador del sistema (root). És una eina fonamental per realitzar tasques administratives sense haver d'iniciar sessió directament com a usuari root.

## Sintaxi Bàsica

```
sudo [opcions] [comandament]
```

## Opcions Principals

- `-u usuari`: Executa el comandament com l'usuari especificat (per defecte és root).
- `-s`: Inicia una shell amb privilegis de superusuari.
- `-i`: Simula un login complet com a superusuari.
- `-l`: Mostra els permisos sudo de l'usuari actual.
- `-k`: Invalida el timeout de la contrasenya, forçant a demanar-la la propera vegada.
- `-v`: Actualitza el temps d'espera de la contrasenya sense executar cap comandament.

## Exemples d'Ús

### Instal·lar un paquet

```bash
sudo apt install firefox
```

### Editar un fitxer del sistema

```bash
sudo nano /etc/hosts
```

### Executar un comandament com un altre usuari

```bash
sudo -u joan ls /home/joan/documents
```

### Obtenir una shell de superusuari

```bash
sudo -s
```

### Veure els permisos sudo disponibles

```bash
sudo -l
```

## Com Funciona

Quan executem `sudo`, el sistema:

1. Verifica si l'usuari té permisos per executar el comandament especificat.
2. Demana la contrasenya de l'usuari (no la de root).
3. Registra l'intent (exitós o no) en els logs del sistema.
4. Si l'autenticació és correcta, executa el comandament amb els privilegis especificats.

## Fitxer de Configuració

Els permisos de sudo es configuren al fitxer `/etc/sudoers`. Aquest fitxer ha de ser editat amb el comandament `visudo`, mai directament, per evitar errors que podrien bloquejar el sistema.

## Consells de Seguretat

- No utilitzeu `sudo` amb aplicacions gràfiques a menys que sigui absolutament necessari.
- Eviteu executar `sudo` amb editors de text o navegadors web.
- Recordeu que amb `sudo` podeu modificar o eliminar fitxers crítics del sistema.
- El privilegi de sudo és una responsabilitat important, utilitzeu-lo amb precaució.

## Observacions

- Després d'introduir la contrasenya, `sudo` recordarà les vostres credencials durant un temps limitat (habitualment 15 minuts).
- Si oblideu la contrasenya de root, podeu utilitzar `sudo passwd root` per restablir-la si teniu permisos de sudo.
