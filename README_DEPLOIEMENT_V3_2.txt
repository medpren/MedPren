M'MEDPREN V3.2 — FRONTEND + BACKEND + PHOTOS PERSISTANTES
==========================================================

CE PACK CONTIENT LES FICHIERS À METTRE À LA RACINE DU DÉPÔT GITHUB :
- index.html
- service-worker.js
- manifest.webmanifest
- MMedPren_Backend_Render.zip  (NE PAS décompresser celui-ci dans GitHub)

1) GITHUB
Remplacer les anciens fichiers par ceux du pack puis faire Commit changes.
Le fichier backend doit garder exactement le nom : MMedPren_Backend_Render.zip

2) RENDER
La Build Command existante peut rester :
python -m zipfile -e MMedPren_Backend_Render.zip backend_runtime && pip install -r backend_runtime/requirements.txt

La Start Command existante peut rester :
cd backend_runtime && alembic upgrade head && python -m app.seed && uvicorn app.main:app --host 0.0.0.0 --port $PORT

3) CLOUDINARY — VARIABLE OBLIGATOIRE POUR LES PHOTOS PERSISTANTES
Dans Render > votre Web Service > Environment, ajouter :
CLOUDINARY_URL=cloudinary://API_KEY:API_SECRET@CLOUD_NAME

Optionnelles :
CLOUDINARY_FOLDER=mmedpren/products
IMAGE_MAX_BYTES=8388608

Ne jamais placer API_SECRET dans index.html ou dans un fichier public GitHub.

4) APRÈS LE REDÉPLOIEMENT
Ouvrir : https://mmedpren-api-v2.onrender.com/health
Attendu :
- version = 0.3.2
- image_storage = configured

Swagger : https://mmedpren-api-v2.onrender.com/docs
Nouvelle route image : POST /api/v1/products/{product_id}/image

5) CE QUI A ÉTÉ MODIFIÉ
- PostgreSQL : ajout image_url et image_public_id aux produits via migration Alembic 0002.
- FastAPI : upload JPEG/PNG/WebP, validation réelle du format, limite 8 Mo, sécurité seller/ownership.
- Stockage : upload serveur signé vers Cloudinary ; secret jamais exposé au navigateur.
- Remplacement photo : l'ancienne image Cloudinary est supprimée après remplacement.
- Suppression photo : DELETE /api/v1/products/{product_id}/image.
- Frontend : compression mobile puis upload multipart vers FastAPI.
- Catalogue : image_url venant de PostgreSQL/Cloudinary est prioritaire et visible sur tous les appareils.
- PWA : cache V3.2 afin d'éviter que l'ancien formulaire reste affiché.

Tests réalisés avant création du pack :
- Python compileall : OK
- Tests backend : 4 passed
- Vérification syntaxe JavaScript avec node --check : OK
