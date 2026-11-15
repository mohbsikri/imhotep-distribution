# STD-03 — Capitalisation des connaissances
Version : 0.5.0-candidate

## Objectif
Transformer les incidents et correctifs observés en connaissances réutilisables, sans propager les particularités métier d'une solution.

## Fiche de connaissance
- Identifiant stable et titre.
- Technologie, contexte et versions pertinentes.
- Symptôme reproductible et message d'erreur exact si disponible.
- Cause : confirmée, probable ou inconnue.
- Correction proposée puis correction effectivement testée.
- Résultat du test et preuve disponible.
- Conditions d'applicabilité, limites et risques de régression.
- Provenance (workspace, date, livrable), sans données sensibles.

## Cycle
1. Enregistrer l'incident dans le workspace concerné.
2. Diagnostiquer sans confondre hypothèse et fait.
3. Vérifier la correction en environnement réel.
4. Promouvoir la connaissance dans le catalogue commun si elle est généralisable.
5. Réutiliser le correctif seulement lorsque les conditions sont comparables.

## Cas initiaux à documenter
- YAML : erreur de parsing PA1001 et valeurs contenant des caractères spéciaux.
- Power Fx : confusion entre séparateurs d'arguments et séparateurs d'instructions.
- Collections : utilisation avant initialisation.
- Galeries : chevauchement de colonnes.

Ces cas sont des pistes de capitalisation, pas des correctifs universellement validés.

## Alignement V0.8 — Mémoire et promotion
- Tracer l'incident et ses preuves en L2 du composant concerné (STD-09), avec références croisées si plusieurs composants sont touchés ; ne pas dupliquer la source canonique.
- Conserver l'état courant du composant en L1 et le résumé global uniquement si l'incident affecte la solution.
- La promotion vers `methodology/catalog/` est un changement partagé soumis à accord ; ne pas généraliser une règle métier ni promouvoir une correction non testée comme validée.
- Les données sensibles et documents métier sources restent hors du dépôt sauf autorisation explicite et conformité aux règles de protection.
