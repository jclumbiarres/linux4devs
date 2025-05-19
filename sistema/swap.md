# El Swap (Intercanvi) en Linux

## Què és el Swap?

El swap, o àrea d'intercanvi, és un espai reservat en el disc dur que Linux utilitza com una extensió de la memòria RAM. Quan el sistema necessita més memòria de la que té disponible físicament, pot moure dades que no s'estan utilitzant activament de la RAM al swap, alliberant així espai per a noves dades.

## Per què és important el Swap?

- **Prevé fallades del sistema**: Quan la RAM s'omple completament, el swap permet que el sistema continuï funcionant.
- **Hibernació**: És necessari per guardar l'estat del sistema durant la hibernació.
- **Rendiment**: Permet gestionar millor els recursos del sistema, tot i que és més lent que la RAM.

## Com configurar el Swap

### Veure l'estat actual del Swap

Per comprovar si el teu sistema té swap configurat:

```bash
free -h
```

O també:

```bash
swapon --show
```

### Crear un fitxer de Swap

Si no tens swap o necessites més, pots crear un fitxer d'intercanvi:

1. **Crear un fitxer buit**:

   ```bash
   sudo fallocate -l 2G /swapfile
   ```

2. **Establir permisos correctes**:

   ```bash
   sudo chmod 600 /swapfile
   ```

3. **Configurar-lo com a swap**:

   ```bash
   sudo mkswap /swapfile
   ```

4. **Activar el swap**:

   ```bash
   sudo swapon /swapfile
   ```

5. **Fer que el swap sigui permanent** (afegir al `/etc/fstab`):
   ```bash
   echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab
   ```

### Ajustar el comportament del Swap

El paràmetre `swappiness` controla la tendència del sistema a utilitzar el swap:

- **Veure el valor actual**:

  ```bash
  cat /proc/sys/vm/swappiness
  ```

- **Canviar-lo temporalment**:

  ```bash
  sudo sysctl vm.swappiness=10
  ```

- **Canviar-lo permanentment** (afegir al `/etc/sysctl.conf`):
  ```bash
  echo 'vm.swappiness=10' | sudo tee -a /etc/sysctl.conf
  ```

Un valor baix (com 10) redueix l'ús del swap, mentre que un valor alt (com 60, que és el valor per defecte en moltes distribucions) fa que el sistema utilitzi el swap més freqüentment.

## Recomanacions

- **Mida del Swap**: Per a sistemes moderns:

  - Si tens < 2GB de RAM: Doble de la RAM
  - Si tens 2-8GB de RAM: Igual a la RAM
  - Si tens > 8GB de RAM: Almenys 4GB per hibernació

- **Tipus de Swap**: Pots utilitzar una partició dedicada o un fitxer de swap. En sistemes moderns, no hi ha pràcticament diferència de rendiment.

- **Múltiples àrees de Swap**: Linux pot utilitzar diverses àrees de swap simultàniament si és necessari.

## Comandes útils relacionades amb el Swap

- **Activar totes les àrees de swap**: `sudo swapon --all`
- **Desactivar totes les àrees de swap**: `sudo swapoff --all`
- **Veure informació detallada**: `cat /proc/swaps`
- **Prioritzar àrees de swap**: Utilitza l'opció `pri=` en `/etc/fstab`
