# STD-02 — Standards techniques Power Platform
Version : 0.8.0-candidate

## Canvas / YAML de collage Studio
- Produire du **Power Apps Source Code YAML** complet, destiné au collage d'écrans/contrôles dans Power Apps Studio ; pas de YAML générique.
- Le format `.pa.yaml` est hors du périmètre standard V0.8.
- Ne pas présumer qu'un exemple documentaire compile dans la version de Studio du développeur.
- Protéger les valeurs YAML contenant `:` ou des caractères spéciaux ; privilégier `|-` pour les formules multilignes.
- Pour une erreur de collage, fournir le bloc YAML complet corrigé.
- Vérifier propriétés et versions de contrôles, initialisation des collections, géométrie et chevauchement des galeries.

### Convention expérimentale d'écran complet — Source Code Studio
Pour un écran complet collé dans l'arborescence Studio, utiliser la structure suivante, confirmée sur `scrBatchPriorityDemo` (Studio du 16/11/2026) :

```yaml
Screens:
  scrExample:
    Properties:
      Fill: =RGBA(255, 255, 255, 1)
    Children:
      - lblTitle:
          Control: Label@2.5.1
          Properties:
            Text: ="Example"
```

- La racine est `Screens:`, suivie de l'identifiant d'écran, `Properties:` et, pour les contrôles, `Children:`. Ne pas déclarer l'écran racine avec `Control: Screen` ni `Control: Screen@1.0.0` : ces variantes ont provoqué PA2101 dans le test de collage.
- Déclarer les **contrôles enfants** avec leur type/version vérifiés pour le Studio cible ; `Label@2.5.1` n'est qu'un exemple testé, pas une garantie de compatibilité universelle.
- Protéger les valeurs YAML ambiguës, notamment les formules contenant `: ` ; employer `|-` pour les formules multilignes ou sensibles lorsque pertinent, sans l'imposer à toutes les formules.
- Le YAML testé sérialise les arguments Power Fx avec des virgules alors que l'éditeur Studio était configuré en fr-FR. Ne pas convertir automatiquement les séparateurs du YAML en séparateurs de l'éditeur ; vérifier la représentation Source Code attendue.
- Ce résultat concerne le **mécanisme de génération**, pas les données fictives ni les règles métier du prototype. Le format Source Code et les versions de contrôles peuvent évoluer : vérifier STD-10 en cas d'incertitude.

## Power Fx et langue de Studio
- Lire `powerFxLocale` dans `PROJECT_CONFIG.yaml` ; demander une fois si absent, ne pas déduire la langue de Studio de la langue du chat.
- `fr-FR` dans l'éditeur : arguments `;`, instructions successives `;;`, décimales `,`.
- `en-US` dans l'éditeur : arguments `,`, instructions successives `;`, décimales `.`.
- **La sérialisation Power Fx dans le YAML de collage peut différer** : utiliser les exemples et essais Studio validés pour le projet, sinon signaler explicitement l'incertitude.
- Ne pas utiliser `;;` comme séparateur d'arguments ; vérifier `Set`, `If`, `Filter`, `Collect`, `Notify`.
- `RGBA` : opacité de 0 à 1 ; contrôler délégation et erreurs de données.

### Formatage numérique dans les galeries Canvas — retour Studio du 16/11/2026
- Pour une propriété `Text` affichant un montant, distinguer **format numérique**, **locale de formatage** et **séparateurs de la formule**. Ne pas transposer mécaniquement un masque de format entre YAML sérialisé et éditeur français.
- Cas réellement corrigé dans l'éditeur fr-FR pour `lblRowCommandeMontant` :

```powerfx
Text(
    ThisItem.Montant;
    "[$-fr-FR]# ##0,00";
    "fr-FR"
) & " €"
```

- Le développeur a confirmé la résolution de l'erreur de montant après correction ; la version exacte du masque finalement retenu n'a pas été distinguée du repli proposé `"0,00"`. **Ne pas affirmer que chacun des deux masques a été testé.**
- Lors de la génération YAML, utiliser la sérialisation adaptée à ce format ; si le masque personnalisé ou l'échappement reste incertain, privilégier une formule simple documentée, puis demander une validation dans Studio. Ne pas qualifier la simple relecture de compilation.

## Dataverse
- Vérifier tables, colonnes, types, relations, clés, contraintes, sécurité et droits à partir du modèle réel.
- Pour les écritures multiples, analyser erreurs, ordre, cohérence et états partiellement mis à jour ; ne pas présumer de transaction atomique Canvas.
- Distinguer test sur collection locale et test réel Dataverse ; ne jamais inventer des schémas ou autorisations.

## Power Automate
- Identifier type de déclencheur, connexions, références de connexion, variables d'environnement, entrées/sorties et expressions.
- Examiner conditions, boucles, pagination, limites, délais, reprises, erreurs, idempotence et exécutions partielles selon la criticité.
- Vérifier les politiques DLP, les droits et les licences lorsque pertinents ; ne pas affirmer leur conformité sans observation dans l'environnement.
- Décrire les tests d'exécution nécessaires ; ne pas déclarer un flux opérationnel sur la seule base d'un schéma.

## Dataflows Power Platform / Power Query M
- Traiter chaque Dataflow comme un composant technique autonome (`technology: dataflow`) avec identité, environnement, propriétaire, statut, sources, dépendances et historique L0/L1/L2 selon STD-09.
- Qualifier le **type de Dataflow** et ses capacités avant conception : Dataflows Power Platform (notamment destination Dataverse) et Dataflow Gen2 Microsoft Fabric sont distincts ; ne pas présumer des mêmes destinations, licences, pipelines, modalités d'export ou déploiement.
- Décrire les connecteurs, schémas, paramètres, passerelles et identités d'accès ; documenter les transformations Power Query M, typage, jointures, valeurs nulles et règles de qualité.
- Vérifier les destinations et mappings, clés, stratégie de chargement, doublons, idempotence, évolution des schémas, comportement en cas d'échec et d'actualisation partielle.
- Décrire actualisation manuelle/planifiée selon capacités, fuseau horaire, durées, historiques, reprises, surveillance et ordre de rafraîchissement des dépendances ; ne pas supposer qu'un Dataflow consommateur actualise automatiquement sa source.
- Examiner sécurité, DLP, licences, volumes, performances et query folding lorsque pertinent. Distinguer conception, déploiement et exécution réellement testée ; vérifier les fonctionnalités et limitations dans la documentation officielle applicable (STD-10).

## Model-driven, solutions et ALM
- Respecter composants, dépendances, rôles, environnements, solutions gérées/non gérées et configuration propre à chaque environnement.
- Avant une procédure de déploiement, identifier les prérequis, les références de connexion, les variables d'environnement et les impacts de sécurité.
- Aucune connexion ni exécution autonome dans Power Platform n'est supposée.

## Traçabilité
Qualifier chaque affirmation : CDC explicite, décision validée, documentation officielle, test observé ou proposition à vérifier. Conserver les références techniques utiles sans recopier les documents source.
