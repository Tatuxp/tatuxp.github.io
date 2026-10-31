---
title: "Gestion des accès et des secrets"
weight: 50
statut: "En cours"
resume: "Un standard d'administration commun à tous les serveurs, des clés SSH par serveur gérées dans un coffre, et une organisation des secrets qui reste lisible."
competences: ["SSH", "Durcissement", "Devolutions RDM / DVLS", "Vaultwarden", "Moindre privilège"]
date: 2026-10-30
---

## Contexte

Les accès s'étaient accumulés au fil des installations : comptes différents, mots de passe partagés, clés API éparpillées. Il devenait difficile de savoir qui avait accès à quoi.

## Objectif

Appliquer partout un standard simple et l'outiller pour qu'il soit tenable au quotidien.

## Ce que j'ai mis en place

- Un **standard d'administration** pour toute nouvelle machine :
  - un compte nominatif avec élévation de privilèges protégée par mot de passe ;
  - connexion directe en root interdite ;
  - durcissement de la configuration SSH.
- Une **clé SSH par serveur**, générée et stockée dans le coffre de l'outil de connexion (Devolutions Remote Desktop Manager / Server), et utilisable uniquement depuis le poste d'administration.
- Une **séparation claire des secrets** : les accès aux interfaces web vont dans un gestionnaire de mots de passe auto-hébergé (Vaultwarden), les connexions techniques (SSH, SQL, clés API) dans le coffre d'administration.
- Une **réorganisation du coffre** (environ 75 entrées, faite par script) : une arborescence qui suit le matériel réel, des identifiants rangés à part, des champs personnalisés et des liens vers la documentation et l'inventaire.
- Un script qui crée automatiquement les entrées du coffre (dossier, identifiants, sessions) à chaque nouvelle machine, à partir de modèles.

## Difficultés et solutions

- **Trouver le bon niveau de sécurité** : multiplier les copies de clés sur plusieurs outils et supports devenait trop lourd à maintenir. J'ai retenu un compromis assumé et documenté entre sécurité et exploitabilité.
- **Limites de licence** : impossible de restreindre finement les droits d'une identité applicative. Je l'ai compensé par l'organisation : accès ponctuel et contrôlé plutôt que permanent.

## Ce que j'en retiens

La sécurité qui tient dans la durée est celle qu'on arrive à appliquer tous les jours.
