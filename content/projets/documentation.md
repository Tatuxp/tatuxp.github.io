---
title: "Documentation vivante et inventaire"
weight: 40
statut: "En cours"
resume: "Une base documentaire pensée pour dépanner et reconstruire, des schémas réseau maintenus au fil de l'eau et un inventaire comme source de vérité."
competences: ["BookStack", "draw.io", "NetBox", "Documentation technique", "Inventaire / DCIM"]
date: 2026-10-30
---

## Contexte

Le savoir était dispersé entre des notes, des fichiers et ma mémoire. Après quelques semaines, il devenait difficile de savoir *pourquoi* un réglage avait été fait.

## Objectif

Pouvoir, à partir de la seule documentation, **dépanner** ou **reconstruire** n'importe quel service.

## Ce que j'ai mis en place

- Un wiki **BookStack**, organisé en livres par domaine (PKI, reverse proxy, réseau, hyperviseur et sauvegardes, accès SSH, conteneurs…). J'applique des règles de rédaction strictes :
  - un sujet par page ;
  - des procédures complètes, sans « voir ailleurs » ;
  - le contenu intégral des scripts utilisés ;
  - chaque blocage rencontré, avec sa solution.
- **draw.io** intégré au wiki : les schémas réseau (vues physique et logique) se modifient directement dans les pages.
- **NetBox** comme inventaire : site, emplacements, équipements, modèles matériels, VLAN, adressage IP, machines virtuelles.
- Des liens croisés entre l'inventaire, le wiki et le coffre d'accès.

## Difficultés et solutions

- **Vue topologique automatique** : le plugin testé n'était pas assez lisible. J'ai choisi des schémas draw.io maintenus à la main, mais intégrés au wiki.
- **Discipline** : la documentation se fait *pendant* le chantier, pas après. Sinon, elle ne se fait jamais.

## Ce que j'en retiens

Une bonne documentation d'exploitation répond à « comment je remets ça en marche à 2 h du matin ».
