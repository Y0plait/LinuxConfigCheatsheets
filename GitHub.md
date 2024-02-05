# Mise en place de Git et GitHub

## Sommaire

1. [Installation de Git](#installation-de-git)
2. [Configuration de Git](#configuration-de-git)
3. [Création d'un dépôt sur GitHub](#création-dun-dépôt-sur-github)
4. [Ajout de fichiers dans le dépôt](#ajout-de-fichiers-dans-le-dépôt)
5. [Mise à jour du dépôt](#mise-à-jour-du-dépôt)
6. [Suppression de fichiers du dépôt](#suppression-de-fichiers-du-dépôt)
7. [Suppression du dépôt](#suppression-du-dépôt)

## Installation de Git

Pour installer Git, il suffit de taper la commande suivante :

```bash
dnf install git
```

## Configuration de Git

Pour configurer Git, il suffit de taper les commandes suivantes :

```bash
git config --global user.name "Votre username"
git config --global user.email "Votre email"
```

## Création d'un dépôt sur GitHub / clonâge d'un dépôt existant

Pour créer un dépôt sur GitHub, il suffit de se rendre sur le site [GitHub](https://github.com) et de cliquer sur le bouton "New" en haut à droite.

Pour cloner un dépôt existant, il suffit de taper la commande suivante :

```bash
git clone [URL du dépôt]
```

## Ajout de fichiers dans le dépôt

Pour ajouter des fichiers dans le dépôt, il suffit de taper les commandes suivantes :

```bash
git add nom_du_fichier
git commit -m "Message de commit"
```

## Mise à jour du dépôt

Pour mettre à jour le dépôt, il suffit de taper les commandes suivantes :

```bash
git push
```

## Suppression de fichiers du dépôt

Pour supprimer des fichiers du dépôt, il suffit de taper les commandes suivantes :

```bash
git rm nom_du_fichier
git commit -m "Message de commit"
```

## Suppression du dépôt

Pour supprimer le dépôt, il suffit de se rendre sur le site [GitHub](https://github.com), de se rendre dans les paramètres du dépôt, puis de cliquer sur le bouton "Delete this repository".