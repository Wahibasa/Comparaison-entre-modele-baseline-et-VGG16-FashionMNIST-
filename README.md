# Comparaison Baseline vs VGG16 pour le Débruitage sur Fashion-MNIST

## 1. Objectif
Ce projet compare deux architectures de réseaux de neurones convolutionnels pour le débruitage d’images **Fashion-MNIST** :

- Un **autoencodeur Baseline**
- Un **modèle basé sur VGG16 pré-entraîné**, adapté au débruitage

L’objectif est d’analyser la qualité de reconstruction, les performances et la complexité des modèles.

---

## 2. Préparation des données
- Les images **28×28** sont normalisées entre 0 et 1.
- Un **bruit gaussien** est ajouté (`noise_factor = 0.2`) pour créer les images bruitées.
- Pour VGG16, les images sont redimensionnées en **32×32** et converties en **3 canaux** RGB.

---

## 3. Architectures des modèles

### 3.1 Baseline
- Autoencodeur convolutionnel simple :
  - Encodeur : 3 couches Conv + MaxPooling
  - Décodeur : 3 couches Conv + UpSampling
  - Sortie : couche Conv avec activation `sigmoid`
- Paramètres : ~250k

### 3.2 VGG16 Denoiser
- Basé sur **VGG16** pré-entraîné (weights=ImageNet, non entraînable)
- Ajout de couches convolutionnelles + UpSampling pour reconstruire les images
- Paramètres : ~15M

---

## 4. Entraînement
- **10 epochs** pour chaque modèle
- Baseline : batch_size = 128
- VGG16 : batch_size = 16
- Optimiseur : **Adam**, fonction de perte : **MSE**

---

## 5. Évaluation
- Métriques calculées sur 500 images test :
  - **MSE** : erreur quadratique moyenne
  - **PSNR** : rapport signal sur bruit
  - **SSIM** : similarité structurelle
- Temps d’entraînement enregistré pour comparaison

---

## 6. Résultats

- Visualisation des images reconstruites pour quelques exemples :
  - Image originale  
  - Image bruitée  
  - Reconstruction Baseline  
  - Reconstruction VGG16

---

