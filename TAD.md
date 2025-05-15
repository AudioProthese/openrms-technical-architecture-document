---
title: "Document d'Architecture Technique"
subtitle: "AudioProthese+"
author:
  - Matteo ZINUTTI
  - Fabien CHEVALIER
  - Hakim AFARMACH
date: "2025-05-15"
titlepage: true
titlepage-logo: "icon.jpeg"
logo: "icon.jpeg"
logo-width: "35mm"
toc: true
toc-own-page: true
keywords: [AudioProthese+, Technical Architecture, Documentation]
lang: fr
titlepage-background: "background/background.pdf"
titlepage-rule-color: "000000"
---

# Introduction

## Objectif du document

Ce document d’architecture technique a pour objectif de présenter, de manière détaillée et structurée, l’architecture de la plateforme AudioProthese+. Il s’adresse principalement aux architectes, développeurs, administrateurs système et toute personne impliquée dans la conception, le déploiement et l’exploitation du système d’information.

## Contexte

AudioProthèse+ est un réseau de centres d'audioprothèse implanté dans plusieurs villes en France, offrant des services de diagnostic, d'appareillage et de suivi pour les personnes souffrant de troubles auditifs.

Avec une présence dans plus de 50 villes et un siège social à Paris, l'entreprise gère des données sensibles de patients et utilise des équipements médicaux de pointe connectés.

Face à l'augmentation des cybermenaces dans le secteur de la santé et à la nécessité de se conformer aux réglementations strictes en matière de protection des données médicales, AudioProthèse+ a décidé de renforcer significativement sa sécurité informatique.

Pour se faire, l'entreprise souhaite mettre en place et déployer des solutions d’automatisation, de résilience et d’observabilité afin d’améliorer la fiabilité de son infrastructure. Ce projet ambitieux vise à concevoir et déployer l'infrastructure nécessaire de manière automatisée, en utilisant des pratiques DevOps et des solutions open source. L'objectif est de créer une infrastructure flexible, évolutive et économiquement efficace, tout en garantissant un niveau de sécurité optimal pour protéger les données des patients et l'intégrité des systèmes d'AudioProthèse+.

## Portée du document

Ce document couvre l’ensemble des aspects techniques de la plateforme, notamment :

- L’architecture globale du système
- Les choix technologiques (Kubernetes, microservices, CI/CD, etc.)
- Les composants principaux et leurs interactions
- Les principes de sécurité et de haute disponibilité
- Les stratégies de déploiement et de supervision

## Public visé

Ce document s’adresse aux :

- Architectes techniques
- Développeurs
- Ingénieurs DevOps
- Administrateurs système
- Responsables de la sécurité informatique

## Présentation des outils et solutions techniques

Dans le cadre de l’industrialisation et de la supervision de la plateforme AudioProthèse+, plusieurs outils et services ont été sélectionnés afin de garantir la sécurité, la fiabilité et la scalabilité de l’infrastructure. Le choix de ces solutions s’inscrit dans une démarche DevOps et repose sur des technologies open source et des services cloud éprouvés.

Cette section présente les outils et solutions retenus, ainsi que leurs rôles respectifs dans l’architecture technique de la plateforme. Le détail des configurations et leur justification seront abordés dans les sections suivantes.

### Azure Cloud

Azure est la plateforme cloud choisie pour héberger l’ensemble de l’infrastructure d’AudioProthèse+. Azure offre une large gamme de services cloud, notamment des machines virtuelles, des bases de données, des services de stockage et des outils de gestion et de sécurité. L’utilisation d’Azure permet à AudioProthèse+ de bénéficier d’une infrastructure scalable, résiliente et sécurisée, tout en réduisant les coûts d’exploitation.

### Kubernetes via AKS

Kubernetes est utilisé comme orchestrateur de conteneurs pour le déploiement et la gestion de l’application OpenMRS. Il permet d’automatiser la mise à l’échelle, la résilience et la maintenance des services applicatifs, tout en offrant une grande flexibilité dans la gestion des ressources. Nous utilisons AKS (Azure Kubernetes Service) pour bénéficier d’une solution managée, simplifiant ainsi la gestion de l’infrastructure sous-jacente.

Le cluster Kubernetes hébergera :

- Les microservices de l’application OpenMRS (frontend/backend et gateway)
- Les bases de données (MariaDB)
- Les services de supervision et de sécurité (Prometheus, Grafana, Loki)
- Les outils de déploiement continu (ArgoCD)

### GitHub et GitHub Actions

GitHub est utilisé comme plateforme de gestion de code source et de collaboration pour l’équipe de développement. Les dépôts GitHub contiennent le code source des microservices, ainsi que les fichiers de configuration nécessaires au déploiement sur Kubernetes.

GitHub Actions est utilisé pour automatiser les processus de CI/CD (Intégration Continue / Déploiement Continu). Il permet de construire, tester et déployer automatiquement les applications à chaque modification du code source. Les workflows GitHub Actions sont configurés pour interagir avec le cluster Kubernetes et déployer les nouvelles versions des microservices.

### Industrialisation et outils DevOps

L’industrialisation de la plateforme repose sur plusieurs outils et pratiques DevOps, notamment :

- **Terraform** : utilisé pour la gestion de l’infrastructure en tant que code (IaC). Terraform permet de définir et de provisionner l’infrastructure Azure de manière automatisée et reproductible.
- **Helm** : utilisé pour la gestion des packages Kubernetes. Helm permet de simplifier le déploiement et la gestion des applications sur Kubernetes en utilisant des charts, qui sont des ensembles de fichiers de configuration.
- **ArgoCD** : utilisé pour la gestion des déploiements Kubernetes. ArgoCD permet de synchroniser l’état de l’application avec le code source, garantissant ainsi que les déploiements sont toujours à jour et conformes aux spécifications.
- **Prometheus** : utilisé pour la collecte et la surveillance des métriques des applications et de l’infrastructure. Prometheus permet de suivre les performances et la santé des services déployés sur Kubernetes.
- **Grafana** : utilisé pour la visualisation des métriques collectées par Prometheus. Grafana permet de créer des tableaux de bord personnalisés pour surveiller l’état de l’infrastructure et des applications.
- **Loki** : utilisé pour la collecte et l’analyse des logs des applications et de l’infrastructure. Loki permet de centraliser les logs et de faciliter leur recherche et leur analyse.
- **SonarQube** : utilisé pour l’analyse statique du code source. SonarQube permet de détecter les problèmes de qualité du code, les vulnérabilités et les problèmes de sécurité.

# Architecture technique

