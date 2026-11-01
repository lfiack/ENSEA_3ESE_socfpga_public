# ENSEA 3ESE SoCFPGA Public
Cours, TD et TP SoCFPGA sur DE10

## Installation Debian VM

Voir la [Vidéo](https://youtu.be/ryTIv9PtaYE).

Cours et TD en salle BYOD, il faudra Linux pour les démos. Vous devrez mettre en place une machine virtuelle.
Vocabulaire :
* VM : Virtual Machine = Machine virtuelle
* Host : Système d'exploitation dans le quel la VM tourne (ex. votre PC sous Windows)
* Guest : Système d'exploitation virtualisé (ex. la distribution Linux Debian que vous allez installer maintenant).

1. Installez virtualbox. Installez virtualbox-host-modules : [link](https://www.virtualbox.org/wiki/Downloads)
2. Téléchargez image debian netinstall : [link](https://www.debian.org/CD/netinst/#netinst-stable)
3. Lancez virtualbox, puis :
    * New
    * VM Name
    * ISO Image
    * Décochez "Proceed with unattended Installation"
    * Install
4. Suivez les instructions de la vidéo
5. Une fois le système installé, loggez vous en tant que `root` et:
```bash
apt update
apt install sudo
usermod -aG sudo <username>
exit
```
6. Loggez-vous en tant qu'utilisateur et :
```bash
sudo apt update
sudo apt install build-essential dkms vim linux-headers-$(uname -r)
```
7. Redémarrez la VM :
```bash
sudo poweroff
```
8. Installez les extensions guest :

> Device > Insert guest...

```bash
sudo mount /dev/cdrom /media/cdrom
cd /media/cdrom
sudo ./VBoxLinuxAdditions.run
sudo usermod -aG vboxsf <username>
sudo poweroff
```

9. Configurez un dossier partagé entre le guest et l'host :
> Settings > Shared Folder

10. Redémarrez une dernière fois :
```bash
sudo reboot
```

## TD Machine : Les bases sous Linux

### Les commandes de base

À l’aide de la commande man, de votre moteur de recherche favori ou simplement par l’expérimentation, trouver l’utilité des commandes suivantes : `mkdir`, `cd`, `ls`, `touch`, `rm`, `cat`, `less`, `tail`, `pwd`, `cp`, `mv`, `chmod`, `chown`, `chgrp`, `ps`, `grep`, `top`.
La plupart des commandes peuvent prendre des options, ce qui peut être nécessaire dans certains cas :
* Copier ou supprimer un dossier
* Aﬃcher les fichiers cachés (sous linux, ce sont les fichiers commençant par un point)
* Mettre en forme la sortie pour différentes commandes
Votre utilisateur dispose des droits d’administrateur. Pour lancer une commande avec les droits d’administrateur, il faut ajouter `sudo` avant la commande.
Savoir utiliser le terminal linux permet d’aller beaucoup plus vite, mais l’appretissage peut être long. Mais ça en vaut la peine. 

> Faites-vous une anti-sèche papier.

### L'éditeur de texte vim

La plupart du temps vous allez utiliser un éditeur de texte en mode graphique comme kate, ou un IDE comme STM32CubeIDE. 
Cela dit, il est souvent plus pratique et rapide d’utiliser un éditeur de texte en ligne de commande, comme vim.
C’est le cas lorsque l’on veut modifier quelques lignes dans un fichier de configuration par exemple.
Parfois, l’interface graphique n’est simplement pas disponible, comme lorsque l’on travaille dans un environnement linux embarqué. 
Dans ce cas ce genre d’éditeur est nécessaire.

Ouvrir un terminal, lancer l’éditeur de texte vim.
Pour taper du texte, il faut se mettre en mode `Insertion`. Pour cela, appuyer sur `i`. Pour sortir du mode `Insertion`, appuyer sur `Echap`.
Voici quelques commandes utiles :
* `:q` puis `Entrée` : Quitter
* `:w` puis `Entrée` : Sauvegarde
* `:wq` puis `Entrée` : Sauvegarde et quitte
* `:q!` puis `Entrée` : Quitter sans sauvegarder
* `u` : annuler
* `i` : mode insertion
* `o` : ajouter une ligne
* `O` : ajouter une ligne au dessus
* `a` : mode insertion après le caractère courant
* `x` : supprimer un caractère
* `d` : supprimer plusieurs caractères
    * `d$` : supprime le contenu de la ligne
    * `dd` : supprime la ligne
    * `dw` : supprime un mot
Pour accéder au tutoriel oﬃciel de vim, ouvrir un terminal et taper vimtutor.
N’hésitez pas à y passer un peu de temps.

## TD Machine : Le C sous Linux

Dans les exercices suivants, vous êtes **encouragés** à utiliser vim dans la VM. Vous me remercierez plus tard.

### Un exercice bête et facile

1. Créez un tableau d’entiers dont la taille sera facilement configurable (avec un #define par exemple).
2. Remplir ce tableau avec des nombres aléatoire entre 0 et 99.
3. Écrire une fonction permettant de trouver le nombre maximal de cette liste, ainsi que son indice dans le tableau.
4. Même question pour trouver le nombre minimal.
5. Écrire une fonction permettant de trier le tableau du nombre le plus petit au nombre le plus grand.
6. Où ce situe le tableau dans la mémoire ? Où sont les diﬀérentes variables ?
7. Montrez votre travail à l’encadrant.

### Allocation de mémoire

1. Demandez à l'utilisateur d'entrer la taille du tableau.
2. Créez le tableau dynamiquement à l'aide de la fonction `malloc`.
3. Où ce situe le tableau dans la mémoire ? Où sont les diﬀérentes variables ?
4. Montrez votre travail à l’encadrant.

### Manipulation de fichiers

Créez un fichier contenant une dizaine de nombres désordonnés.
1. Modifier le programme de l’exercice précédent pour qu’il aille lire les nombres dans le fichier au lieu de les générer aléatoirement.
2. Écrire le résultat dans un autre fichier
3. Montrez votre travail à l’encadrant.