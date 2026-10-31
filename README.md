# projets.sunkipa.ovh

Site de présentation de mes projets d'infrastructure, généré avec [Hugo](https://gohugo.io) et publié automatiquement sur GitHub Pages.

## Modifier le site

Tout le contenu est dans `content/`, au format Markdown :

| Fichier | Contenu |
|---|---|
| `content/_index.md` | Texte de la page d'accueil |
| `content/projets/*.md` | Une page par projet |
| `content/feuille-de-route.md` | Chantiers en cours et à venir |
| `hugo.toml` | Nom, sous-titre, liens de contact |

Après chaque modification enregistrée (commit) sur `main`, le site se reconstruit tout seul en une à deux minutes. Le suivi est dans l'onglet **Actions**.

## Ajouter un projet

Créer un fichier `content/projets/mon-projet.md` en copiant un projet existant, puis adapter l'en-tête :

```yaml
---
title: "Titre du projet"
weight: 90            # ordre d'affichage
statut: "En cours"    # Terminé | En cours | Prévu
resume: "Une phrase qui résume le projet."
competences: ["Outil 1", "Outil 2"]
date: 2026-11-01
---
```

## Règles de publication

Ce dépôt est public. Ne jamais y mettre :

- adresses IP, numéros de VLAN, plan d'adressage, convention de numérotation ;
- noms d'hôtes, FQDN internes ou sous-domaines publics des services ;
- versions logicielles, règles de pare-feu ;
- captures d'écran d'interfaces ou schémas réseau réels ;
- mots de passe, clés, jetons (même expirés).

## Tester en local (facultatif)

```bash
hugo server
```
