# ExtraMobs

**ExtraMobs** ajuste certaines règles de génération de mobs pour obtenir des Blazes, des Wither Skeletons et des Shulkers.

Créé et maintenu par [BONNe](https://github.com/BONNe).

{{ addon_description("ExtraMobs", beta=True) }}

## Installation

1. Placez le fichier jar de l'addon dans le dossier des addons du plugin BentoBox
2. Redémarrez le serveur
3. En jeu, vous pouvez modifier les indicateurs qui permettent d'utiliser l'addon actuel.

## Informations

Cet addon ne modifie pas les règles de génération de Minecraft. Au lieu de cela, il utilise d'autres mobs qui sont générés naturellement et change leur type avec une nouvelle entité, si toutes les conditions sont remplies.

##### Pour Wither Skeleton et Blaze :

L'addon remplacera Zombie Pigmen par Blaze ou Wither Skeleton par hasard à partir de la configuration, si :
 - le monde donné est généré par le addon GameMode.
 - le monde donné est le Nether
 - Zombie Pigmen se tient sur la brique du Nether, la dalle de brique du Nether ou les escaliers en brique du Nether.

##### Pour Shulkers :

L'addon remplacera Enderman par Shulker par hasard à partir de la configuration si :
 - le monde donné est généré par le addon GameMode.
 - le monde donné est l'End
 - Enderman se tient sur un bloc purpur, escalier purpur ou dalle purpur.

##### Pour Guardians :

L'addon remplacera Cod, Salmon ou Tropical fish par Guardian par hasard à partir de la configuration si :
 - le monde donné est généré par le addon GameMode.
 - le monde donné est l'Overworld
 - le biome dans l'emplacement donné est océan profond ou l'une de ses variantes
 - le premier bloc au-dessus de l'eau où le poisson est généré est prismarine, brique prismarine ou prismarine foncée (blocs, dalles et escaliers).

## Configuration

Le dernier `config.yml` est disponible [ici](https://github.com/BentoBoxWorld/ExtraMobs/blob/develop/src/main/resources/config.yml).

??? note "disabled-gamemodes"
    Une liste des modes de jeu dans lesquels l'addon ne doit pas fonctionner. Chaque entrée va sur sa propre ligne commençant par `-`.

    Par défaut : `[]` (vide — l'addon fonctionne dans tous les modes de jeu)

??? note "nether-chances"
    Chances de remplacer un Zombified Piglin dans le Nether. `wither-skeleton` et `blaze` sont chacun une probabilité comprise entre 0.0 et 1.0.

    Par défaut : `wither-skeleton: 0.01`, `blaze: 0.1`

??? note "end-chances"
    `shulker` — chance de remplacer un Enderman dans l'End par un Shulker.

    Par défaut : `0.1`

??? note "overworld-chance"
    `guardian` — chance de remplacer un Cod, un Salmon ou un Tropical Fish dans l'Overworld par un Guardian.

    Par défaut : `0.1`

??? note "gamemode-settings"
    Règles de remplacement par mode de jeu, qui surchargent les chances globales ci-dessus. Ajouté en 1.15.0.

    Chaque clé est le nom exact de l'addon de mode de jeu (sensible à la casse), et chaque mode de jeu peut définir jusqu'à trois sections d'environnement — `world:` pour l'Overworld, `nether:` et `end:`. Chaque section est une liste de règles avec `old` (l'`EntityType` à remplacer), `new` (l'`EntityType` de remplacement) et `chance` (0.0–1.0).

    Les règles par mode de jeu sont essayées dans l'ordre avant les valeurs globales par défaut de cet environnement. Si une règle correspond à l'entité en cours d'apparition **et** que son tirage réussit, le remplacement est appliqué et le traitement s'arrête pour cet événement. Si aucune règle ne correspond, ou si le tirage de chaque règle correspondante échoue, les valeurs globales `nether-chances` / `end-chances` / `overworld-chance` sont utilisées en repli.

    Par défaut : `{}` — c'est une option à activer, donc les chances globales continuent de s'appliquer à tout mode de jeu non listé ici.

    ```yaml
    gamemode-settings:
      BSkyBlock:
        nether:
          - old: ZOMBIFIED_PIGLIN
            new: WITHER_SKELETON
            chance: 0.05
          - old: ZOMBIFIED_PIGLIN
            new: BLAZE
            chance: 0.1
        end:
          - old: ENDERMAN
            new: SHULKER
            chance: 0.3
        world:
          - old: COD
            new: GUARDIAN
            chance: 0.15
      AcidIsland:
        end:
          - old: ENDERMAN
            new: SHULKER
            chance: 0.5
    ```

## Compatibilité

- [x] BentoBox 3.14.0 ou version ultérieure
- [x] Paper Minecraft 1.21.x
- [x] Java 21 ou version ultérieure

L'addon supporte tous les addons de mode de jeu.

## Traductions

{{ translations("ExtraMobs") }}

## Journal des modifications

!!! note "Nouveautés dans v1.15.0 — Java 21 et BentoBox 3.14.0 requis"
    **Publié :** 31 mai 2026

    Compatibilité : API BentoBox 3.14.0+ · Paper Minecraft 1.21.x · Java 21+.

    - ⚙️ **Règles de remplacement d'apparition par mode de jeu.** Un nouveau bloc de configuration `gamemode-settings` définit des règles de remplacement pour chaque mode de jeu BentoBox séparément, au lieu de partager un unique paramètre global pour tout le serveur. Il vaut `{}` par défaut et doit être activé explicitement, donc les valeurs de chance globales existantes continuent de fonctionner pour tout mode de jeu non listé. Voir la section Configuration ci-dessus.
    - 🔺 **Java 21 et BentoBox 3.14.0 sont désormais requis.** Assurez-vous que votre serveur satisfait les deux avant de mettre à niveau.
    - **Point d'entrée Pladdon et `plugin.yml` ajoutés,** afin que l'addon se charge comme un addon BentoBox moderne.
    - Suite de tests reconstruite sur JUnit 5 et MockBukkit, build GitHub Actions avec analyse SonarCloud ajouté, et divers problèmes de maintenabilité résolus.

    [Release v1.15.0](https://github.com/BentoBoxWorld/ExtraMobs/releases/tag/1.15.0)
