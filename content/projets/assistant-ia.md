---
title: "Assistant IA encadré pour l'exploitation"
weight: 70
statut: "Terminé"
resume: "Un assistant IA relié à l'infrastructure par des connecteurs MCP, avec des droits minimaux et des secrets centralisés hors du poste de travail."
competences: ["IA / MCP", "Python", "API REST", "Moindre privilège", "Sécurité"]
date: 2026-10-29
---

## Contexte

Un assistant IA est utile pour diagnostiquer, documenter ou auditer, à condition de pouvoir lire l'état réel de l'infrastructure. Lui donner des accès pose immédiatement la question du contrôle.

## Objectif

Donner à l'assistant une **visibilité** sur l'infrastructure sans lui donner la **main** : il propose, je décide et j'exécute.

## Ce que j'ai mis en place

- Un conteneur dédié qui héberge tous les **connecteurs MCP** : hyperviseur, sauvegardes, réseau, inventaire, wiki, coffre (via un export nettoyé) et diagnostic SSH.
- Pour chaque connecteur, un **compte technique à droits minimaux** : rôles d'audit ou de lecture seule, jetons restreints par adresse source, écriture limitée à un espace dédié du wiki.
- Un **compte SSH de diagnostic** en lecture seule, déployé sur les serveurs.
- Plus **aucun jeton sur le poste de travail** : le client se connecte au conteneur par SSH, avec des clés dédiées à commande forcée.
- Quelques connecteurs écrits sur mesure en Python, quand aucun connecteur existant ne convenait.

## Difficultés et solutions

- **Droits trop larges au départ** sur certains jetons. Je les ai ramenés au strict nécessaire après revue.
- **Coupures de session** sur inactivité. Je les ai corrigées par la configuration SSH côté client (keepalive).

## Ce que j'en retiens

Intégrer l'IA dans l'exploitation, c'est surtout un projet de gestion des droits : chaque accès est explicitement accordé, limité et révocable.
