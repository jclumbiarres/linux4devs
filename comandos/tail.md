# Comanda `tail`

`tail` és una comanda en GNU/Linux que mostra les últimes línies d'un arxiu o entrada. És molt útil per visualitzar el final d'un fitxer sense necessitat de mostrar-lo sencer.

## Sintaxi bàsica

```bash
tail [OPCIONS] [ARXIU]
```

Si no s'especifica cap arxiu, `tail` llegeix de l'entrada estàndard.

## Opcions principals

- `-n N` o `--lines=N`: Mostra les últimes N línies. Per defecte són 10 línies.
- `-f` o `--follow`: Mostra les últimes línies i continua llegint l'arxiu, mostrant noves línies a mesura que s'afegeixen. Molt útil per monitoritzar logs en temps real.
- `-c N` o `--bytes=N`: Mostra els últims N bytes.
- `-q` o `--quiet`: No mostra els noms dels arxius quan se n'especifiquen diversos.
- `--retry`: Segueix intentant obrir un arxiu si no és accessible.

## Exemples

### Veure les últimes 10 línies d'un arxiu

```bash
tail /clases/linux4devs/comandos/tail.md
```

### Veure les últimes 5 línies d'un arxiu

```bash
tail -n 5 /clases/linux4devs/comandos/tail.md
```

### Monitoritzar un arxiu en temps real

```bash
tail -f /clases/linux4devs/comandos/tail.md
```

### Veure els últims 100 bytes d'un arxiu

```bash
tail -c 100 /clases/linux4devs/comandos/tail.md
```

### Veure les últimes línies de múltiples arxius

```bash
tail -n 3 /clases/linux4devs/comandos/*.md
```

## Usos comuns

- Monitoritzar arxius de registre (logs) en temps real
- Veure les últimes entrades en un arxiu de dades
- Comprovar els últims canvis en un fitxer de configuració
- Verificar els resultats més recents d'un procés que escriu a un arxiu

## Combinació amb altres comandes

La comanda `tail` es pot combinar amb altres utilitzant pipes:

```bash
cat /clases/linux4devs/comandos/tail.md | grep "exemple" | tail -n 5
```

Aquest exemple mostra les últimes 5 línies que contenen la paraula "exemple" en l'arxiu.

## Diferències amb `head`

Mentre que `head` mostra el principi (les primeres línies) d'un arxiu, `tail` mostra el final (les últimes línies). Sovint s'utilitzen juntes per inspeccionar diferents parts d'un arxiu.
