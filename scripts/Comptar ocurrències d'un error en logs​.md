
Objectiu: Comptar quantes vegades apareix "ERROR" en un fitxer de log.​

​
```bash
#!/bin/bash ​  
comptador=$(grep -c "ERROR" /var/log/syslog) ​  
echo "Hi ha $comptador errors registrats." ​
```
​

Explicació:​
- grep -c compta les línies que contenen la paraula.​
- Pots substituir "ERROR" per altres paraules clau.​