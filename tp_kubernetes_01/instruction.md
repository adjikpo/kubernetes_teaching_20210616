# TP Kubernetes n°1

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

## AVEC KUBERNETES (déploiement)

5. détruisez les objets présents sur le cluster
6. vérifiez que vous arrivez bien à tout re-créer avec `kubectl apply -f .`
7. vérifier que ça fonctionne encore

## RAPPELS

* kubectl run ...
* kubectl expose ...
* kubectl get ... -o yaml > fichier