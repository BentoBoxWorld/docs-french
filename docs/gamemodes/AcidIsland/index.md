# AcidIsland

**AcidIsland** est un mode de survie dans lequel les joueurs doivent survivre sur une île entourée d'une mer d'acide.

Créé et maintenu par [tastybento](https://github.com/tastybento).

{{ addon_description("AcidIsland") }}

## L'histoire
Vous êtes sur une île, dans une mer d'acide ! Si vous aimez Skyblock, essayez AcidIsland pour un nouveau défi !

C'est une variation de SkyBlock. Au lieu de tomber, vous devez faire face à l'eau acide lorsque vous agrandissez votre île et les joueurs peuvent naviguer en bateau vers les îles les uns des autres.

## Installation

0. Installez BentoBox et exécutez-le sur le serveur au moins une fois pour créer ses dossiers de données.
1. Placez ce jar dans le dossier addons du plugin BentoBox.
2. Redémarrez le serveur.
3. L'addon créera des mondes et un dossier de données contenant un fichier config.yml.
4. Arrêtez le serveur.
5. Modifiez le fichier config.yml selon vos préférences.
6. Supprimez tous les mondes créés par défaut si vous avez apporté des modifications qui les affecteraient.
7. Redémarrez le serveur.

## Permissions

Les permissions peuvent être trouvées [ici](Permissions).

## Commandes

Les commandes peuvent être trouvées [ici](Commands).

## Placeholders

Les placeholders peuvent être trouvés [ici](Placeholders).

## Journal des modifications

??? warning "Nouveautés dans v1.21.0 — BentoBox 3.14.0 requis, migration des locales"
    **Publié :** 12 avril 2026

    - **Île de départ Sanctuaire Grove de Cerisiers.** Un nouveau blueprint d'île de départ sur le thème du biome Grove de Cerisiers est inclus pour les serveurs Minecraft 1.21+. Pour l'activer, supprimez `BentoBox/addons/AcidIsland/blueprints/` pour que les blueprints se régénèrent au prochain démarrage.
    - 🔺 **BentoBox API 3.14.0 est maintenant requis.** Mettez à jour BentoBox avant d'installer cette version.
    - 🔡 **Les 24 fichiers de locale migrés des codes `&` vers MiniMessage.** Supprimez `BentoBox/locales/AcidIsland/` et redémarrez pour régénérer. Les codes `&` restants dans les fichiers personnalisés s'afficheront en texte brut.
    - Correction : NullPointerException dans la vérification du mode dieu EssentialsX quand EssentialsX échoue à se charger au démarrage.
    - Plusieurs bugs de locale pré-existants corrigés lors de la migration.

    [Release v1.21.0](https://github.com/BentoBoxWorld/AcidIsland/releases/tag/1.21.0)

## Traductions

{{ translations("AcidIsland") }}
