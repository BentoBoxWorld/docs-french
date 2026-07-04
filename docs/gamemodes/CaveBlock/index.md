# CaveBlock

**CaveBlock** permet aux ~~nains~~ joueurs de survivre sous terre. Minez, fabriquez et creusez un trou (*diggy diggy hole*) !

Créé et maintenu par [BONNe](https://github.com/BONNe).

{{ addon_description("CaveBlock") }}

## Installation

0. Installez BentoBox et exécutez-le sur le serveur au moins une fois pour créer ses dossiers de données.
1. Placez ce jar dans le dossier addons du plugin BentoBox.
2. Redémarrez le serveur.
3. L'addon créera des mondes et un dossier de données contenant un fichier config.yml.
4. Arrêtez le serveur.
5. Modifiez le fichier config.yml selon vos préférences.
6. Supprimez tous les mondes créés par défaut si vous avez apporté des modifications qui les affecteraient.
7. Redémarrez le serveur.

## Configuration

Le fichier principal `config.yml` contient les informations de base sur la configuration de l'addon du mode de jeu.

### config.yml

Après que l'addon soit installé avec succès, il créera un fichier config.yml. Chaque option de ce fichier est accompagnée de commentaires. Veuillez vérifier le fichier pour plus d'informations.

Vous pouvez trouver le dernier fichier config : [config.yml](https://github.com/BentoBoxWorld/CaveBlock/blob/develop/src/main/resources/config.yml)

!!! info "Génération du monde remaniée dans 1.21.0"
    Depuis la version **1.21.0**, l'Overworld est taillé par le propre générateur de bruit vanilla 1.18+ de Minecraft, donc les îles traversent de véritables cavernes fromage, spaghetti, luxuriantes, pierre à stalactite et ombre profonde — complètes avec des minerais vanilla, des décorations, des structures et des biomes souterrains. Chaque colonne est ensuite plafonnée pour que le monde reste du roc solide sans ciel ouvert. Parce que le serveur gère désormais la taille, les minerais et les biomes, les anciennes options de génération de remplacement de blocs (`generation-tries`, `use-new-material-generator`, les listes `blocks` par dimension et les bascules `natural-*`) ont été supprimées. Le Nether et l'End conservent une approche de remplissage-et-décoration avec un nouveau générateur de veines de minerai. Consulter le journal des modifications au bas de cette page avant de mettre à jour.

## Commandes

Les commandes peuvent être trouvées [ici](Commands).

## Permissions

Les permissions peuvent être trouvées [ici](Permissions).

## Placeholders

Les placeholders peuvent être trouvés [ici](Placeholders).

## Journal des modifications

!!! warning "Nouveautés dans v1.21.0 — Modification : génération du monde remaniée"
    **Publié :** 27 juin 2026

    Un remaniement majeur de la génération. CaveBlock cible désormais **Paper 1.21.11 sur Java 21** et l'**API BentoBox 3.14**.

    - 🔺 **Génération vanilla du monde en cavernes.** L'Overworld se confie au propre générateur de bruit 1.18+ de Minecraft, donc les îles sont taillées à travers de véritables cavernes fromage, spaghetti, luxuriantes, pierre à stalactite et ombre profonde, complètes avec des minerais, décorations, structures (mines, donjons, salles d'épreuve, géodes d'améthyste, villes antiques) et biomes souterrains vanilla. Le ciel est plafonné avec de la pierre pour que le monde reste du roc solide de la bedrock au plafond.
    - 💎 **Veines de minerai Nether & End remaniées.** Le Nether et l'End conservent l'approche de remplissage-et-décoration avec un nouveau générateur de veines qui place des blobs de minerai de taille appropriée (débris anciens, quartz, obsidienne, pierre lumineuse et plus) au lieu de blocs uniques.
    - ⚙️ **Nettoyage de la configuration.** Les paramètres de génération du monde ont été remaniés et les options mortes supprimées — `generation-tries`, `use-new-material-generator`, les listes `blocks` par dimension, les bascules `natural-surface`/`natural-caves`/`natural-bedrock` et les anciens paramètres `netherBlocks`/`endBlocks`/`debug` sont partis. Sauvegardez votre `config.yml` existant avant de laisser l'addon écrire les nouveaux défauts.
    - 🔡 **Locales MiniMessage.** Tous les fichiers de locale ont été migrés des codes couleur legacy vers MiniMessage, et la clé du message de limite de hauteur a été renommée en `caveblock.general.errors.cave-limit-reached`. Régénérez vos fichiers de locale si vous les avez personnalisés.
    - 🧪 Une suite de tests complète JUnit 5 + MockBukkit a été ajoutée pour garder la génération, les limites de hauteur et le cycle de vie de l'addon.

    🔺 **Génération du monde modifiée :** Les chunks nouvellement générés de l'Overworld utilisent maintenant les cavernes de bruit vanilla au lieu de la taille de remplissage solide. Les chunks déjà générés restent inchangés, mais le nouveau terrain aux bords de votre monde aura un aspect différent des zones plus anciennes. Testez d'abord sur une copie si cela importe pour vous.

    [Release v1.21.0](https://github.com/BentoBoxWorld/CaveBlock/releases/tag/1.21.0)

## Traductions

{{ translations("CaveBlock") }}
