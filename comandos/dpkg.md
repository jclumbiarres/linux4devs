# El Comando `dpkg`

## Què és `dpkg`?

`dpkg` (Debian Package) és el sistema base de gestió de paquets de Debian i distribucions derivades com Ubuntu. És una eina de baix nivell que permet instal·lar, eliminar i proporcionar informació sobre paquets `.deb`.

## Sintaxi bàsica

```bash
dpkg [opcions] acció
```

## Accions principals

### Instal·lació de paquets

```bash
# Instal·lar un paquet
dpkg -i paquet.deb

# Instal·lar múltiples paquets
dpkg -i paquet1.deb paquet2.deb
```

### Eliminar paquets

```bash
# Eliminar un paquet (manté els fitxers de configuració)
dpkg -r nom_del_paquet

# Eliminar completament un paquet (inclosos fitxers de configuració)
dpkg -P nom_del_paquet
```

### Consultar informació

```bash
# Llistar tots els paquets instal·lats
dpkg -l

# Buscar un paquet específic
dpkg -l | grep nom_del_paquet

# Mostrar informació detallada d'un paquet
dpkg -s nom_del_paquet

# Llistar fitxers instal·lats per un paquet
dpkg -L nom_del_paquet

# Esbrinar a quin paquet pertany un fitxer
dpkg -S /camí/al/fitxer
```

### Altres operacions útils

```bash
# Reconfigurar un paquet instal·lat
dpkg-reconfigure nom_del_paquet

# Verificar la integritat d'un paquet
dpkg --verify nom_del_paquet

# Extreure contingut d'un paquet sense instal·lar-lo
dpkg -x paquet.deb directori_destí
```

## Opcions comunes

- `-i, --install`: Instal·la un paquet
- `-r, --remove`: Elimina un paquet (conserva fitxers de configuració)
- `-P, --purge`: Elimina completament un paquet i els seus fitxers de configuració
- `-l, --list`: Llista els paquets instal·lats
- `-s, --status`: Mostra l'estat d'un paquet
- `-L, --listfiles`: Llista els fitxers instal·lats per un paquet
- `-S, --search`: Cerca el paquet que conté un determinat fitxer

## Problemes comuns i solucions

### Dependències no resoltes

Si `dpkg` mostra errors de dependències, pots utilitzar:

```bash
# Corregir dependències trencades
sudo apt install -f
```

### Paquets trencats

```bash
# Reconfigurar paquets trencats
sudo dpkg --configure -a
```

## Diferència entre `dpkg` i `apt`

- **dpkg**: És una eina de més baix nivell que només gestiona els paquets `.deb` locals. No resol dependències automàticament.
- **apt**: És una capa d'alt nivell que utilitza `dpkg` internament, però afegeix la capacitat de descarregar paquets de repositoris i resoldre dependències automàticament.

## Exemples pràctics

```bash
# Descarregar un paquet .deb i instal·lar-lo
wget https://exemple.com/paquet.deb
sudo dpkg -i paquet.deb

# Veure paquets recentment instal·lats
dpkg -l | grep "^ii" | head -n 10

# Veure tots els fitxers instal·lats per Firefox
dpkg -L firefox

# Esbrinar quin paquet proporciona un determinat binari
dpkg -S $(which ls)
```

## Notes importants

- Generalment es recomana utilitzar `apt` per a la gestió quotidiana de paquets.
- `dpkg` requereix privilegis d'administrador per a la majoria d'operacions (utilitzar `sudo`).
- A diferència d'`apt`, `dpkg` no descarrega paquets ni resol dependències automàticament.
- Abans d'eliminar paquets, és recomanable comprovar si altres paquets en depenen.
