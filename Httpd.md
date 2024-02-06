# Mise en place et configuration d'un serveur HTTP (httpd / apache2)

## Sommaire

> **Note** : Précision importante, la configuration des Virtual Hosts est faculative. Si vous n'avez qu'un seul site web à héberger, vous pouvez vous contenter de la configuration par défaut. Et donc ne pas suivre l'étape 3.

1. [Installation de httpd](#installation-de-httpd)
2. [Configuration de httpd](#configuration-de-httpd)
3. [Configuration des virtual hosts](#configuration-des-virtual-hosts)
4. [Configuration du pare-feu](#configuration-du-pare-feu)

## Installation de httpd

Pour installer httpd, il suffit de taper la commande suivante :

```bash
dnf install httpd
```

## Configuration de httpd

Pour activer le démarrage automatique de httpd au démarrage de la machine, il suffit de taper la commande suivante :
```bash
systemctl enable httpd
```

Pour démarrer le service, il suffit de taper la commande suivante : 
```bash
systemctl start httpd
```

## Configuration des virtual hosts

Pour créer un virtual host, il suffit de créer un fichier de configuration dans le dossier ```/etc/httpd/conf.d/```. Par exemple, pour créer un virtual host pour le domaine ```monsite.com```, il suffit de créer un fichier ```/etc/httpd/conf.d/monsite.com.conf``` avec le contenu suivant :

```apache
<VirtualHost *:80>
    ServerName monsite.com
    DocumentRoot /var/www/monsite.com
    ErrorLog /var/log/httpd/monsite.com-error.log
    CustomLog /var/log/httpd/monsite.com-access.log combined
</VirtualHost>
```

Il suffit ensuite de créer le dossier ```/var/www/monsite.com``` et d'y mettre les fichiers de votre site web.

Pour activer le virtual host, il suffit de taper la commande suivante :
```bash
systemctl reload httpd
```

## Configuration du pare-feu

Pour autoriser le trafic HTTP, il suffit de taper la commande suivante :
```bash
firewall-cmd --add-service=http --permanent --zone=public
firewall-cmd --reload
```

Pour autoriser le trafic HTTPS, il suffit de taper la commande suivante :
```bash
firewall-cmd --add-service=https --permanent --zone=public
firewall-cmd --reload
```

> **Note** : Le contenu du site web (fichiers HTML, CSS, JavaScript, etc.) doit être placé dans le dossier ```/var/www/monsite.com``` si utilisation des Virtual Hosts. Sinon, il doit être placé dans le dossier ```/var/www/html```.

> **Note** : Pour tester si le serveur web fonctionne, il suffit de taper l'adresse ```http://localhost``` dans un navigateur web. Si tout est bien configuré, vous devriez voir une page d'accueil.
