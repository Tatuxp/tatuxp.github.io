---
title: "Virtualisation et sobriété des ressources"
weight: 80
statut: "Terminé"
resume: "Faire tenir une vingtaine de services sur un mini-PC : réglage de la mémoire, démarrage ordonné, économies d'énergie et maintenance automatisée."
competences: ["Proxmox VE", "LXC / KVM", "ZFS", "Linux", "systemd", "Docker"]
date: 2026-10-29
---

## Contexte

L'infrastructure tourne sur un mini-PC peu gourmand, mais limité en mémoire. Les services s'ajoutant, la mémoire saturait.

## Objectif

Rendre de la marge sans dégrader le service, et rendre le démarrage complet fiable et prévisible.

## Ce que j'ai mis en place

- **Conteneurs LXC** privilégiés aux VM chaque fois que c'est possible. Les applications Docker sont regroupées sur une VM, avec une arborescence normalisée (`/opt/stacks`, `/opt/appdata`).
- Une **mémoire allouée au plus juste** pour chaque machine. Le ballooning est désactivé là où il perturbait l'application.
- Un **cache ZFS (ARC) plafonné**, et un **swap compressé en RAM (zram)**.
- Un **ordre et des délais de démarrage** définis : le DNS et les services d'infrastructure d'abord, les applications ensuite. Les services occasionnels sont en démarrage manuel.
- Un **gouverneur CPU économe** et un nettoyage automatique des anciens noyaux (script et timer systemd).
- La normalisation des identifiants de machines, en cohérence avec l'inventaire.

## Ce que j'en retiens

Avant d'acheter du matériel, mesurer et régler. L'extension mémoire reste prévue, mais elle est maintenant justifiée par des chiffres.
