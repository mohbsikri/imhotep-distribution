# STD-02 — Standards techniques Power Platform
Version : 0.8.0-candidate

## Canvas / YAML de collage Studio
- Produire du **Power Apps Source Code YAML** complet, destiné au collage d'écrans/contrôles dans Power Apps Studio ; pas de YAML générique.
- Le format `.pa.yaml` est hors du périmètre standard V0.8.
- Ne pas présumer qu'un exemple documentaire compile dans la version de Studio du développeur.
- Protéger les valeurs YAML contenant `:` ou des caractères spéciaux ; privilégier `|-` pour les formules multilignes.
- Pour une erreur de collage, fournir le bloc YAML complet corrigé.
- Vérifier propriétés et versions de contrôles, initialisation des collections, géométrie et chevauchement des galeries.

## Power Fx et langue de Studio
- Lire `powerFxLocale` dans `PROJECT_CONFIG.yaml` ; demander une fois si absent, ne pas déduire la langue de Studio de la langue du chat.
- `fr-FR` dans l'éditeur : arguments `;`, instructions successives `;;`, décimales `,`.
- `en-US` dans l'éditeur : arguments `,`, instructions successives `;`, décimales `.`.
- **La sérialisation Power Fx dans le YAML de collage peut différer** : utiliser les exemples et essais Studio validés pour le projet, sinon signaler explicitement l'incertitude.
- Ne pas utiliser `;;` comme séparateur d'arguments ; vérifier `Set`, `If`, `Filter`, `Collect`, `Notify`.
- `RGBA` : opacité de 0 à 1 ; contrôler délégation et erreurs de données.

## Dataverse
- Vérifier tables, colonnes, types, relations, clés, contraintes, sécurité et droits à partir du modèle réel.
- Pour les écritures multiples, analyser erreurs, ordre, cohérence et états partiellement mis à jour ; ne pas présumer de transaction atomique Canvas.
- Distinguer test sur collection locale et test réel Dataverse ; ne jamais inventer des schémas ou autorisations.

## Power Automate
- Identifier type de déclencheur, connexions, références de connexion, variables d'environnement, entrées/sorties et expressions.
- Examiner conditions, boucles, pagination, limites, délais, reprises, erreurs, idempotence et exécutions partielles selon la criticité.
- Vérifier les politiques DLP, les droits et les licences lorsque pertinents ; ne pas affirmer leur conformité sans observation dans l'environnement.
- Décrire les tests d'exécution nécessaires ; ne pas déclarer un flux opérationnel sur la seule base d'un schéma.

## Model-driven, solutions et ALM
- Respecter composants, dépendances, rôles, environnements, solutions gérées/non gérées et configuration propre à chaque environnement.
- Avant une procédure de déploiement, identifier les prérequis, les références de connexion, les variables d'environnement et les impacts de sécurité.
- Aucune connexion ni exécution autonome dans Power Platform n'est supposée.

## Traçabilité
Qualifier chaque affirmation : CDC explicite, décision validée, documentation officielle, test observé ou proposition à vérifier. Conserver les références techniques utiles sans recopier les documents source.
