# Monitoring Platform

Plateforme de surveillance reseau deployee automatiquement.

## Objectif
Superviser le reseau avec ntopng, Smokeping et tshark, deployes sur kubernetes (Minikube) via un pipeline CI/CD.

## Architecture
GitHub -> Jenkins -> Docker (build + push Docker Hub) -> Minikube (kubectl apply)

Le Poll SCM de Jenkins verifie GitHub toutes les 2 minutes et lance le pipeline automatiquement.

## Structure du depot
- docker/ : un Dockerfile par outil (ntopng, smokeping, tshark)
- k8s/ : manifests Kubernetes
- Jenkinsfile : pipeline Build, Push, Deploy

## Acces aux interfaces
- ntopng : http://192.168.49.2:32356
- smokeping : http://192.168.49.2:32491/smokeping/
- tshark : pas d interface web (CLI)

## Problemes rencontres et solutions
- Reseau/DNS de la VM instable : VM en NAT, DNS verifie.
- ntopng introuvable sur Ubuntu 24.04 : image officielle ntop/ntopng:latest.
- Dockerfile casse par un copie-coller : RUN sur une seule ligne.
- Token Docker Hub refuse : nouveau token Read et Write dans Jenkins.
- Deploy en echec : kubeconfig copie pour lutilisateur jenkins.
- Pas de build automatique : Poll SCM active dans le job.

## Avancement
- [x] Phases 0 a 8 terminees
