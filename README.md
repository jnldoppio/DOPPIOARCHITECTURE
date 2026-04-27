# Doppio Architecture — Site web

Site vitrine construit avec [Jekyll](https://jekyllrb.com) et déployé sur GitHub Pages
via GitHub Actions. Domaine : **doppioarchitecture.com**.

---

## Structure du projet

```
.
├── _config.yml           # Configuration Jekyll
├── _layouts/             # Gabarits HTML (default, page, project)
├── _projects/            # Collection des projets (1 fichier .md par projet)
├── assets/css/main.scss  # Feuille de style principale
├── index.html            # Page d'accueil
├── a-propos.md           # Page À propos
├── projets.html          # Liste des projets
├── contact.html          # Page contact
├── CNAME                 # Domaine personnalisé
└── .github/workflows/    # Déploiement automatique
```

## Lancer le site en local

Prérequis : Ruby ≥ 3.0 et Bundler installés.

```bash
bundle install
bundle exec jekyll serve --livereload
```

Le site est servi sur http://localhost:4000.

## Ajouter un projet

Créer un fichier dans `_projects/` (par ex. `_projects/04-mon-projet.md`) :

```markdown
---
layout: project
title: Nom du projet
location: Ville
year: 2025
summary: Phrase de résumé.
cover: /assets/images/projets/mon-projet/cover.jpg
gallery:
  - /assets/images/projets/mon-projet/01.jpg
  - /assets/images/projets/mon-projet/02.jpg
---

Texte descriptif du projet en Markdown…
```

Place les images dans `assets/images/projets/<slug>/`.

## Déploiement

Le déploiement est automatique : à chaque `git push` sur la branche `main`,
GitHub Actions construit le site et le publie sur GitHub Pages.

Voir `DEPLOIEMENT.md` pour le guide complet de mise en ligne (création
du repo, configuration DNS du domaine, etc.).
