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

## Compatibilité

- [x] BentoBox - version 1.11.0

L'addon est construit sur Minecraft 1.15.2 et BentoBox version 1.11.0, cependant, il devrait fonctionner même sur Minecraft 1.13.2 et BentoBox 1.0 Release.

L'addon supporte tous les addons Game mode.

## Traductions

{{ translations("ExtraMobs") }}
