M'MEDPREN V3.3 — Mise à jour GitHub + Render
===========================================

1) GitHub / dépôt MedPren
Remplacer à la racine :
- index.html
- service-worker.js
- manifest.webmanifest
- MMedPren_Backend_Render.zip
Puis Commit changes.

2) Render
Le service auto-déploie le commit GitHub. Les commandes restent inchangées :
Build:
python -m zipfile -e MMedPren_Backend_Render.zip backend_runtime && pip install -r backend_runtime/requirements.txt

Start:
cd backend_runtime && alembic upgrade head && python -m app.seed && uvicorn app.main:app --host 0.0.0.0 --port $PORT

3) Vérification
Ouvrir https://mmedpren-api-v2.onrender.com/health
Attendu : version 0.3.3 et image_storage configured.

4) Nouveautés
- Galerie de photos : plus de capture caméra forcée.
- Modifier sa boutique depuis Mon compte > Ma boutique.
- L'administrateur peut modifier toute boutique, dont Poules Élevage.
- Suspendre/réactiver un vendeur ; suspension masque automatiquement tout son catalogue.
- Suspendre/réactiver un produit individuellement.
- Supprimer définitivement un produit tout en conservant les lignes des anciennes commandes.
- Supprimer définitivement un vendeur (profil vendeur, boutique, produits), en conservant son compte utilisateur/client.

IMPORTANT
- Ne modifiez pas CLOUDINARY_URL : elle reste dans Environment sur Render.
- Le secret Cloudinary ne doit jamais être ajouté à GitHub.
- La migration Alembic 0003 est appliquée automatiquement au redéploiement.
