# systemd-analyze

## Introducció

`systemd-analyze` és una eina de línia de comandes que ens ajuda a entendre i analitzar el procés d'arrencada del sistema operatiu. Aquesta eina és part de systemd, el sistema d'inicialització utilitzat en moltes distribucions GNU/Linux modernes.

## Funcionalitat bàsica

`systemd-analyze` ens permet veure quant temps triga el sistema a arrencar i quins serveis són els més lents durant el procés d'inicialització. Això és molt útil per optimitzar el temps d'arrencada del sistema.

## Ús bàsic

### Veure el temps d'arrencada

```bash
systemd-analyze
```

Això mostrarà el temps que ha necessitat el nucli (kernel), l'espai d'usuari inicial (userspace) i el temps total d'arrencada.

### Veure el temps dels serveis

```bash
systemd-analyze blame
```

Aquesta ordre mostra una llista de tots els serveis arrencats, ordenats pel temps que han trigat a iniciar-se (de més a menys).

### Generar un gràfic del procés d'arrencada

```bash
systemd-analyze plot > arrencat.svg
```

Aquest comandament genera un gràfic SVG que es pot visualitzar amb qualsevol navegador web o visor d'imatges. El gràfic mostra visualment com s'han iniciat els diferents serveis i quant temps ha trigat cadascun.

## Opcions avançades

### Analitzar l'arbre de dependències crítiques

```bash
systemd-analyze critical-chain
```

Mostra la cadena de serveis que determinen el temps d'arrencada (les dependències de serveis). És útil per entendre quins serveis estan retardant l'arrencada.

### Verificar unitats systemd

```bash
systemd-analyze verify [nom_unitat]
```

Comprova si hi ha errors en la configuració d'una unitat de systemd específica.

### Seguretat dels serveis

```bash
systemd-analyze security [nom_unitat]
```

Avalua la configuració de seguretat d'una unitat de systemd i mostra una puntuació i recomanacions.

## Exemples pràctics

### Exemple 1: Analitzar els serveis més lents

```bash
systemd-analyze blame | head -n 10
```

Mostra els 10 serveis que més temps han trigat a iniciar-se.

### Exemple 2: Veure l'arbre de dependències del servei de xarxa

```bash
systemd-analyze critical-chain network.target
```

Analitza les dependències del servei de xarxa i com afecten al temps d'arrencada.

## Consells

- Si vols un sistema que arrenqui més ràpidament, considera desactivar els serveis que triguen molt i que no necessites.
- Utilitza `systemd-analyze plot` per tenir una visió gràfica del procés d'arrencada completa.
- Quan actualitzis el sistema, comprova si hi ha canvis en el temps d'arrencada amb `systemd-analyze`.

## Conclusió

`systemd-analyze` és una eina molt valuosa per a l'optimització del sistema i per entendre millor com funciona el procés d'arrencada en GNU/Linux. Fins i tot sense coneixements tècnics avançats, pots utilitzar-la per identificar problemes d'arrencada i millorar el rendiment del teu sistema.
