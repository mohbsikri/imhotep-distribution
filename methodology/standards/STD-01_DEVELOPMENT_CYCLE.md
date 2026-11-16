# STD-01 — Cycle de développement assisté par IA
Version : 0.8.0-candidate

## Cycle
1. **Analyser** : identifier sources métier, décisions validées, contraintes, composants et critères d'acceptation. Avant de proposer un nouveau modèle ou de rouvrir un arbitrage, vérifier les décisions déjà validées et la conception existante, y compris les sources de clôture ; relever les contradictions avec leurs références précises. Pour une interaction complexe, dresser une matrice déclencheur / préconditions / résultat / données / erreur / permission / source, sans inventer les cases inconnues.
2. **Générer** : fournir un livrable complet, contextualisé et intégrable, en réutilisant les éléments éprouvés seulement si compatibles (STD-07).
3. **Pré-vol** : contrôler statiquement les erreurs plausibles, la cohérence des dépendances et les règles de syntaxe ; distinguer explicitement ce qui n'a pas été exécuté.
4. **Intégrer** : expliquer les étapes concrètes ; attendre le retour du développeur.
5. **Recetter** : appliquer STD-05, avec niveau standard ou allégé selon impact et risque.
6. **Diagnostiquer/corriger** : appliquer STD-08, produire une correction exploitable et cibler la non-régression.
7. **Valider** : distinguer intégration technique, conformité métier et approbation explicite.
8. **Capitaliser** : tracer révision, état, incidents et preuves au bon niveau L0/L1/L2 (STD-09).

## Proportionnalité
Une correction cosmétique ou une formule locale ne déclenche pas obligatoirement une matrice complète ni 5 à 8 tests. Un nouvel écran, une nouvelle fonctionnalité, une modification de droits ou de règles métier nécessite une recette standard adaptée. Si l'impact réel est incertain, demander confirmation et retenir le niveau de test le plus prudent.

## Critères de passage
- Une relecture statique n'est ni un import Studio ni un test Dataverse ou de flux.
- Aucun test n'est déclaré réussi sans retour utilisateur ou preuve d'exécution.
- Un test obligatoire en échec ou non exécuté empêche la validation complète.
- Après correction, rejouer les scénarios impactés et les non-régressions pertinentes.
- Les décisions métier/architecture ne sont pas validées implicitement par capitalisation.
