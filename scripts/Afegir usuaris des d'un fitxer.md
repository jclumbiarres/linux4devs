​

Objectiu: Crear usuaris llegint noms d'un fitxer usuaris.txt.​

​
```bash
#!/bin/bash ​  
while read usuari; do ​  
useradd "$usuari" ​  
echo "Usuari $usuari creat." ​  
done < usuaris.txt ​
```
​

Explicació:​
- Executa amb sudo per permisos d'administrador.​
- El fitxer usuaris.txt ha de tenir un nom per línia.