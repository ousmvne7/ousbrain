# Bibliothèque personnelle

**Fonctionnalité mise de côté.** Les boutons de révision et de réglages sont retirés.
Les fichiers, les données déjà enregistrées et les fonctions sont conservés pour une
reprise ultérieure. Les accès décrits ci-dessous ne sont plus actifs.

## Rangement dans VS Code
`private-lessons/la-madrassah/pages-017-020.json`

Premiers extraits du livre « Apprendre l’arabe avec la vie des Prophètes ».
Chaque extrait porte un identifiant stable, une page, une leçon, un texte arabe
et une traduction de travail à relire. Ce premier lot comprend 14 extraits,
pas une transcription complète de toutes les pages.

Le dossier private-lessons est exclu de Git. Ne pas utiliser git add -f dessus,
ni publier le dossier entier par un autre hébergeur.

## Fonctionnement
En local, l’application charge ce lot lorsque « Voir dans ma leçon » ou
« Aperçu des leçons » est ouvert pour le paquet Al-Madrassah.
Elle fusionne les extraits par identifiant dans les données du paquet, sans
supprimer les autres lots. Les données sont enregistrées avec la collection
et utilisent sa synchronisation Supabase existante quand le compte est connecté.
La version GitHub ne télécharge pas les fichiers privés : elle utilise la collection.
Ouvrir une fois la bibliothèque sur le serveur local et laisser la synchronisation
aboutir avant de la retrouver sur un autre appareil avec le même compte.

## Pages suivantes
Créer un lot portant les nouveaux numéros de pages dans le même dossier,
avec des identifiants distincts. Ajouter son chemin à LESSON_LOCAL_BATCHES
dans app.js. Préserver les identifiants des anciens extraits lors des corrections.
Les traductions restent signalées comme provisoires jusqu’à relecture.

## Aperçu
Réglages → Aperçu des leçons, ou depuis « Voir dans ma leçon ».
L’aperçu regroupe les extraits par leçon et liste les cartes sans correspondance.
Une absence de correspondance peut aussi venir d’une conjugaison non reconnue.
