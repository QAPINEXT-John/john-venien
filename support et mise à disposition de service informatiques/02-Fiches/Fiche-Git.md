---
tags: [git, github, b1]
source: Cours Educentre « Git & GitHub — Versionner, collaborer, livrer »
---
# Fiche — Git & GitHub

- **Git** = système de gestion de versions distribué, fonctionne en local, sans internet.
- **Commit** = une version enregistrée. **Dépôt** (repository) = dossier suivi par Git.
- **GitHub** n'est pas Git : c'est une plateforme en ligne qui héberge des dépôts Git et facilite la collaboration.

## Configuration initiale (une fois par machine)
```bash
git config --global user.name "Prénom Nom"
git config --global user.email "vous@exemple.com"
git config --global init.defaultBranch main
```

## Les trois zones
```
Répertoire de travail ──git add──► Zone de préparation (staging) ──git commit──► Dépôt local
```

## Cycle de base
```bash
git init                         # créer un dépôt
git status                       # voir l'état des fichiers
git add fichier.txt              # préparer un fichier
git commit -m "Ajoute fichier.txt"   # enregistrer une version
```
Un bon message de commit décrit ce que fait le changement, **à l'impératif**, en une ligne claire.

## Lire et comparer l'historique
| Commande | Rôle |
|---|---|
| `git log` | Historique complet |
| `git log --oneline` | Version condensée |
| `git log --oneline --graph --all` | Avec les branches |
| `git diff` | Modifications non préparées |
| `git diff --staged` | Modifications préparées |
| `git show a1b2c3d` | Contenu d'un commit précis |

## Annuler sans danger
| Situation | Commande |
|---|---|
| Abandonner les modifications d'un fichier | `git restore fichier.txt` |
| Retirer un fichier de la zone de préparation | `git restore --staged fichier.txt` |
| Corriger le dernier commit (non partagé) | `git commit --amend` |
| Annuler un commit déjà partagé | `git revert a1b2c3d` |

⚠️ `git reset --hard` supprime définitivement les modifications non commitées.

## .gitignore
Liste ce que Git ne doit jamais suivre : dépendances (`node_modules/`), fichiers temporaires (`*.log`), secrets (`.env`).
**Ne jamais commiter de mots de passe ni de clés d'API.**

## Branches
```bash
git branch                      # lister
git switch -c ma-fonctionnalite # créer et basculer
git switch main                 # revenir sur main
git merge ma-fonctionnalite     # fusionner dans la branche courante
git branch -d ma-fonctionnalite # supprimer après fusion
```
- **Fast-forward** : main n'a pas bougé, Git avance le pointeur.
- **Merge commit** : les deux branches ont évolué, Git crée un commit de fusion.

## Dépôt distant (GitHub)
```bash
git clone https://github.com/utilisateur/projet.git
git remote add origin <url>
git push -u origin main
git pull          # = fetch + merge
git fetch         # récupérer sans fusionner
```
- **Clone** : copie locale d'un dépôt où j'ai les droits d'écriture.
- **Fork** : copie dans mon compte GitHub pour contribuer à un projet qui n'est pas le mien.

## Collaborer
- Workflow : branche → commits → push → **Pull Request** → revue de code → fusion dans main.
- Bonne PR : titre clair, description (pourquoi / quoi / comment tester), petite taille, lien vers l'issue (`Closes #12`).
- Conflit : repérer `<<<<<<<`, `=======`, `>>>>>>>`, garder la bonne version, supprimer les marqueurs, `git add` puis `git commit`.
- Bonnes pratiques : commits petits et fréquents, `git pull` régulier, protéger main, **jamais de `push --force`** sur une branche partagée.

## Aide-mémoire
| Je veux… | Commande |
|---|---|
| Voir l'état du dépôt | `git status` |
| Enregistrer mon travail | `git add . && git commit -m "..."` |
| Créer une branche | `git switch -c nom` |
| Envoyer mon travail | `git push` |
| Récupérer le travail des autres | `git pull` |
| Annuler un commit partagé | `git revert <hash>` |

Voir aussi : [[Fiche-commandes-Linux]]
