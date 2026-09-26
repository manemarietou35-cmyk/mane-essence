# Mané Essences — site vitrine

Site vitrine statique pour la boutique **Mané Essences** (Mariétou Mané, Dakar) — parfums 50 ml, huiles de parfum et Collection Authentique de Paris.

## Structure

```
mane-essences/
├── index.html      → toute la page (HTML + CSS, un seul fichier)
├── images/          → photos produits (déjà optimisées, fond studio harmonisé)
└── README.md
```

Site 100% statique : pas de build, pas de dépendances, pas de backend. Tout tourne dans `index.html`.

## Modifier le contenu

Ouvre `index.html` dans VS Code. Tout le texte est en clair dedans (pas de CMS) :
- Stocks / prix des parfums : cherche la section `id="parfums"`
- Huiles : section `id="huiles"`
- Collection Authentique : section `id="collection"`
- Numéro Wave / Orange Money : cherche `76 383 42 48` (2 occurrences dans la section paiement + une dans le pied de page)

Pour changer une photo, remplace le fichier correspondant dans `images/` **en gardant le même nom**, ou change le chemin `src="images/xxx.jpg"` dans le HTML.

## Déployer sur Vercel

**Option 1 — via le site Vercel (le plus simple)**
1. Va sur [vercel.com](https://vercel.com) et connecte-toi (ou crée un compte gratuit).
2. Clique sur **Add New → Project**.
3. Choisis **Deploy without Git** puis glisse-dépose le dossier `mane-essences` complet (ou le zip dézippé).
4. Vercel détecte automatiquement un site statique — aucune configuration nécessaire. Clique sur **Deploy**.
5. Ton site est en ligne en quelques secondes, avec une URL du type `mane-essences.vercel.app`.

**Option 2 — via GitHub (recommandé si tu veux mettre à jour le site facilement)**
1. Crée un dépôt GitHub et pousse ce dossier dedans :
   ```bash
   cd mane-essences
   git init
   git add .
   git commit -m "Site Mané Essences"
   git branch -M main
   git remote add origin <URL_DE_TON_REPO>
   git push -u origin main
   ```
2. Sur [vercel.com](https://vercel.com), clique **Add New → Project**, choisis **Import Git Repository** et sélectionne ton dépôt.
3. Laisse les réglages par défaut (aucun *build command* n'est nécessaire pour un site statique) et clique **Deploy**.
4. À chaque `git push`, Vercel republie automatiquement le site.

**Option 3 — via la CLI Vercel**
```bash
npm i -g vercel
cd mane-essences
vercel
```
Suis les instructions à l'écran (connexion, nom du projet) puis `vercel --prod` pour la mise en ligne définitive.

## Nom de domaine personnalisé

Une fois déployé, dans le tableau de bord Vercel du projet : **Settings → Domains** → ajoute ton propre nom de domaine (ex. `maneessences.com`) si tu en achètes un.

## Panier d'achat

Le site a maintenant un panier complet, 100% fonctionnel, en JavaScript pur (aucune dépendance, aucun serveur) :

- Bouton **« Ajouter au panier »** sur chacun des 21 produits (parfums, huiles, Collection Authentique).
- Icône panier dans le menu avec un badge qui compte les articles.
- Tiroir latéral avec quantités **[ − ] [ + ]**, sous-totaux, suppression, plafonnées au stock affiché quand il est défini.
- Panier **conservé automatiquement** (localStorage du navigateur) : il survit à la navigation entre les pages et même à la fermeture du navigateur, sur cet appareil.
- Formulaire de commande (nom, téléphone, adresse, ville), choix du moyen de paiement (Wave / Orange Money / virement), génération d'une référence de commande et affichage du statut « En attente de paiement ».
- Comme le site n'a pas de serveur, la commande n'est **pas envoyée automatiquement** : un bouton « Envoyer la commande via WhatsApp » ouvre WhatsApp avec le récapitulatif pré-rempli, prêt à envoyer vers le numéro de la boutique.

Le catalogue (noms, prix, formats, photos, stocks) est centralisé tout en haut du `<script>` dans `index.html`, dans l'objet `PRODUCTS` — c'est le seul endroit à modifier pour changer un prix, un stock ou ajouter un produit.

### Numéro utilisé pour WhatsApp

Le bouton WhatsApp utilise **+221 76 383 42 48** (ton numéro Wave/Orange Money, avec l'indicatif Sénégal +221) — cherche `SHOP_PHONE` dans `index.html` si tu veux le changer.

## À compléter

- Les coordonnées bancaires pour le virement ne sont pas affichées publiquement (comme prévu) — pense à les avoir prêtes à envoyer manuellement aux clients.
- Aucun réseau social / e-mail n'est encore lié dans le pied de page — ajoute-les si tu veux qu'on te contacte autrement que par Wave/Orange Money.
- Le panier est propre à chaque navigateur/appareil (pas de compte client, pas de base de données partagée) — c'est normal pour un site 100% statique.
