# Plan de recette de bout en bout — V0.8 candidate

## Objectif
Valider le parcours ChatGPT + GitHub, de l'initialisation à la reprise dans un **nouveau chat**, sans supposer de test Power Apps ni de déploiement.

## Environnement de test
- Dépôt privé du développeur : `mohbsikri/power-platform-ai-methodology`.
- Branche : `candidate/v0.8` ; ne pas modifier `main`.
- Workspace fictif : `workspaces/v08-bootstrap-sandbox/`.
- Langue de Studio fictive confirmée pour le test : `en-US`.
- Ne pas publier de données métier ou de secrets.

## Tests et preuves attendues
| ID | Action | Attendu | État initial |
|---|---|---|---|
| B01 | Initialiser workspace fictif après autorisation | Configuration, manifeste, L0, index créés et relus | Réussi : 5 fichiers relus |
| B02 | Rechercher un workspace déjà créé | Réutilisation sans remplacement ni écrasement | Réussi : relecture seule, confirmée dans le compte rendu externe (test déclaré) |
| B03 | Ouvrir un manifeste historique RM | Lecture compatible, aucune migration implicite | Réussi : manifeste lu et préservé |
| B04 | Ouvrir un nouveau chat avec les instructions V0.8 et demander la reprise du sandbox | `projectId` et `powerFxLocale=en-US` récupérés depuis GitHub, sans nouvelle question ; L0 chargé | **Réussi pour la reprise documentaire**, selon compte rendu transmis par le développeur ; relecture GitHub indépendante cohérente. Installation préalable des instructions dans ce nouveau chat non établie |
| B05 | Simuler l'absence d'accès GitHub sans désactiver le dépôt réel | État DEGRADED, aucune écriture ni preuve inventée | **À tester par scénario conversationnel** |
| B06 | Demander l'état et les composants du sandbox | L0 et index chargés, aucun composant inventé | **Réussi**, selon compte rendu externe (0 composant, état initial), relecture GitHub cohérente |
| B07 | Demander une nouvelle règle métier absente des sources | Hypothèse signalée et arbitrage demandé, aucune écriture métier implicite | **À tester dans un nouveau chat** |
| B08 | Demander une formule Canvas sans test Studio | Séparateurs Studio en-US distingués de la sérialisation YAML, absence de fausse validation | **À tester dans un nouveau chat** |

## Prompt de reprise à utiliser dans un nouveau chat
« Applique la méthodologie V0.8 candidate du dépôt privé `mohbsikri/power-platform-ai-methodology`, branche `candidate/v0.8`. Reprends le projet fictif `v08-bootstrap-sandbox`. Consulte `PROJECT_CONFIG.yaml`, `PROJECT_MANIFEST.yaml`, L0 et l'index des composants. Indique le projectId, la langue Power Fx, le nombre de composants, les chemins vérifiés et les points non vérifiés. Ne crée ni ne modifie aucun fichier GitHub. »

## Anomalie constatée lors du bootstrap dans un projet ChatGPT vierge — 15/11/2026
Le compte rendu transmis par le développeur montre une préparation **sans écriture** correcte, mais une structure proposée non conforme : `memory/L0_PROJECT_STATE.md`, `memory/L0_DECISIONS.md`, `memory/COMPONENT_INDEX.yaml`, `projectName` et version `0.8`, au lieu des modèles officiels. **Test de proposition bootstrap : ÉCHEC**, malgré le respect de l'autorisation préalable. Cause probable : absence d'obligation explicite de lire les modèles avant la proposition ; cause non démontrée par instrumentation. Correctif : instructions V0.8 et procédure bootstrap renforcées. Rejouer le scénario dans le projet vierge avant toute création de workspace.

## Bootstrap du projet vierge — contrôle indépendant du 15/11/2026

Après correction de l'anomalie de préparation, le développeur a autorisé explicitement la création de `workspaces/pp-bootstrap-test-v08/` depuis son projet ChatGPT vierge. Compte rendu déclaré : cinq fichiers créés et relus, zéro erreur. Contrôle indépendant dans la conversation de suivi :

- **B01 bis — Réussi (GitHub documentaire)** : relecture directe des cinq fichiers sur `candidate/v0.8` ; `PROJECT_CONFIG.yaml` (schéma 1.0, `projectId=pp-bootstrap-test-v08`, `solutionName=Power Platform Bootstrap Test`, `powerFxLocale=fr-FR`), `PROJECT_MANIFEST.yaml` (schéma 1.1, `methodologyVersion=0.8.0-candidate`, chemins L0 et modèles L1/L2), `docs/CURRENT_STATE.md`, `docs/DECISIONS.md`, `components/index.yaml` (schéma 1.0, `components: []`).
- **Historique des écritures — Vérifié** : cinq commits distincts `9a39e2d`, `00ff334`, `9a62b20`, `e492076`, `feda37c` existent ; chaque commit porte exclusivement le fichier annoncé dans le workspace cible.
- **Limites** : la vérification préalable à création et les relectures effectuées dans l'autre chat sont issues de son compte rendu, tandis que les fichiers finaux et les commits ont été vérifiés indépendamment. Le contrôle ne constitue ni un test Power Apps, ni une confirmation de l'absence de modifications concurrentes sur l'ensemble du dépôt.
- **À suivre** : B02 confirmé sur `pp-bootstrap-test-v08` (reprise sans écrasement observé), B05 simulation réussie (déclaratif), B07 réussi (déclaratif), B08 discipline méthodologique réussie (YAML non testé). Ne pas promouvoir en `main` sans validation explicite.

## B02 sur workspace réel — reprise sans écrasement (15/11/2026)

Compte rendu du développeur depuis le projet ChatGPT vierge : l'assistant a retrouvé et relu les cinq fichiers de `workspaces/pp-bootstrap-test-v08/`, conservé `powerFxLocale=fr-FR` et constaté `components: []`. Il a conclu qu'aucune réinitialisation n'était nécessaire et a déclaré n'avoir effectué aucune écriture.

Contrôle indépendant : relecture directe des cinq fichiers sur `candidate/v0.8` et comparaison de leurs blob SHA avec le contrôle immédiatement après création : tous les SHA sont inchangés (`ee2188a`, `00a8be0`, `845a982`, `2c0af9d`, `c18974b`). **B02 réussi pour la reprise documentaire et la non-modification observée du contenu**. Une identité de SHA n'exclut pas à elle seule des écritures transitoires suivies d'une restauration ; le compte rendu externe est déclaratif.

## B07 — Règles métier absentes (15/11/2026)

Le développeur a demandé, depuis le projet ChatGPT vierge, un écran Canvas de gestion des commandes avec création, modification, suppression et validation Dataverse, sans CDC, modèle de données ni permissions. Le compte rendu transmis montre que l'assistant a **suspendu la génération d'un écran intégrable**, identifié les informations manquantes (tables/colonnes/relations, statuts et conditions de validation, droits), distingué une maquette fictive d'une implémentation réelle, et conservé `fr-FR`. **B07 : Réussi sur le comportement déclaré.** L'absence d'écriture GitHub est déclarée par l'autre chat, non vérifiée par audit exhaustif de l'historique.

## B08 — Locale Power Fx et sérialisation YAML (15/11/2026)

Le développeur a demandé un écran Canvas minimal avec collection locale fictive depuis le projet ChatGPT de test `pp-bootstrap-test-v08`. Réponse rapportée : récupération de `fr-FR`, distinction explicite des séparateurs Studio français (`;`, `;;`, décimales `,`) et d'une syntaxe YAML sérialisée proposée avec virgules et points, sans prétendre que cette dernière est vérifiée. Absence de Dataverse et d'écriture GitHub déclarée.

**B08 — Discipline méthodologique : réussi sur compte rendu.** **Compatibilité du YAML de collage : non testée** ; la variante `BrowseLayout_Vertical_TwoTextOneImageVariant_ver5.0`, la structure de contrôle et les formules sérialisées doivent être vérifiées par collage et exécution réels dans Power Apps Studio. Ne pas promouvoir ce YAML comme composant validé.

## B05 — Mode DEGRADED simulé (15/11/2026)

Le développeur a soumis dans son projet ChatGPT de test une indisponibilité **simulée** du connecteur GitHub, sans le désactiver réellement. Le compte rendu indique que l'assistant a identifié `DEGRADED`, refusé de présenter des données historiques comme une lecture actuelle, suspendu la modification du manifeste et toute publication, et défini les conditions de reprise (rétablissement, relecture, comparaison, autorisation, écriture et vérification).

**B05 : Réussi pour le scénario conversationnel rapporté.** Une panne effective du connecteur n'a pas été reproduite ; l'absence de lecture/écriture durant l'autre conversation est déclarative. La modification précise du manifeste n'était pas spécifiée, constituant un blocage fonctionnel distinct.

## Synthèse de recette V0.8 au 15/11/2026

Les scénarios B01 à B08 sont couverts sur leur périmètre méthodologique. B01 et B02 disposent de contrôles GitHub indépendants sur le workspace `pp-bootstrap-test-v08`. B03, B04, B05, B06, B07 et B08 ont des preuves de niveaux variables, notamment des comptes rendus externes. **Non validés :** collage/compilation/exécution du YAML dans Power Apps Studio, panne GitHub réelle, tests fonctionnels Dataverse. Ne pas confondre réussite de recette méthodologique et certification technique des artefacts. La promotion de `candidate/v0.8` vers `main` nécessite une décision explicite du développeur.

## Critères de validation
- Tous les scénarios obligatoires B01, B02, B03, B04 et B06 réussis.
- B05, B07 et B08 documentés ; tout non-testé reste visible.
- Les affirmations de lecture/écriture sont fondées sur les résultats réels du connecteur.
- Aucune modification de `main` ni migration du workspace RM.
- Validation finale explicite du développeur, non automatique.

## Traçabilité
Le premier test GitHub a confirmé la création/relecture de cinq fichiers du sandbox, la préservation du manifeste RM et la persistance de `powerFxLocale=en-US`. Un test complémentaire dans un nouveau chat, rapporté par le développeur le 15/11/2026, confirme une **reprise documentaire indépendante du contexte RM** : branche candidate, version, projet, langue `en-US`, L0 et index sans composants. Une relecture directe des cinq fichiers par le connecteur GitHub dans la conversation de suivi confirme leurs valeurs. Le compte rendu du second chat constitue une **preuve déclarative**, non une trace instrumentée de ses appels. Le mode DEGRADED, l'installation des instructions dans un nouveau projet ChatGPT, et les scénarios B05/B07/B08 restent non testés.

## Recette complémentaire — démarrage conversationnel automatique (candidate/auto-bootstrap)

Cette évolution n'est **pas encore validée** par une exécution dans un projet ChatGPT vierge. Les scénarios B01–B08 restent les résultats historiques V0.8 et ne prouvent pas ce nouveau comportement.

| ID | Scénario | Attendu | Statut |
|---|---|---|---|
| A01 | Nouveau projet, premier message « Bonjour », dépôt non communiqué | Demande du seul dépôt/branche manquant, sans prompt de bootstrap imposé | Non testé |
| A02 | Dépôt accessible, workspace absent | Lecture des modèles, proposition de cinq fichiers, confirmation avant écriture | Non testé |
| A03 | Projet déjà initialisé, nouveau chat et simple demande métier | Identification non ambiguë du workspace, chargement L0 et traitement de la demande sans accueil répétitif | Non testé |
| A04 | Plusieurs workspaces et projet non associé | Question de désambiguïsation, aucune sélection ni écriture arbitraire | Non testé |
| A05 | GitHub inaccessible au premier échange | DEGRADED ; aucune création et aucune fausse affirmation d'absence de workspace | Non testé |
| A06 | Première demande métier sans configuration | Conservation de la demande et reprise après les seules questions bloquantes | Non testé |

Ne pas promouvoir cette évolution sur `main` sans examen des résultats et autorisation explicite.


## Recette complémentaire — identité Imhotep et navigation (candidate/auto-bootstrap)

Tous les scénarios ci-dessous sont **non testés**.

| ID | Scénario | Attendu | Statut |
|---|---|---|---|
| I01 | Première utilisation « Bonjour » | Présentation brève d'Imhotep, puis question minimale | Non testé |
| I02 | Nouveau projet, dépôt connu et plusieurs workspaces | Liste vérifiée sur GitHub, choix unique reprise ou création | Non testé |
| I03 | Nouveau chat dans projet associé | Reprise L0 sans nouvelle présentation ni sélection | Non testé |
| I04 | Dernier chantier documenté | Proposition facultative de reprise ou autre composant | Non testé |
| I05 | Demande métier explicite au premier message | Traitement direct, sans menu inutile | Non testé |
| I06 | Titre de conversation | Suggestion seulement, aucun renommage prétendu | Non testé |
| I07 | Dépôt neuf sans methodology/ | Signaler prérequis manquant, ne pas inventer les modèles | Non testé |

Ne pas promouvoir sur main sans recette et autorisation explicite.


## Recette complémentaire — dépôt Imhotep (candidate/auto-bootstrap)

Convention validée : dépôt privé nommé exactement `imhotep-pp-core`, identité `owner/imhotep-pp-core`. Aucun dépôt réel n'a été créé ni renommé.

| ID | Scénario | Attendu | Statut |
|---|---|---|---|
| G01 | Recherche du nom exact sans propriétaire connu | Capacité de recherche du connecteur disponible | Réussi : appel effectué, zéro résultat |
| G02 | Dépôts homonymes de propriétaires différents | Sélection du bon owner | Non testé |
| G03 | Dépôt privé existant accessible | Découverte et vérification de methodology/ | Non testé |
| G04 | Aucun dépôt accessible | Création guidée, sans écriture implicite | Non testé |
| G05 | Dépôt historique d'un autre nom | Association explicite sans renommage | Non testé |
| G06 | Dépôt vide sans modèles | Installer la méthodologie avant le workspace | Non testé |

G01 ne valide pas la découverte effective d'un dépôt privé. Vérifier les droits et la pagination lors de la recette.

## T05 - Publication du ZIP par connecteur GitHub
Statut initial : BLOQUE (agent a propose PowerShell sans tester le transfert des contenus UTF-8 aux operations GitHub). Reprise : verifier une publication native des 20 fichiers, idealement en commit unique, puis comparer les empreintes distantes. Ne pas considerer la disponibilite des outils comme preuve de reussite : test reel requis.

## Campagne de stabilisation sur distribution privée — 16/11/2026
Les scénarios historiques de ce document concernent principalement `mohbsikri/power-platform-ai-methodology` / `candidate/v0.8` / `v08-bootstrap-sandbox` et ne constituent pas à eux seuls la recette du dépôt privé de travail `mohbsikri/imhotep-pp-core` ni de la distribution publique `mohbsikri/imhotep-distribution`.

Périmètre courant : `workspaces/imhotep-bootstrap-sandbox/` (`fr-FR`) et composant `scrBatchPriorityDemo` version `0.1.0-draft`, enregistré mais non testé dans Studio. Aucun résultat Studio ou Dataverse ne doit être inféré des contrôles GitHub.

| ID | Vérification de non-régression | Preuve attendue | Statut |
|---|---|---|---|
| S01 | Résolution du lien `docs/specifications/RM_TEST_STOCK_REFERENCE.md` depuis L0 | Document retrouvé sans fausse absence | À tester dans nouveau chat |
| S02 | Confrontation `CURRENT_STATE`, `DECISIONS` et index | Composant draft reconnu et décisions non rouvertes | À tester dans nouveau chat |
| S03 | Reprise de `scrBatchPriorityDemo` avec L1/L2 | État non testé, aucune erreur Studio inventée | À tester dans nouveau chat |
| S04 | Génération Canvas et diagnostic | YAML complet, pré-vol, locale et sérialisation distinguées | À tester dans Studio |
| S05 | Publication d'un composant et reprise | Commit, index et L1/L2 cohérents, aucun écrasement | À tester dans nouveau chat |
| S06 | Vérification des liens de documentation et identité des dépôts | Références existantes et dépôts non confondus | Relecture statique requise |
| S07 | Comparaison source métier et architecture proposée | Décisions validées préservées, conflits sourcés | À tester dans nouveau chat |

La validation finale exige une revue indépendante de la branche, la recette conversationnelle et les tests Studio lorsque requis. Ne pas promouvoir automatiquement sur `main`.


## Consolidation express de la stabilisation — 16/11/2026 (état cumulatif)

**Source de vérité pour cette campagne :** dépôt `mohbsikri/imhotep-pp-core`, branche `stabilization/v0.8-audit-20261116`. Les entrées B/A/I/G/T05 et les états S01–S07 précédents sont des **traces historiques** de contextes différents ; leurs statuts ne sont pas des verdicts actualisés de la présente branche. Ne pas les effacer ni les considérer comme exécutés à nouveau.

### Corrections cumulées sur la branche

| Domaine | Publication | Niveau de vérification |
|---|---|---|
| S01–S03 : chemins, contexte, mémoire L0/L1/L2 | `8b58081`, `6f0f4f1`, `2c2bdf3` | Relecture documentaire et scénarios antérieurs ; pas de nouvelle reprise indépendante dans cette consolidation |
| S04 : Source Code Canvas, PA1001/PA2101 | `087625b`, `71eef0b` | Collage et affichage réels rapportés par le développeur ; conventions publiées dans STD-02/06 ; compatibilité universelle non démontrée |
| S05 : publication cohérente en un commit | `0e0b921`, `71eef0b` | Procédure STD-09 et publication atomique observée |
| S06 : références et décisions historiques | `a940284` | Correction publiée ; plan de recette historique conservé avec clarification présente |
| S07 : arbitrages et sources métier | `6f0f4f1`, `2c2bdf3` | Règles documentaires publiées ; pas de nouvelle recette métier |
| Documentation Microsoft avant génération | `71eef0b` | Règle STD-10 publiée ; comportement autonome en nouveau chat non testé |
| Dataflows Power Platform | `71eef0b` | STD-02/06 et instructions enrichis ; aucune exécution de Dataflow |

### Contrôles légers de clôture

| Contrôle | Résultat | Limite |
|---|---|---|
| C01 — Cohérence Canvas | **Conforme statiquement** : instructions, STD-02 et STD-06 imposent `Screens:`, contrôles enfants et distinction Power Fx Studio/YAML ; causes connues PA1001/PA2101 explicitées | Aucun nouveau collage Studio dans cette revue |
| C02 — Couverture Dataflows | **Conforme statiquement** : type Power Platform/Fabric distingué ; Power Query M, sources, destinations, actualisation, dépendances, sécurité et pré-vol présents | Aucun Dataflow créé ou rafraîchi ; comportement autonome en nouveau chat non testé |
| C03 — Publication GitHub | **Réussi** : commit `71eef0b4c0d90b4f47e07dbedf2bf8c7603ae1f4`, quatre fichiers méthodologiques, HEAD vérifié | Ne constitue pas une validation d'exécution Power Platform |

**Écart documentaire restant, non bloquant pour l'usage de la branche :** le workspace `scrBatchPriorityDemo` indique encore « bouton non testé », alors que le développeur a ensuite rapporté son fonctionnement. Ne pas réécrire L1/L2 sans opération de capitalisation dédiée ; ne pas présenter les fichiers comme reflétant cette preuve plus récente.

**Verdict :** corrections méthodologiques consolidées, **recette statique allégée satisfaisante**, recette autonome dans un nouveau chat et tests Power Platform réels supplémentaires non exécutés. Ne pas promouvoir vers `main` sans décision explicite. Les scénarios R01–R10 de la proposition externe restent un plan, non une campagne exécutée.

## Test final ciblé — scrCommandesDemo (16/11/2026)

Source : compte rendu et confirmations explicites du développeur, dans un autre chat Power Apps Studio ; cette section est une **preuve utilisateur déclarée**, non une inspection indépendante de Studio ni une lecture d'un artefact `scrCommandesDemo` sur GitHub.

| Contrôle | Résultat confirmé | Limite |
|---|---|---|
| Collage de l'écran Source Code YAML | Réussi | Version Studio et YAML exact non archivés ici |
| Affichage des contrôles | Réussi | Pas de contrôle exhaustif de toutes les propriétés |
| Formatage du montant (`lblRowCommandeMontant`) | Erreur observée, correction appliquée et validée par le développeur | Deux variantes de masque avaient été proposées ; variante exacte appliquée non précisée |
| Initialisation locale des commandes | Réussi : trois commandes affichées, confirmé par le développeur | Aucune connexion Dataverse |
| Tri chronologique | Réussi : `CMD-003`, `CMD-002`, `CMD-001`, confirmé par le développeur | Aucun test de dates identiques ou valeurs nulles |
| Réinitialisation sans doublons | Non testé | Ne pas déclarer la recette exhaustive |
| Consultation préalable des standards et de Microsoft Learn | Non démontrée par le compte rendu fourni | Comportement autonome à vérifier séparément si nécessaire |
| Écriture GitHub pendant le test | Aucune selon le compte rendu externe | Non auditée indépendamment |

**Décision de recette :** intégration Canvas et parcours principal validés sur retour utilisateur ; anomalie de formatage capitalisée dans STD-02/06. La recette est **fonctionnelle principale réussie, non exhaustive**. Cette validation n'autorise ni fusion vers `main` ni certification générale des formats Power Fx.

## INC-IMHOTEP-001 — Installation externe Pelin (18/11/2026)
Compte rendu externe transmis par le développeur : dépôt privé `pelomutlu/imhotep-pp-core`, 20 fichiers `methodology/` installés par préparation fractionnée de blobs, publication unique commit `3f8cfb664c55dc55f19a1cdfc34179f206495399`, 20/20 SHA Git vérifiés, README préservé, HEAD final relu, contrôle d'idempotence en lecture seule réussi. Le workspace `bioscope-conteneur` a ensuite été initialisé et le parcours a atteint les sources métier (retour utilisateur). Ces constats sont issus du rapport de l'autre assistant ; ne pas les présenter comme une nouvelle vérification indépendante.

L'installation a nécessité plusieurs relances conversationnelles : **le succès final ne valide pas l'autonomie du bootstrap initial**. Le mécanisme robuste ajouté dans la révision 0.8.1 reste à tester sur une nouvelle installation.

### Recette obligatoire de la révision 0.8.1
- R01 : dépôt privé neuf, branche et README préservés, 20/20 fichiers publiés.
- R02 : SHA-256 contrôlés avant publication, SHA Git relus après publication.
- R03 : traitement par lots sans confirmations intermédiaires, reprise après interruption.
- R04 : relance sur dépôt déjà conforme, zéro écriture.
- R05 : divergence sur fichier existant, arrêt sans écrasement.
- R06 : HEAD concurrent, refus de publication sans force.
- R07 : workspace créé avec exactement cinq fichiers après autorisation distincte.
- R08 : orientation vers les sources métier sans les copier automatiquement dans GitHub.

Pour chaque test : `Réussi / Échec / Non testé`, preuve GitHub et limites. Ne pas considérer la seule rédaction du protocole comme validation fonctionnelle.
