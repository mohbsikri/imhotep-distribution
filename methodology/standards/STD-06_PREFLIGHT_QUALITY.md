# STD-06 — Pré-vol et qualité des livrables
Version : 0.8.0-candidate

## Objectif
Détecter avant intégration les incohérences statiquement identifiables, sans présenter une revue du modèle comme une preuve de compilation, de collage réussi ou d'exécution.

## Proportionnalité
- **Standard** : nouveau composant, écran, flux, modèle, changement métier, permission ou dépendance significative.
- **Ciblé** : correction mineure à impact circonscrit ; vérifier le changement et les régressions plausibles.
- Si l'impact est incertain, identifier les dépendances et élargir le contrôle utile, sans imposer une checklist artificielle.

## Checklist adaptée au livrable
- **Sources et périmètre** : exigences, décisions, hypothèses, éléments ouverts, révision et composant.
- **YAML Canvas** : Power Apps Source Code YAML destiné au collage Studio, structure, indentation, chaînes contenant `:`, blocs `|-`, versions et propriétés de contrôles ; `.pa.yaml` hors périmètre standard V0.8.
- **Canvas — pré-vol ciblé PA1001/PA2101** : pour un écran complet, vérifier la racine `Screens:`, l'identifiant d'écran, `Properties:` et la liste `Children:` ; refuser `Control: Screen` / `Control: Screen@1.0.0` à la racine (cause PA2101 observée). Contrôler indentation, guillemets, `: ` non protégé, blocs `|-` et valeurs YAML ambiguës (causes possibles de PA1001). Vérifier types/versions des contrôles enfants et ne pas transformer les virgules de formules YAML en `;` au seul motif que Studio est en fr-FR. Pré-vol statique ≠ validation du parseur Studio.
- **Power Fx** : lire `powerFxLocale` dans `PROJECT_CONFIG.yaml` ; fr-FR (arguments `;`, séquences `;;`) ou en-US (arguments `,`, séquences `;`) pour l'éditeur. Vérifier séparément la sérialisation YAML à partir d'exemples ou tests Studio confirmés. Contrôler types, références et initialisation.
- **Montants et formats numériques** : pour les propriétés `Text` utilisant `Text(nombre; format; langue)`, vérifier séparateurs Studio vs YAML, masque de format, locale explicite et caractères spéciaux (espaces, `#`, symbole monétaire). Prévoir un test d'affichage réel, notamment dans les galeries ; une formule de formatage peut échouer malgré un collage YAML réussi. Référence : retour `scrCommandesDemo` du 16/11/2026 (STD-02).
- **Interactions** : événements, visibilité, états et transitions, matrice STD-01 si pertinente.
- **Données / Dataverse** : tables, champs, relations, clés, délégation, permissions, erreurs et écritures partielles ; ne pas inventer de schéma.
- **Power Automate** : déclencheur, expressions, connexions, variables d'environnement, conditions, reprises et erreurs ; DLP et droits à vérifier en environnement si pertinents.
- **Dataflows** : identifier Power Platform ou Fabric Gen2, sources/connecteurs, paramètres, passerelles, transformations M, typage, destinations et mappings, clés/doublons, idempotence, actualisation et ordre des dépendances, schéma évolutif, erreurs et actualisations partielles, sécurité/DLP/licences, performances/query folding si applicable. Ne pas déclarer un rafraîchissement ou un déploiement réussi sans preuve réelle.
- **Model-driven / ALM** : dépendances, rôles, solutions et prérequis de déploiement selon la tâche.
- **Ergonomie** : dimensions, débordements, chevauchements et responsive si applicable.
- **Livraison** : identifiant et révision (STD-07), intégration, points non vérifiés et recette adaptée (STD-05).

## Rapport de pré-vol
Pour les contrôles pertinents : **Conforme statiquement**, **À corriger**, **Non vérifiable ici** ou **Non applicable**. Signaler les défauts bloquants avant livraison. Les points non vérifiables sont transférés à la recette.

## Limites
Une inspection par modèle n'est ni un parseur YAML, ni un compilateur Power Fx, ni un test Studio, Dataverse ou Power Automate. Ne pas déclarer « compilé », « exécuté » ou « validé » sans preuve. Aucun outil local, PAC CLI ou exécution autonome n'est requis.
