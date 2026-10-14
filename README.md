# Oh My Donut Reims

Site vitrine et commande en click & collect pour Oh My Donut, 19 rue des Capucins, 51100 Reims.

Site 100 % statique : aucune installation, aucun build. Tous les fichiers sont à la racine.

## Fichiers

| Fichier | Rôle |
|---|---|
| `index.html` | Le site complet : animation d'accueil, carte, composition de box, panier, créneaux de retrait |
| `mentions-legales.html` | Mentions légales et RGPD |
| `404.html` | Page d'erreur |
| `favicon.svg` | Icône d'onglet et d'écran d'accueil |
| `manifest.webmanifest` | Ajout à l'écran d'accueil sur mobile |
| `robots.txt`, `sitemap.xml` | Référencement Google |
| `vercel.json` | URLs propres et en-têtes de sécurité sur Vercel |

## Mise en ligne

**Vercel (recommandé)**
1. Pousser ce dossier sur un dépôt GitHub.
2. Sur vercel.com : Add New, Project, importer le dépôt, Framework Preset « Other », Deploy.

**GitHub Pages**
Settings, Pages, Source « Deploy from a branch », branche `main`, dossier `/ (root)`.

## À personnaliser avant la mise en ligne

Tout se règle en haut du `<script>` de `index.html` :

- `SHOP` : téléphone, numéro qui reçoit les SMS de commande, horaires, délai de préparation.
- `SHOP.orderEndpoint` : URL qui reçoit les commandes en JSON (Formspree, Make, n8n, route API). Vide = la commande part par SMS pré-rempli depuis le téléphone du client.
- `PRODUCTS` : noms, descriptions et prix (prix actuels indicatifs).
- `BOX_SIZES` : prix des box de 4, 6 et 12.
- Animation d'accueil : jouée à chaque chargement, durée réglée par `setTimeout(done, 2700)` dans `runIntro()`. Pour la retirer, supprimer le bloc `<div class="intro">` et l'appel `runIntro();`.

Autres points :

- Remplacer `ohmydonut-reims.vercel.app` par le vrai domaine dans `index.html`, `robots.txt` et `sitemap.xml`.
- Compléter les champs surlignés dans `mentions-legales.html`.

## Format d'une commande envoyée à `orderEndpoint`

```json
{
  "code": "OMD-X47O",
  "name": "Prénom",
  "phone": "06 12 34 56 78",
  "note": "",
  "pickup": "aujourd'hui à 19h00",
  "total": 24.9,
  "lines": [{ "name": "Box de 6 donuts", "opts": "2 Rainbow, ...", "qty": 1, "price": 15.9 }],
  "createdAt": "2026-10-14T09:30:00.000Z"
}
```
