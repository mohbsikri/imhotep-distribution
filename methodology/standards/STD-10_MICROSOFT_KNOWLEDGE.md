# STD-10 — Expertise Microsoft à la demande
Version : 0.8.0-candidate

## Objectif
Mobiliser les sources techniques Microsoft pertinentes pour concevoir, expliquer et diagnostiquer Canvas, Power Fx, Dataverse, Power Automate, Model-driven et ALM. La méthodologie n'exige ni connexion à un environnement Power Platform ni outil d'exécution local.

## Sources
- Microsoft Learn : https://learn.microsoft.com/power-platform/
- Microsoft Power Platform Skills : https://github.com/microsoft/power-platform-skills
- Références officielles des connecteurs, SDK, Power Fx et produits concernés.

## Démarche
1. Identifier la question précise et la version/technologie concernée.
2. Consulter à la demande les références officielles utiles ; relever URL et, si pertinent, date, version ou commit.
3. Distinguer recommandations documentaires, syntaxe confirmée et comportement réellement observé.
4. Confronter la source aux règles métier et décisions validées ; signaler les contradictions sans écraser les arbitrages.
5. Produire des instructions et artefacts exploitables manuellement ; indiquer clairement les tests restant à faire.
6. Si la source a déterminé une correction, conserver sa référence dans la mémoire du composant (STD-09).

## Limites
- Une page Microsoft n'est pas une preuve de compilation ou d'exécution dans l'environnement utilisateur.
- La langue de l'éditeur Power Fx et la sérialisation YAML doivent être vérifiées séparément.
- Si les références sont indisponibles, déclarer la limite et ne pas inventer de consultation.
- La lecture d'un dépôt de skills n'implique ni installation ni activation automatique d'un agent.
- Ne pas introduire de dépendance au Bridge, à Claude Code, à PAC CLI ou à un environnement local.
