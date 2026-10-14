---
tags: [linux, gameshell, b1]
source: Fiche GameShell — commandes (missions 1 à 44)
---
# Fiche — commandes Linux

Toutes les commandes vues dans GameShell, avec une explication simple et un exemple.

## Se déplacer et regarder

Sous Linux, les lieux du jeu sont des dossiers : on s'y déplace avec `cd` et on regarde dedans avec `ls`.

| Commande | À quoi ça sert | Exemple |
|---|---|---|
| `pwd` | Dire où je suis | `pwd` |
| `ls` | Voir ce qu'il y a dans le dossier | `ls Garden` |
| `ls -A` | Voir aussi les fichiers cachés | `ls -A Garden` |
| `ls -l` | Voir les détails (droits, taille, date) | `ls -l` |
| `tree` | Voir toute l'arborescence en arbre | `tree ~/Garden` |
| `cd DOSSIER` | Entrer dans un dossier | `cd Castle/Cellar` |
| `cd` | Revenir au point de départ | `cd` |
| `cd ..` | Monter d'un niveau (dossier parent) | `cd ..` |
| `cd -` | Revenir où j'étais juste avant | `cd -` |

Raccourcis de chemin :
- `~` = le point de départ (ma maison)
- `.` = ici, le dossier où je suis
- `..` = le dossier au-dessus
- `/` sépare les dossiers : `Castle/Main_building/Throne_room`
- `Tab` complète les noms tout seul ; `Tab Tab` montre les choix possibles

## Gérer fichiers et dossiers

`mv` déplace, `cp` copie, `rm` supprime. ⚠️ `rm` n'a pas de corbeille : c'est définitif.

| Commande | À quoi ça sert | Exemple |
|---|---|---|
| `mkdir NOM` | Créer un dossier | `mkdir Hut` |
| `mv SOURCE DEST` | Déplacer (l'original part) | `mv Garden/coin_1 ~/Forest/Hut/Chest` |
| `mv ANCIEN NOUVEAU` | Renommer | `mv Garden Jardin` |
| `cp SOURCE DEST` | Copier (l'original reste) | `cp *tapestry* ~/Forest/Hut/Chest` |
| `cp -r DOSSIER DEST` | Copier un dossier avec son contenu | `cp -r Garden Backup` |
| `rm FICHIER` | Supprimer un fichier | `rm *spider*` |
| `rm -f FICHIER` | Supprimer sans question | `rm -f crown` |
| `rmdir DOSSIER` | Supprimer un dossier vide | `rmdir Garden` |
| `touch FICHIER` | Créer un fichier vide | `touch test.txt` |

Jokers :
- `*` = n'importe quoi, même rien : `*spider*` = tout ce qui contient « spider »
- `?` = exactement un caractère : `bat_?` = `bat_1`, `bat_2`… mais pas `bat_12`
- Toujours tester avec `ls *spider*` avant un `rm *spider*`

Fichiers cachés : leur nom commence par un point (`.26201_coin_1`). `ls` et `*` ne les voient pas : il faut `ls -A` et un point dans le joker (`rm .*spider*`).

## Lire et chercher

`cat` affiche un fichier, `find` cherche par nom, `grep` cherche dans le contenu.

| Commande | À quoi ça sert | Exemple |
|---|---|---|
| `cat FICHIER` | Afficher tout le fichier | `cat journal.txt` |
| `cat F1 F2` | Afficher plusieurs fichiers à la suite | `cat page_01 page_02` |
| `cat -n FICHIER` | Afficher avec les numéros de ligne | `cat -n page_12` |
| `head -n K FICHIER` | Les K premières lignes | `head -n 6 page_07` |
| `tail -n K FICHIER` | Les K dernières lignes | `tail -n 9 page_12` |
| `less FICHIER` | Lire page par page (Espace, `/mot`, `q` pour quitter) | `less page_12` |
| `nano FICHIER` | Modifier un fichier (Ctrl+O sauver, Ctrl+X quitter) | `nano journal.txt` |
| `man COMMANDE` | Lire le manuel d'une commande | `man find` |
| `find DOSSIER -name "MOTIF"` | Chercher un fichier par son nom | `find ~/Garden/Maze -name "*copper*"` |
| `find … -iname "MOTIF"` | Pareil, sans se soucier des majuscules | `find ~/Garden/Maze -iname "*gold*"` |
| `find … -type f` | Seulement les fichiers (`-type d` = dossiers) | `find ~/Garden/Maze -type f` |
| `find … -exec CMD {} \;` | Lancer une commande sur chaque résultat | `find … -exec mv {} ~/Forest/Hut/Chest \;` |
| `grep MOT FICHIER` | Afficher les lignes qui contiennent le mot | `grep King scroll` |
| `grep -i` | Ignorer les majuscules | `grep -i gsh grimoire_*` |
| `grep -l` | Afficher seulement le nom des fichiers trouvés | `grep -il gsh grimoire_*` |
| `grep -r` | Chercher dans tous les sous-dossiers | `grep -rl ruby ~/Garden/Maze` |
| `grep -v` | Garder les lignes qui NE contiennent PAS le mot | `grep -v PAID` |

## Combiner les commandes

Le pipe `|` est un tuyau : le résultat de la commande de gauche devient l'entrée de celle de droite.

| Symbole / commande | À quoi ça sert | Exemple |
|---|---|---|
| `A \| B` | Envoyer le résultat de A dans B | `cat page_03 page_04 \| tail -n 16` |
| `A > FICHIER` | Écrire le résultat dans un fichier (écrase) | `ls grimoire_* > Drawer/inventory.txt` |
| `A >> FICHIER` | Ajouter à la fin d'un fichier | `echo "note" >> journal.txt` |
| `A 2> FICHIER` | Écrire les erreurs dans un fichier | `./merlin 2> /tmp/cle.txt` |
| `A < FICHIER` | Donner un fichier à lire à la place du clavier | `gsh check < /tmp/cle.txt` |
| `/dev/null` | Poubelle : tout ce qu'on y envoie disparaît | `grep -il gsh * 2> /dev/null` |
| `$( A )` | Mettre le résultat de A au milieu d'une autre commande | `mv "$(grep -rl ruby ~/Garden/Maze)" ~/Forest/Hut/Chest` |
| `xargs CMD` | Transformer les lignes reçues en arguments de CMD | `find … -type f \| xargs grep -l diamond` |
| `wc -l` | Compter les lignes | `… \| grep -v PAID \| wc -l` |
| `tr ABC XYZ` | Remplacer des lettres par d'autres | `tr a-z b-za < message` |
| `alias NOM='CMD'` | Créer un raccourci | `alias la='ls -A'` |
| `./PROGRAMME` | Lancer un programme du dossier | `./merlin` |

Deux sorties à connaître : **stdout** = les résultats normaux (`>`), **stderr** = les messages d'erreur (`2>`).

## Processus (programmes qui tournent)

Chaque programme qui tourne a un numéro, le **PID**. On l'utilise pour l'arrêter.

| Commande | À quoi ça sert | Exemple |
|---|---|---|
| `CMD &` | Lancer en arrière-plan (sans attendre) | `flarigo &` |
| `A ; B` | Lancer A puis B, l'un après l'autre | `cd ; ls` |
| `ps` | Lister les programmes qui tournent | `ps` |
| `pstree -p` | Voir la famille des programmes avec leurs PID | `pstree -p` |
| `kill PID` | Demander à un programme de s'arrêter | `kill 99743 99745` |
| `kill -9 PID` | Forcer l'arrêt (impossible à ignorer) | `kill -9 76760` |
| `Ctrl + C` | Arrêter la commande en cours | — |
| `Ctrl + L` | Nettoyer l'écran | — |

Les PID changent à chaque relance : toujours reprendre les numéros du dernier `ps` ou `pstree`.

## Permissions

`ls -l` montre qui a le droit de faire quoi ; `chmod` change ces droits.

Lire `drwxr-x---` : la 1re lettre dit le type (`d` = dossier, `-` = fichier), puis 3 groupes de 3 lettres : moi (`u`), mon groupe (`g`), les autres (`o`).

| Lettre | Sur un fichier | Sur un dossier |
|---|---|---|
| `r` | Lire le contenu | Lister ce qu'il contient |
| `w` | Modifier | Ajouter / retirer des fichiers |
| `x` | L'exécuter comme un programme | Entrer dedans (`cd`) |
| `-` | Droit absent | Droit absent |

| Commande | À quoi ça sert |
|---|---|
| `chmod u+r FICHIER` | Me donner le droit de lire |
| `chmod u+rx DOSSIER` | Me donner le droit de lister et d'entrer |
| `chmod u+rwx DOSSIER` | Me donner tous les droits |
| `chmod u-w FICHIER` | M'enlever le droit d'écriture |

## Système et réseau (cours « Créer une VM »)

| Commande | À quoi ça sert |
|---|---|
| `whoami` | Afficher l'utilisateur connecté |
| `hostname` | Afficher le nom de la machine |
| `ip addr` | Voir les adresses IP (repérer 192.168.x.x) |
| `sudo apt update` | Mettre à jour la liste des paquets |
| `sudo apt install PAQUET` | Installer un logiciel |
| `sudo systemctl status ssh` | Voir l'état du service SSH |
| `ssh utilisateur@IP` | Se connecter à une machine à distance |
| `exit` | Quitter le terminal / la session SSH |

## GameShell

| Commande | À quoi ça sert |
|---|---|
| `gsh goal` | Afficher l'objectif de la mission |
| `gsh check` | Vérifier la mission |
| `gsh reset` | Recommencer la mission |
| `gsh help` | Aide |

Voir aussi : [[Fiche-Git]]
