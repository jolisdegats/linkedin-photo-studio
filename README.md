# 📸 linkedin-photo-studio

Recadrer et ajuster sa photo de profil LinkedIn **en la voyant directement dans
une page de profil qui ressemble à LinkedIn**, puis la télécharger prête à
l'emploi.

Un seul fichier, `index.html`, sans build ni dépendance : double-clique dessus
et il s'ouvre dans le navigateur. Les photos ne quittent jamais ta machine.

## Ce que ça fait

- **Page de profil façon LinkedIn** : nav, bannière, avatar, nom, titre,
  boutons, fil d'activité (pour voir la photo en 48 px et en 32 px). Le nom, le
  titre, la ville et l'entreprise sont modifiables d'un clic.
- **Modale « Edit image » avec les mêmes réglages que LinkedIn** :
  - *Crop* : rotation gauche/droite, miroir horizontal/vertical, Zoom, Rotate
    (±45°), glisser pour déplacer, molette ou pincement pour zoomer, flèches du
    clavier ;
  - *Filter* : Original, Studio, Spotlight, Prime, Classic, Edge, Luminate ;
  - *Adjust* : Brightness, Contrast, Saturation, Vignette.
- **Repères de cadrage** : grille des tiers, ovale cible pour la tête, repères
  de hauteur des yeux.
- **Assistant** : détection du visage (MediaPipe, en local dans le navigateur)
  et conseils en direct : taille du visage, hauteur des yeux, centrage,
  inclinaison, lumière, résolution. Le bouton **✨ Auto-cadrer** redresse la
  tête et la place sur les repères.
- **Avant / Après** : importe ta photo actuelle, puis bascule entre les deux
  avec la barre d'espace ou le bouton « Actuelle / Nouvelle ».
- **Téléchargement** : JPG carré (à uploader sur LinkedIn, qui découpe le rond
  lui-même) ou PNG rond à fond transparent. Le fichier est exporté à la
  résolution de la photo d'origine, de 400 à 1200 px.

Tout est mémorisé dans le navigateur (`localStorage`) : en rouvrant la page,
on retrouve ses photos et ses réglages.

## Lancer

```sh
open index.html             # macOS
# ou, pour servir en local :
npx http-server -c-1 .
```

La détection du visage charge MediaPipe depuis `cdn.jsdelivr.net` et son modèle
depuis `storage.googleapis.com` : il faut donc être en ligne. Hors ligne, tout le
reste marche, sauf les conseils automatiques ; il reste alors la grille et
l'ovale.

## Repères utilisés

Ils sont exprimés en fractions du diamètre du cercle et ont été mesurés sur des
photos de profil réussies :

| Repère | Cible | Toléré |
|---|---|---|
| Hauteur des yeux | 37 % | 31 – 43 % |
| Écart entre les yeux (≈ tête à 60 % du cercle) | 16 % | 12,5 – 21 % |
| Centrage horizontal | 50 % | ± 6 % |
| Inclinaison | 0° | ± 2,5° |
