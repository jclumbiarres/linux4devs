Objectiu: Menú per llistar, crear i eliminar fitxers.​

```bash
#!/bin/bash ​  
while true; do ​  
	echo "1. Llistar fitxers" ​  
	echo "2. Crear fitxer" ​  
	echo "3. Eliminar fitxer" ​  
	echo "4. Sortir" ​  
	read -p "Escull una opció: " opcio ​  
​  
case $opcio in ​  
	1) ls ;; ​  
	2) read -p "Nom del fitxer: " nom; touch "$nom" ;; ​  
	3) read -p "Nom del fitxer: " nom; rm "$nom" ;; ​  
	4) break ;; ​  
	*) echo "Opció no vàlida." ;; ​  
	esac ​  
done ​
```