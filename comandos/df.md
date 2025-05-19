# df - Mostra l'espai disponible al disc

## Descripció

El comandament `df` (disk free) ens permet veure quant espai lliure i ocupat hi ha als discs i sistemes d'arxius del nostre ordinador.

## Sintaxi bàsica

```bash
df [opcions] [sistema_arxius]
```

## Exemples d'ús

### Veure l'espai en format llegible

```bash
df -h
```

Aquest és l'ús més comú. L'opció `-h` mostra les mides en format llegible (GB, MB, etc.)

### Veure només un disc específic

```bash
df -h /home
```

Mostra l'espai només pel directori /home

## Opcions principals

- `-h`: Mostra les mides en format humà (GB, MB, KB)
- `-T`: Mostra el tipus de sistema d'arxius
- `-i`: Mostra informació sobre els inodes
- `-a`: Mostra tots els sistemes d'arxius

## Sortida explicada

Quan executem `df -h`, veurem una taula amb aquesta informació:

- **S.fitxers**: El nom del sistema d'arxius
- **Mida**: Mida total del disc
- **Usats**: Espai utilitzat
- **Disp**: Espai disponible
- **% Ús**: Percentatge d'ús
- **Muntat a**: Punt de muntatge

## Consells pràctics

- Utilitzeu sempre l'opció `-h` per veure les mides de forma comprensible
- Reviseu periòdicament l'espai disponible per evitar problemes
- Si un disc està més del 90% ple, considereu netejar arxius innecessaris
