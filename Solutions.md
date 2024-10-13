# SAE52 - Présentation de solution de collecte et de traitement des logs de fonctionnement

Fait par Carmella NGUIMBI, SOW Thierno et Darly LAWSON

Groupe B BUT3 FA

## Résumé

Ce document de synthèse présente des solutions libres permettant la collecte, la centralisation et la présentation des logs. Notamment leurs points-clés, avantages et inconvénients. Il se compose de la présentation de 3 solutions différentes avec un descriptif de chaque et un tableau comparatif avantages vs inconvenients correspondant:

### I- Fluentd  
### II- Graylog  
### III- Grafana Loki

## I - La solution Fluentd

**Description**  

C'est une solution open source, est une solution de centralisation de logs permettant de combiner plusieurs types de logs à traiter, puis rediriger par Fluentd vers leur traitement respectif (solution supplémentaire): analyse, alerte, archive...

La solution Fluentd permet d'embarquer de nombreux plug-in de source ou de sortie.

Il existe une version avec une interface utilisateur (UI) s'appelant fluentd-ui ainsi qu'une interface utilisateur d'entreprise avec Calyptia.

| Avantages                                                  | Inconvénients                                       |
|------------------------------------------------------------|-----------------------------------------------------|
| - Flexibilité dans la collecte et le routage des logs.     | - Configuration initiale peut être complexe.      |
| - Supporte de nombreux plugins et intégrations.            | - Peut nécessiter des ressources supplémentaires selon l'usage. |


## II - La solution Graylog

**Description**

Graylog est une solution open source de gestion des logs qui offre des capacités de recherche et d'analyse. Il dispose d'une interface utilisateur intuitive et permet une gestion centralisée des logs.

| Avantages                                            | Inconvénients                                       |
|------------------------------------------------------|-----------------------------------------------------|
| - Interface utilisateur intuitive.                  | - Moins populaire que certaines alternatives, ce qui peut entraîner moins de support communautaire. |
| - Capacité de recherche rapide.                     | - Peut être limité en termes de personnalisation.  |

## III - La solution Grafana Loki

**Description**

Grafana Loki est un système de collecte et d'indexation de logs conçu pour s'intégrer facilement avec Grafana. Il permet de collecter des logs à partir de diverses sources tout en offrant une interface simple pour la visualisation des données.

| Avantages                                            | Inconvénients                                       |
|------------------------------------------------------|-----------------------------------------------------|
| - Intégration facile avec Grafana.                 | - Moins de fonctionnalités avancées que d'autres solutions. |
| - Léger et performant.                              | - Indexe uniquement les métadonnées.               |
