# userdel - Eliminar un usuari del sistema

## Descripció

El comando `userdel` s'utilitza per eliminar un usuari del sistema GNU/Linux. Aquest comando elimina totes les referències a l'usuari específic de la base de dades del sistema.

## Sintaxi

```
userdel [OPCIONS] USUARI
```

## Opcions principals

- `-r, --remove`: Elimina el directori d'inici de l'usuari juntament amb el seu contingut i també elimina el directori de correu de l'usuari.
- `-f, --force`: Força l'eliminació encara que l'usuari estigui connectat o tingui processos en execució.
- `-Z, --selinux-user`: Elimina qualsevol mapatge d'usuari SELinux per a l'usuari.

## Exemples

1. **Eliminar un usuari sense eliminar el seu directori d'inici**

   ```bash
   sudo userdel marc
   ```

   Aquest comando elimina l'usuari "marc" del sistema, però manté el seu directori d'inici.

2. **Eliminar un usuari i el seu directori d'inici**

   ```bash
   sudo userdel -r anna
   ```

   Aquest comando elimina l'usuari "anna" i també elimina el seu directori d'inici juntament amb tots els seus fitxers.

3. **Forçar l'eliminació d'un usuari**

   ```bash
   sudo userdel -f jordi
   ```

   Aquest comando força l'eliminació de l'usuari "jordi", fins i tot si està connectat actualment.

4. **Eliminar un usuari i els seus directoris forçosament**
   ```bash
   sudo userdel -rf maria
   ```
   Aquest comando elimina l'usuari "maria", el seu directori d'inici i força l'eliminació si és necessari.

## Notes importants

- Cal tenir privilegis de superusuari (root) per utilitzar aquest comando.
- L'eliminació d'un usuari no elimina automàticament el seu directori d'inici o els seus arxius a menys que s'utilitzi l'opció `-r`.
- És recomanable fer una còpia de seguretat de les dades importants de l'usuari abans d'eliminar-lo.
- Si l'usuari que es vol eliminar està actualment connectat o té processos en execució, és millor utilitzar l'opció `-f` (force).
- Utilitzeu aquest comando amb precaució, ja que no es pot desfer l'eliminació d'un usuari i les seves dades.
