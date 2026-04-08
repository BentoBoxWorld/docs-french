# AOneBlock

**AOneBlock** est notre interprétation de la célèbre carte de survie OneBlock d'**IJAminecraft**.
Les joueurs doivent survivre sur un seul bloc, qui semble être magique...

Créé et maintenu par [tastybento](https://github.com/tastybento).

{{ addon_description("AOneBlock") }}

OneBlock vous met sur un bloc dans l'espace. Il n'y a qu'un seul bloc. Que fais-tu ensuite ?

## Installation

0. Installez BentoBox et exécutez-le sur le serveur au moins une fois pour créer ses dossiers de données.
1. Placez ce jar dans le dossier addons du plugin BentoBox.
2. Redémarrez le serveur.
3. L'addon créera des mondes et un dossier de données contenant un fichier config.yml et des fichiers de configuration dans le dossier phases.
4. Arrêtez le serveur.
5. Modifiez le fichier config.yml et les fichiers .yml du dossier phases selon vos préférences.
6. Supprimez tous les mondes créés par défaut si vous avez apporté des modifications qui les affecteraient.
7. Redémarrez le serveur.

## Configuration

Le fichier `config.yml` principal contient les informations de base sur la configuration de l'addon du mode de jeu.

`phases` contient toutes les informations sur les phases qui seront présentes dans votre monde AOneBlock.

`panels` vous permet de personnaliser certains panneaux accessibles aux utilisateurs.

### config.yml

Après que l'addon soit installé avec succès, il créera un fichier config.yml. Chaque option de ce fichier est accompagnée de commentaires les expliquant. Veuillez vérifier le fichier pour plus d'informations.
Vous pouvez trouver le dernier fichier config : [config.yml](https://github.com/BentoBoxWorld/AOneBlock/blob/develop/src/main/resources/config.yml)

### Fichiers de configuration de phase

Les fichiers de configuration pour créer les phases se trouvent dans le dossier `phases`.

Il y a deux fichiers par phase — un fichier qui contient les blocs et les mobs, et un fichier qui contient les coffres.

Le premier nombre de tout fichier est le nombre de blocs qui doivent être minés pour atteindre cette phase. C'est le numéro clé de la phase.

=== "name"
    !!! summary "Description"
        Le nom d'affichage des phases. Ce nom sera affiché dans tous les endroits où les joueurs essaient de voir une phase.

=== "icon"
    !!! summary "Description"
        L'icône de la phase n'est utilisée que dans le panel `phases`.

        L'icône est créée en utilisant [BentoBox ItemParser](https://docs.bentobox.world/en/latest/BentoBox/ItemParser/)

=== "fixedBlocks"
    !!! summary "Description"
        La section fixedBlocks permet de forcer certains blocs lorsqu'un joueur les casse. Le premier est le numéro du bloc dans la phase, puis il est suivi d'un matériau Bukkit. Le premier bloc de la phase a l'index 0, tandis que l'ajout d'un nombre plus grand que le temps d'exécution de la phase signifie qu'il ne sera pas atteint.

        Les valeurs disponibles que vous pouvez trouver ici : [Materials](https://hub.spigotmc.org/javadocs/bukkit/org/bukkit/Material.html)

        Nous recommandons d'utiliser des blocs qui ne nécessitent pas de bloc de support (comme une torche, des rails, des plantes).

    !!! example "Exemple"
        ```yaml
            0: GRASS_BLOCK
            1: GRASS_BLOCK
            2: GRASS_BLOCK
            50: SPONGE
        ```

=== "holograms"
    !!! summary "Description"
        AOneBlock utilise des hologrammes natifs pour afficher ces lignes. La première ligne affichée avant le début d'une phase se trouve dans le fichier de paramètres régionaux d'aoneblock.

        Similaire à `fixedBlocks`, `holograms` commence également par un nombre quand il doit être affiché suivi du texte affiché.

    !!! example "Exemple"
        ```yaml
            0: "&aFirst block is grass!"
            1: "&aSecond block is grass!"
            2: "&cWhat if there will be no next block?"
            3: "&aGood Luck!"
        ```

=== "biome"
    !!! summary "Description"
        `biome` est une option expérimentale. Cependant, elle change le biome uniquement pour l'emplacement du bloc « magique ».
        Nous vous suggérons donc d'utiliser l'addon Biomes qui a une option pour changer le biome sur l'île entière.
        Vous pouvez le faire avec les commandes de démarrage de phase qui déclencheraient le changement de biome.

=== "start-commands"
    !!! summary "Description"
        La section `start-commands` permet de définir des commandes qui seront déclenchées au démarrage d'une phase.

        Les commandes sont exécutées en tant que console sauf si la commande est préfixée par `[SUDO]`, auquel cas la commande est exécutée en tant que joueur déclenchant les commandes.

        Ces placeholders dans la chaîne de commande seront remplacés par la valeur appropriée :

        - `[island]` - Nom de l'île
        - `[owner]` - Nom du propriétaire de l'île
        - `[player]` - Le nom du joueur qui a cassé le bloc déclenchant les commandes
        - `[phase]` - le nom de cette phase
        - `[blocks]` - le nombre de blocs cassés
        - `[level]` - le niveau de votre île (Nécessite l'addon Levels)
        - `[bank-balance]` - le solde de la banque de votre île (Nécessite l'addon Bank)
        - `[eco-balance]` - solde économique du joueur (Nécessite Vault et un plugin d'économie)

    !!! example "Exemple"
        ```yaml
            start-commands:
            - 'give [player] WOODEN_AXE 1'
            - 'broadcast [player] just started OneBlock!'
            - 'obadmin biomes set [player] aoneblock_fields ISLAND!'
        ```

=== "end-commands"
    !!! summary "Description"
        La section `end-commands` permet de définir des commandes qui seront déclenchées à la fin d'une phase.

        Les commandes sont exécutées en tant que console sauf si la commande est préfixée par `[SUDO]`, auquel cas la commande est exécutée en tant que joueur déclenchant les commandes.

        Ces placeholders dans la chaîne de commande seront remplacés par la valeur appropriée :

        - `[island]` - Nom de l'île
        - `[owner]` - Nom du propriétaire de l'île
        - `[player]` - Le nom du joueur qui a cassé le bloc déclenchant les commandes
        - `[phase]` - le nom de cette phase
        - `[blocks]` - le nombre de blocs cassés
        - `[level]` - le niveau de votre île (Nécessite l'addon Levels)
        - `[bank-balance]` - le solde de la banque de votre île (Nécessite l'addon Bank)
        - `[eco-balance]` - solde économique du joueur (Nécessite Vault et un plugin d'économie)

    !!! example "Exemple"
        ```yaml
            end-commands:
            - '[SUDO]say Just finished [phase]'
        ```

=== "end-commands-first-time"
    !!! summary "Description"
        La section `end-commands-first-time` permet de définir des commandes qui seront déclenchées **uniquement la première fois** qu'un joueur complète cette phase. Celles-ci ne seront pas exécutées lors des complétions suivantes.

        Les commandes sont exécutées en tant que console sauf si la commande est préfixée par `[SUDO]`, auquel cas la commande est exécutée en tant que joueur déclenchant les commandes.

        Ces placeholders dans la chaîne de commande seront remplacés par la valeur appropriée :

        - `[island]` - Nom de l'île
        - `[owner]` - Nom du propriétaire de l'île
        - `[player]` - Le nom du joueur qui a cassé le bloc déclenchant les commandes
        - `[phase]` - le nom de cette phase
        - `[blocks]` - le nombre de blocs cassés
        - `[level]` - le niveau de votre île (Nécessite l'addon Levels)
        - `[bank-balance]` - le solde de la banque de votre île (Nécessite l'addon Bank)
        - `[eco-balance]` - solde économique du joueur (Nécessite Vault et un plugin d'économie)

    !!! example "Exemple"
        ```yaml
            end-commands-first-time:
            - 'broadcast &c&l[!] &b[player] &fhas completed the &d&n[phase]&f phase for the first time.'
        ```

=== "requirements"
    !!! summary "Description"
        La section `requirements` permet de limiter l'accès à la phase suivante jusqu'à ce que les exigences spécifiées soient remplies.
        Actuellement, il y a 5 champs d'exigence :

        - `economy-balance` - le solde économique minimum du joueur (Nécessite Vault et un plugin d'économie)
        - `bank-balance` - le solde minimum de la banque de l'île (nécessite l'addon Bank)
        - `level` - le niveau de l'île (Nécessite l'addon Levels)
        - `permission` - une chaîne de permission
        - `cooldown` - le nombre minimum de secondes qui doivent passer depuis le dernier démarrage de la phase (prévient le changement rapide de phase)

    !!! example "Exemple"
        ```yaml
            requirements:
              bank-balance: 10000
              level: 10
              permission: ready.for.battle
              cooldown: 60
        ```

=== "blocks"
    !!! summary "Description"
        La section blocs répertorie les matériaux Bukkit suivis d'une probabilité relative.

        Les valeurs disponibles que vous pouvez trouver ici : [Materials](https://hub.spigotmc.org/javadocs/bukkit/org/bukkit/Material.html)

        Toutes les valeurs de probabilité sont additionnées pour l'ensemble de la phase et la chance du bloc à placer est la probabilité relative divisée par le total de toutes les probabilités.

    !!! example "Exemple"
        ```yaml
            blocks:
              GRASS_BLOCK: 2
              STONE: 3
        ```

        Cet exemple montre qu'il y a 40% de chances de générer un bloc d'herbe tandis que 60% de chances de générer de la pierre. (2 / (2+3)) et (3 / (2+3))

=== "mobs"
    !!! summary "Description"
        La section mob répertorie les mobs qui peuvent apparaître et leur probabilité relative ainsi que les blocs.
        Vous ne pouvez énumérer que les entités vivantes qui peuvent apparaître dans cette liste. [EntityTypes](https://hub.spigotmc.org/javadocs/bukkit/org/bukkit/entity/EntityType.html)

    !!! example "Exemple"
        ```yaml
            mobs:
              COW: 150
              SPIDER: 75
        ```

=== "Custom Blocks"
    !!! summary "Description"
        Depuis la version 1.11, vous pouvez maintenant spécifier des blocs personnalisés (grâce à [@HSGamer](https://github.com/HSGamer)).
        Vous pouvez le faire dans les deux endroits : blocs et blocs fixes.

        Pour définir des blocs personnalisés dans la section `blocks`, vous devez ajouter un `-` avant chaque élément.
        De plus, les blocs doivent être définis avec les champs type, data et probability values.
        Les types supportés sont :

          - `block-data`: utilise la commande `/setblock` pour placer un bloc dans le monde. Nécessite un champ `data`
          - `mob`: utilise l'API Spawn Entity pour créer l'entité demandée. Nécessite le champ `mob` et éventuellement le champ `underlying-block` (par défaut : STONE)
          - `itemsadder`: utilise l'API [ItemsAdder](https://itemsadder.devs.beer/) pour créer un bloc. Nécessite le champ `id`. Le plugin ItemsAdder doit être installé.
          - `nexo`: utilise l'API [Nexo](https://polymart.org/resource/nexo.6901) pour créer un bloc. Nécessite le champ `id`. Le plugin Nexo doit être installé.

    !!! example "Exemple"
        ```yaml
            fixedBlocks:
              0:
                type: block-data
                data: minecraft:chest[waterlogged=true]
              1: GRASS_BLOCK
              2: GRASS_BLOCK
            blocks:
              - type: block-data
                data: minecraft:chest[waterlogged=true]
                probability: 10
              - type: block-data
                data: minecraft:chest
                probability: 10
              - type: mob
                mob: ZOMBIE
                underlying-block: STONE
                probability: 5
              - type: itemsadder
                id: mypack:ruby_ore
                probability: 10
              - type: nexo
                id: mypack:custom_block
                probability: 10
              - DIRT: 10     # old syntax still works.
        ```

    !!! tip "ItemsAdder et Nexo"
        Pour utiliser des blocs personnalisés d'ItemsAdder ou Nexo, le plugin respectif doit être installé sur votre serveur.
        AOneBlock détecte automatiquement ces plugins au démarrage et enregistre les gestionnaires de blocs appropriés.
        Si vous configurez un bloc `itemsadder` ou `nexo` mais que le plugin n'est pas installé, le bloc reviendra à STONE.


Dans le fichier de coffres, il y a simplement le numéro de phase et une section coffres.

=== "chests"
    !!! summary "Description"
        Si CHEST est listé dans la section blocs, il sera rempli aléatoirement selon cette section.
        Vous pouvez définir autant de coffres que vous le souhaitez. Le premier nombre est un numéro de coffre unique.
        Puis suit le contenu du coffre qui inclut le numéro d'emplacement et le contenu de la pile d'articles.
        Enfin, il y a la rareté du coffre, qui peut être COMMON, UNCOMMON, RARE ou EPIC. Les chances sont codées en dur avec les valeurs : 62%, 25%, 9% et 4%.

        Le meilleur moyen de définir des coffres est de le faire en jeu.
        Remplissez un coffre avec le contenu que vous souhaitez, puis en le regardant, entrez la commande `/[admin_cmd] setchest <phase> <rarity>` où <phase> est le nom de la phase et rarity est la rareté. Utilisez Tab Complete pour voir les options. Le coffre sera automatiquement ajouté au fichier oneblocks.yml et prêt à être utilisé. La suppression des coffres doit être effectuée en modifiant le fichier oneblocks.yml pour l'instant et en rechargeant l'addon.

        Soyez très prudent lors de la modification des éléments du coffre et vérifiez que le matériel est un véritable matériau Bukkit et épelé correctement.


### Interfaces utilisateur personnalisables

BentoBox 1.17 API a introduit une fonction qui permet d'implémenter des interfaces utilisateur personnalisables. Cet addon est l'un des premiers qui utilise cette fonctionnalité. Nous avons essayé d'être aussi simple que possible pour la personnalisation, cependant, certaines fonctionnalités nécessitent une explication.
Vous pouvez trouver plus d'informations sur le fonctionnement des interfaces utilisateur personnalisées BentoBox ici : [Interfaces utilisateur personnalisées](/en/latest/Tutorials/generic/Customizable-GUI/)

??? question "Comment puis-je personnaliser les interfaces utilisateur"
    Pour personnaliser les interfaces utilisateur d'Addon, vous devez avoir la version 1.10. C'est la première version qui les a implémentées. L'addon créera un nouveau répertoire sous `/plugins/BentoBox/addons/AOneBlock` avec le nom `panels`

??? question "Que fait le type de bouton `PREVIOUS`|`NEXT` ?"
    Les types de boutons PREVIOUS et NEXT permettent de créer une pagination automatique lorsque vous avez plus d'îles que d'espaces dans l'interface utilisateur.
    Ces types ont des paramètres supplémentaires sous data :

    - `indexing` - indique si le bouton affichera le numéro de page.

    Exemple :
    ```yaml
        icon: tipped_arrow[potion_contents={custom_color:11546150}]
        title: aoneblock.gui.buttons.previous.name
        description: aoneblock.gui.buttons.previous.description
        data:
          type: PREVIOUS
          indexing: true
        actions:
          previous:
            click-type: LEFT
            tooltip: aoneblock.gui.tips.click-to-previous
    ```

??? question "Qu'est-ce que le type de bouton `PHASE` ?"
    Ce bouton permet aux joueurs de visualiser le nom de la phase et les exigences. Si les utilisateurs ont accès au changement de phase et qu'ils ont déjà atteint une phase, ils peuvent la sélectionner à nouveau et la rejouer.

    icon, title et description sont générés dynamiquement en fonction des propriétés de la phase. Cependant, vous pouvez le modifier manuellement.

    Exemple :
    ```yaml
      # icon: PLAYER_HEAD
      # title: aoneblock.gui.buttons.phase.name
      # description: aoneblock.gui.buttons.phase.description
      data:
        type: PHASE
      actions:
        select:
          click-type: LEFT
          tooltip: aoneblock.gui.tips.click-to-change
    ```


## Commandes

!!! tip
    `[player_command]` et `[admin_command]` sont des commandes qui diffèrent selon le mode de jeu que vous exécutez.

    Le fichier `config.yml` des modes de jeu contient des options qui vous permettent de modifier ces valeurs.

    Par exemple, sur AOneBlock, la commande `[player_command]` par défaut est `ob`, et la commande `[admin_command]` par défaut est `oba`.

    Sachez que cet addon permet de modifier les alias de commandes des joueurs dans le fichier `config.yml` de l'addon.

=== "Commandes uniques pour joueur AOneBlock"
    - `/[player_command] count` : envoie un message dans le chat sur la progression actuelle de la phase.
    - `/[player_command] phases` : ouvre une interface qui permet de visualiser et de choisir les phases.
    - `/[player_command] setcount <number>` : permet de modifier la phase actuelle où `<number>` est le numéro de démarrage de la phase.
    - `/[player_command] check` : génère des particules autour du bloc magique ou le respawn s'il a disparu pour une raison quelconque.
    - `/[player_command] bossbar` : bascule l'affichage de la barre de boss affichant la progression de la phase. (Depuis 1.21.2, nécessite `bossbar: true` dans config)
    - `/[player_command] actionbar` : bascule l'affichage de la barre d'action affichant la progression de la phase. (Depuis 1.21.2, nécessite `actionbar: true` dans config)

=== "Commandes admin"
    - `/[admin_command] sanity [<phase>]` : envoie un message si les coffres des phases (ou `<phase>`) sont corrects.
    - `/[admin_command] setcount <player> <number>` : permet de modifier la phase actuelle d'un `<player>` où `<number>` est le numéro de démarrage de la phase.
    - `/[admin_command] setchest <phase> <rarity>` : enregistre un coffre que le joueur regarde dans la section coffres de `<phase>` avec `<rarity>`.


Par défaut, les addons du mode de jeu BentoBox sont livrés avec l'ensemble de sous-commandes par défaut, cependant, chaque addon peut introduire encore plus de sous-commandes.

[Liste complète des commandes AOneBlock](Commands)


## Permissions

!!! tip
    Le préfixe `[gamemode]` partout pour l'addon AOneBlock doit être remplacé par `aoneblock`.

=== "Permissions du joueur"
    - `aoneblock.count` - Permettre au joueur d'utiliser la commande '/[player_command] count'. Activé par défaut.
    - `aoneblock.phases` - Permettre au joueur d'utiliser la commande '/[player_command] phases'. Désactivé par défaut.
    - `aoneblock.island.setcount` - Permettre au joueur d'utiliser la commande '/[player_command] setcount'. Désactivé par défaut.
    - `aoneblock.respawn-block` - Permettre au joueur d'utiliser la commande '/[player_command] check'. Activé par défaut.
    - `aoneblock.island.bossbar` - Permettre au joueur d'utiliser la commande '/[player_command] bossbar'. Activé par défaut. (Nécessite `bossbar: true` dans config)
    - `aoneblock.island.actionbar` - Permettre au joueur d'utiliser la commande '/[player_command] actionbar'. Activé par défaut. (Nécessite `actionbar: true` dans config)

=== "Permissions admin"
    - `aoneblock.admin.sanity` - Permettre au joueur d'utiliser la commande '/[admin_command] sanity'. Par défaut OP.
    - `aoneblock.admin.setchest` - Permettre au joueur d'utiliser la commande '/[admin_command] setchest'. Par défaut OP.
    - `aoneblock.admin.setcount` - Permettre au joueur d'utiliser la commande '/[admin_command] setcount'. Par défaut OP.

Par défaut, les addons du mode de jeu BentoBox sont livrés avec l'ensemble de sous-permissions par défaut, cependant, chaque addon peut introduire encore plus de sous-permissions.

[Liste complète des permissions AOneBlock](Permissions)


## Drapeaux

AOneBlock introduit plusieurs drapeaux personnalisés qui contrôlent le comportement du jeu :

| Drapeau | Type | Description | Par défaut |
|------|------|-------------|---------|
| `START_SAFETY` | Paramètre mondial | Lorsqu'il est activé, les joueurs ne peuvent pas se déplacer pendant une brève période après la création d'une nouvelle île, ce qui les empêche de tomber immédiatement. La durée est définie par `starting-safety-duration` dans config. | false |
| `ONEBLOCK_BOSSBAR` | Paramètre d'île | Bascule si la barre de boss de progression de phase OneBlock est affichée pour le joueur. Disponible uniquement si `bossbar: true` est défini dans config. | true |
| `ONEBLOCK_ACTIONBAR` | Paramètre d'île | Bascule si la barre d'action de progression de phase OneBlock est affichée pour le joueur. Disponible uniquement si `actionbar: true` est défini dans config. | true |
| `MAGIC_BLOCK` | Protection | Définit le rang d'île minimum requis pour casser le bloc magique. Le rang par défaut est Coop. | COOP |


## Placeholders

L'addon AOneBlock a ses propres placeholders uniques. Ces placeholders se rapportent aux données que AOneBlock stocke.

|Placeholder|Description|Version AOneBlock|
|--- |--- |--- |
|%aoneblock_my_island_phase%|la phase de votre île|1.1.2|
|%aoneblock_my_island_count%|le nombre de blocs de votre île|1.1.2|
|%aoneblock_visited_island_phase%|la phase de l'île sur laquelle vous vous tenez|1.1.2|
|%aoneblock_visited_island_count%|le nombre de blocs de l'île sur laquelle vous vous tenez|1.1.2|
|%aoneblock_my_island_next_phase%|la prochaine phase de votre île|1.1.2|
|%aoneblock_visited_island_next_phase%|la prochaine phase de l'île sur laquelle vous vous tenez|1.1.2|
|%aoneblock_my_island_blocks_to_next_phase%|blocs à miner jusqu'à la prochaine phase, ou "infini" s'il n'y a pas de prochaine phase|1.5.2|
|%aoneblock_visited_island_blocks_to_next_phase%|blocs jusqu'à la prochaine phase pour l'île sur laquelle vous vous tenez|1.5.2|
|%aoneblock_my_island_percent_done%|pourcentage de complétion de la phase|1.5.2|
|%aoneblock_visited_island_percent_done%|pourcentage de complétion de la phase de l'île sur laquelle vous vous tenez|1.5.2|
|%aoneblock_my_island_done_scale%|échelle de complétion de la phase de votre île|1.5.2|
|%aoneblock_visited_island_done_scale%|échelle de complétion de la phase de l'île sur laquelle vous vous tenez|1.5.2|
|%aoneblock_my_island_lifetime_count%|le nombre de blocs de vie pour votre île|1.10.0|
|%aoneblock_visited_island_lifetime_count%|le nombre de blocs de vie de l'île sur laquelle vous vous tenez|1.10.0|

Par défaut, les addons du mode de jeu BentoBox sont livrés avec [l'ensemble de placeholders par défaut](../../BentoBox/Placeholders), cependant, chaque addon peut introduire encore plus de placeholders.

[Liste complète des placeholders AOneBlock](Placeholders)

## FAQ

??? question "Pouvez-vous ajouter une fonctionnalité X ?"
    Veuillez l'ajouter à la liste [ici](https://github.com/BentoBoxWorld/AOneBlock/issues).

??? question "J'ai un bug, où dois-je le signaler ?"
    Veuillez l'ajouter à la liste [ici](https://github.com/BentoBoxWorld/AOneBlock/issues).

??? question "Quelles phases y a-t-il ?"
    Il y a 11 phases : Plains, Underground, Winter, Ocean, Jungle, Swamp, Dungeon, Desert, The Nether, Plenty, Desolation, and The End.

    Chaque phase propose un ensemble de blocs, d'articles et de mobs appropriés pour l'environnement.

??? question "Combien de blocs y a-t-il dans les 11 phases ?"
    Il y a actuellement 11 mille blocs !

??? question "Que se passe-t-il après la dernière phase ?"
    Les phases se répètent.

??? question "Pourquoi je ne cesse de tomber et de mourir !"
    Il y a des astuces pour survivre, mais c'est peut-être difficile ! Vous devez construire des défenses.

??? question "Pourquoi certains blocs s'apparaissent plus fréquemment que d'autres ?"
    C'est comme ça ! Vous pouvez définir la probabilité relative dans les fichiers de configuration du dossier phases.

??? question "Comment sais-je quel est le bloc magique ?"
    Frappez-le et il libérera des particules vertes.

??? question "Mon bloc magique n'est plus là ! Comment en obtenir un autre ?"
    Vous devrez placer un bloc là. Dans le pire des cas, tuez-vous et un sera généré.

??? question "Mon bloc magique est liquide ! Comment puis-je le miner ?"
    Utilisez un seau.

??? question "Quels mobs peuvent apparaître ?"
    Chaque phase a un ensemble différent de mobs qui peuvent apparaître. Soyez prudent car ils pourraient vous faire tomber ! Si vous écoutez attentivement, vous pouvez entendre des mobs hostiles arriver.

??? question "Je n'ai aucune chance de réagir à l'apparition de mobs hostiles !"
    Soyez préparé. Écoutez attentivement quand vous minez un bloc et vous entendrez les mobs hostiles arriver avant qu'ils n'apparaissent. Si vous êtes dans une phase hostile, attendez-vous à des mobs et construisez des défenses pour vous protéger. Vous pouvez miner un bloc à une distance assez éloignée.

??? question "Quand les mobs apparaissent, mes défenses sont détruites ! Pourquoi ?"
    Les mobs font de la place pour apparaître. S'il y a quelque chose en travers, il sera cassé et lâché. Vous devrez construire en conséquence.

??? question "Les coffres apparaissent-ils ?"
    Oui. Les coffres apparaissent avec des articles aléatoires de la phase actuelle. Il existe des coffres common, uncommon, rare et epic. Les coffres avec des paillettes sont bons.

??? question "Est-il possible d'atteindre le Nether ou l'End sur cette carte ?"
    Le Nether vanilla existe par défaut mais il n'y a pas de monde End.

    Cependant, BentoBox est personnalisable, et vous pouvez activer les îles du nether et le monde de fin dans le fichier de configuration d'AOneBlock.

    Sachez que le bloc magique est situé uniquement dans le monde principal.

??? question "Quel est l'objectif final ?"
    C'est ce que vous voulez que ce soit !

??? question "Comment utiliser les hologrammes ?"
    AOneBlock utilise [Holographic Displays](https://dev.bukkit.org/projects/holographic-displays) pour les hologrammes si vous utilisez la version 1.12.3 et antérieure.
    Vous devez installer ce plugin pour utiliser les sections d'hologrammes !

    Cependant, depuis la version 1.13 et Minecraft 1.19.4, vous n'avez besoin d'aucun plugin supplémentaire pour les hologrammes. Ils seront affichés en utilisant Minecraft Text Entity.

??? question "Dois-je utiliser l'addon Levels ?"
    C'est à vous de décider, mais si vous le faites, sachez que les niveaux pourraient devenir très élevés car les joueurs ont un bloc infini.
    Je préfère ne pas l'utiliser et utiliser à la place l'addon Likes.


## Traductions

{{ translations("AOneBlock") }}

## Api

Depuis que BentoBox 1.17 API a implémenté une fonctionnalité qui a résolu un problème avec les classloaders. Les plugins qui souhaitent accéder au code directement peuvent maintenant le faire.

Vous avez juste besoin d'ajouter AOneBlock à votre projet en tant que dépendance. Vous pouvez utiliser Maven pour cela :

```xml
<dependency>
    <groupId>world.bentobox</groupId>
    <artifactId>aoneblock</artifactId>
    <version>1.10.0</version>
    <scope>provided</scope>
</dependency>
```

L'addon AOneBlock stocke les données dans un tableau de base de données séparé.

=== "OneBlockIslands"
    !!! summary "Description"
        OneBlockIslands stocke toutes les informations sur la progression des îles à travers les phases.

        Lien vers le code source : [OneBlockIslands](https://github.com/BentoBoxWorld/AOneBlock/blob/develop/src/main/java/world/bentobox/aoneblock/dataobjects/OneBlockIslands.java)

    !!! question "Variables"
        - "uniqueId": l'ID unique de l'île. Il est égal à l'ID unique de l'île.
        - "blockNumber": le numéro de bloc cassé actuel.
        - "lifetime": le nombre total de blocs cassés.
        - "phaseName": le nom de la phase actuelle.
        - "hologram": le texte hologramme qui est affiché.

    !!! example "Exemple de code"
        Pour accéder à ces données, vous devez accéder à l'addon AOneBlock. Il peut y avoir plusieurs façons, mais l'exemple ci-dessous montre une manière générique accessible de partout.

        ```java
        public void accessToAOneBlockData(@NonNull Island island) {
           BentoBox.getInstance().getAddonsManager().<AOneBlock>getAddonByName("AOneBlock").ifPresent(aOneBlock -> {
                OneBlockIslands oneBlockData = aOneBlock.getOneBlocksIsland(island);

                String islandUniqueId = oneBlockData.getUniqueId();
                int brokenBlocks = oneBlockData.getBlockNumber();
                long lifetimeBlocks = oneBlockData.getLifetime();
                String phase = oneBlockData.getPhaseName();
                String hologram = oneBlockData.getHologram();
           });
        }
        ```

### Événements

AOneBlock a quelques événements personnalisés qui ne sont appelés que dans AOneBlock. Mais les événements du mode de jeu BentoBox sont toujours déclenchés dans AOneBlock.

=== "BlockClearEvent"
    !!! summary "Description"
        Cet événement est déclenché avant qu'une entité ne soit générée. Il contient une liste de blocs qui seront supprimés ou remplacés par de l'eau.

        Peut être annulé.

        Lien vers la classe : [BlockClearEvent](https://github.com/BentoBoxWorld/AOneBlock/blob/develop/src/main/java/world/bentobox/aoneblock/events/BlockClearEvent.java)

    !!! question "Variables"
        - `Entity entity` - l'entité qui est générée.
        - `List<Block> airBlocks` - la liste des blocs qui seront remplacés par de l'air.
        - `List<Block> waterBlocks` - la liste des blocs qui seront remplacés par de l'eau.
        - `boolean cancelled` - le booléen qui indique si l'événement est annulé.

    !!! example "Exemple de code"
        ```java
        @EventHandler(priority = EventPriority.MONITOR)
        public void onBlockClear(BlockClearEvent event) {
            Entity entity = event.getEntity();
            List<Block> airBlocks = event.getAirBlocks();
            List<Block> waterBlocks = event.getWaterBlocks();

            boolean cancelled = event.isCancelled();
        }
        ```

=== "MagicBlockEntityEvent"
    !!! summary "Description"
        Cet événement est déclenché après qu'une entité soit générée. Il contient simplement les informations de base sur l'entité générée.

        Lien vers la classe : [MagicBlockEntityEvent](https://github.com/BentoBoxWorld/AOneBlock/blob/develop/src/main/java/world/bentobox/aoneblock/events/MagicBlockEntityEvent.java)

    !!! question "Variables"
        - `EntityType entityType` - le type d'entité qui est généré.
        - `@NonNull Island island` - l'île où l'entité est invoquée
        - `@Nullable UUID playerUUID` - l'ID utilisateur qui a déclenché la génération d'entité. Peut être Null.
        - `@NonNull Block block` - l'emplacement du bloc magique.

    !!! example "Exemple de code"
        ```java
        @EventHandler(priority = EventPriority.MONITOR)
        public void onMagicBlockEntity(MagicBlockEntityEvent event) {
            EntityType entityType = event.getEntityType();

            Island island = event.getIsland();
            UUID playerUUID = event.getPlayerUUID();
            Block block = event.getBlock();
        }
        ```

=== "MagicBlockEvent"
    !!! summary "Description"
        Cet événement est déclenché après qu'un bloc magique soit cassé.

        Lien vers la classe : [MagicBlockEvent](https://github.com/BentoBoxWorld/AOneBlock/blob/develop/src/main/java/world/bentobox/aoneblock/events/MagicBlockEvent.java)

    !!! question "Variables"
        - `@Nullable ItemStack tool` - l'outil qui a cassé le bloc magique.
        - `@NotNull Material nextBlockMaterial` - le matériau du prochain bloc magique.
        - `@NonNull Island island` - l'île où le bloc est invoqué.
        - `@Nullable UUID playerUUID` - l'ID utilisateur qui a cassé le bloc magique. Peut être Null.
        - `@NonNull Block block` - l'emplacement du bloc magique.

    !!! example "Exemple de code"
        ```java
        @EventHandler(priority = EventPriority.MONITOR)
        public void onMagicBlock(MagicBlockEvent event) {
            ItemStack tool = event.getTool();
            Material nextBlockMaterial = event.getNextBlockMaterial();

            Island island = event.getIsland();
            UUID playerUUID = event.getPlayerUUID();
            Block block = event.getBlock();
        }
        ```

=== "MagicBlockPhaseEvent"
    !!! summary "Description"
        Cet événement est déclenché après qu'une nouvelle phase ait commencé.

        Lien vers la classe : [MagicBlockPhaseEvent](https://github.com/BentoBoxWorld/AOneBlock/blob/develop/src/main/java/world/bentobox/aoneblock/events/MagicBlockPhaseEvent.java)

    !!! question "Variables"
        - `String phase` - le nom de la nouvelle phase.
        - `String oldPhase` - le nom de la phase précédente.
        - `int blockNumber` - le numéro de bloc au démarrage de la nouvelle phase.
        - `@NonNull Island island` - l'île où le bloc est invoqué.
        - `@Nullable UUID playerUUID` - l'ID utilisateur qui a cassé le bloc magique. Peut être Null.
        - `@NonNull Block block` - l'emplacement du bloc magique.

    !!! example "Exemple de code"
        ```java
        @EventHandler(priority = EventPriority.MONITOR)
        public void onMagicBlockPhase(MagicBlockPhaseEvent event) {
            String phase = event.getPhase();
            String oldPhase = event.getOldPhase();
            int blockNumber = event.getBlockNumber();

            Island island = event.getIsland();
            UUID playerUUID = event.getPlayerUUID();
            Block block = event.getBlock();
        }
        ```
