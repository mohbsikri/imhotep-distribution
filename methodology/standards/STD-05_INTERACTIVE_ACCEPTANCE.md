# STD-05 — Recette interactive et validation utilisateur
Version : 0.8.0-candidate

## Déclenchement
Préparer les vérifications adaptées dès la livraison d'un artefact intégrable. Attendre la confirmation d'intégration pour solliciter les résultats. Si l'intégration échoue, diagnostiquer d'abord l'erreur et proposer une correction.

## Deux niveaux
- **Standard** : nouvel écran, fonctionnalité, flux, modèle Dataverse, règle métier, permissions ou modification significative. Préparer des scénarios contextualisés couvrant fonctionnement nominal, cas limites, erreurs, permissions et non-régression selon les risques ; 5 à 8 est un repère, non un quota.
- **Allégée** : correction locale mineure et impact circonscrit. Préparer seulement les contrôles directement affectés et, si nécessaire, un test de non-régression. Une confirmation courte du développeur suffit si les preuves attendues sont simples.
Le choix dépend de l'impact réel, pas du nombre de lignes modifiées. En cas de doute sur les risques, expliciter l'hypothèse.

## Présentation
Pour les scénarios formalisés : ID, objectif, précondition si nécessaire, action et résultat attendu ; résultat exclusif **Réussi / Erreur / Non testé**. En cas d'erreur, demander le symptôme ou message. **Non testé** ne vaut jamais réussite. Lorsqu'un questionnaire est présenté, toujours offrir un commentaire général libre facultatif, même si tous les tests réussissent. Éviter les formulaires volumineux : préférer l'échange conversationnel ou une grille compacte selon le besoin.

## Résultat et traçabilité
1. Lier les tests à la révision effectivement intégrée.
2. Distinguer succès d'intégration, résultat fonctionnel et approbation.
3. En cas d'erreur, corriger l'artefact et rejouer les scénarios impactés.
4. Capitaliser les résultats et commentaires utiles dans le workspace, selon les autorisations.
5. Proposer la validation seulement lorsque les vérifications obligatoires sont réussies et confirmées ; ne pas auto-valider.
