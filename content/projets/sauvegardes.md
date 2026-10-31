---
title: "Sauvegardes et restauration"
weight: 30
statut: "En cours"
resume: "Des sauvegardes automatiques de toutes les machines virtuelles et conteneurs sur un serveur dédié, avec des restaurations réellement testées."
competences: ["Proxmox Backup Server", "ZFS", "Plan de reprise", "Planification"]
date: 2026-10-29
---

## Contexte

Au départ, les sauvegardes étaient stockées sur le même disque que les machines sauvegardées. Une panne de ce disque aurait tout emporté, sauvegardes comprises.

## Objectif

Séparer physiquement les sauvegardes de la production, les automatiser, et surtout **prouver** qu'on sait restaurer.

## Ce que j'ai mis en place

- **Proxmox Backup Server** migré sur une machine physique dédiée, avec un disque réservé aux sauvegardes.
- Des sauvegardes planifiées chaque soir pour toutes les VM et tous les conteneurs, suivies des tâches de maintenance du datastore (vérification, nettoyage).
- Des **tests de restauration** de conteneurs pour valider la chaîne de bout en bout.
- Le nettoyage des volumes orphelins laissés par les anciennes configurations, une fois leur contenu vérifié.

## Reste à faire

- Sauvegarder automatiquement la **configuration des hyperviseurs et du serveur de sauvegarde** vers un NAS.
- Ajouter une **seconde copie** des sauvegardes sur un autre équipement (règle 3-2-1).
- Démarrer le serveur de sauvegarde à la demande (Wake-on-LAN) et l'éteindre une fois les tâches finies, pour économiser l'énergie.

## Ce que j'en retiens

Une sauvegarde qu'on n'a jamais restaurée n'est qu'une hypothèse.
