# LinuxConfigCheatsheets
Petite liste de tutos pour configurer différents services sur Linux.

### Avant de commencer:

> **Important**: les commandes présentes dans les différents fichier sont destinées à être utilisées sur des systèmes basés sur Fedora / AlmaLinux. Pour les systèmes basés sur Debian, il faudra remplacer ```dnf``` par ```apt```, et ```firewall-cmd``` par ```ufw```.

La plupart des commandes devront être réalisés en tant qu'administrateur. Pour éviter de devoir mettre ```sudo``` devant toutes les commandes, il est conseillé de se mettre en "root" avec la commande ```sudo su```.

#### Utilisation de nano (éditeur de texte)

Pour éditer les fichiers de configuration, il est conseillé d'utiliser l'éditeur de texte ```nano```. Pour l'installer, il suffit de taper la commande suivante : 
```bash
dnf install nano
```
Pour éditer un fichier, il suffit de taper la commande suivante :
```bash
nano /chemin/vers/le/fichier
```
Pour sauvegarder les modifications, il suffit de taper ```Ctrl + O```, puis ```Entrée```. Pour quitter l'éditeur, il suffit de taper ```Ctrl + X```.

## Sommaire

- [Bind9](Bind9.md)
- [Docker](Docker.md)
- [GitHub / Git](GitHub.md)
- [Httpd / Apache](Httpd.md)
- [MariaDB](MariaDB.md)