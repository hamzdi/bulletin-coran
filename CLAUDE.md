# CLAUDE.md

Guide pour Claude Code lors de toute intervention sur ce dépôt.

## Nature du projet

Bulletin scolaire numérique pour une école d'apprentissage du Coran (Bee Learning).
**Application web mono-fichier, autonome** : aucun serveur, aucune dépendance, aucun
build. Tout — HTML, CSS, JavaScript, images — tient dans `index.html`.

Hébergé sur **GitHub Pages** depuis la branche `main`. Tout push sur `main` est
publié automatiquement.

## Structure du dépôt

| Fichier                  | Rôle                                                       |
|--------------------------|------------------------------------------------------------|
| `index.html`             | Application complète. Publiée sur GitHub Pages.            |
| `index.beelearning.html` | **Non versionné** (`.gitignore`). Version interne avec la signature de la direction embarquée en base64. Distribuée hors dépôt. |
| `README.md`              | Documentation utilisateur.                                 |
| `CLAUDE.md`              | Ce fichier.                                                |

## Règles importantes

- **Ne jamais committer `index.beelearning.html`.** Il contient la signature de la
  direction embarquée et doit rester hors du dépôt public. Il est listé dans
  `.gitignore` — ne pas l'en retirer.
- **`index.html` ne doit pas contenir de signature de direction préchargée.** La
  direction importe sa signature via la zone d'upload, comme le professeur.
- **`index.html` n'applique aucun logo par défaut.** Le logo Bee Learning est stocké
  dans la constante `BEE_LOGO` et proposé dans la galerie de logos, mais n'est
  appliqué que si l'utilisateur le sélectionne.
- Toute modification fonctionnelle faite sur `index.html` doit être reportée
  manuellement sur `index.beelearning.html`, **sauf** les divergences voulues
  listées ci-dessous.
- **Compte GitHub** : ce dépôt appartient au compte personnel `hamzdi`
  (`hamza.diouane@try-it.fr`), pas au compte professionnel FNCCR. L'identité Git est
  fixée en local au dépôt — ne pas la remplacer par l'identité globale.
  Avant tout push, basculer le compte actif : `gh auth switch -u hamzdi` (le compte
  actif peut revenir sur FNCCR entre deux sessions).

## Divergences voulues entre `index.html` et `index.beelearning.html`

Ces différences sont intentionnelles — ne pas les « réaligner ».

| Aspect | `index.html` (public) | `index.beelearning.html` (interne) |
|--------|-----------------------|------------------------------------|
| Signature direction | Importée par l'utilisateur | Embarquée en base64 par défaut |
| Logo | Galerie ; aucun logo appliqué au départ | Logo Bee Learning préchargé automatiquement |

Toute autre modification fonctionnelle (calculs, thème, mise en page…) doit, elle,
être reportée sur les deux fichiers.

## Architecture de `index.html`

- **CSS** dans un `<style>` en tête de document.
- **JavaScript** dans un `<script>` en fin de `<body>`, exécuté dans une IIFE.
- **État** : objet `state` (`logo`, `logoGallery`, `sigProf`, `sigDir`, bulletins…),
  persisté dans `localStorage` via `save()` / clé `LS_KEY`.
- **État initial** : `logo`, `sigProf` et `sigDir` sont `null` ; `logoGallery` est un
  tableau vide. Rien n'est préchargé — l'utilisateur choisit ou importe.
- **Galerie de logos** : `BEE_LOGO` (constante, logo Bee Learning) + les uploads de
  `state.logoGallery`. Fonctions `renderLogoGallery()`, `applyLogo()`,
  `removeGalleryLogo()`, hook `onLogoUpload()` passé à `setupUpload()`.
- **`save()`** retourne `true`/`false` : en cas de quota `localStorage` dépassé, il
  affiche une alerte et renvoie `false` ; l'appelant annule alors la modification.
- **Signatures** : fonctions `propagateSigProf()` / `propagateSigDir()` ; balises
  `<img data-role="sig-prof|sig-dir">`.
- **Calculs** : les moyennes sont recalculées automatiquement à la saisie des notes.
- **Thème** : palette de 11 couleurs configurable.
- **Responsive** : optimisé pour iPhone.

## Conventions

- Commentaires et docstrings du code en **anglais**.
- Garder le projet **mono-fichier** : ne pas introduire de build, de framework ni de
  dépendance externe sans raison explicite.

## Évolutions prévues (v4+)

- Conversion en **PWA** : `manifest.json`, icône, balises meta iOS, ajout à l'écran
  d'accueil. À traiter comme une itération séparée.
