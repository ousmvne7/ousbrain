# OusBrain — direction graphique

## Intention
Une application de mémorisation adulte, calme, centrée sur le texte et les cartes.
Le logo fourni (ض, A, cartes pliées) est la référence. Le nom reste OusBrain.
Le fichier PNG fourni est intégré tel quel ; ce n’est pas encore un master vectoriel.

## Palette
- Action principale : émeraude #087F5B, texte blanc #FFFFFF.
- Fond : presque blanc #F8FAF9. Surfaces : #FFFFFF. Encre anthracite : #252B2A.
- Texte secondaire : #626D69. Bordures : #E3E8E5. Surfaces secondaires neutres : #F3F5F4.
- Émeraude : actions principales et sélection. Bleu : information, nouvelles cartes, note « Bien » et graphiques d’activité.
- Orange : apprentissage en cours, difficulté et avertissement. Vert : réussite, « Facile » et cartes à réviser (convention de l’application).
- Rouge : erreurs, « Encore », suppression, remise à zéro, déconnexion et fin volontaire de session.
- Gris : navigation secondaire, annulation et simple fermeture de fenêtre sans perte de données.
- Les couleurs sont des conventions explicites, pas un langage universel : conserver les libellés et icônes associés.
- Nuit : fond #101D19, surface #182923, texte #EEF4E9 ; action claire #B4E3C6.

## Règles
- Le contenu arabe conserve KFGQPC Hafs v18 ; ne jamais substituer la police coranique.
- Interface : police système/Inter existante, corps 16 px, métadonnées 12–14 px.
- Icônes Lucide, aucun emoji ajouté. Commandes tactiles 44 px minimum.
- Espacements par multiples de 4, surfaces arrondies 12–22 px, ombres discrètes.
- Un seul accent principal par écran. Pas de gros dégradés décoratifs dans les cartes.
- Même système sur téléphone, tablette, ordinateur et en mode sombre.
- Le logo ne doit pas être recoloré automatiquement en mode sombre.

## Inspiration et limites
Tarteel inspire la concentration sur l’apprentissage et l’accès direct aux commandes,
pas la reproduction de ses écrans, de son logo ni l’ajout de ses fonctionnalités.
Sources consultées :
- https://tarteel.ai/blog/new-settings-in-tarteel-a-i/amp/
- https://support.tarteel.ai/en/articles/12414375-layout-options

## Organisation
brand.css porte les règles transversales et se charge après styles.css.
Les classes historiques blue/blue2 servent désormais d’alias de couleur de marque.
La planification FSRS, les données, les sessions et la synchronisation restent inchangées.
