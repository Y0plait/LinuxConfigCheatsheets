# Tutoriel : Installation de GLPI avec Docker sur Linux

## Prérequis
- Docker et Docker Compose installés sur votre système Linux
- Git installé sur votre système

## Étapes d'installation

### 1. Cloner le dépôt

Ouvrez un terminal et exécutez la commande suivante :

```bash
git clone https://github.com/elestio-examples/glpi.git
cd glpi
```

### 2. Configurer le fichier .env

Copiez le fichier .env d'exemple et modifiez-le avec vos propres valeurs :

```bash
cp ./tests/.env ./.env
```

Ouvrez le fichier .env avec votre éditeur de texte préféré :

```bash
nano .env
```

**IMPORTANT** : Assurez-vous de remplir le fichier .env avec les informations finales/de production avant de démarrer le conteneur. Cela inclut :

- ADMIN_EMAIL
- ADMIN_PASSWORD
- DOMAIN
- MYSQL_ROOT_PASSWORD
- MYSQL_DATABASE
- MYSQL_USER
- MYSQL_PASSWORD

### 3. Lancer GLPI avec Docker Compose

Une fois le fichier .env correctement configuré, lancez les conteneurs avec la commande suivante :

```bash
docker-compose up -d
```

Cette commande va télécharger les images nécessaires et démarrer les conteneurs en arrière-plan.

### 4. Accéder à GLPI

Une fois les conteneurs démarrés, vous pouvez accéder à l'interface web de GLPI à l'adresse suivante :

```
http://votre-domaine:22571
```

Remplacez `votre-domaine` par l'adresse IP de votre serveur ou le nom de domaine que vous avez configuré.

## Maintenance

### Consulter les logs

Pour voir les logs des conteneurs :

```bash
docker-compose logs -f
```

### Arrêter les conteneurs

Pour arrêter tous les conteneurs :

```bash
docker-compose down
```

### Sauvegarder et restaurer

1. Arrêtez les conteneurs :
   ```bash
   docker-compose down
   ```

2. Créez une archive ZIP du répertoire :
   ```bash
   zip -r glpi_backup.zip .
   ```

3. Pour restaurer, décompressez l'archive dans le répertoire original :
   ```bash
   unzip glpi_backup.zip -d /chemin/vers/repertoire/original
   ```

4. Redémarrez les conteneurs :
   ```bash
   docker-compose up -d
   ```

## Conclusion

Vous avez maintenant GLPI installé et fonctionnel sur votre système Linux en utilisant Docker. N'oubliez pas de sauvegarder régulièrement vos données et de maintenir vos conteneurs à jour.
