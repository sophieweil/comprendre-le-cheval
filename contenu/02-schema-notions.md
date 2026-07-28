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

## 3. Les 15 mécaniques de jeu

**Point d'attention** : la liste des 15 mécaniques n'a pas été retransmise dans le message de brief reçu par le moteur (elle a été évoquée mais son détail ne figure pas dans la transcription fournie). La liste ci-dessous est donc une **proposition de reconstruction**, cohérente avec les 5 mini-jeux déjà prototypés sur le Dossier D-02 (composants `rws-*` existants) et avec les formats déjà utilisés ailleurs dans l'app (QCM, Interrogatoire Flash). **Elle doit être relue et confirmée par le QG avant que le moteur ne s'appuie dessus.**

1. `qcm` — **QCM classique** : une question, plusieurs choix, une bonne réponse.
2. `vrai_faux` — **Vrai / Faux** : affirmation à trancher, souvent utile pour casser une croyance fréquente.
3. `association` — **Association** : relier deux colonnes (ex. son ↔ signification, sens ↔ organe).
4. `classification` — **Classification / tri** : répartir des éléments dans des catégories (existe déjà : `rws-classify-zone`).
5. `sequence` — **Remise en ordre** : reconstituer une séquence chronologique ou logique (existe déjà : `rws-sequence-item`).
6. `texte_a_trous` — **Texte à trous** : compléter une phrase clé avec le bon terme de vocabulaire.
7. `etude_de_cas` — **Étude de cas / scénario** : une situation concrète à interpréter, avec plusieurs indices.
8. `identification_erreur` — **Identification d'erreur** : repérer l'affirmation fausse glissée dans un lot (format « Kiro se trompe »).
9. `estimation` — **Estimation / curseur** : approcher une valeur chiffrée sans exiger la précision exacte.
10. `indices_progressifs` — **Indices progressifs** : révéler des indices un par un avant de faire trancher.
11. `comparaison` — **Comparaison** : mettre en regard deux situations (nature/domestique, avant/après).
12. `reconnaissance_posture` — **Reconnaissance de posture/situation** : à partir d'une description textuelle ou d'un pictogramme, identifier ce qui est montré.
13. `priorisation` — **Priorisation / hiérarchisation** : classer des éléments par ordre d'importance ou de probabilité.
14. `rappel_differe` — **Rappel différé** : revenir sur une notion vue plus tôt dans le parcours, après un délai.
15. `dilemme_guide` — **Dilemme guidé** : choisir une action face à une situation, puis découvrir la conséquence.

Une notion n'est jamais taguée avec les 15 : seules les mécaniques qui ont un sens pour son contenu réel sont retenues (ex. une notion purement anatomique se prête mal à un « dilemme guidé »).

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

- **`validable_directement`** — fait stable, formulation déjà prudente, pas de chiffre isolé fragile.
- **`a_reformuler`** — le fond est correct mais la formulation des notes est trop catégorique ou trop « il faut » normatif pour un exercice grand public.
- **`a_verifier_scientifiquement`** — contient un chiffre précis, une donnée datée, ou une généralisation à sourcing faible qui mériterait une relecture par Sophie ou une source récente avant diffusion.
- **`a_exclure_temporairement`** — trop proche d'un diagnostic médical, ou repose sur une information interne aux notes jugée incertaine/contradictoire, à ne pas exposer tant que non tranchée.

Motifs de flag typiques : chiffre précis (%, durée, seuil), formulation médicale, généralisation peu sourcée, ton trop certain, contenu potentiellement daté (étude antérieure aux années 2000, ou terminologie qui a pu évoluer).
