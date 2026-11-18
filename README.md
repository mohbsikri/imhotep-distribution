# Imhotep — Distribution officielle

Source publique de la méthodologie Imhotep pour Microsoft Power Platform.

## Première utilisation
1. Ouvrez `IMHOTEP_INSTRUCTIONS.txt`, copiez son contenu dans les instructions d'un nouveau projet ChatGPT (nom libre).
2. Connectez GitHub à ChatGPT et autorisez votre dépôt privé.
3. Écrivez « Bonjour ». Imhotep vous guidera pour créer ou retrouver votre dépôt privé `imhotep-pp-core`.
4. Après votre autorisation, Imhotep installe `methodology/` depuis ce dépôt public et vérifie les fichiers.

Aucun ZIP ni script local n'est nécessaire pour l'utilisateur final.

## Organisation
- `IMHOTEP_INSTRUCTIONS.txt` : instructions à coller dans ChatGPT.
- `methodology/` : standards, procédures et templates publiés.
- `RELEASE_MANIFEST.yaml` : inventaire et empreintes SHA-256.

La branche `main` peut évoluer. Pour une installation reproductible, Imhotep doit relever le commit Git de la version choisie et le conserver dans le dépôt privé.

Les projets métier et les workspaces restent exclusivement dans les dépôts privés des utilisateurs.

## Installation robuste — version 0.8.2
La procédure détaillée est dans `methodology/BOOTSTRAP_V0.8.md`. L'assistant vérifie les empreintes par petits lots, prépare les blobs Git, conserve un inventaire de reprise, puis publie en un commit sans écrasement. Une interruption peut nécessiter une reprise conversationnelle ; aucune exécution continue n'est garantie. L'initialisation du premier workspace intervient séparément après autorisation. Toujours figer le commit de distribution et vérifier `RELEASE_MANIFEST.yaml` avant installation.

Les instructions du projet ChatGPT sont limitées à 8 000 caractères ; la révision 0.8.2 contient un fichier de 6 415 caractères. Les procédures détaillées restent dans methodology/.
