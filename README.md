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
