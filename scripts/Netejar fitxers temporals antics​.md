
Objectiu: Eliminar fitxers .tmp de més de 7 dies.​

```bash
#!/bin/bash ​  
find /tmp -name "*.tmp" -mtime +7 -exec rm {} \; ​  
echo "Fitxers temporals antics eliminats." ​
```

Explicació:​
- find /tmp busca a la carpeta /tmp.​
- -mtime +7 selecciona fitxers de més de 7 dies.​