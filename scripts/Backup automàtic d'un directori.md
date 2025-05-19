
**Objectiu**: fer una còpia de seguretat diària d'una carpeta (ho farem amb cron despres)​

```bash
#!/bin/bash ​  
# Directori a copiar i destí ​  
origen="/home/usuari/documents" ​  
desti="/backups" ​  
data=$(date +"%d%m%Y") ​  
​  
# Comprimeix el directori ​  
tar -czf "$desti/backup_$data.tar.gz" "$origen" ​  
echo "Backup del $data creat a $desti!"
```

**Explicació** 
* tar -czf comprimeix el directori en un fitxer tar.gz
* date +"%d/%m/%Y" agafa la data actual (ex 15072024)