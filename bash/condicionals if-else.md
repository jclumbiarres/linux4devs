Els condicionals executen codi segons una condició.

## Estructura bàsica

```bash
if [ $edat -ge 18 ]; then ​  
	echo "Ets major d'edat." ​  
else ​  
	echo "Ets menor." ​  
fi
```

## Operadors comuns

* Números: -eq (igual), -ne (diferent), -gt (major), -lt (menor).
* Text: =, !=
* Fitxers: -f (existeix el fitxer?), -d (és un directori?)

## Example amb elif

```bash
if [ $nota -ge 9 ]; then ​  
	echo "Excel·lent!" ​  
elif [ $nota -ge 7 ]; then ​  
	echo "Notable!" ​  
else ​  
	echo "A recuperar..." ​  
fi
```
