
## Introducció

LazyVim és una configuració de NeoVim que facilita el seu ús amb molts plugins preconfigurats. Aquesta guia cobreix les dreceres de teclat (shortcuts) més essencials per a usuaris principiants.

## Comandaments Bàsics

### Modes de NeoVim

- `i` - Entrar en mode d'inserció
- `Esc` o `Ctrl+[` `Ctrl+C` - Tornar al mode normal
- `v` - Mode visual (selecció de text)
- `:` - Mode de comandes

### Desar i Sortir

- `:w` - Desar el fitxer
- `:q` - Sortir (si no hi ha canvis)
- `:wq` o `:x` - Desar i sortir
- `:q!` - Sortir sense desar

## Gestió de Finestres

### Crear Finestres

- `<espai>sv` - Dividir verticalment
- `<espai>sh` - Dividir horitzontalment
- `<espai>sc` - Tancar finestra actual però mantenir el buffer

### Moure's Entre Finestres

- `Ctrl+h` - Moure's a la finestra de l'esquerra
- `Ctrl+j` - Moure's a la finestra inferior
- `Ctrl+k` - Moure's a la finestra superior
- `Ctrl+l` - Moure's a la finestra de la dreta

### Redimensionar Finestres

- `Ctrl+Up` - Augmentar l'alçada
- `Ctrl+Down` - Disminuir l'alçada
- `Ctrl+Left` - Disminuir l'amplada
- `Ctrl+Right` - Augmentar l'amplada

## Gestió de Pestanyes (Tabs)

- `<espai>fb` - Veure tots els buffers
- `<espai>bb` - Anar al buffer anterior
- `<espai>bd` - Tancar el buffer actual

## Explorador de Fitxers

- `<espai>e` - Obrir l'explorador de fitxers (NeoTree)
- `<espai>fe` - Mostrar l'explorador de fitxers centrat en el fitxer actual
- A dins de l'explorador:
    - `a` - Crear un nou fitxer/directori
    - `d` - Eliminar fitxer/directori
    - `r` - Reanomenar
    - `Enter` - Obrir fitxer

## Cerca i Navegació

- `<espai>ff` - Cercar fitxers
- `<espai>fg` - Cercar text a tots els fitxers
- `<espai>/` - Cercar amb grep a tots els fitxers
- `n` - Anar a la següent coincidència
- `N` - Anar a l'anterior coincidència

## Edició de Codi

- `gcc` - Comentar/Descomentar línia
- `<espai>cf` - Format del codi
- `K` - Mostrar documentació
- `gd` - Anar a la definició
- `gr` - Veure referències

## Teclat Numèric del Mode Normal

- `h` - Moure's a l'esquerra
- `j` - Moure's avall
- `k` - Moure's amunt
- `l` - Moure's a la dreta
- `w` - Paraula següent
- `b` - Paraula anterior
- `0` - Inici de línia
- `$` - Final de línia
- `gg` - Inici del document
- `G` - Final del document

## Terminals

- `<espai>ft` - Obrir terminal flotant
- `<espai>fT` - Obrir terminal en una nova pestanya

## Consells per a Principiants

- Utilitza `<espai>?` per veure totes les dreceres de teclat disponibles
- Pots personalitzar LazyVim editant els fitxers de configuració a `~/.config/nvim/`
- Practica amb `vimtutor` per aprendre els comandaments bàsics de Vim

Recorda que a LazyVim, la tecla líder per defecte és `<espai>`.