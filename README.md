# Bulletin Coran — Bee Learning

Bulletin scolaire numérique pour une école d'apprentissage du Coran.
Application web autonome, sans serveur ni base de données : tout tient dans une seule page HTML.

## Accès

**https://hamzdi.github.io/bulletin-coran/**

Le lien s'ouvre directement dans le navigateur, y compris sur iPhone et iPad.
Aucune installation requise.

## Fonctionnalités

- **Calcul automatique des moyennes** à partir des notes saisies
- **Palette de 11 couleurs** configurable pour adapter le bulletin à l'école
- **Logo de l'école embarqué**, affiché sur chaque bulletin
- **Signatures par image** : le professeur et la direction chargent leur signature
  manuscrite ; le parent signe sur le bulletin imprimé
- **Sauvegarde locale** : la configuration et les bulletins sont conservés dans le
  navigateur (`localStorage`), sans envoi de données vers un serveur
- **Affichage responsive**, optimisé pour iPhone
- **Impression** directe au format bulletin

## Utilisation

1. Ouvrir le lien ci-dessus.
2. Renseigner les informations de l'élève, du professeur et les notes.
3. Charger les signatures via les zones prévues (professeur et direction).
4. Imprimer ou exporter le bulletin terminé.

Les données saisies restent sur l'appareil utilisé. Vider le cache du navigateur
efface la configuration sauvegardée.

## Pour les enseignants Bee Learning

La version publiée ici ne contient pas de signature de direction préchargée :
chacun importe la sienne localement. Une version interne, avec la signature de la
direction déjà intégrée, est distribuée séparément par l'administration de l'école
(elle n'est pas hébergée sur ce dépôt public).

## Structure du dépôt

| Fichier      | Rôle                                                      |
|--------------|-----------------------------------------------------------|
| `index.html` | Application complète, publiée sur GitHub Pages            |
| `README.md`  | Ce document                                               |

## Hébergement

Le site est hébergé gratuitement via **GitHub Pages**, servi depuis la branche `main`.
Toute modification de `index.html` poussée sur `main` est mise en ligne automatiquement.

## Évolutions prévues (v4+)

- Conversion en **PWA** : `manifest.json`, icône, ajout à l'écran d'accueil iOS
  pour un accès en un geste, sans passer par le navigateur.
