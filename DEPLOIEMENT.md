# Guide de déploiement — Doppio Architecture

Ce guide te conduit pas à pas de ton dossier local jusqu'au site en ligne sur **doppioarchitecture.com**.

---

## 1. Créer le dépôt GitHub

1. Va sur https://github.com/new
2. **Repository name** : `doppio-architecture` (ou le nom de ton choix)
3. Visibilité : **Public** (obligatoire pour GitHub Pages gratuit, sauf si tu as un compte Pro)
4. **Ne coche rien** d'autre (ni README, ni .gitignore — déjà créés ici)
5. Clique sur **Create repository**

GitHub affiche ensuite l'URL du repo, par exemple :
`https://github.com/<ton-utilisateur>/doppio-architecture`

---

## 2. Pousser le site depuis ton ordinateur

Ouvre un terminal dans le dossier du site (`SITE DOPPIO`) et exécute :

```bash
git init
git add .
git commit -m "Initial commit — site Doppio Architecture"
git branch -M main
git remote add origin https://github.com/<ton-utilisateur>/doppio-architecture.git
git push -u origin main
```

Remplace `<ton-utilisateur>` par ton nom d'utilisateur GitHub.

---

## 3. Activer GitHub Pages

1. Sur GitHub, ouvre ton repo → **Settings** → **Pages** (menu de gauche)
2. **Source** : sélectionne **GitHub Actions** (et non « Deploy from a branch »)
3. C'est tout — le workflow `.github/workflows/jekyll.yml` se déclenche automatiquement au prochain push.

Va dans l'onglet **Actions** pour suivre la build. Une fois verte, le site est en ligne sur :
`https://<ton-utilisateur>.github.io/doppio-architecture/`

---

## 4. Connecter le domaine doppioarchitecture.com

### a) Côté GitHub

Le fichier `CNAME` est déjà présent — GitHub détectera automatiquement le domaine.
Vérifie dans **Settings → Pages** que `doppioarchitecture.com` apparaît bien dans le champ **Custom domain**.

Coche également **Enforce HTTPS** une fois le DNS propagé (cela peut prendre 1 à 24 h).

### b) Côté registrar (là où tu as acheté le domaine)

Connecte-toi à l'interface DNS de ton registrar (OVH, Gandi, Namecheap, Google Domains, etc.) et ajoute :

**4 enregistrements `A` pour le domaine racine** (`@`) :

| Type | Hôte | Valeur |
|------|------|--------|
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |

**1 enregistrement `CNAME` pour le sous-domaine www** :

| Type | Hôte | Valeur |
|------|------|--------|
| CNAME | www | `<ton-utilisateur>.github.io.` |

> ⚠️ Le point final après `.github.io.` est important sur certains registrars.

Supprime tout ancien enregistrement A ou CNAME conflictuel sur `@` et `www`.

### c) Vérifier la propagation

Après quelques minutes (jusqu'à 24 h), tester :

```bash
dig doppioarchitecture.com +short
dig www.doppioarchitecture.com +short
```

Tu dois voir les IP `185.199.108-111.153` ou ton URL `*.github.io`.

Tu peux aussi utiliser https://www.whatsmydns.net pour visualiser la propagation.

---

## 5. Mettre à jour le site

Pour toute modification ultérieure :

```bash
git add .
git commit -m "Mise à jour du contenu"
git push
```

Le site se redéploie automatiquement en 1 à 2 minutes.

---

## 6. Personnaliser

Avant la mise en ligne, pense à compléter / remplacer :

- `_config.yml` — email, comptes Instagram / LinkedIn
- `a-propos.md` — texte de présentation, équipe
- `_projects/*.md` — tes vrais projets (les 3 fournis sont des exemples)
- `contact.html` — adresse, téléphone, et **l'ID Formspree** (créer un compte gratuit sur https://formspree.io et remplacer `VOTRE_ID`)
- Ajouter tes images dans `assets/images/projets/<slug>/`

---

## En cas de souci

- **Build qui échoue dans Actions** : vérifie l'onglet Actions sur GitHub, le log indique la ligne précise.
- **Site accessible mais avec un mauvais style (CSS cassé)** : vérifie que `baseurl: ""` dans `_config.yml`.
- **Domaine qui ne pointe pas** : la propagation DNS peut prendre jusqu'à 24 h.

Bonne mise en ligne.
