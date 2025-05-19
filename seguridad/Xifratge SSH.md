## Tipus de xifratges principals

### RSA

```bash 
ssh-keygen -t rsa -b 4096 
```
El xifratge RSA és un dels més antics i àmpliament utilitzats. La seva seguretat es basa en la dificultat de factoritzar nombres primers grans. Tot i que encara és segur, es recomana utilitzar claus de com a mínim 2048 bits, i preferiblement 4096 bits per garantir una seguretat adequada en els propers anys.

### DSA

```bash 
ssh-keygen -t dsa 
``` 
El DSA (Digital Signature Algorithm) és un algorisme més antic i té limitacions en la mida de la clau (1024 bits). Ja no es recomana per a noves implementacions degut a les seves limitacions de seguretat.

### ECDSA

```bash 
ssh-keygen -t ecdsa -b 521 
``` 
L'ECDSA (Elliptic Curve Digital Signature Algorithm) utilitza criptografia de corba el·líptica, que ofereix una seguretat equivalent a RSA però amb claus més petites i operacions més ràpides. Les mides disponibles són 256, 384 i 521 bits.

### Ed25519

```bash 
ssh-keygen -t ed25519 
``` 
Aquest és l'algorisme més modern i recomanat actualment. Ed25519 ofereix un excel·lent rendiment, claus molt curtes però extremadament segures, i és resistent a diversos atacs criptogràfics. No cal especificar la mida perquè sempre utilitza 256 bits, que proporcionen seguretat suficient.

## Opcions addicionals importants

### Afegir un comentari

```bash 
ssh-keygen -t ed25519 -C "correu@example.net" 
``` 
El comentari ajuda a identificar per a què s'utilitza la clau.

### Canviar la ubicació de la clau

```bash 
ssh-keygen -t ed25519 -f ~/.ssh/clau_personalitzada 
``` 
Per defecte, la clau es guarda a ~/.ssh/id_ALGORITME, però podem canviar aquesta ubicació.

### Protegir amb contrasenya

```bash 
ssh-keygen -t ed25519 -o -a 100 
``` 
L'opció `-o` utilitza el format OpenSSH per a la clau privada, més segur que el format tradicional. L'opció `-a` estableix el nombre de rondes KDF (Key Derivation Function), fent més difícil els atacs de força bruta contra la contrasenya.

## Comparativa de xifratges

| Algorisme | Seguretat  | Velocitat   | Mida de clau | Recomanació  |
| --------- | ---------- | ----------- | ------------ | ------------ |
| RSA       | Bona       | Lenta       | 4096 bits    | Acceptable   |
| DSA       | Baixa      | Mitjana     | 1024 bits    | No recomanat |
| ECDSA     | Molt bona  | Ràpida      | 256-521 bits | Bona opció   |
| Ed25519   | Excel·lent | Molt ràpida | 256 bits     | Recomanada   |
