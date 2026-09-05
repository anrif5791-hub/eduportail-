# EDUPORTAIL

Portail multi-espaces pour la gestion scolaire (Super Administrateur, Chef d'établissement, Professeur, Élève, Parent) — Académie de La Réunion.

## État actuel du prototype

Ce dépôt contient la **première brique** : l'espace **Super Administrateur** (thème violet), avec :

- **Établissements** — registre des établissements (RNE, nom, commune, type) + création d'un nouvel établissement.
- **Inscription élève** — fiche d'identité complète (état civil, informations administratives, coordonnées), indexée par numéro national (INE).
- **Bulletins officiel (INE)** — recherche d'un élève par son INE, pour retrouver sa fiche quel que soit l'établissement qui l'a inscrit.

Les autres espaces (Chef d'établissement, Professeur, Élève, Parent) sont prévus dans la page de connexion mais pas encore développés.

## ⚠️ Important avant toute utilisation réelle

1. **Hébergement sur GitHub Pages** : GitHub Pages ne sert que du contenu **statique** (HTML/CSS/JS). Il n'y a pas de serveur, pas de base de données, pas d'authentification côté serveur.
2. **Stockage des données** : dans ce prototype, tout est enregistré dans le `localStorage` du navigateur (voir `js/data.js`). Cela veut dire :
   - les données restent **sur l'ordinateur qui les saisit**, elles ne sont pas partagées entre le Super Administrateur et les futurs espaces "Chef d'établissement" tant qu'il n'y a pas de vrai backend ;
   - il n'y a **aucune vraie protection par mot de passe** ni chiffrement des données ;
   - rien n'est adapté pour stocker de vraies données d'élèves mineurs (état civil, adresse, numéro national, etc.) en conditions réelles.
3. **Pour une vraie mise en production**, il faudra ajouter un vrai backend (API + base de données), une vraie authentification, et s'assurer de la conformité RGPD / protection des mineurs (hébergement, droits d'accès par établissement, journalisation, etc.) — idéalement avec l'avis d'un professionnel du droit du numérique éducatif.
4. **Liste des établissements** : la liste fournie dans `js/data.js` n'est qu'un **jeu d'exemple** de quelques lycées, à titre de démonstration. Elle doit être vérifiée et complétée avec les RNE réels avant tout usage sérieux.

## Héberger sur GitHub Pages

1. Crée un nouveau dépôt GitHub, par exemple `eduportail`.
2. Pousse le contenu de ce dossier à la racine du dépôt :
   ```bash
   git init
   git add .
   git commit -m "Premier prototype EDUPORTAIL — espace Super Administrateur"
   git branch -M main
   git remote add origin https://github.com/<ton-compte>/eduportail.git
   git push -u origin main
   ```
3. Dans le dépôt GitHub : **Settings → Pages → Build and deployment → Source : Deploy from a branch**, choisis la branche `main` et le dossier `/ (root)`.
4. Le site sera disponible à `https://<ton-compte>.github.io/eduportail/`.

## Structure du projet

```
eduportail/
├── index.html          # page de connexion / choix d'espace
├── superadmin.html      # espace Super Administrateur
├── css/
│   └── style.css        # tokens de design (couleurs, typographie, layout)
├── js/
│   ├── data.js           # couche de données (localStorage, jeu d'exemple)
│   └── superadmin.js      # logique de l'espace Super Administrateur
└── README.md
```

## Prochaines étapes possibles

- Espace **Chef d'établissement** : inscription d'élèves via le RNE, consultation des fiches/bulletins, génération de certificat de scolarité, rubrique Pronote (multi-adresses), messagerie Mailo, livret scolaire annuel.
- Espace **Professeur** (thème bleu) : Pronote, Mailo, site web du lycée.
- Espace **Élève** (thème vert) : Pronote, Mailo, accès bulletins/certificat.
- Espace **Parent** : Pronote, choix d'orientation (Voie Professionnelle Essentielle / Sportive, Voie Générale Intégrale).
- Remplacement du stockage local par un vrai backend partagé entre tous les espaces.
