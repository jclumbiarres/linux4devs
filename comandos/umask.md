# umask

El comandament `umask` (abreviatura de "user mask") és una eina del sistema que determina els permisos predeterminats que s'assignaran als arxius i directoris nous que creïs.

## Sintaxi

```
umask [opcions] [mode]
```

## Descripció

Quan crees un nou arxiu o directori, el sistema li assigna permisos d'accés predeterminats. El `umask` defineix quins permisos es restringeixen d'aquests valors predeterminats.

El sistema opera de la següent manera:

- Per a arxius, el valor predeterminat és 666 (rw-rw-rw-)
- Per a directoris, el valor predeterminat és 777 (rwxrwxrwx)

El valor del `umask` es resta d'aquests permisos predeterminats. Per exemple, un `umask` de 022 resultarà en:

- Arxius: 666 - 022 = 644 (rw-r--r--)
- Directoris: 777 - 022 = 755 (rwxr-xr-x)

## Opcions comunes

- `-S`: Mostra el valor de `umask` en format simbòlic (com ara 'u=rwx,g=rx,o=rx')
- `-p`: Mostra el valor en un format que pot ser utilitzat com a entrada

## Exemples

### Veure el valor actual de umask

```bash
umask
```

Això mostrarà el valor actual, normalment en format octal (per exemple, 0022).

### Veure el valor en format simbòlic

```bash
umask -S
```

Podria mostrar alguna cosa com ara 'u=rwx,g=rx,o=rx'.

### Establir un nou valor de umask

```bash
umask 027
```

Aquest valor evitarà que el grup tingui permís d'escriptura i que altres usuaris tinguin qualsevol permís als nous arxius i directoris.

### Valors comuns de umask

- 022: Permet lectura i execució per a tothom, però només l'usuari pot escriure (típic en sistemes multiusuari)
- 002: Permet al grup escriure, però només lectura per a altres (comú en entorns col·laboratius)
- 077: Només l'usuari té accés, ningú més (màxima privacitat)

## Notes importants

- El `umask` només afecta els arxius i directoris que es creen després d'establir-lo
- Els canvis de `umask` són temporals i només s'apliquen a la sessió actual, llevat que s'incloguin en arxius de configuració com `.bashrc` o `.profile`
- Recordeu que el `umask` funciona restant permisos, no afegint-los
