# 🍱 Documentation BentoBox (Français)

Bienvenue dans le dépôt source officiel de la documentation BentoBox en français. Ce dépôt contient tous les fichiers de documentation bruts (en Markdown) utilisés pour construire le site de documentation officiel en langue française.

-----

## 📖 Lire la documentation

La documentation publiée et à jour est consultable à l'adresse suivante :

**[https://docs.bentobox.world](https://docs.bentobox.world)**

> Si vous cherchez simplement à lire la documentation ou à obtenir de l'aide sur BentoBox, veuillez visiter le lien ci-dessus. Ce dépôt est destiné à **contribuer** à la documentation.

La documentation anglaise de référence se trouve dans le dépôt principal : [BentoBoxWorld/docs](https://github.com/BentoBoxWorld/docs).

-----

## 🌐 À propos de cette traduction

Ce dépôt contient la traduction française de la documentation BentoBox. Il couvre :

- La documentation du cœur BentoBox
- Les modes de jeu (AcidIsland, AOneBlock, BSkyBlock, CaveBlock, etc.)
- Les extensions (Bank, Border, Challenges, Level, Limits, Warps, etc.)
- Les tutoriels pour les développeurs

Les traductions sont synchronisées régulièrement avec la documentation anglaise principale. Si vous constatez un contenu manquant ou obsolète, les contributions sont les bienvenues !

-----

## 🤝 Contribuer

Toute contribution est la bienvenue, qu'il s'agisse de corriger une faute de frappe ou de traduire un guide complet. Votre aide améliore BentoBox pour tous les joueurs francophones.

### Comment contribuer

1. **Forkez** ce dépôt sur votre compte GitHub.
2. **Créez une nouvelle branche** pour vos modifications (par ex. `fix/correction-config` ou `feat/traduction-addon-xyz`).
3. **Effectuez vos modifications** dans les fichiers Markdown.
4. **Committez et poussez** vos modifications sur votre fork.
5. **Ouvrez une Pull Request (PR)** depuis votre branche vers la branche `master` de ce dépôt.

### Conseils de traduction

- Conservez les noms techniques en anglais : noms de commandes (ex. `/island`), clés YAML (ex. `disabled-gamemodes`), noms de classes Java, macros MkDocs (ex. `{{ addon_description("Level") }}`).
- Traduisez les titres de sections, les descriptions et les textes explicatifs.
- Respectez la mise en forme Markdown existante (blocs de code, admonitions, tableaux).

-----

## 🚀 Processus de publication automatique

Ce dépôt est connecté au service **[ReadTheDocs](https://readthedocs.org/)**, qui gère la compilation et le déploiement.

- **À chaque commit/fusion :** lorsque des commits sont poussés vers la branche `master`, un webhook est envoyé à ReadTheDocs.
- **Compilation :** ReadTheDocs récupère les dernières modifications et compile les fichiers Markdown en site HTML statique.
- **Publication :** si la compilation réussit, la nouvelle version de la documentation est automatiquement mise en ligne.

Votre contribution apparaîtra sur le site de documentation dans les quelques minutes suivant la fusion de votre Pull Request.

## 📄 Licence

Le texte et le contenu de la documentation BentoBox (ce dépôt) sont sous licence **[Creative Commons Attribution-ShareAlike 4.0 International (CC BY-SA 4.0)](https://creativecommons.org/licenses/by-sa/4.0/)**.

Les extraits de code inclus dans la documentation sont, sauf indication contraire, sous licence **[MIT](https://opensource.org/licenses/MIT)**.
