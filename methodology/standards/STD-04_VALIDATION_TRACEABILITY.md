# STD-04 — Validation et traçabilité
Version : 0.5.0-candidate

## Statuts distincts
- **Proposé** : solution décrite, non générée.
- **Généré** : artefact produit, non intégré.
- **Intégré** : utilisateur confirme l'installation.
- **Testé** : au moins un scénario exécuté, résultats enregistrés.
- **Validé** : critères d'acceptation obligatoires satisfaits et validation utilisateur explicite.

Un statut Testé ne signifie pas que tous les tests sont réussis. Les tests non exécutés et bloqués restent visibles.

## Traçabilité minimale
Chaque campagne de recette conserve :
- solution/workspace, identifiant de livrable, version ou commit, date ;
- exigences ou comportements attendus, scénarios et résultats ;
- commentaires par échec, commentaire libre général, anomalies complémentaires ;
- identité déclarative de la personne ayant testé si disponible et sans inventer de preuve ;
- décision de validation et points ouverts.

## Règles
- Un résultat communiqué par l'utilisateur est un test déclaré, sauf preuve instrumentée.
- Ne pas déduire une conformité fonctionnelle de la seule réussite de l'import YAML.
- Après modification, identifier les tests à rejouer ; les résultats antérieurs restent attachés à l'ancienne version.
- Publier les résultats opérationnels dans le workspace, sous réserve des autorisations et de la réussite de l'écriture.

## Alignement V0.8 — Portée des preuves
- Le statut **Testé** signifie qu'au moins un scénario a été exécuté, sans impliquer la réussite de tous les scénarios ; conserver les résultats partiels et non testés.
- Distinguer **intégration technique**, **conformité fonctionnelle** et **approbation explicite**. Un contrôle de bootstrap GitHub ne prouve pas la reprise dans un nouveau chat ni l'exécution Power Platform.
- Une recette allégée (STD-05) reste liée à une révision et à un périmètre d'impact ; ne pas la présenter comme une validation complète de composants non couverts.
- Les preuves détaillées sont rattachées à L2 (STD-09), avec résumé L1 si l'état du composant change.
