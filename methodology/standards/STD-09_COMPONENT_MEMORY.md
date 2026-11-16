# STD-09 — Mémoire par composant et santé du contexte
Version : 0.8.0-candidate

## Périmètre
Un développeur possède un dépôt GitHub privé unique ; un projet ChatGPT = une solution fonctionnelle Power Platform = un workspace `workspaces/<projectId>/`. Une solution peut contenir Canvas, Dataverse, Power Automate, Model-driven et autres composants. Aucun workspace par technologie.

## Trois granularités
- **L0 global** : état du projet, décisions structurantes, version de méthode, architecture et index des composants.
- **L1 par composant** : état actuel, objectif, dépendances connues, version et chemins des artefacts.
- **L2 par composant** : historique, incidents, corrections, tests et preuves détaillés.

Les niveaux sont des granularités de chargement de mémoire, **pas** des catégories de documents (SPECIFICATIONS, TESTS, etc.). Le manifeste référence L0 et l'index ; l'index référence L1/L2 de chaque composant.

## Organisation
- `PROJECT_CONFIG.yaml` : identité et préférences du projet, notamment `powerFxLocale`.
- `PROJECT_MANIFEST.yaml` : version méthodologique, chemins L0 et index.
- `docs/CURRENT_STATE.md`, `docs/DECISIONS.md` : mémoire globale.
- `components/index.yaml` : index des composants et dépendances.
- `components/<technology>/<componentId>/` : mémoire ciblée et traces détaillées uniquement pour les composants réellement créés.

Chaque composant de l'index a un `componentId` stable, `technology`, `type`, `name`, `status`, `version`, `l1Path`, `l2Path`, `artifactPaths` et `dependencies` connues. Une dépendance inconnue reste inconnue, jamais inventée. Les références d'incidents transversaux pointent vers une seule trace canonique.

## Chargement, provenance et cohérence
Au début d'une tâche, lire L0 et l'index, puis L1 et éventuellement L2 des composants pertinents. Résoudre les chemins du manifeste et de l'index depuis la racine du workspace, les liens Markdown depuis leur fichier source. Si un chemin échoue, rechercher le chemin réel dans l'arborescence de la branche lue avant d'affirmer que le document est absent. Recouper `CURRENT_STATE.md`, `DECISIONS.md` et l'index ; un état périmé ne doit pas masquer un composant ou une décision persistée. Noter la révision GitHub lue si disponible. Si une source ChatGPT diffère de GitHub, signaler l'écart : ne pas synchroniser silencieusement. En cas de contradiction métier ou d'architecture, ne pas remplacer une décision validée sans arbitrage. Éviter les écritures simultanées concurrentes ; relire l'état avant remplacement.

## Santé du contexte
Sur « Audit contexte », évaluer qualitativement :
1. Continuité des décisions et objectifs.
2. Cohérence des versions, règles et hypothèses.
3. Traçabilité des informations critiques.
4. Capacité de reprise dans un nouveau chat.

Restituer vigilance faible/modérée/élevée, incertitudes et recommandation de poursuite ou passation. Alerter en présence de contradictions répétées ou de perte de références. Aucune mesure exacte de saturation du contexte n'est disponible ; un audit ne garantit pas la détection d'informations déjà tronquées.

## Passation
Produire une synthèse structurée des objectifs, sources, décisions validées, état des composants, artefacts, erreurs ouvertes et prochaine action. Après accord, enregistrer les éléments opérationnels non sensibles dans le workspace. Le nouveau chat relit L0 et les composants concernés plutôt que de dépendre uniquement d'un résumé conversationnel.

## Publication
Ne pas restructurer ni migrer automatiquement un workspace existant. Vérifier chaque écriture ; conserver les versions et les preuves. Faire approuver les décisions structurantes. Ne pas publier automatiquement les documents métier ni les secrets.

### Publication cohérente d'un composant — règle opérationnelle
Quand une création ou évolution de composant touche plusieurs fichiers (artefact, `STATE.md`, `HISTORY.md`, `components/index.yaml`, `docs/CURRENT_STATE.md`), préparer l'ensemble avant écriture et privilégier **un seul commit Git**. N'inclure que les fichiers réellement modifiés. Un ensemble de `create_file`/`update_file` successifs peut laisser des états intermédiaires incohérents ; ne pas qualifier une série de commits de publication atomique.

1. Lire le **SHA de commit HEAD** de la branche cible (`H0`) et son **SHA d'arbre** ; ne pas confondre les deux. Vérifier les chemins actuels et les références L0/L1/L2.
2. Préparer les contenus complets, vérifier identifiants, statuts, dépendances, chemins, version et preuves de test ; demander l'autorisation d'écriture si nécessaire.
3. Créer les blobs et un nouvel arbre basé sur l'arbre de `H0`, puis un commit `C1` ayant `H0` pour parent. À ce stade, la branche n'est pas publiée.
4. Vérifier que le HEAD de la branche vaut toujours `H0`. Déplacer la référence vers `C1` **sans force**, avec condition sur le HEAD attendu quand l'API le permet ; en cas de conflit, arrêter, relire et reconstruire sans écraser.
5. Relire le nouveau HEAD, le commit réellement publié et les chemins modifiés ; vérifier le contenu et la cohérence de l'ensemble avant d'annoncer le succès. Ne jamais attribuer à un commit des fichiers créés dans d'autres commits.

**Échec / reprise :** blobs, arbre ou commit créés sans déplacement de référence ne constituent pas une publication visible ; vérifier le HEAD avant de reprendre. Si la référence a déjà avancé, examiner ce qui est réellement publié avant toute nouvelle écriture (reprise idempotente). Après publication d'un contenu incorrect, produire un nouveau commit correctif autorisé, sans réécrire l'historique. Si l'API ne permet pas le commit unique ou le contrôle du HEAD attendu, signaler la limite, obtenir l'accord pour une publication séquentielle et en tracer les étapes/risques. Une publication Git réussie ne prouve pas un test dans Power Apps Studio.
