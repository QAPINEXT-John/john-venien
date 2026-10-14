---
tags: [linux, fiche, b1]
auteur: John Venien
date: 2026-10-14
---
# Fiche mémo — 10 commandes Linux essentielles

Notation : `MAJUSCULES` = à remplacer · `[ ]` = facultatif · `~` = mon dossier personnel · `.` = ici · `..` = dossier parent

| # | Commande | À quoi ça sert | Syntaxe | Exemple |
|---|---|---|---|---|
| 1 | `pwd` | Afficher le dossier où je me trouve | `pwd` | `pwd` → `/home/john/Documents` |
| 2 | `ls` | Lister le contenu d'un dossier | `ls [-l] [-A] [DOSSIER]` | `ls -lA ~/Documents` |
| 3 | `cd` | Changer de dossier | `cd [DOSSIER]` | `cd ~/Documents/cours` · `cd ..` · `cd` |
| 4 | `mkdir` | Créer un dossier | `mkdir [-p] DOSSIER` | `mkdir -p bts/b1/tp1` |
| 5 | `cp` | Copier un fichier ou un dossier | `cp [-r] SOURCE DESTINATION` | `cp -r tp1 tp1-sauvegarde` |
| 6 | `mv` | Déplacer ou renommer | `mv SOURCE DESTINATION` | `mv notes.txt cours-linux.txt` |
| 7 | `rm` | Supprimer (définitif, pas de corbeille) | `rm [-r] [-i] CIBLE` | `rm -ri tp1-sauvegarde` |
| 8 | `cat` | Afficher le contenu d'un fichier | `cat [-n] FICHIER` | `cat -n /etc/hostname` |
| 9 | `grep` | Chercher un mot dans des fichiers | `grep [-i] [-r] MOT FICHIER` | `grep -ri "debian" /etc/os-release` |
| 10 | `chmod` | Modifier les droits d'accès | `chmod QUI±DROITS FICHIER` | `chmod u+x script.sh` |

## Options à connaître

- `ls -l` : détails (droits, propriétaire, taille, date) · `ls -A` : fichiers cachés (commençant par `.`)
- `mkdir -p` : crée aussi les dossiers parents manquants
- `cp -r` / `rm -r` : agir sur un dossier **et tout son contenu**
- `rm -i` : demande confirmation avant chaque suppression
- `cat -n` : numérote les lignes
- `grep -i` : ignore les majuscules · `grep -r` : cherche dans les sous-dossiers · `grep -v` : lignes qui ne contiennent **pas** le mot
- `chmod` : `u` = moi, `g` = groupe, `o` = les autres ; `r` = lire, `w` = écrire, `x` = exécuter / entrer dans un dossier

## Réflexes

- `Tab` complète les noms ; `Tab Tab` propose les choix possibles.
- `man COMMANDE` affiche le manuel (`q` pour quitter).
- Toujours vérifier avec `ls` avant un `rm`, surtout avec un joker (`*`).
- Combiner : `ls -l | grep txt` envoie le résultat de `ls` dans `grep`.

Voir aussi : [[Fiche-commandes-Linux]] (fiche complète GameShell)
