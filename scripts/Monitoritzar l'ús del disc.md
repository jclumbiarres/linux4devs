Objectiu: Enviar un avís si el disc té més del 90% d'ús.​


```bash
#!/bin/bash ​  
usu_disc=$(df -h / | awk 'NR==2 {print $5}' | tr -d '%') ​  
​  
if [ $usu_disc -gt 90 ]; then ​  
echo "ATENCIÓ: Disc ple al $usu_disc%!" | mail -s "Alerta de Disc" admin@example.com ​  
fi ​
```
​
Explicació:​
- df -h / mostra l'ús del disc de la partició arrel.​
- Necessites mailutils instal·lat per enviar correus.