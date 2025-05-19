## Bucle for:​​

Itera sobre una llista d'elements​

```bash
# lista explícita: ​  
for amic in "Anna" "Pere" "Laia"; do ​  
echo "Hola, $amic!" ​  
done ​  
```
​  
```bash
# Amb números (seq és una comanda útil): ​  
for i in {1..5}; do ​  
echo "Número: $i" ​  
done ​
```
​
## Bucle while:

Executa mentre es cumpleix una condició:​

```bash
comptador=1 ​  
while [ $comptador -le 5 ]; do ​  
echo "Comptador: $comptador" ​  
comptador=$((comptador + 1)) ​  
done
```

Control amb break i continue:​

```bash
while true; do ​  
read -p "Escriu 'sortir' per acabar: " entrada ​  
if [ "$entrada" = "sortir" ]; then ​  
	break ​  
else ​  
	echo "Has escrit: $entrada" ​  
fi ​  
done
```
