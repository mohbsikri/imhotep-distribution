# STD-08 — Diagnostic structuré et analyse d'impact
Version : 0.6.0-candidate

## Déclencheur
Erreur d'import, de formule, d'affichage, de données ou échec d'un scénario STD-05.

## Procédure
1. **Constater** : version exacte du livrable, scénario, étapes de reproduction, attendu/observé, message et capture ou trace si fournis.
2. **Qualifier** : bloquant ou non ; erreur syntaxique, référence, données, permission, interface, règle métier, performance ou cause inconnue.
3. **Formuler des hypothèses** : distinguer fait confirmé, cause probable et possibilité non testée. Ne pas multiplier les modifications sans lien avec le symptôme.
4. **Isoler** : comparer à une version fonctionnelle si disponible, examiner les dépendances et proposer un test discriminant. Le Moniteur Power Apps peut aider lorsque l'utilisateur peut fournir une trace.
5. **Corriger** : produire un livrable complet et révisé. Pour YAML Canvas, renvoyer le YAML complet corrigé.
6. **Rejouer** : tests échoués, tests dépendants et non-régression ; conserver les résultats liés à la nouvelle révision.
7. **Capitaliser** : enregistrer symptôme, cause et correction selon STD-03, avec niveau de preuve.

## Précautions
- Une hypothèse par test de diagnostic lorsque c'est raisonnablement possible ; ne pas imposer une multiplication de builds pour une correction évidente.
- Ne jamais présenter un script, une trace ou une correction comme exécutés sans résultat réel.
- Ne pas confondre une erreur d'intégration avec une erreur de logique métier.
- Les scripts PowerShell, le packaging PAC CLI et la bissection automatique relèvent d'une éventuelle automatisation future ; ils ne sont pas des prérequis à la méthode ChatGPT.

## Alignement V0.8 — Diagnostic proportionné
- Pour une correction mineure, privilégier une vérification ciblée et les non-régressions plausibles ; pour un changement transversal, identifier les composants dépendants via l'index (STD-09).
- Relier les incidents, tests et preuves à la révision en L2 du composant concerné, et mettre à jour son état L1 seulement si nécessaire.
- Pour Canvas, le format standard reste le YAML complet à coller dans Studio ; les fichiers `.pa.yaml` ne sont pas requis dans la V0.8.
- Une cause probable ou une correction proposée ne devient confirmée qu'après preuve appropriée ; ne pas extrapoler un test local à Dataverse ou à Power Automate.
