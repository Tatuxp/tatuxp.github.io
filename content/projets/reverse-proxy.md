---
title: "Reverse proxy et publication des services"
weight: 20
statut: "Terminé"
resume: "Un point d'entrée unique en HTTPS pour toutes les applications, avec une séparation nette entre l'accès interne et une éventuelle exposition externe."
competences: ["Reverse proxy", "Nginx Proxy Manager", "SWAG / CrowdSec", "TLS", "DNS", "Pare-feu"]
date: 2026-10-28
---

## Contexte

Chaque application était joignable directement, sur son adresse et son port, souvent en HTTP. Ce n'était ni pratique (des ports à retenir) ni sain (des flux en clair, des règles de pare-feu dispersées).

## Objectif

Centraliser l'accès : chaque service a un nom lisible, est servi en HTTPS, et seul le proxy est autorisé à joindre les applications.

## Ce que j'ai mis en place

- Un **reverse proxy interne** (Nginx Proxy Manager) qui publie les applications sous des noms DNS internes, avec le certificat wildcard de la PKI maison.
- Un **reverse proxy distinct dédié à l'externe** (SWAG avec CrowdSec), isolé dans une zone réseau à part. Je ne mélange pas l'interne et l'externe sur le même composant.
- Un certificat public wildcard obtenu par **défi DNS** chez le registrar (clé API dédiée, aux droits limités), pour les services qui doivent avoir le même nom en interne et en externe.
- Le DNS interne géré en un seul endroit (BIND), avec un filtrage DNS en amont.
- Les règles de pare-feu entre zones réduites au strict nécessaire : les applications n'acceptent plus que le proxy.
- Les applications reconfigurées pour fonctionner derrière un proxy (URL publique, proxys de confiance, en-têtes).

## Difficultés et solutions

- **Applications sensibles au proxy** : certaines refusaient les requêtes (protection CSRF, hôtes autorisés, en-têtes réécrits). Je les ai corrigées application par application, et j'ai noté la correction dans la documentation.
- **Exposition externe** : après un premier essai, j'ai **coupé l'accès entrant**. Je ne le rouvrirai qu'une fois la sécurisation finie (SSO, filtrage). Désactiver est parfois la meilleure décision de sécurité.

## Ce que j'en retiens

Un reverse proxy est aussi un outil de sécurité : il réduit la surface exposée et centralise TLS et la journalisation.
