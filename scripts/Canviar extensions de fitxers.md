
**Objectiu**: Canviar l'extensió .txt a .md en un directori

```bash
#!/bin/bash ​  
for fitxer in *.txt; do ​  
	nou_nom="${fitxer%.txt}.md" ​  
	mv "$fitxer" "$nou_nom" ​  
	echo "Canviat: $fitxer → $nou_nom" ​  
done ​
```

**Explicació**
* ${fitxer%.txt} elimina .txt del nom.
* **Important** prova abans amb echo mv per evitar errors.