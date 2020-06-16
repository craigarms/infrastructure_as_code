# Infrastructure As Code

## Introduction

*L’objectif du TP est de construire et faire fonctionner un « Pipeline » CI/CD pour la gestion d’un « parc » de serveurs Windows et Linux.*

Les éléments de notre Pipeline seront :

- Gogs : Le gestionnaire de version de source

- Drone : Le « Build » Server capable de lancer les tests d’intégration

o Docker : Dépendance de Drone pour lancer les tests mais aussi gestionnaire des conteneurs Drone et Gogs

- Ansible / Vargrant : L’outil d’orchestration qui permettra de déployer l’infrastructure de notre Pipeline

- VMware / Hyper-V / Virtualbox / Azure / GCP / AWS : L’outil de virtualisation de l’infrastructure, on-premise ou à distance.

## Topologie logique de l’infrastructure

![Schema0](https://i.imgur.com/15bX8Ki.png)


**Objectif de fonctionnement de la « Pipeline »**


Modification de l’infrastructure (via le code)
![schema1](https://i.imgur.com/Gb6C1Zk.png)

1. Clone du repository contenant l’infrastructure as code
2. Modification du code (fichier de variable de l’infrastructure)
3. Commit & Push des modifications sur le repository central

**Déclenchement du Build**

![schema2](https://i.imgur.com/MPNtuc1.png)

4. Déclenchement du Webhook de Push de Gogs vers Drone
5. Lancement des « Test » d’intégrations - Qui ne seront dans notre cas que la livraison/configuration des serveurs
6. Configuration des Applications / Features / Rôle etc… - Livraison de la configuration

## Liens utiles

- https://github.com/craigarms/gogs_bare_docker/blob/master/docker-compose.yml
- https://github.com/craigarms/infrastructure_as_code
