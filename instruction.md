# TP Kubernetes

Envoyer votre réponse à teaching@glenux.net (en précisant votre nom)

Le rendu doit avoir la forme d'un dépot GIT (public) contenant des fichiers yaml
(et une eventuelle documentation d'usage).

## A. Avec docker-compose

1. vérifier que le fichier docker-compose.yml fourni fonctionne dans
   docker-compose (que vous arrivez à vous connecter sur le port 8080 et que
   wordpress apparait et s'installe)

## AVEC KUBERNETES (préparation)

2. créer un pod pour chaque container présent dans docker-compose 
3. utilisez les meme variables d'environnement que dans la version docker-compose
   (voir `kubectl explain pod.spec.containers.env` si besoin)
3. créer un service pour chaque pod créé (en respectant les ports ouvert dans
   docker-compose)
4. vérifier que ça fonctionne 

## AVEC KUBERNETES Tp1 (préparation)

2. créer un deploiement + service K8S pour chaque "service" présent dans `docker-compose.yml`
  * wp-app: le container wordpress:5.7 (avec 2 répliques)
  * wp-db: le container mariadb:5.7 (avec 1 réplique)
4. créer des configmap ou des secrets pour mutualiser la configuration entre les déploiements
   * BLOG_DB_NAME=blog
   * BLOG_DB_USERNAME=userblog
   * BLOG_DB_PASSWORD=passblog42@
   * BLOG_DB_HOST=wp-db
5. utilisez les meme variables d'environnement que dans la version docker-compose
   (voir `kubectl explain pod.spec.containers.env` si besoin)
5. créer un service pour chaque pod créé (en respectant les ports ouvert dans
   docker-compose)
6. vérifier que ça fonctionne 


## AVEC KUBERNETES Tp2 (déploiement)

5. détruisez les objets présents sur le cluster
6. vérifiez que vous arrivez bien à tout re-créer avec `kubectl apply -f .`
7. vérifier que ça fonctionne encore

## RAPPELS

* kubectl run ...
* kubectl expose ...
* kubectl create ... 
* kubectl get ... -o yaml > fichier

## Réponse
Voici les étapes pour avoir les fichiers yaml
### Creation des fichiers yaml pod et service 
- `kubectl run wordpress-ad --image=wordpress --dry-run=client --port=80 -o yaml > pod.wordpress-ad.yaml`
- `kubectl run mysql-ad --image=mysql:5.7 --dry-run=client  --port=3306 -o yaml > pod.mysql-ad.yaml`
- ajouter les informations du docker-compose pour l'env `kubectl explain pod.spec.containers.env`
- `kubectl create -f . `

- `kubectl expose pod wordpress-ad --type=NodePort -o yaml > service.wordpress-ad.yaml`
- `kubectl expose pod mysql-ad -o yaml > service.mysql-ad.yaml`
- `kubectl delete pod wordpress-ad mysql-ad`
- `kubectl delete service wordpress-ad mysql-ad`

### Creation des fichiers yaml deployment et service 
- `kubectl create deployment wordpress-ad --image=wordpress:5.7 --port=80 --replicas=2 --dry-run=client -o yaml> deployment.wordpress-ad.yaml`

- `kubectl create deployment mysql-ad --image=mysql:5.7 --port=3306 --replicas=1 --dry-run=client -o yaml> deployment.mysql-ad.yaml`

- `kubectl expose deployment wordpress-ad --type=NodePort -o yaml > service.wordpress-ad.yaml`
- `kubectl expose deployment mysql-ad -o yaml > service.mysql-ad.yaml`


### Déploiment avec les fichiers yaml
- `kubectl apply -f .`