---
title: "Préparation automatisée des serveurs"
weight: 60
statut: "En cours"
resume: "Un serveur de scripts interne et un bootstrap qui appliquent en une commande le standard d'administration à toute nouvelle VM ou conteneur."
competences: ["Bash", "Automatisation", "Alpine Linux", "nginx", "PowerShell"]
date: 2026-10-30
---

## Contexte

Chaque nouvelle machine demandait les mêmes étapes manuelles : compte administrateur, clés, durcissement SSH, compte de diagnostic. Elles étaient longues et sujettes aux oublis.

## Objectif

Qu'une machine neuve soit conforme au standard en une seule commande, et que l'inventaire et le coffre suivent automatiquement.

## Ce que j'ai mis en place

- Un **serveur de scripts** léger (conteneur Alpine + nginx), servi en HTTPS interne. Il ne fait que distribuer les scripts : pas d'application dessus, pour limiter la surface d'attaque.
- Un **script de bootstrap** qui télécharge et exécute la préparation :
  - création du compte administrateur nominatif ;
  - dépôt des clés ;
  - durcissement SSH ;
  - en option, compte de diagnostic en lecture seule.
- Côté coffre, un script **PowerShell** qui crée les entrées de la nouvelle machine à partir de modèles.
- Une convention de nommage et de numérotation des machines, qui permet de déduire les informations utiles du seul identifiant.

## Suite prévue

- Mises à jour centralisées de toutes les VM et conteneurs (**Ansible**).
- Création automatique de la fiche d'inventaire et de la page de documentation.
- Automatiser la publication d'un nouveau service : certificat, entrée DNS, proxy, règle de pare-feu.

## Ce que j'en retiens

On automatise ce qu'on a d'abord fait à la main et documenté. Le script n'est que la procédure écrite, rendue exécutable.
