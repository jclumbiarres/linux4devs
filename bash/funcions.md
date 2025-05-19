Les funcions són blocs de codi reutilitzables. Es defineixen aixi:

```bash
saluda() {
	echo "Bon dia, $1!" # $1 = primer argument
}
```

## Cridar la funció

```bash
saluda "Anna" # Mostra "Bon dia, Anna!"
```

## Retornar valors

Bash retorna un estat de sortida (0 = èxit, 1-255 = error)

```bash
suma() {
	return $(($1+$2))
}
suma 3 5
echo "Resultat: $?" # $? = valor retornat
```
