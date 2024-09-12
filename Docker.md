# Tutoriel : Installation de Docker et Docker Compose sur Fedora

## 1. Installation de Docker

### Mise à jour du système
Commencez par mettre à jour votre système :
```
sudo dnf update -y
```

### Installation des dépendances nécessaires
Installez les packages requis :
```
sudo dnf install -y dnf-plugins-core
```

### Ajout du référentiel Docker
Ajoutez le référentiel Docker officiel :
```
sudo dnf config-manager --add-repo https://download.docker.com/linux/fedora/docker-ce.repo
```

### Installation de Docker
Installez Docker et ses composants :
```
 sudo dnf install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

### Démarrage et activation du service Docker
Démarrez le service Docker et configurez-le pour qu'il démarre au démarrage du système :
```
sudo systemctl start docker
sudo systemctl enable docker
```

### Ajout de votre utilisateur au groupe Docker (optionnel)
Pour utiliser Docker sans sudo, ajoutez votre utilisateur au groupe docker :
```
sudo usermod -aG docker $USER
```
Déconnectez-vous et reconnectez-vous pour que les changements prennent effet.

## 2. Installation de Docker Compose

### Téléchargement de Docker Compose
Téléchargez la dernière version stable de Docker Compose :
```
sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```

### Attribution des permissions d'exécution
Rendez le binaire exécutable :
```
sudo chmod +x /usr/local/bin/docker-compose
```

### Vérification de l'installation
Vérifiez que Docker Compose est correctement installé :
```
docker-compose --version
```

## 3. Vérification de l'installation

Pour vérifier que Docker fonctionne correctement, exécutez :
```
docker run hello-world
```

Si tout est bien configuré, vous devriez voir un message de confirmation.

Félicitations ! Vous avez maintenant Docker et Docker Compose installés sur votre système Fedora.
