# BSkyBlock

Les joueurs doivent survivre sur une île perdue dans les cieux.

Créé et maintenu par [tastybento](https://github.com/tastybento).

{{ addon_description("BSkyBlock") }}

## Histoire
**BSkyBlock** est l'évolution d'**ASkyBlock** pour les versions de serveur Minecraft plus récentes.

## Installation

0. Installez BentoBox et exécutez-le sur le serveur au moins une fois pour créer ses dossiers de données.
1. Placez ce jar dans le dossier addons du plugin BentoBox.
2. Redémarrez le serveur.
3. L'addon créera des mondes et un dossier de données contenant un fichier config.yml.
4. Arrêtez le serveur.
5. Modifiez le fichier config.yml selon vos préférences.
6. Supprimez tous les mondes créés par défaut si vous avez apporté des modifications qui les affecteraient.
7. Redémarrez le serveur.

## Config.yml

Le config.yml est similaire à ASkyBlock mais *pas le même*. Notez que la distance entre les îles et la portée de protection sont des **valeurs de rayon** donc la taille de l'île sera deux fois ces valeurs en blocs ! De plus, la distance entre les îles sera définie automatiquement à une limite de chunk (un multiple de 16 blocs).

## Permissions

Les permissions peuvent être trouvées [ici](Permissions).

## Commandes

Les commandes peuvent être trouvées [ici](Commands).

## Placeholders

Les placeholders peuvent être trouvés [ici](Placeholders).

## Journal des modifications

??? warning "Nouveautés dans v1.20.0 — requiert BentoBox 3.13.0 et Paper 1.21.11"
    **Publié le :** 2026-04-27

    - 🐛 **Correction de la génération des mobs.** Le générateur de chunk ne surchargeait pas `shouldGenerateMobs()`, ce qui supprimait silencieusement la génération de mobs vanille dans tous les mondes générés par BSkyBlock. Les mobs apparaissent à nouveau correctement.
    - 🐛 **Correction de la génération des animaux aquatiques (poissons, calamars).** Restaure l'apparition naturelle des poissons et calamars, brisée depuis la migration vers la plateforme 1.21. Corrige [BentoBox #2593](https://github.com/BentoBoxWorld/BentoBox/issues/2593).
    - ⚡ **Génération de chunks modernisée.** Le générateur de monde a été migré de l'ancienne approche `generateChunkData()` + `BiomeGrid` (dépréciée) vers l'API actuelle de Paper `generateNoise()` + `BiomeProvider`.
    - 🔡 Les 17 fichiers de locale de panneau de signe ont été migrés des codes couleur `&c` legacy vers le format MiniMessage.
    - Build modernisé : JDK 21, stack de tests JUnit 5 + MockBukkit.

    🔺 **Requiert BentoBox 3.13.0 ou plus récent et Paper 1.21.11.** Les anciennes versions de BentoBox ne chargeront pas cet addon.

    🔡 **Note locale :** le texte des panneaux utilise désormais des balises MiniMessage (par ex. `<red>…</red>` au lieu de `&c`). Les fichiers de locale personnalisés doivent être mis à jour.

    [Release v1.20.0](https://github.com/BentoBoxWorld/BSkyBlock/releases/tag/1.20.0)

## Traductions

{{ translations("BSkyBlock") }}
