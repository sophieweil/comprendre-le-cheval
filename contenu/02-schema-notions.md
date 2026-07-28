# Base de connaissances Ride With So — schéma des notions

Statut : **matière première du moteur, non branchée à l'interface**. Rien dans ce dossier n'est encore lu par `ethologie_cheval_app.html`. En attente de validation QG avant toute intégration ou construction de session finale.

Source unique : `01-notes-transcription-source.md` (transcription des notes de DU de Sophie, chapitres 1 à 6).

---

## 1. Schéma de données d'une notion

Chaque notion est une unité de contenu autonome, exploitable seule pour générer un ou plusieurs exercices. Elle correspond à un fait ou mécanisme précis (ex : « le cheval est dichromate », pas « la vision du cheval » en bloc).

| # | Champ | Type | Description |
|---|-------|------|--------------|
| 1 | `id` | string | Identifiant court stable, ex. `MS-01`. Préfixe = catégorie. |
| 2 | `chapitre` | string | Chapitre source des notes (1 à 6). |
| 3 | `categorie` | enum | Une des 6 catégories pédagogiques (voir §2). Alignée sur le chapitre. |
| 4 | `sous_theme` | string | Sous-partie précise dans le chapitre (ex. « vision — champ visuel »). |
| 5 | `titre_court` | string | Titre affichable, orienté utilisateur (pas un titre de cours). |
| 6 | `difficulte` | enum | `facile` / `moyen` / `difficile` — complexité conceptuelle, pas gravité. |
| 7 | `fait_scientifique_principal` | string | La notion centrale, formulée comme un fait établi et sourcé par les notes. |
| 8 | `explication_courte` | string | 2-4 phrases de vulgarisation, sans jargon inexpliqué. |
| 9 | `observations_possibles` | liste | Ce qu'un observateur peut concrètement voir/entendre chez un cheval réel, en lien avec la notion. |
| 10 | `contextes_possibles` | liste | Situations où l'observation prend un sens différent (ex. même posture ≠ même cause selon le contexte). |
| 11 | `hypotheses_prudentes` | liste | Interprétations plausibles à formuler au conditionnel, jamais en certitude. |
| 12 | `erreurs_ou_croyances_frequentes` | liste | Idées reçues ou raccourcis que la notion vient corriger. |
| 13 | `informations_complementaires_a_rechercher` | liste | Zones où les notes elles-mêmes indiquent une incertitude, un manque d'étude, ou une piste à creuser. |
| 14 | `conclusions_possibles` | liste | Ce que l'on peut raisonnablement conclure d'une observation isolée. |
| 15 | `conclusions_non_etablies` | liste | Ce que cette même observation ne permet PAS de conclure (garde-fou anti-sur-interprétation). |
| 16 | `vocabulaire_cle` | liste | Termes techniques introduits, avec leur définition courte. |
| 17 | `exemple_concret` | string | Exemple tiré des notes (marqué `Ex :` dans la transcription) ou reformulé à l'identique. |
| 18 | `feedback_positif_court` | string | Phrase de validation si l'apprenant répond juste — encourageante, non redondante avec l'explication. |
| 19 | `feedback_correctif_court` | string | Phrase si l'apprenant se trompe — corrige sans décourager, redirige vers le fait clé. |
| 20 | `precaution_scientifique` | string | Rappel spécifique à cette notion : ce qu'il ne faut pas en déduire, ou son caractère daté/isolé. |
| 21 | `references_notes` | liste | Auteurs/études cités explicitement dans les notes pour cette notion (vide si les notes ne citent personne — ne jamais inventer une référence). |
| 22 | `mecaniques_compatibles` | liste | Sous-ensemble des 15 mécaniques (§3) jugées adaptées à cette notion. |

Deux champs supplémentaires, ajoutés par l'étape de contrôle (étape 6, pas partie du schéma de contenu lui-même) :

| Champ | Type | Description |
|-------|------|--------------|
| `statut_revue` | enum | `validable_directement` / `a_reformuler` / `a_verifier_scientifiquement` / `a_exclure_temporairement` |
| `motif_revue` | string | Pourquoi ce statut a été attribué (vide si `validable_directement`). |

---

## 2. Les 6 catégories pédagogiques

Correspondance directe avec les chapitres des notes :

1. **Monde sensoriel** (chapitre 1)
2. **Apprentissage** (chapitre 2)
3. **Communication** (chapitre 3)
4. **Budget temps** (chapitre 4)
5. **Domestication** (chapitre 5, structure générale)
6. **Bien-être et observation** (chapitre 6 + les passages « stéréotypies / mal-être » du chapitre 5)

Le chapitre 6 (cours Hausberger) recoupe largement les chapitres 4 et 5 mais apporte des données chiffrées et des références d'études précises. Ses notions sont réparties entre « domestication » et « bien-être et observation » selon leur objet, plutôt que traitées comme une 7ᵉ catégorie — décision prise pour respecter la consigne des 6 catégories, à valider par Sophie si elle préfère une septième catégorie « sources scientifiques ».

---

## 3. Les 15 mécaniques de jeu — liste officielle

La liste ci-dessous est la liste **officielle**, confirmée par le QG. Elle remplace la liste reconstruite utilisée dans une version précédente de ce document et des fichiers de données. Chaque mécanique conserve un nom technique interne en `snake_case` (utilisé dans `mecaniques_compatibles` et dans le champ `mecanique` des exercices), avec correspondance explicite vers l'intitulé officiel.

| # | Intitulé officiel | Nom technique | Ancien nom reconstruit (abandonné) |
|---|---|---|---|
| 1 | Mot manquant | `mot_manquant` | texte_a_trous |
| 2 | Phrase à reconstruire | `phrase_a_reconstruire` | (absent de la liste reconstruite) |
| 3 | Observation ou interprétation | `observation_ou_interpretation` | (absent de la liste reconstruite) |
| 4 | Vrai, faux ou pas assez d'indices | `vrai_faux_ou_indices_insuffisants` | vrai_faux (sans la 3ᵉ option) |
| 5 | Trouver l'intrus | `trouver_intrus` | identification_erreur (partiellement) |
| 6 | Associer deux éléments | `associer_deux_elements` | association |
| 7 | Remettre une séquence dans l'ordre | `remettre_sequence_ordre` | sequence |
| 8 | Choisir plusieurs indices avant de conclure | `indices_avant_conclusion` | indices_progressifs |
| 9 | Éliminer une conclusion abusive | `eliminer_conclusion_abusive` | (absent de la liste reconstruite) |
| 10 | Choisir un niveau de certitude | `niveau_de_certitude` | (absent de la liste reconstruite) |
| 11 | Corriger le rapport d'un enquêteur | `corriger_rapport_enqueteur` | identification_erreur (autre partie ; proche du format « Kiro se trompe » déjà présent dans l'app) |
| 12 | Comparer deux contextes | `comparer_deux_contextes` | comparaison |
| 13 | Identifier l'information manquante | `information_manquante` | (absent de la liste reconstruite) |
| 14 | Classer plusieurs éléments | `classer_elements` | classification |
| 15 | Choisir la meilleure étape suivante | `meilleure_etape_suivante` | dilemme_guide |

**Le QCM classique n'appartient pas à cette liste de 15.** Il reste un format de base déjà utilisé ailleurs dans l'app (ex. Interrogatoire Flash), utilisable en complément mais plafonné à 1 occurrence par notion (voir consigne du lot pilote). Son nom technique dans les exercices est `qcm_classique`, distinct du champ `mecaniques_compatibles` qui ne référence que les 15 mécaniques officielles.

Une notion n'est jamais taguée avec les 15 : seules les mécaniques qui ont un sens pour son contenu réel sont retenues (ex. une notion purement anatomique se prête mal à « choisir la meilleure étape suivante »). Certaines mécaniques (`phrase_a_reconstruire`, `information_manquante`) ne sont pas encore utilisées dans ce lot pilote de 25 notions ; cela ne signifie pas qu'elles sont invalides, seulement qu'aucune notion actuelle ne s'y prêtait mieux qu'à une autre.

## 3bis. Structure du champ `references_notes`

Pour distinguer explicitement l'origine de chaque élément d'une notion, `references_notes` est structuré en trois parties plutôt qu'une simple liste :

```
"references_notes": {
  "bibliographie_explicite": [...],            // références auteur/année réellement citées dans les notes (ex. "Hausberger 2009") — vide si les notes ne citent personne pour cette notion
  "affirmations_notes_sans_reference": [...],   // noms des champs qui paraphrasent un contenu affirmé par les notes elles-mêmes, sans qu'une étude y soit nommée
  "interpretations_structuration": [...]        // noms des champs qui sont une valeur ajoutée par la structuration (hypothèses, mises en garde, feedback...), absents tels quels du texte source
}
```

Par construction, `interpretations_structuration` contient presque toujours les mêmes champs (`observations_possibles`, `contextes_possibles`, `hypotheses_prudentes`, `erreurs_ou_croyances_frequentes`, `informations_complementaires_a_rechercher`, `conclusions_possibles`, `conclusions_non_etablies`, `precaution_scientifique`, `feedback_positif_court`, `feedback_correctif_court`) : ce sont par nature des ajouts pédagogiques, pas des citations. `bibliographie_explicite` ne doit jamais contenir de référence absente du document source — aucune référence n'est inventée.

---

## 4. Règles d'écriture scientifique (appliquées à chaque notion et exercice)

- Ne jamais attribuer un sens certain à un comportement isolé observé une seule fois.
- Toujours distinguer explicitement : fait établi / interprétation / hypothèse. Les hypothèses sont formulées au conditionnel.
- Rappeler que le contexte change le sens d'une observation (même signal ≠ même cause selon la situation).
- Encourager la recherche de plusieurs indices convergents plutôt qu'un seul signe.
- Rappeler la variabilité individuelle (deux chevaux ne réagissent pas forcément pareil).
- Ne jamais transformer une observation comportementale en diagnostic médical. Un signe de mal-être potentiel oriente vers « en parler à un professionnel / vétérinaire », jamais vers un nom de maladie affirmé.
- Signaler explicitement les affirmations prudentes, anciennes ou non confirmées par les notes elles-mêmes (les notes le font déjà par endroits — ex. « pas d'étude précise, tout reste à démontrer » — ces réserves doivent être conservées dans l'exercice, pas lissées).

---

## 5. Statuts de revue (étape de contrôle)

**Règle de disqualification automatique (posée par le QG) :** une notion contenant un chiffre précis, un seuil, une affirmation médicale, une causalité, ou une généralisation absolue **ne peut pas** recevoir automatiquement le statut `validable_directement`, même si sa formulation semble par ailleurs prudente. Elle doit systématiquement être classée dans l'un des trois statuts suivants — le classement en `validable_directement` est réservé aux notions ne comportant strictement aucun de ces cinq éléments.

- **`validable_directement`** — fait stable, formulation déjà prudente, aucun chiffre, seuil, affirmation médicale, causalité ou généralisation absolue.
- **`a_reformuler`** — le fond est correct mais la formulation est trop catégorique, normative, ou présente une interprétation comme un résultat démontré (confusion résultat/interprétation).
- **`a_verifier_scientifiquement`** — contient un chiffre précis, un seuil, une donnée datée, une affirmation à caractère médical/physiologique, ou une généralisation à sourcing faible qui mériterait une relecture par Sophie ou une source récente avant diffusion.
- **`a_exclure_temporairement`** — trop proche d'un diagnostic médical individuel, ou repose sur une information interne aux notes jugée incertaine/contradictoire, à ne pas exposer tant que non tranchée.

Motifs de flag typiques : chiffre précis (%, durée, seuil), formulation médicale ou physiologique, causalité affirmée à partir d'une simple corrélation, généralisation absolue (« jamais », « toujours »), ton trop certain, contenu potentiellement daté (étude antérieure aux années 2000, ou terminologie qui a pu évoluer).
