# STD-07 — Catalogue de composants et versionnement
Version : 0.6.0-candidate

## Objectif
Réutiliser des artefacts éprouvés et relier chaque livraison à sa recette et à ses corrections.

## Identité minimale du livrable
- `artifactId` : identifiant stable, unique dans le workspace.
- `revision` : version explicite ou identifiant de commit.
- `kind` : écran, composant, formule, flux ou autre.
- `sourcePath` : chemin GitHub si publié.
- `status` : Proposé, Généré, Intégré, Testé ou Validé (STD-04).
- `compatibility` : type de contrôle, version/propriétés, contexte de Studio, sources de données, langue Power Fx, restrictions pertinentes.
- `evidence` : liens vers les tests, erreurs et décisions ; ne pas inventer de preuves.

## Catalogue commun
Un composant n'est déclaré **validé** qu'après test correspondant et approbation explicite. Les composants générés mais non testés peuvent être conservés comme exemples **non validés**, clairement identifiés. Un comportement éprouvé dans une collection locale ne vaut pas preuve Dataverse.

## Réutilisation
1. Rechercher un composant correspondant au besoin et au contexte.
2. Comparer ses conditions de compatibilité ; si elles diffèrent, marquer la réutilisation comme hypothèse à tester.
3. Adapter sans introduire de règles métier étrangères.
4. Attribuer une nouvelle révision et préparer les tests de régression.
5. Capitaliser les résultats dans le workspace, puis promouvoir les enseignements génériques.

## GitHub
Le catalogue commun vit sous `methodology/catalog/` ; les artefacts spécifiques restent sous `workspaces/<projectId>/`. La promotion vers le catalogue commun est une évolution méthodologique à valider, pas une écriture automatique inter-workspace.

## Alignement V0.8 — Index et compatibilité
- Distinguer `componentId` (identité stable du composant dans `components/index.yaml`) de `artifactId` (livrable ou révision associée). Une même entité fonctionnelle peut avoir plusieurs livrables.
- Les traces L1/L2 sont référencées depuis l'index du composant (STD-09) ; conserver les dépendances connues sans en inventer.
- Pour Canvas, consigner la langue de l'éditeur `powerFxLocale` issue de la configuration du projet et distinguer celle-ci de la syntaxe Power Fx effectivement testée dans le YAML de collage.
- La réutilisation d'un composant validé dans un autre contexte nécessite une nouvelle vérification de compatibilité, sans transférer automatiquement son statut de validation.
