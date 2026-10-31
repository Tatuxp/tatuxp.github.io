---
title: "PKI interne et gestion des certificats"
weight: 10
statut: "Terminé"
resume: "Une autorité de certification privée pour que tous les services internes soient en HTTPS avec des certificats de confiance, sans alerte de sécurité dans les navigateurs."
competences: ["PKI / X.509", "step-ca", "ACME", "TLS", "DNS"]
date: 2026-10-20
---

## Contexte

Les interfaces d'administration internes (hyperviseur, sauvegardes, outils web) utilisaient des certificats auto-signés, chacun différent. Résultat : des alertes à chaque connexion, et une habitude dangereuse, celle de cliquer sur « continuer quand même ».

## Objectif

Disposer d'une chaîne de confiance unique pour le domaine interne. La racine est installée une seule fois sur les postes d'administration, et chaque service reçoit ensuite un certificat valide.

## Ce que j'ai mis en place

- Une autorité de certification **step-ca** à deux niveaux : une racine, qui reste à l'écart, et une autorité intermédiaire qui signe les certificats.
- Deux modes d'émission :
  - **ACME**, pour les services capables de renouveler seuls leur certificat (même protocole que Let's Encrypt) ;
  - **émission manuelle**, pour les autres, avec une procédure écrite reproductible.
- Un **certificat wildcard interne**, porté par le reverse proxy, pour éviter de gérer un certificat par application.
- La racine intégrée au reverse proxy (image de conteneur reconstruite) pour qu'il fasse confiance aux backends internes en HTTPS.
- Une procédure documentée de bout en bout : enregistrement DNS, émission, import, vérification.

## Difficultés et solutions

- **Inspection TLS de l'antivirus** : le poste d'administration remplaçait les certificats à la volée et cassait la chaîne. J'ai exclu le domaine interne de l'inspection.
- **Renouvellement** : un certificat par application devenait vite ingérable. Je suis passé au wildcard derrière le reverse proxy, et l'ACME est réservé aux services qui le gèrent nativement.

## Ce que j'en retiens

Une PKI tient moins à l'outil qu'à la discipline autour : durées de validité, procédure d'émission écrite, et inventaire de ce qui a été émis.
