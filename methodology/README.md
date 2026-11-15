# Méthodologie Power Platform / ChatGPT — V0.8 candidate

**Statut : candidate, non validée fonctionnellement.** La branche `main` et les versions antérieures restent inchangées.

## Architecture
Un dépôt GitHub privé **par développeur**, plusieurs solutions sous `workspaces/<projectId>/`, et des règles partagées dans `methodology/`. Un projet ChatGPT correspond à une solution fonctionnelle, qui peut contenir plusieurs technologies et composants.

## Démarrage d'un nouveau projet
1. Créer un projet ChatGPT et y coller [les instructions V0.8](instructions/CHATGPT_PROJECT_INSTRUCTIONS_V0.8_CANDIDATE.txt).
2. Ajouter les documents métier comme sources du projet ChatGPT, sans publication automatique dans GitHub.
3. Donner le nom/identifiant de solution ; confirmer une seule fois la langue de l'éditeur Power Apps Studio (`fr-FR` ou `en-US`).
4. L'assistant vérifie le dépôt, recherche un workspace existant et propose l'initialisation.
5. Après accord, l'assistant crée la configuration, le manifeste et les fichiers de mémoire, puis relit les écritures pour les vérifier.

Aucun YAML de configuration à écrire manuellement. Si GitHub est indisponible, continuer l'analyse sans prétendre avoir enregistré les résultats.

## Références
- [Standards STD-01 à STD-10](standards/README.md)
- [Décisions V0.8](V0.8_DECISIONS.md)
- [Modèles](templates/)
- [Instructions V0.8](instructions/CHATGPT_PROJECT_INSTRUCTIONS_V0.8_CANDIDATE.txt)

## Compatibilité
Les workspaces historiques restent en place, sans migration automatique. Leur manifeste peut utiliser une ancienne interprétation de L1/L2 ; la nouvelle structure n'est appliquée qu'après analyse et accord. Ne pas écraser des données ou des décisions existantes.

## Vérification
La candidate doit réussir un test d'initialisation sur workspace fictif, puis une reprise sans écrasement, avant proposition de validation. Les tests Studio et Dataverse restent distincts.
