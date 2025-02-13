# RAPPORT - PROJET DE PRÉDICTION DES ANNULATIONS DE RÉSERVATIONS HÔTELIÈRES 

## CONTEXTE : 

Un acteur majeur dans les solutions technologiques pour l'industrie du voyage fait face à un défi majeur : les annulations de réservations d'hôtel. Ces annulations ont un impact significatif sur les revenus des hôtels et sur l'efficacité de notre système de réservation. En 2023, le taux moyen d'annulation dans l'industrie hôtelière était d'environ 30%, représentant des pertes importantes pour nos partenaires hôteliers. OBJECTIF DU PROJET : Développer une solution data end-to-end comprenant un pipeline de données robuste et un modèle prédictif capable d'identifier en amont les réservations à haut risque d'annulation, permettant ainsi aux hôtels d'optimiser leur stratégie de revenue management.

## PHASE 1 - ARCHITECTURE DATA SUR GCP

Configuration initiale GCP

Création d'un nouveau projet GCP
Activation des APIs nécessaires :
Cloud Storage
BigQuery
Cloud Composer (Airflow managé)
Cloud Build
Container Registry
Kubernetes Engine
Pub/Sub
Cloud Functions
Dataflow
Secret Manager
Configuration des rôles IAM et des comptes de service
Mise en place de la facturation et des budgets
Configuration du VPC et des règles de firewall

Mise en place du Data Lake (Cloud Storage)

Création de 3 buckets distincts :
hotel-raw-data : données brutes
hotel-processed-data : données transformées
hotel-config : fichiers de configuration
Configuration du lifecycle management
Mise en place des règles de rétention
Configuration des IAM pour chaque bucket
Activation du versioning
Configuration des règles de transfert de données

Configuration BigQuery

Création des datasets :
raw_data : données brutes
staging : données intermédiaires
prod : données finales
Configuration des tables partitionnées
Mise en place des vues matérialisées
Configuration des jobs de transfert
Définition des politiques de rétention
Configuration des quotas et limites
Mise en place des autorisations par dataset

Déploiement Cloud Composer

Création de l'environnement Composer
Configuration des ressources :
Taille du cluster GKE
Nombre de workers
Version d'Airflow
Configuration du networking
Mise en place des connexions vers BigQuery et Storage
Configuration des variables d'environnement
Mise en place du monitoring
Configuration des backups

## PHASE 2 - DATA INTEGRATION

Pipeline d'Ingestion

Configuration de Cloud Functions pour :
Réception des données API
Validation des données
Transformation initiale
Mise en place de Pub/Sub topics pour :
Nouvelles réservations
Mises à jour
Annulations
Configuration de Dataflow pour le streaming
Mise en place des schémas de validation

Transformation avec dbt sur BigQuery

Installation et configuration de dbt-bigquery
Structuration du projet dbt :
Sources
Staging models
Intermediate models
Mart models
Configuration des tests dbt
Mise en place du scheduling
Configuration des documentations
Déploiement via Cloud Build

Pipeline de Monitoring

Mise en place de Cloud Monitoring
Création des dashboards pour :
Performances des pipelines
Qualité des données
Coûts
Latence
Configuration des alertes
Mise en place des logs exports
Configuration de l'error tracking

Sécurité et Gouvernance

Configuration du DLP (Data Loss Prevention)
Mise en place des politiques de classification
Configuration des règles d'export
Mise en place des audits
Configuration de Cloud Asset Inventory
Mise en place des politiques de sécurité

Disaster Recovery

Configuration des backups automatiques
Mise en place des procédures de restauration
Documentation des procédures d'urgence
Tests de recovery
Configuration de la réplication

Documentation

Architecture technique détaillée
Procédures opérationnelles
Guides de troubleshooting
Documentation des APIs
Guides de maintenance
Plans de continuité

Tests et Validation

Tests de performance
Tests de charge
Tests de failover
Tests de sécurité
Tests d'intégration
Validation des SLAs

Points d'attention spécifiques à GCP :

Optimisation des coûts BigQuery
Gestion des quotas et limites
Configuration du networking
Sécurisation des APIs
Monitoring des coûts
Gestion des identités
Optimisation des performances
