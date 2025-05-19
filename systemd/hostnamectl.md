# Hostnamectl: Gestionar el nom de l'host

El comandament `hostnamectl` a GNU/Linux permet gestionar el nom de l'ordinador (conegut com a "hostname"). Aquest nom és utilitzat per identificar la màquina dins d'una xarxa i és una informació bàsica del sistema.

## Visió general

`hostnamectl` forma part de systemd i proporciona una interfície senzilla per veure i modificar la configuració del nom de l'host del sistema.

## Ús bàsic

### Consultar la informació de l'host

Per veure tota la informació relacionada amb el nom de l'ordinador, simplement executeu el comandament sense cap opció:

```bash
hostnamectl
```

Això mostrarà una sortida similar a aquesta:

```
    Static hostname: el-meu-ordinador
            Icon name: computer-laptop
              Chassis: laptop
          Machine ID: 1a2b3c4d5e6f7g8h9i0j1k2l3m4n5o6p
              Boot ID: 7a8b9c0d1e2f3g4h5i6j7k8l9m0n1o2p
  Operating System: Ubuntu 22.04 LTS
                Kernel: Linux 5.15.0-48-generic
        Architecture: x86-64
```

### Modificar el nom de l'host

Per canviar el nom de l'ordinador, utilitzeu l'opció `set-hostname`:

```bash
sudo hostnamectl set-hostname "nom-del-meu-ordinador"
```

Aquest canvi és permanent i es mantindrà després de reiniciar el sistema.

## Opcions principals

`hostnamectl` ofereix diverses opcions útils:

### Tipus de noms d'host

El sistema emmagatzema diferents tipus de noms d'host que podeu gestionar:

- **Static hostname**: El nom principal de l'ordinador

  ```bash
  sudo hostnamectl set-hostname "nom-estatic"
  ```

- **Pretty hostname**: Un nom més descriptiu que pot contenir espais i caràcters especials

  ```bash
  sudo hostnamectl set-hostname "Ordinador d'en Joan" --pretty
  ```

- **Transient hostname**: Un nom temporal gestionat pel kernel
  ```bash
  sudo hostnamectl set-hostname "nom-temporal" --transient
  ```

### Altres opcions

- Per veure l'estat de forma més concisa:

  ```bash
  hostnamectl status
  ```

- Per veure només el nom de l'host:
  ```bash
  hostnamectl --no-pager
  ```

## Configuració addicional

El canvi de nom mitjançant `hostnamectl` s'emmagatzema al fitxer `/etc/hostname`. Si cal, també podríeu editar directament aquest fitxer, però es recomana utilitzar `hostnamectl` per evitar configuracions incorrectes.

També és bona pràctica actualitzar el fitxer `/etc/hosts` quan canvieu el nom de l'ordinador, afegint-hi el nou nom:

```
127.0.0.1   localhost
127.0.1.1   nom-del-meu-ordinador
```

## Consideracions

- Canviar el nom de l'host pot afectar aplicacions de xarxa que depenen d'aquesta configuració
- Els noms d'host només han de contenir lletres, números i guions (sense espais)
- Algunes aplicacions poden requerir reiniciar després de canviar el nom de l'host per reconèixer el canvi

## Exemples pràctics

1. Consultar només el nom de l'host actual:

   ```bash
   hostnamectl --static
   ```

2. Establir un nom d'host més descriptiu:

   ```bash
   sudo hostnamectl set-hostname "portatil-anna" --static
   sudo hostnamectl set-hostname "Portàtil de l'Anna" --pretty
   ```

3. Comprovar el tipus de càrrega (chassis):
   ```bash
   hostnamectl chassis
   ```

Aquesta sortida pot mostrar valors com `laptop`, `desktop`, `server`, etc.
