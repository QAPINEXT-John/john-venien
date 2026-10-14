---
tags: [procedure, git, github, b1]
auteur: John Venien
date: 2026-10-14
source: Cours Educentre « Git & GitHub — Versionner, collaborer, livrer »
---
# Procédure — Créer un dépôt GitHub

> **Objectif** : créer un dépôt sur GitHub, le relier à son poste, puis y envoyer ses premiers changements.
> **Prérequis** : un navigateur web, Git installé (Git for Windows → *Git Bash*).

## 1. Créer le compte GitHub

1. Aller sur https://github.com et cliquer sur **Sign up**.
2. Renseigner l'adresse e-mail, un mot de passe solide et un nom d'utilisateur.
3. Valider l'adresse e-mail grâce au code reçu.
4. Activer la double authentification : **Settings → Password and authentication**.

## 2. Configurer Git sur le poste (une seule fois par machine)

1. Ouvrir **Git Bash**.
2. Déclarer son identité, qui apparaîtra dans chaque commit :

```bash
git config --global user.name "John Venien"
git config --global user.email "adresse-du-compte@github.com"
git config --global init.defaultBranch main
```

3. Vérifier la configuration :

```bash
git config --global --list
```

## 3. Créer le dépôt sur GitHub

1. Cliquer sur **+** (en haut à droite) puis **New repository**.
2. Remplir le formulaire :
    1. **Repository name** : `john-venien`
    2. **Description** (facultatif) : « Dépôt de travail BTS SIO »
    3. Visibilité : **Public** (visible sans compte) ou **Private**
    4. Cocher **Add a README file**
3. Cliquer sur **Create repository**.
4. Copier l'adresse du dépôt : bouton vert **Code** → onglet **HTTPS**.

## 4. Récupérer le dépôt sur son poste (clone)

1. Se placer dans le dossier de travail :

```bash
cd "/c/Users/johnv/OneDrive/Documents/Efrei/03-Projets"
```

2. Cloner le dépôt :

```bash
git clone https://github.com/PSEUDO/john-venien.git
cd john-venien
```

3. Vérifier le lien avec GitHub (le dépôt distant s'appelle `origin`) :

```bash
git remote -v
```

## 5. Premier cycle modifier → commit → push

1. Modifier le fichier `README.md`.
2. Vérifier l'état du dépôt :

```bash
git status
```

3. Préparer puis enregistrer le changement, avec un message à l'impératif :

```bash
git add README.md
git commit -m "Présente le dépôt dans le README"
```

4. Envoyer sur GitHub (au premier envoi, une fenêtre de connexion GitHub s'ouvre) :

```bash
git push
```

5. Rafraîchir la page du dépôt sur GitHub : la modification est en ligne.

## 6. Variante : relier un dossier déjà existant

Si le projet existe déjà en local, créer le dépôt GitHub **sans** README, puis :

```bash
git init
git add .
git commit -m "Initialise le projet"
git remote add origin https://github.com/PSEUDO/nom-du-depot.git
git push -u origin main
```

## À retenir

- Git versionne **en local**, GitHub **héberge et partage** en ligne.
- Le cycle de base : **modifier → `git add` → `git commit` → `git push`**.
- Toujours faire `git pull` avant de commencer à travailler.
- Ne **jamais** commiter de mot de passe, de clé ou de jeton (utiliser un fichier `.gitignore`).

Voir aussi : [[Fiche-Git]]
