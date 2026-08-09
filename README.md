# OusBrain — Arabe & Coran

Application web de cartes mémoire inspirée du fonctionnement d’Anki, pensée pour l’apprentissage du vocabulaire arabe et la future révision de contenus coraniques.

> **Statut :** version locale en développement. L’application fonctionne sur ordinateur et téléphone, mais elle n’est pas encore publiée sur GitHub ni déployée sur un domaine permanent.

---

## Sommaire

1. [Objectif du projet](#1-objectif-du-projet)
2. [Fonctionnalités disponibles](#2-fonctionnalités-disponibles)
3. [Démarrage rapide](#3-démarrage-rapide)
4. [Utilisation sur téléphone](#4-utilisation-sur-téléphone)
5. [Guide utilisateur](#5-guide-utilisateur)
6. [Structure du projet](#6-structure-du-projet)
7. [Architecture de l’application](#7-architecture-de-lapplication)
8. [Structure des données](#8-structure-des-données)
9. [Répétition espacée](#9-répétition-espacée)
10. [Affichage arabe](#10-affichage-arabe)
11. [Règles pour le texte coranique](#11-règles-pour-le-texte-coranique)
12. [Sauvegarde et migration](#12-sauvegarde-et-migration)
13. [Import et export](#13-import-et-export)
14. [Contrôles et tests](#14-contrôles-et-tests)
15. [Dépannage](#15-dépannage)
16. [Publication future](#16-publication-future)
17. [Feuille de route](#17-feuille-de-route)
18. [Règles de contribution](#18-règles-de-contribution)

---

## 1. Objectif du projet

OusBrain doit permettre de :

- mémoriser du vocabulaire arabe avec ses ḥarakāt ;
- créer et organiser plusieurs paquets ;
- réviser dans les deux directions ;
- planifier automatiquement les prochaines révisions ;
- afficher correctement l’arabe avec une police locale ;
- ajouter plus tard des cartes coraniques sans altérer le texte du muṣḥaf ;
- fonctionner sur ordinateur et téléphone ;
- devenir ensuite une application installable et synchronisée.

Le projet est volontairement construit en HTML, CSS et JavaScript simples. Aucun framework n’est nécessaire pour lancer la version actuelle.

---

## 2. Fonctionnalités disponibles

### Collection et paquets

- Tableau de bord des paquets
- Création d’un paquet
- Renommage d’un paquet
- Menu d’actions par paquet : étudier, ajouter, parcourir, renommer, options, exporter, archiver et supprimer
- Protection du dernier paquet actif contre l’archivage et la suppression
- Compteurs de cartes nouvelles, en apprentissage et à réviser
- Premier paquet arabe–français allégé à 12 cartes

### Cartes

- Ajout d’une carte
- Modification d’une carte
- Suppression d’une carte
- Champ Recto
- Champ Verso
- Note facultative
- Recherche dans les cartes
- Filtrage par paquet

### Révision

- Recto → Verso
- Verso → Recto
- Direction mixte
- Boutons **Encore**, **Difficile**, **Bien** et **Facile**
- Affichage de l’intervalle avant de répondre
- Barre de progression
- Compteurs de session
- Anticipation des cartes d’apprentissage

### Interface

- Tableau de bord d’accueil
- Barre latérale sur ordinateur
- Navigation inférieure sur téléphone
- Reprise rapide d’une carte
- Journal d’activité alimenté par les données réelles
- Navigation entre plusieurs écrans
- Interface responsive
- Mode sombre
- Raccourcis clavier
- Statistiques de révision
- Notifications internes

### Données

- Sauvegarde automatique locale
- Import JSON
- Export JSON
- Migration automatique du vocabulaire corrigé

---

## 3. Démarrage rapide

### Prérequis

- Un navigateur moderne
- Python 3 pour le serveur local
- Le dossier complet du projet

### Lancer le serveur

Ouvrir un terminal dans le dossier `Anki2.0`, puis exécuter :

```bash
python3 -m http.server 5500
```

Ouvrir ensuite :

```text
http://localhost:5500
```

### Pourquoi utiliser un serveur local ?

Il ne faut pas ouvrir simplement `index.html` avec une adresse `file://`.

Le serveur local est nécessaire pour charger correctement :

- `hafsData_v18.json` ;
- les fichiers de police ;
- les futurs fichiers de données ;
- les fonctions hors connexion qui seront ajoutées plus tard.

---

## 4. Utilisation sur téléphone

### Sur le même Wi-Fi

1. Lancer le serveur sur le Mac.
2. Trouver l’adresse IP locale du Mac.
3. Ouvrir l’adresse suivante sur le téléphone :

```text
http://ADRESSE-IP-DU-MAC:5500
```

Exemple :

```text
http://192.168.1.117:5500
```

### Depuis la 4G ou l’extérieur

Une adresse locale `192.168.x.x` ne fonctionne pas depuis la 4G.

Il faut utiliser temporairement un tunnel HTTPS ou publier l’application. Une URL de tunnel :

- est temporaire ;
- change lorsqu’on relance le tunnel ;
- fonctionne uniquement si le Mac reste allumé ;
- fonctionne uniquement si le serveur local reste lancé ;
- ne remplace pas un vrai déploiement.

La solution permanente prévue est un déploiement GitHub Pages ou une plateforme similaire.

---

## 5. Guide utilisateur

### 5.1 Paquets

L’écran **Paquets** affiche :

- le nom du paquet ;
- le nombre de nouvelles cartes ;
- le nombre de cartes en apprentissage ;
- le nombre de cartes à réviser.

Cliquer sur un paquet ouvre son aperçu.

### 5.2 Ajouter une carte

1. Ouvrir **Ajouter**.
2. Choisir le paquet.
3. Remplir le Recto.
4. Remplir le Verso.
5. Ajouter éventuellement une note.
6. Cliquer sur **Ajouter**.

Lorsqu’un texte arabe est saisi :

- il est détecté automatiquement ;
- la direction passe en RTL ;
- la police KFGQPC Hafs v18 est appliquée ;
- le texte original est conservé dans les données.

### 5.3 Parcourir les cartes

L’écran **Parcourir** permet de :

- afficher toute la collection ;
- filtrer par paquet ;
- rechercher un mot ;
- sélectionner une carte ;
- modifier ses champs ;
- supprimer la carte.

### 5.4 Lancer une session

1. Ouvrir un paquet.
2. Cliquer sur **Commencer à étudier**.
3. Lire la question.
4. Essayer de répondre mentalement.
5. Cliquer sur **Afficher la réponse**.
6. Choisir une note.

### 5.5 Signification des boutons

- **Encore** : la réponse est fausse ou oubliée.
- **Difficile** : la réponse est correcte, mais avec beaucoup d’hésitation.
- **Bien** : la réponse est correcte avec un effort normal.
- **Facile** : la réponse est immédiate et sans effort.

### 5.6 Raccourcis clavier

| Touche | Action |
|---|---|
| `Espace` | Afficher la réponse |
| `1` | Encore |
| `2` | Difficile |
| `3` | Bien |
| `4` | Facile |

---

## 6. Structure du projet

```text
Anki2.0/
├── index.html
├── styles.css
├── app.js
├── README.md
├── assets/
│   └── fonts/
│       ├── hafs.18.woff2
│       └── hafs.18.ttf
└── data/
    └── hafsData_v18.json
```

### `index.html`

Contient :

- la structure globale ;
- la barre de navigation ;
- les modèles des différents écrans ;
- les formulaires ;
- les boutons de révision ;
- les fenêtres modales.

### `styles.css`

Contient :

- le thème clair et sombre ;
- les styles responsive ;
- l’interface des paquets ;
- les cartes de révision ;
- le navigateur de cartes ;
- les statistiques ;
- la déclaration `@font-face` de KFGQPC Hafs v18 ;
- les règles RTL.

### `app.js`

Contient :

- l’état de la collection ;
- la navigation ;
- le moteur de révision ;
- la sauvegarde ;
- les migrations ;
- la gestion des cartes ;
- le chargement coranique ;
- la détection de l’arabe ;
- les statistiques.

### `hafsData_v18.json`

Contient notamment :

- les 114 sourates ;
- le nom des sourates ;
- les alias de recherche ;
- les versets KFGQPC Hafs v18 ;
- les numéros de pages ;
- les informations de lignes.

---

## 7. Architecture de l’application

La version actuelle est une application monopage sans framework.

### Navigation

Les écrans sont rendus depuis des balises `<template>` :

```text
home     → tableau de bord
decks    → liste des paquets
overview → aperçu du paquet
review   → session de révision
add      → ajout d’une carte
browse   → recherche et modification
stats    → statistiques
settings → réglages
```

L’URL utilise un fragment :

```text
#home
#decks
#overview
#review
#add
#browse
#stats
#settings
```

### État

L’état principal contient :

- les paquets ;
- les cartes ;
- l’historique des révisions ;
- les réglages ;
- la série quotidienne ;
- la version des migrations.

### Rendu

Chaque changement de route :

1. copie le modèle HTML correspondant ;
2. l’insère dans la zone principale ;
3. connecte les événements ;
4. affiche les données actuelles ;
5. applique la typographie arabe si nécessaire.

---

## 8. Structure des données

### Paquet

Exemple simplifié :

```json
{
  "id": "identifiant-unique",
  "name": "Arabe — Vocabulaire",
  "created": 1786230000000
}
```

### Carte standard

```json
{
  "id": "identifiant-unique",
  "deckId": "identifiant-du-paquet",
  "front": "اِسْمٌ / أَسْمَاءٌ",
  "back": "nom(s)",
  "note": "Note facultative",
  "due": 1786230000000,
  "interval": 0,
  "ease": 2.5,
  "reps": 0,
  "lapses": 0,
  "learningStep": null,
  "phase": null,
  "created": 1786230000000,
  "modified": 1786230000000
}
```

### Future carte coranique

Une carte coranique ne doit pas stocker une copie libre du verset comme source principale.

Elle doit conserver sa référence :

```json
{
  "source": "quran",
  "surah": 1,
  "ayah": 1,
  "quranSide": "front"
}
```

Au moment de l’affichage, l’application récupère le texte dans :

```text
chapters[1].verses[1]
```

---

## 9. Répétition espacée

### Configuration par défaut

```text
Étapes d’apprentissage : 1 min, 10 min
Intervalle de graduation : 1 jour
Intervalle Facile : 4 jours
Anticipation : 20 min
```

### Première étape

| Bouton | Prochain affichage |
|---|---:|
| Encore | 1 min |
| Difficile | 6 min |
| Bien | 10 min |
| Facile | 4 jours |

Le délai **Difficile** correspond à la moyenne des deux premières étapes :

```text
(1 min + 10 min) / 2 = 5,5 min ≈ 6 min
```

### Deuxième étape

| Bouton | Prochain affichage |
|---|---:|
| Encore | 1 min |
| Difficile | 10 min |
| Bien | 1 jour |
| Facile | 4 jours |

### Anticipation

Lorsqu’il ne reste aucune autre carte à étudier, une carte d’apprentissage peut être montrée jusqu’à 20 minutes plus tôt.

Cette valeur est modifiable dans **Réglages**.

---

## 10. Affichage arabe

### Police officielle du projet

Le projet utilise :

```text
KFGQPC HAFS Uthmanic Script Version 0.18
```

Fichiers :

```text
assets/fonts/hafs.18.woff2
assets/fonts/hafs.18.ttf
```

### Déclaration CSS

```css
@font-face {
  font-family: "KFGQPC Hafs";
  src:
    url("assets/fonts/hafs.18.woff2") format("woff2"),
    url("assets/fonts/hafs.18.ttf") format("truetype");
  font-weight: 400;
  font-style: normal;
  font-display: swap;
}
```

### Détection automatique

Lorsqu’un champ contient des caractères arabes :

- la classe `arabic-text` est ajoutée ;
- `lang="ar"` est appliqué ;
- `dir="rtl"` est appliqué ;
- la police KFGQPC est utilisée ;
- la synthèse artificielle du gras est désactivée.

### Vocabulaire vérifié

Les 12 formes conservées dans le premier paquet ont été comparées avec la page du manuel fournie.

Liste actuelle :

```text
آزَرُ
بَائِعٌ
بَيْتٌ / بُيُوتٌ
رَجُلٌ / رِجَالٌ
صَنَمٌ / أَصْنَامٌ
فِي
قَرْيَةٌ / قُرًى
كَبِيرٌ
كَسَرَ / يَكْسِرُ
مَشْهُورٌ
نَاسٌ
وَ
```

---

## 11. Règles pour le texte coranique

### Source unique obligatoire

Tous les versets doivent provenir de :

```text
data/hafsData_v18.json
```

Le chargeur vérifie que le fichier déclare :

```text
KFGQPC Hafs Uthmanic v18
KFGQPC HAFS Uthmanic Script Version 0.18
```

### Sources interdites dans cette chaîne

Ne jamais utiliser ou mélanger :

- `uthmanic_hafs_v22` ;
- `quran-uthmani.json` ;
- `quran-tajweed.json` ;
- une autre police de muṣḥaf ;
- une copie saisie manuellement ;
- une API distante comme solution de secours silencieuse.

### Principe de sécurité

Si un verset est introuvable dans `hafsData_v18.json`, l’application doit afficher une erreur technique.

Elle ne doit jamais remplacer silencieusement le verset par une autre version.

### Invocations non coraniques

Pour une invocation :

- conserver le texte arabe original ;
- appliquer la police KFGQPC ;
- ne pas remplacer les mots ou les ḥarakāt ;
- contrôler les caractères non pris en charge.

### Cas du caractère `ﷺ`

Le caractère Unicode `U+FDFA` n’est pas présent dans la table de caractères de `hafs.18.ttf`.

Pour éviter un rond noir :

- la valeur originale reste enregistrée ;
- seule la valeur affichée est développée ;
- aucune donnée source n’est réécrite.

---

## 12. Sauvegarde et migration

### Stockage actuel

La collection est sauvegardée dans le navigateur avec :

```text
localStorage
```

Clé principale :

```text
anki2_collection
```

### Conséquence importante

Les données sont liées :

- au navigateur ;
- à l’appareil ;
- à l’origine de l’URL.

Par exemple, ces deux adresses peuvent posséder des collections différentes :

```text
http://localhost:5500
http://192.168.1.117:5500
```

### Migration du vocabulaire

Une migration corrige les anciennes formes arabes du paquet initial et réduit la sélection de départ à 12 cartes.

Elle :

- reconnaît les cartes initiales ;
- remplace uniquement les anciennes formes connues ;
- conserve l’intervalle ;
- conserve l’historique ;
- conserve le nombre de révisions ;
- n’écrase pas une carte personnalisée arbitraire ;
- archive les 12 cartes initiales retirées et leurs révisions pour permettre leur réintroduction ultérieure.

### Limite actuelle

La suppression des données du navigateur peut supprimer la collection locale.

Il est donc recommandé d’exporter régulièrement la collection.

---

## 13. Import et export

### Export

L’export produit un fichier JSON contenant :

- les paquets ;
- les cartes ;
- les intervalles ;
- l’historique ;
- les réglages ;
- la série quotidienne.

### Import

L’import remplace la collection locale par celle du fichier choisi.

Avant un import important :

1. exporter la collection actuelle ;
2. conserver le fichier de sauvegarde ;
3. importer la nouvelle collection ;
4. vérifier le nombre de paquets et de cartes.

### Compatibilité

Le format JSON actuel est propre à OusBrain.

Il n’est pas encore compatible directement avec les fichiers `.apkg` d’Anki Desktop.

---

## 14. Contrôles et tests

### Contrôles déjà effectués

- Validation syntaxique de `app.js`
- Navigation entre les écrans
- Ouverture d’un paquet
- Lancement d’une session
- Affichage de la réponse
- Boutons de notation
- Intervalles de la première étape
- Intervalles de la deuxième étape
- Anticipation des cartes
- Chargement de `hafsData_v18.json`
- Chargement de `hafs.18.woff2`
- Police calculée `KFGQPC Hafs`
- Direction RTL
- Poids typographique `400`
- Migration du paquet initial vers les 12 cartes sélectionnées
- Absence visuelle de rond noir sur les cartes testées

### Contrôles à refaire avant publication

- Safari sur iPhone
- Chrome sur Android
- Navigation tactile
- Import/export sur mobile
- Collection volumineuse
- Changement de date
- Changement de fuseau horaire
- Mise à jour d’une ancienne collection
- Mode hors connexion
- Installation PWA
- Accessibilité clavier et lecteur d’écran

---

## 15. Dépannage

### La page est vide

Vérifier :

- que le serveur local fonctionne ;
- que `index.html` existe ;
- que `app.js` est chargé ;
- que la console du navigateur ne contient pas d’erreur.

### La police arabe ne s’affiche pas

Vérifier la présence de :

```text
assets/fonts/hafs.18.woff2
assets/fonts/hafs.18.ttf
```

Vérifier aussi le chemin dans `styles.css`.

### Le texte coranique ne charge pas

Vérifier :

```text
data/hafsData_v18.json
```

L’application doit être ouverte avec un serveur HTTP, pas directement avec `file://`.

### Les cartes ont disparu

Causes possibles :

- changement de navigateur ;
- changement d’URL ;
- suppression des données du site ;
- navigation privée ;
- import d’une autre collection.

Restaurer alors un export JSON récent.

### L’URL locale ne fonctionne pas en 4G

C’est normal. Une adresse `192.168.x.x` n’est accessible que sur le réseau local.

Utiliser un tunnel temporaire ou déployer l’application.

---

## 16. Publication future

### GitHub

Le futur dépôt devra contenir au minimum :

```text
index.html
styles.css
app.js
README.md
assets/fonts/hafs.18.woff2
assets/fonts/hafs.18.ttf
data/hafsData_v18.json
```

### GitHub Pages

Une application statique comme celle-ci peut être publiée avec GitHub Pages.

Avant le déploiement :

- vérifier tous les chemins relatifs ;
- ajouter un favicon ;
- ajouter les métadonnées ;
- tester le chargement direct d’une route ;
- tester les polices ;
- contrôler la taille du JSON ;
- ajouter un cache adapté.

### Nom de domaine

Le nom de domaine sera configuré après validation de la version publique.

### Synchronisation

GitHub Pages ne synchronise pas automatiquement les collections entre appareils.

Une vraie synchronisation demandera plus tard :

- une authentification ;
- une base de données ;
- une API ;
- une gestion des conflits ;
- un chiffrement adapté.

---

## 17. Feuille de route

### Prochaine étape

- Sélecteur **Sourate + Verset**
- Création d’une carte coranique sans saisie manuelle du verset
- Affichage depuis `hafsData_v18.json`
- Aperçu avant enregistrement

### Court terme

- Types de notes
- Modèles de cartes
- Duplication d’une carte
- Options propres à chaque paquet
- Limite maximale de révisions
- Ordre d’affichage configurable
- Amélioration des statistiques
- Sauvegardes automatiques exportables

### Moyen terme

- Import Anki
- Export compatible Anki
- Audio
- Enregistrement de la voix
- Cartes à trous
- Tags
- Sous-paquets
- Cartes suspendues et enfouies
- Recherche avancée

### Long terme

- Compte utilisateur
- Synchronisation multi-appareils
- PWA installable
- Fonctionnement hors connexion
- Dépôt GitHub public
- Déploiement permanent
- Nom de domaine

---

## 18. Règles de contribution

### Avant une modification

1. Exporter la collection de test si nécessaire.
2. Identifier les fichiers concernés.
3. Ne pas modifier les fichiers KFGQPC.
4. Ne pas introduire une autre source coranique.

### Après une modification

1. Vérifier la syntaxe JavaScript.
2. Tester l’écran modifié.
3. Tester sur une largeur mobile.
4. Contrôler l’affichage arabe.
5. Vérifier que la progression est conservée.
6. Mettre à jour ce README si le comportement change.

### Règle absolue pour le Coran

> Une carte coranique doit toujours afficher le texte provenant de `hafsData_v18.json` avec la police KFGQPC Hafs v18 correspondante. Aucun remplacement silencieux par une autre version n’est autorisé.

---

## Licence et ressources

La police KFGQPC Hafs v18 provient du King Fahd Glorious Quran Printing Complex.

Les informations de licence sont intégrées dans les métadonnées de la police. La police ne doit pas être modifiée, décompilée ou vendue seule.

La licence propre au code de l’application devra être choisie avant la publication du dépôt GitHub.
