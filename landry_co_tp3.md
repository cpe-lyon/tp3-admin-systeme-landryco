# Exercice 1. Commandes de base

__Commencez par mettre à jour votre système avec les commandes vues dans le cours.__<br>
`sudo apt update && sudo apt upgrade`

1. __Quels sont les 5 derniers paquets installés sur votre machine ?__<br>
`grep "installed" /var/log/dpkg.log | tail -S`

2. __Utiliser dpkg et apt pour compter le nombre de paquets installés (ne pas hésiter à consulter le manuel !). Comment explique-t-on la (petite) différence de comptage ?__<br>
`dpkg --list | wc --lines` (524)<br>
`apt list --installed | wc --lines` (520)

3. __Combien de paquets sont disponibles en téléchargement ?__<br>
`apt list | wc --lines` (64118)

4. __Créer un alias “maj” qui met à jour le système__<br>
`touch ~/.bash_aliases`<br>
`alias maj='sudo apt update && apt upgrade'`

5. __A quoi sert le paquet fortunes ? Installez-le.__<br>
`sudo apt install fortune`<br>
Il s'agit d'une collection de phrases provenant de diverses sources.

6. __Quels paquets proposent de jouer au sudoku ?__<br>
`apt search sudoku`
```
fltk1.1-games/disco 1.1.10-26ubuntu1 amd64
  Boîte à outils Fast Light - exemples de jeux : jeux de dames, sudoku

fltk1.3-games/disco 1.3.4-9ubuntu1 amd64
  Boîte à outils Fast Light - exemples de jeux : jeux de dames, sudoku

gnome-sudoku/disco 1:3.32.0-1 amd64
  Casse-tête Sudoku pour GNOME

hitori/disco 3.31.0-1 amd64
  Jeu de puzzle logique similaire au sudoku

ksudoku/disco 4:18.12.3-0ubuntu1 amd64
  Jeu et Solveur de Sudoku

libqqwing-dev/disco 1.3.4-1.1 amd64
  outil pour générer et résoudre des casse-tête Sudoku (développement)

libqqwing2v5/disco 1.3.4-1.1 amd64
  outil pour générer et résoudre des casse-tête Sudoku (bibliothèque)

nudoku/disco 1.0.0-1 amd64
  ncurses based sudoku games

qqwing/disco 1.3.4-1.1 amd64
  tool for generating and solving Sudoku puzzles (application)

sudoku/disco 1.0.5-2build3 amd64
  Sudoku en mode console

texlive-games/disco 2018.20190227-1 all
  TeX Live : Composition de jeux
```

7. __Lister les derniers paquets installés explicitement avec la commande apt install__<br>
`grep " apt install " /var/log/apt/history.log`

# Exercice 2.

__A partir de quel paquet est installée la commande ls ? Comment obtenir cette information en une seule
commande, pour n’importe quel programme (indice : la réponse est dans le poly de cours 2, dans la liste des
commandes utiles) ? Utilisez la réponse à pour écrire un script appelé origine-commande (sans l’extension
.sh) prenant en argument le nom d’une commande, et indiquant quel paquet l’a installée.__<br>

`which -a ls | tail -1 | xargs dpkg -S`
`which -a $1 | tail -1 | xargs dpkg -S`

# Exercice 3.

__Ecrire une commande qui affiche “INSTALLÉ” ou “NON INSTALLÉ” selon le nom et le statut du package
spécifié dans cette commande.__<br>

```
#!/bin/bash

dpkg -s $1 &> /dev/null

if [ $? -eq 0 ]; then
        echo "INSTALLÉ"
else
        echo "NON INSTALLÉ"
fi
```

# Exercice 4.

__Lister les programmes livrés avec coreutils. A quoi sert la commande ’\[’ et comment afficher ce qu’elle
retourne ?__<br>

`apt show coreutils`

# Exercice 5. aptitude

__Installez le paquet emacs à l’aide de la version graphique d’aptitude.__<br>

```
aptitude
SHIFTD + :
^emacs$
+
g
g
```

# Exercice 6. Installation d’un paquet par PPA

1. __Installer la version Oracle de Java (avec l’ajout des PPA)__<br>
```
sudo add-apt-repository ppa:linuxuprising/java
sudo apt update
sudo apt install oracle-java11-installer
```

2. __Vérifiez qu’un nouveau fichier a été créé dans /etc/apt/sources.list.d. Que contient-il ?__<br>

`linuxuprising-ubuntu-java-disco.list`
