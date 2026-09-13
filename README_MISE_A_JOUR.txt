M'MEDPREN V3.1 — MISE À JOUR GITHUB PAGES
Date : 13 septembre 2026

FICHIERS À METTRE À LA RACINE DU DÉPÔT GITHUB PAGES
1. index.html               -> remplacer l'ancien index.html
2. service-worker.js        -> ajouter/remplacer
3. manifest.webmanifest     -> ajouter/remplacer

PRINCIPAUX CORRECTIFS
- Le bouton « Ma boutique » distingue désormais création et gestion d'une boutique.
- Un vendeur en attente ne peut plus arriver directement à un formulaire qui échoue silencieusement.
- Les comptes admin peuvent ouvrir « Administration » et approuver/suspendre les vendeurs.
- Un admin vendeur peut approuver sa propre boutique depuis le tableau de bord vendeur.
- Le formulaire « Ajouter un produit » possède maintenant un sélecteur de photo + aperçu.
- La photo est compressée puis conservée localement sur l'appareil, car le backend FastAPI actuel n'a pas encore d'endpoint d'upload de fichiers.
- Favoris produits fonctionnels.
- Nouvelle vente locale, clients/mini-CRM et génération de facture fonctionnels.
- Profil Work4Future local, programmes de formation et marque d'intérêt fonctionnels.
- Publication d'un besoin Services et soumission d'une initiative Mundu ku Gundi fonctionnelles en local.
- Centre de notifications et assistant d'orientation améliorés.
- Gestion plus claire des erreurs réseau et du démarrage lent du backend Render.
- PWA : manifest + service worker ajoutés.

IMPORTANT — PHOTOS PRODUITS
Le produit (nom, prix, stock, etc.) continue d'être enregistré par l'API/PostgreSQL. La photo choisie est actuellement stockée dans le navigateur du téléphone après compression. Elle s'affiche donc sur cet appareil, mais elle ne sera pas synchronisée sur d'autres téléphones tant qu'un stockage d'images côté backend (Cloudinary/S3/R2/etc.) n'est pas ajouté.

APRÈS L'IMPORT GITHUB
- Attendre 1 à 3 minutes que GitHub Pages republie le site.
- Sur Android/Chrome, actualiser fortement la page. Si l'ancienne version reste en cache, fermer l'onglet puis rouvrir le site.
- Aller dans Mon compte > Ma boutique. Si le compte a le rôle admin et la boutique est « En attente », utiliser « Approuver cette boutique maintenant ».
