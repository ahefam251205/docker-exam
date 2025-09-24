#  Docker Cheatsheet - Fondamentaux

## 1. Vérifications de base
```
docker --version : Affiche la version du client Docker installé  
docker info : Affiche des informations détaillées sur Docker et l’hôte  
docker version : Affiche la version du client et du serveur Docker  
```

## 2. Gestion des images
```
docker search <image> : Chercher une image sur Docker Hub  
docker pull <image> : Télécharger une image  
docker pull <image>:<tag> : Télécharger une version spécifique d’une image  
docker images : Lister les images locales  
docker rmi <image_id> : Supprimer une image locale  
docker tag <image> <new_tag> : Renommer ou retagger une image  
```

## 3. Gestion des conteneurs  
### Créer et exécuter
```
docker run <image> : Créer et démarrer un conteneur  
docker run -it <image> /bin/bash : Lancer un conteneur interactif avec bash  
docker run -d <image> : Exécuter un conteneur en arrière-plan (détaché)  
docker run --name <nom> <image> : Démarrer un conteneur avec un nom personnalisé  
docker run -p 8080:80 <image> : Mapper un port (host:container)  
docker run -v /host:/container <image> : Monter un volume local dans le conteneur  
```

### Lister et inspecter
```
docker ps : Lister les conteneurs en cours d’exécution  
docker ps -a : Lister tous les conteneurs (y compris arrêtés)  
docker logs <container_id> : Afficher les logs d’un conteneur  
docker inspect <container_id> : Voir les informations détaillées d’un conteneur  
```

### Arrêter / supprimer
```
docker stop <container_id> : Arrêter un conteneur  
docker start <container_id> : Démarrer un conteneur arrêté  
docker restart <container_id> : Redémarrer un conteneur  
docker rm <container_id> : Supprimer un conteneur arrêté  
docker rm -f <container_id> : Forcer la suppression d’un conteneur (même actif)  
docker prune : Supprimer tous les conteneurs arrêtés, réseaux inutilisés, caches…  
```

## 4. Dockerfile - Construire une image
\`\`\`dockerfile
FROM ubuntu:22.04
LABEL maintainer="bob@example.com"
RUN apt update && apt install -y curl
WORKDIR /app
COPY . /app
CMD ["bash"]
\`\`\`
```
docker build -t monimage:1.0 . : Construire une image à partir d’un Dockerfile  
```

## 5. Volumes - Gestion des données
```
docker volume create monvolume : Créer un volume persistant  
docker volume ls : Lister les volumes disponibles  
docker run -v monvolume:/data <image> : Monter un volume dans un conteneur  
docker volume rm monvolume : Supprimer un volume  
```

## 6. Réseaux Docker
```
docker network ls : Lister les réseaux existants  
docker network create monreseau : Créer un réseau personnalisé  
docker run --network monreseau <image> : Attacher un conteneur à un réseau  
docker network inspect monreseau : Inspecter les détails d’un réseau  
```

## 7. Docker Compose - Multi-conteneurs  
### Exemple `docker-compose.yml`
\`\`\`yaml
version: '3'
services:
  web:
    image: nginx
    ports:
      - "8080:80"
  db:
    image: mysql
    environment:
      MYSQL_ROOT_PASSWORD: rootpass
\`\`\`
### Commandes utiles
```
docker-compose up -d : Lancer les services définis dans docker-compose.yml  
docker-compose down : Arrêter et supprimer les services, réseaux et volumes associés  
docker-compose logs -f : Suivre les logs des services en temps réel  
docker-compose ps : Lister les services actifs du projet Compose  
```

## 8. Commandes avancées
```
docker exec -it <container_id> /bin/bash : Entrer dans un conteneur déjà en cours  
docker commit <container> monimage : Créer une nouvelle image à partir d’un conteneur  
docker save -o image.tar <image> : Exporter une image au format tar  
docker load -i image.tar : Importer une image depuis un fichier tar  
docker stats : Afficher l’utilisation des ressources en temps réel (CPU, RAM, réseau)  
```
