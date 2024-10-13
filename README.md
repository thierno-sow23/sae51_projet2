# SAE 51 projet 2: Collectes et traitement des logs

**fait par Carmella NGUIMBI, Darly LAWSON et SOW Thierno**  

**Groupe B BUT3 FA**

## Contexte

Dans le cadre de ce projet, nous avons mis en palce un système de supervision permettant la collecte et de visualisation des logs système d'une machine hôte et ceux  d'un serveur web nginx qui possède uniquement une page web static par défaut à l'aide des outils promtail, loki et grafana.

## Objectif

Notre objectif principal était de :

- Mettre en place une solution de collecte des logs via Promtail et Loki.
- Visualiser les logs collectés dans Grafana pour obtenir des statistiques sur les connexions, notamment le nombre de visites, les logins et les éventuelles erreurs.
- Assurer la persistance des données de Grafana pour éviter la perte des configurations en cas de redémarrage des conteneurs.

# Etapes réalisées

## Installation et configuration de Docker-compose.yaml

- Un fichier docker-compose.yml a été pour automatiser le déploiement des services Grafana, Loki, Promtail et Nginx.
  
- Les services déployés:
   - **Grafana** : pour la visualisation des logs
   - **Loki** : pour le stockage et le traitements des logs
   - **Promtail** : pour la collecte des logs de Nginx et ceux du système
   - **Nginx** : serveur web servant de source de logs à superviser.

## 1- Mise en place de la collecte des logs avevc Promtail

  **Promtail** est un agent de collecte de logs pour le système de surveillance Loki, développé par Grafana Labs. Son rôle principal est de récupérer les logs de différentes sources et de les envoyer à Loki pour stockage et analyse. 

 - Sa configuration dans docker-compose:
   - Image docker: nous avons utiliser l'image officielle de promtail depuis le docker hub : grafana/promtail:2.9.2
   - Volumes: deux volumes (system et nginx) ont été monté pour accéder aux logs du system et ceux de nginx
 
 Ci-dessous le bout de code:  
 
 promtail:  

    image: grafana/promtail:2.9.2
    volumes:
      - /var/log/nginx:/var/log/nginx
      - /var/log:/var/log
      - /home/user/projetlogs/promtail/config.yml:/etc/promtail/config.yml
    command:  
      -config.file=/etc/promtail/config.yml
    networks:
      - loki
  

  ## 2- Stockage et analyse des logs avec Loki

  
 **Loki** est un système de stockage de logs développé par Grafana Labs, conçu pour être à la fois simple et performant. Contrairement à d'autres solutions de stockage de logs qui indexent chaque ligne de log, Loki indexe uniquement les étiquettes (labels) associées aux logs, ce qui le rend léger et rapide.

   ## 3- Visualisation des logs dans Grafana

Grafana est une plateforme de visualisation et d'analyse de données open source qui permet de créer des tableaux de bord interactifs et des graphiques à partir de diverses sources de données, y compris Loki. Son interface utilisateur intuitive permet aux utilisateurs de visualiser des métriques, des logs et d'autres types de données en temps réel.

 ### Ce que grafana peut faire:
  
  - Intégration avec loki comme source de données
  - Création des tableaux de bord
  - Requêtes et filtrages grâce au langage de requête Loki (LogQL) pour intérroger les logs
  - Altertes en temps réel 
     

 ## 4- Gestion des volumes Docker pour persister les données

Dans un environnement Docker, les conteneurs sont par nature éphémères. Cela signifie que toutes les données stockées à l'intérieur d'un conteneur sont perdues lorsque le conteneur est supprimé ou arrêté. Pour cette raison, nous avons penser à la gestion des volumes Docker  pour garantir la persistance des données importantes, telles que les configurations réalisés, le compte de connexion, les dashboards crées, les logs, et les bases de données...

## Procédure de connexion

Se connecter à grafana via l'url: http://localhost:3000 Une fois Grafana démarré, l'utilisateur peut se connecter pour la première fois avec les identifiants par défaut (admin, admin) est ensuite invité à le changer. Une fois loggé, pour que les logs apparaissent dans l'interface de Grafana, il est nécessaire de créer un tableau de bord qui interroge Loki à l'aide des requêtes appropriées. Les utilisateurs peuvent alors visualiser les logs en temps réel, appliquer des filtres pour affiner les résultats, et créer des graphiques ou des alertes basés sur les données de log.

