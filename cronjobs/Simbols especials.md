```
*: Qualsevol valor (ex: * a l’hora = cada hora).​
,: Llista (ex: 2,5 en dia de la setmana = dimarts i divendres).​
-: Rang (ex: 1-5 en dies laborables).​
/: Interval (ex: */10 en minuts = cada 10 minuts).​
```

​
# Cada dilluns a les 18:30: ​  
```
30 18 * * 1 /ruta/script.sh ​  
```
​  
# Cada 10 minuts de dilluns a divendres: ​  
```
*/10 * * * 1-5 echo "Hola!" ​  
```
# El primer de gener a mitjanit: ​  
```
0 0 1 1 * /ruta/felicitats.sh
```
