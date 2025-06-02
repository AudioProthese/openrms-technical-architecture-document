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

Il ne s'agira pas ici de détailler les aspects fonctionnels de la plateforme, qui sont eux détaillés dans un [wiki dédié](https://audioprothese.github.io/openmrs-architecture-documentation/). Ce document se concentre sur l'architecture technique et les choix technologiques qui sous-tendent la mise en œuvre de la plateforme AudioProthèse+.

## Public visé

Ce document s’adresse aux :

- Architectes techniques
- Développeurs
- Ingénieurs DevOps
- Administrateurs système
- Responsables de la sécurité informatique

## Répartition des rôles et responsabilités

**Matteo ZINUTTI**  
*Rôle : Ingénieur DevOps*  
Responsabilités :  

- Mise en œuvre des stacks d'observabilité Open-Source (Grafana, Prometheus, Loki)  
- Synchronisation des secrets Azure

---

**Fabien CHEVALIER**  
*Rôle : Ingénieur DevOps*  
Responsabilités :  

- Mise en place de l'industrialisation de la plateforme (Terraform, Helm, ArgoCD)  
- Gestion des déploiements CI/CD  
- Mise en place de la documentation as code

---

**Hakim AFARMACH**  
*Rôle : Ingénieur DevOps*  
Responsabilités :  

- Mise en place des solutions de sécurité (Oath2, Zero-trust)  
- Mise en place des configurations Kubernetes

---

### Méthodologie de travail

Mise en place de feature branches pour chaque fonctionnalité ou correctif, avec des pull requests pour la revue de code. Organisation de sprints de développement de deux semaines, avec des réunions quotidiennes pour le suivi de l'avancement et la résolution des blocages. Utilisation d'outils de gestion de projet inclus à GitHub pour le suivi des tâches et des bugs.

Le plateforme à été développée en collaboration constante, avec une spécialité pour chaque membre de l'équipe. Les rôles ont été répartis en fonction des compétences et des intérêts de chacun, et sont détaillés ci-dessus.

Un soin important à été apporté à la documentation, tant au niveau du code source (commentaires, README) qu'au niveau de la documentation technique (ce document). La documentation est considérée comme un élément essentiel pour assurer la maintenabilité et la compréhension de l'architecture par les futurs intervenants. Il a d'ailleurs été décidé de mettre en place une documentation as code, permettant de versionner la documentation avec le code source et de la maintenir à jour de manière cohérente. Cette documentation est hébergée sur GitHub et accessible aux membres de l'équipe ainsi qu'aux parties prenantes du projet.

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

Cette section présente sous forme schématique l’architecture technique de la plateforme AudioProthèse+. Elle illustre les différents composants de l’infrastructure, leurs interactions et les flux de données entre eux.

## Diagramme d'architecture globale (Azure/Kubernetes)

![Diagramme d'architecture globale AKS](./imgs/k8s-scheme.png)

### Répartition des namespaces

![Namespaces Kubernetes](./imgs/k8s-namespace.png)

La répartition des namespaces Kubernetes est organisée de manière à isoler les différents environnements et services de la plateforme. Chaque namespace correspond à un environnement spécifique (développement, test, production) ou à un service particulier (frontend, backend, gateway). Dans notre cas, nous avons organisé les namespaces par service, l'environnement de production étant hébergé sur un cluster AKS dédié. Les namespaces sont les suivants :

- **monitoring** : pour les services de supervision (Prometheus, Grafana)
- **loki** : pour le service de collecte et d'analyse des logs (Loki)
- **alloy** : pour le service Alloy, permettant de scrapper les métriques OpenMRS
- **openmrs** : pour les services OpenMRS (frontend, backend, gateway)
- **external-secret-operator** : pour le service de synchronisation des secrets Azure
- **argocd** : pour le service de gestion des déploiements (ArgoCD)
- **app-rooting-system** : pour le service de routage des applications (gateway)
- **cert-manager** : pour la gestion des certificats SSL/TLS

Cette répartition est identique sur tous les environnements (dev, prod).

### Architecture des microservices

L'application OpenRMS consiste en plusieurs microservices :

- **OpenMRS Frontend** : l'interface utilisateur de l'application
- **OpenMRS Backend** : le service backend qui gère la logique métier et les interactions avec la base de données.
- **OpenMRS Gateway** : le service de routage qui permet de diriger les requêtes vers les différents microservices en fonction des routes définies.
- **MariaDB** : la base de données relationnelle utilisée par OpenMRS pour stocker les données des patients et des services.

La communication entre les microservices se fait via des API REST, et chaque service est déployé dans son propre pod Kubernetes. Les services sont configurés pour être accessibles via des Ingress, permettant de gérer les routes et les certificats SSL/TLS.

#### App Routing System

Côté AKS, le load-balancer frontal est configuré pour diriger le trafic vers l'`app-routing-system`, qui est le point d'entrée principal de l'application. `App Routing System` est un service offert par Azure permettant de synchroniser Azure DNS avec les Ingress Kubernetes. Il s'agit d'un proxy `NGINX` managé par Azure.

#### Oath2 Proxy et Zero Trust

![Oath2 Proxy](./imgs/oath2-zero-trust.png)

Prometheus, Alloy et Grafana sont situés derrière un proxy Oath2, qui permet de sécuriser l'accès à ces services en exigeant une authentification via Oath2. La source de vérité pour les utilisateurs est l'annuaire Entra ID, permettant donc aux différents acteurs de se connecter via leurs identifiants Azure pour accéder aux services de supervision et de monitoring.

#### External Secret Operator

External Secret Operator est utilisé pour synchroniser les secrets Azure avec Kubernetes. Il permet de gérer les secrets de manière sécurisée et centralisée, en les stockant dans Azure Key Vault et en les synchronisant automatiquement avec les secrets Kubernetes. Cela permet de garantir que les secrets sont toujours à jour et accessibles aux services qui en ont besoin.

![External Secret Operator](./imgs/external-secret-operator.png)

#### Stack d'observabilité

La stack d'observabilité est composée de plusieurs outils open source permettant de collecter, stocker et visualiser les métriques et les logs des applications et de l'infrastructure. Elle comprend :

- **Prometheus** : pour la collecte des métriques des applications et de l'infrastructure.
- **Grafana** : pour la visualisation des métriques collectées par Prometheus.
- **Loki** : pour la collecte et l'analyse des logs des applications et de l'infrastructure.
- **Alloy** : pour le scrapping des métriques OpenMRS et leur exposition à Prometheus.

**Insérer capture d'écran des dashboards Grafana ici.**

## Configuration Azure Cloud

La sécurité étant un enjeu majeur pour AudioProthèse+, l'architecture Azure est configurée pour garantir un niveau de sécurité élevé. Voici les principales configurations mises en place.

### OIDC pour les pipelines GitHub Actions

![OIDC GitHub Actions](./imgs/oidc-azure.png)

Pour sécuriser les pipelines GitHub Actions, nous avons configuré l'authentification OIDC (OpenID Connect) avec Azure Active Directory. Cela permet aux workflows GitHub Actions de s'authentifier auprès d'Azure sans avoir à gérer des secrets ou des clés d'accès.

Ce système d'authentification permet de garantir que seuls les workflows autorisés peuvent accéder aux ressources Azure, renforçant ainsi la sécurité des déploiements.

### Sécurisation des dépôts GitHub infrastructure

Des règles de sécurité sont appliquées aux dépôts GitHub contenant les fichiers de configuration Terraform et Helm. Ces règles incluent :

- L'utilisation de branches protégées pour les modifications de code
- L'exigence de revues de code avant la fusion des pull requests
- L'activation de l'analyse statique du code avec Trivia au sein des workflows GitHub Actions

### Gestion de l'état des ressources Azure

Le `tfstate` (état des ressources Terraform) est stocké dans un `Azure Storage Account` sécurisé. Cela permet de garantir la cohérence de l'état des ressources et d'éviter les conflits lors des déploiements. Sa mise en place est scriptée au sein d'un fichier `init.sh`, permettant la reproduction de l'environnement de manière automatisée.