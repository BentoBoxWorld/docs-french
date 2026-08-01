# AOneBlock

Un bloc. C'est tout. C'est par là que vous commencez.

Cassez-le et il réapparaît en tant que quelque chose d'autre — un bloc d'herbe, un arbre, un coffre, un mob. Cassez-le à nouveau. Continuez. Lentement, péniblement, vous construisez une île à partir de rien, en débloquant de nouvelles phases à mesure que vous progressez : Plaines, Souterrain, Océan, Jungle, Nether, et au-delà. Chaque phase apporte de nouveaux blocs, de nouveaux mobs et de nouvelles surprises. Certaines très hostiles.

**AOneBlock** est l'interprétation de BentoBox de la célèbre carte OneBlock d'**IJAminecraft** — reconstruite comme une expérience serveur multijoueur complète avec 20 phases thématiques, 15 000+ blocs de contenu, des coffres de butin de rareté variable, et suffisamment de profondeur pour que les joueurs reviennent pendant des semaines.

Créé et maintenu par [tastybento](https://github.com/tastybento).

{{ addon_description("AOneBlock") }}

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

### L'index des phases — `phases_index.yml`

!!! new "Ajouté dans AOneBlock 1.26.0"
    `phases_index.yml` se trouve à côté du dossier `phases` et fait autorité sur les phases qui se chargent, dans quel ordre, sur la longueur de chacune, et sur la version de Minecraft requise par chacune. Il est lu **avant** qu'aucun fichier de phase ne soit analysé, donc une phase nécessitant une version de Minecraft plus récente est ignorée sans que son YAML — ni aucun objet qu'il contient — ne soit jamais touché.

Chaque entrée de la liste `phases:` accepte ces champs :

| Champ | Signification |
|---|---|
| `file` | Nom de base du fichier de phase dans le dossier `phases`, sans `.yml`. Le fichier de coffres est `<file>_chests.yml`. |
| `section` | La clé de premier niveau dans le fichier de phase (historiquement le bloc de départ). |
| `name` | Nom d'affichage, utilisé dans les journaux et dans le panneau `/[admin_command] phases`. |
| `length` | Nombre de blocs dans la phase. |
| `enabled` | Facultatif, `true` par défaut. Mettez `false` pour exclure une phase. |
| `requiredMinecraftVersion` | Facultatif. La phase est ignorée — sans occuper le moindre bloc — sur les serveurs antérieurs à cette version. |

Les blocs de départ sont **calculés** : ils correspondent à la somme cumulée des longueurs des phases activées situées au-dessus, en partant de 0. Cela signifie que les phases peuvent être réordonnées librement et qu'une phase ignorée disparaît de la progression. Après la dernière phase, le décompte de blocs revient à `gotoAtEnd`.

Un `adminLengths: true` de premier niveau est écrit automatiquement la première fois que vous modifiez une longueur dans `/[admin_command] phases`. À partir de ce moment, la réconciliation ne recalcule plus jamais les longueurs, donc vos valeurs survivent aux ajouts de fichiers, renommages et mises à niveau ultérieurs.

#### Réconciliation

!!! note "Depuis la 1.26.1, le dossier phases fait autorité"
    L'index est réconcilié avec les fichiers réellement présents sur le disque à chaque chargement, et à chaque enregistrement depuis le panneau admin, donc ce que `/[admin_command] phases` affiche correspond à ce que votre serveur exécute réellement. Surveillez dans le journal de démarrage les lignes commençant par `Phase index:` — elles indiquent exactement ce qui a été modifié.

- Une entrée dont le fichier a été **renommé d'une version de l'addon à l'autre** est repointée vers votre fichier d'après le nom de la phase, afin que la phase se charge à nouveau.
- Une entrée dont le fichier est **absent mais fourni dans le jar** est restaurée automatiquement. C'est ce qui fait apparaître les nouvelles phases sur les serveurs mis à niveau, puisque les fichiers de `phases/` ne sont jamais écrasés.
- Les **fichiers de phase personnalisés** déposés dans le dossier sont ajoutés automatiquement. Une clé numérique s'insère à son bloc de départ historique ; tout autre nom est ajouté à la fin pour que vous l'organisiez dans le panneau.
- Les entrées dont les fichiers ont définitivement disparu sont retirées avec un avertissement, afin que le panneau ne liste jamais des phases inexistantes.
- Quand une réparation a été nécessaire, les longueurs sont recalculées d'après les clés de bloc de départ historiques de vos fichiers, ce qui préserve la disposition que votre serveur exécutait réellement avant l'existence de l'index — sauf si `adminLengths` est défini.

!!! warning "Supprimer une phase"
    Pour retirer une phase définitivement, supprimez ses fichiers, ou désactivez-la dans `/[admin_command] phases`. Supprimer uniquement son entrée d'index ne fonctionne pas — la réconciliation réajoute tout fichier de phase qu'elle trouve dans le dossier.

    Un index mal formé retombe sur l'ancien chargement direct des fichiers, donc une mauvaise modification ne peut pas bloquer l'addon.

### Fichiers de configuration de phase

Les fichiers de configuration pour créer les phases se trouvent dans le dossier `phases`.

Il y a deux fichiers par phase — un fichier qui contient les blocs et les mobs, et un fichier qui contient les coffres.

Le premier nombre de tout fichier est le nombre de blocs qui doivent être minés pour atteindre cette phase. C'est le numéro clé de la phase.

!!! tip "Les nombres dans les noms de fichiers de phase sont facultatifs depuis la 1.26.1"
    Les fichiers de phase personnalisés n'ont plus besoin d'un bloc de départ numérique dans le nom du fichier ni comme clé de section YAML — `desert.yml` avec une section `desert:` fonctionne. Les fichiers de coffres sont toujours appariés par nom de fichier (`<file>_chests.yml`). Les nombres dans les fichiers fournis sont historiques : avec l'index aux commandes, les valeurs de départ et de longueur du panneau font autorité. Les clés numériques restent utiles car elles indiquent à la réconciliation où un fichier se situe et quelle était sa longueur.

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

    !!! tip "Notation CHEST_WITH_X"
        Les entrées de blocs fixes peuvent utiliser le raccourci `CHEST_WITH_X` pour placer un coffre pré-rempli avec un objet spécifique, par exemple `CHEST_WITH_WATER_BUCKET`. L'objet doit être un nom de matériau Bukkit valide.

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

=== "requiredMinecraftVersion"
    !!! summary "Description"
        Depuis la 1.26.0, une phase, un bloc isolé ou un mob isolé peut déclarer la version minimale de Minecraft dont il a besoin. Tout ce pour quoi le serveur est trop ancien est ignoré avec une simple ligne d'information dans le journal, au lieu de lever des erreurs `Tried to load invalid item` ou `ConfigurationSerialization`.

        Au niveau de la phase, la valeur va également dans `phases_index.yml`, afin que la phase puisse être ignorée avant même que son fichier ne soit analysé. Définie au niveau de la phase, celle-ci n'occupe aucun bloc sur un serveur plus ancien et les phases suivantes se décalent vers le haut.

        Les entrées individuelles de `blocks` et de `mobs` acceptent une forme d'objet avec `weight` plus leur propre `requiredMinecraftVersion`. Les fichiers de coffres sont lus objet par objet, donc un objet que votre version de serveur ne connaît pas est ignoré individuellement et le reste du coffre se charge quand même.

    !!! example "Exemple"
        ```yaml
            blocks:
              NETHERRACK: 300
              DRIED_GHAST:
                weight: 25
                requiredMinecraftVersion: '1.21.6'
        ```

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
          - `craftengine`: utilise l'API [CraftEngine](https://github.com/Xiao-MoMi/craft-core) pour créer un bloc. Nécessite le champ `id`. Le plugin CraftEngine doit être installé. Requiert BentoBox 3.15.0+.

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
              - type: craftengine
                id: mypack:custom_block
                probability: 10
              - DIRT: 10     # old syntax still works.
        ```

    !!! tip "ItemsAdder, Nexo et CraftEngine"
        Pour utiliser des blocs personnalisés d'ItemsAdder, Nexo ou CraftEngine, le plugin respectif doit être installé sur votre serveur.
        AOneBlock détecte automatiquement ces plugins au démarrage et enregistre les gestionnaires de blocs appropriés.
        Si vous configurez un bloc `itemsadder`, `nexo` ou `craftengine` mais que le plugin n'est pas installé, le bloc reviendra à STONE.


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
    - `/[admin_command] phases` : ouvre l'éditeur d'ordre des phases. (Depuis 1.26.0)

    ??? tip "Utiliser l'éditeur d'ordre des phases"
        `/[admin_command] phases` affiche chaque phase dans l'ordre avec son bloc de départ calculé, sa longueur et son état. Il modifie `phases_index.yml`, et les dépôts et bascules enregistrent l'index et rechargent les phases immédiatement.

        - **Clic gauche** sur une phase pour la prendre — les autres se resserrent vers la gauche. Cliquez là où elle doit aller pour pousser les autres vers la droite et la déposer, ou utilisez l'emplacement de dépôt en fin de liste. Cliquez n'importe où ailleurs, ou fermez le panneau, pour la remettre en place sans enregistrer.
        - **Clic droit** active ou désactive une phase.
        - **Maj + clic gauche** définit la longueur d'une phase (depuis la 1.26.1). Le panneau se ferme et une invite dans le chat affiche la longueur actuelle ; saisissez un nombre entier pour l'appliquer, ou `cancel` pour la conserver. Une saisie invalide relance l'invite, et l'invite expire après 60 secondes. La première modification de longueur écrit `adminLengths: true` dans l'index afin que vos valeurs ne soient plus jamais recalculées.

        Les phases désactivées apparaissent en verre gris et celles verrouillées par version en barrières — les deux peuvent toujours être réordonnées. Une phase sans icône configurée utilise son premier bloc.


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
    - `aoneblock.admin.phases` - Permettre au joueur d'utiliser la commande '/[admin_command] phases' pour ouvrir l'éditeur d'ordre des phases. Par défaut OP. (Depuis 1.26.0)

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
    Il y a 20 phases fournies, dans cet ordre : Plains, Underground, Winter, Ocean, Jungle, Swamp, Dungeon, Desert, The Nether, Plenty, Desolation, Deep Dark, The End, Lush Caves, Dripstone Caves, Mangrove Swamp, Meadow, Cherry Grove, Jagged Peaks et Sulfur Caves.

    Chaque phase propose un ensemble de blocs, d'articles et de mobs appropriés pour l'environnement.

    Sulfur Caves nécessite Minecraft 26.2 ou une version ultérieure. Sur les serveurs plus anciens, elle est ignorée et Jagged Peaks s'étend jusqu'au point de bouclage à la place. Vous pouvez réordonner, désactiver et redimensionner les phases vous-même avec `/[admin_command] phases`, et ajouter vos propres fichiers de phase dans le dossier `phases`.

??? question "Combien de blocs y a-t-il dans toutes les phases ?"
    15 500 blocs avec les phases fournies sur un serveur Minecraft 26.2+, ou 15 000 sans la phase Sulfur Caves.

??? question "Que se passe-t-il après la dernière phase ?"
    Les phases se répètent — le décompte de blocs revient à la valeur `gotoAtEnd` de `phases_index.yml`, qui est 0 par défaut.

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

## Journal des modifications

??? warning "Nouveautés dans v1.23.0 — mise à jour de locale et configuration requise"
    **Publié :** 11 avril 2026

    - **Support des blocs personnalisés Nexo.** AOneBlock supporte maintenant les blocs personnalisés [Nexo](https://github.com/Nexo-MC/Nexo) dans les définitions de phase (en plus du support existant pour ItemsAdder). Définissez-les avec `type: nexo` et un champ `id` dans votre configuration de phases.
    - **Support des couleurs HEX / MiniMessage dans la barre d'action.** Le texte de `/ob actionbar` affiche maintenant correctement les couleurs HEX et le formatage MiniMessage complet.
    - 🔡 Locale russe mise à jour au format MiniMessage avec corrections grammaticales.
    - Plusieurs corrections de bugs de locale et traduction pour la barre d'action.

    🔺 **Le support Nexo est une nouvelle option de configuration.** Si vous utilisez Nexo, ajoutez des entrées de type Nexo à vos fichiers de phase `.yml`.

    🔡 **Régénérez les fichiers de locale** si vous avez des personnalisations.

    [Release v1.23.0](https://github.com/BentoBoxWorld/AOneBlock/releases/tag/1.23.0)

??? warning "Nouveautés dans v1.24.0 — requiert BentoBox 3.15.0"
    **Publié le :** 2026-04-26

    - **Support des blocs personnalisés CraftEngine.** Les phases peuvent désormais générer des blocs [CraftEngine](https://github.com/Xiao-MoMi/craft-core) en utilisant `type: craftengine` dans les définitions de phase. Requiert BentoBox 3.15.0+.
    - **Particules de coffre configurables par rareté.** Le type et la couleur des particules affichées au-dessus des coffres UNCOMMON/RARE/EPIC sont désormais configurables dans `config.yml` sous `world.chest-particles`. Définissez une particule sur `NONE` pour la désactiver.
    - **Notation `CHEST_WITH_X` pour les blocs fixes.** Les `fixedBlocks` de phase acceptent désormais les entrées `CHEST_WITH_<ITEM>` pour placer un coffre pré-rempli avec cet objet (ex. `CHEST_WITH_WATER_BUCKET`).
    - **`OBSIDIAN_SCOOPING` désactivé par défaut.** Les nouvelles installations ont ce drapeau défini sur `false`. Les serveurs existants avec un paramètre explicite ne sont pas affectés.
    - 🔡 Valeurs par défaut des placeholders pour les joueurs sans île : `%aoneblock_my_island_phase%`, `%aoneblock_my_island_count%` et `%aoneblock_my_island_percent_done%` retournent désormais `Unknown`, `0` et `0%` au lieu de chaînes vides.

    🔺 **Requiert BentoBox 3.15.0 ou supérieur** — cette version ne se chargera pas avec des versions antérieures de BentoBox.

    ⚙️ **Nouvelle section de config** `world.chest-particles` — copiez depuis le dernier `config.yml` si vous souhaitez des effets de particules configurables.

    🔡 **Régénérez les fichiers de locale** pour récupérer les nouvelles clés.

    [Release v1.24.0](https://github.com/BentoBoxWorld/AOneBlock/releases/tag/1.24.0)

??? note "Nouveautés dans v1.25.0"
    **Publié le :** 2026-05-03

    - **Nid d'abeilles peuplé dans Plenty.** La phase Plenty fait désormais apparaître un `bee_nest` (3 abeilles à l'intérieur, `honey_level=0`) à la même densité que les autres objets de miel, comblant la lacune de longue date sur l'élevage du miel.
    - **Resync client du bloc magique après tirage de mob.** Quand le bloc magique tirait un mob, l'événement de cassure annulé laissait le bloc transparent côté client jusqu'à la prochaine resync de chunk. L'état du bloc est maintenant renvoyé au joueur immédiatement.
    - 🐛 **Correctif d'ordre de démarrage CraftEngine.** Le `onEnable` d'`AOneBlock` s'exécute avant que CraftEngine ne peuple son registre de blocs, ce qui provoquait auparavant une avalanche de fausses erreurs `Bad custom block`. Le parseur de blocs fait désormais confiance à une déclaration explicite `type: craftengine` au chargement de la config, et valide l'ID au moment du placement.
    - 🐛 **Validation plus stricte de l'ID de bloc CraftEngine au chargement.** Les IDs vides et ceux qui n'ont pas la forme `namespace:key` sont désormais rejetés au chargement de la config au lieu d'être silencieusement acceptés et d'échouer plus tard.
    - 🐛 **Les particules de coffre configurables ne plantent plus sur les types non `DUST`.** Les types de particules dont le type de données n'est pas `Void` (par ex. `ITEM`, `BLOCK`, `ENTITY_EFFECT`) lançaient une `IllegalArgumentException`. Elles sont maintenant détectées, journalisées en avertissement et ignorées. `DUST` et les particules à données void (par ex. `FLAME`) fonctionnent comme avant.

    🔺 Si vous voulez le nouveau nid d'abeilles, copiez la nouvelle entrée dans votre `phases/8500_plenty.yml` (ou supprimez le dossier phases pour qu'il se régénère) — les fichiers de phase personnalisés ne sont pas écrasés à la mise à jour.

    [Release v1.25.0](https://github.com/BentoBoxWorld/AOneBlock/releases/tag/1.25.0)

??? note "Nouveautés dans v1.25.1"
    **Publié :** 3 juillet 2026

    Version de correction de bugs — remplaçable direct, pas de modification de configuration ou de locale.

    - 🐛 **Les minions mineur peuvent à nouveau casser le bloc magique.** Casser le bloc magique avec un Miner minion de JetsMinions levait une `NullPointerException` et laissait le bloc manquant jusqu'à sa restauration manuelle avec `/ob respawnblock`. Le chemin de cassure du minion ne passe plus la vérification de protection du bloc magique réservée au joueur qui causait le crash, donc le bloc se recycle et réapparaît comme prévu. Cette régression était présente depuis 1.22.0.
    - 🐛 **Les placeholders `my_island_*` corrigés pour les membres d'équipe en visite.** Quand un joueur appartenant à une équipe visitait une autre île, les placeholders `my_island_*` se résolvaient aux données d'équipe de l'île visitée au lieu de sa propre île. Ils se résolvent maintenant toujours à l'île propre du joueur.

    [Release v1.25.1](https://github.com/BentoBoxWorld/AOneBlock/releases/tag/1.25.1)

??? note "Nouveautés dans v1.25.2"
    **Publié :** 18 juillet 2026

    Version de correction de bugs — remplaçable direct, pas de modification de configuration ou de locale.

    - 🐛 **Exploit de récompenses infinies avec Jobs Reborn corrigé.** Quand le drapeau `MAGIC_BLOCK` empêchait un joueur de casser le bloc magique, les plugins qui écoutent les cassures de blocs — comme Jobs Reborn — voyaient tout de même la cassure comme réussie et versaient les récompenses. Comme le bloc réapparaît instantanément, un visiteur pouvait miner indéfiniment le même bloc de valeur pour obtenir des récompenses de métier infinies. La cassure refusée est désormais annulée avant que les autres plugins ne la traitent.
    - 🐛 **`actionbar: false` désactive désormais réellement la barre d'action.** Si la barre de boss était activée, l'affichage de progression dans la barre d'action continuait à apparaître même avec `actionbar: false`, et l'inverse s'appliquait à la barre de boss. Les deux paramètres sont désormais respectés, et les affichages de progression ne sont plus mis à jour deux fois par cassure de bloc lorsque les deux sont activés.

    [Release v1.25.2](https://github.com/BentoBoxWorld/AOneBlock/releases/tag/1.25.2)

!!! warning "Nouveautés dans v1.26.0 — l'index des phases (à vérifier après la mise à niveau)"
    **Publié :** 20 juillet 2026

    Ajoute la phase Sulfur Caves pour les serveurs Minecraft 26.2 et — parce que livrer une phase réservée à la 26.2 dans un addon qui fonctionne aussi sur les serveurs 1.21.x demandait une véritable gestion des versions — introduit l'index des phases qui contrôle quelles phases se chargent, dans quel ordre et sur quelles versions de serveur. Compatibilité : API BentoBox 3.15.0+ · Minecraft 1.21.5 ou version ultérieure · Java 21.

    - **Phase Sulfur Caves.** Une nouvelle phase à l'emplacement 15000 : du soufre et du cinabre en couches parmi les blocs souterrains habituels, avec des Sulfur Cubes, des araignées des cavernes et compagnie aux poids d'apparition du wiki, ainsi que des coffres thématiques pouvant contenir le disque de musique *Bounce*. Le point de bouclage de fin de partie passe de 15000 à 15500. La phase déclare `requiredMinecraftVersion: '26.2'`, donc elle apparaît automatiquement sur les serveurs 26.2+ et est ignorée avec une simple ligne d'information sur les plus anciens — Jagged Peaks s'étend simplement jusqu'au point de bouclage à la place.
    - 🔺 **Nouveau `phases_index.yml`.** Il fait désormais autorité sur l'ordre des phases, leur longueur, leur état d'activation et la version de Minecraft requise. Les blocs de départ correspondent à la somme cumulée des longueurs au-dessus, donc les phases peuvent être déplacées librement et une phase ignorée disparaît de la progression. L'index est lu **avant** qu'aucun fichier de phase ne soit analysé, ce qui élimine les traces d'appel `Tried to load invalid item` et `ConfigurationSerialization` que les objets de versions plus récentes provoquaient sur les serveurs plus anciens. Voir la section Configuration ci-dessus.
    - **Blocs, mobs et objets de coffres soumis à une version.** Les fichiers de coffres sont désormais lus objet par objet, donc un objet que cette version de serveur ne connaît pas est ignoré avec une seule ligne de journal et le reste du coffre se charge. Les entrées de blocs et de mobs acceptent une forme d'objet avec un `requiredMinecraftVersion` propre à chaque entrée.
    - 🔡 **Nouveau panneau `/[admin_command] phases`** (permission `aoneblock.admin.phases`, OP par défaut) pour réordonner, insérer et activer/désactiver les phases en les faisant glisser par clics dans un panneau d'inventaire.

    🔺 **Un `phases_index.yml` est généré au premier démarrage** à partir des fichiers de phase de votre dossier de données, et à partir de là, il contrôle l'ordre et les longueurs des phases. Cela vaut une vérification rapide après le premier démarrage, surtout si vous avez modifié des phases à la main. Un index mal formé retombe sur l'ancien chargement direct des fichiers, donc rien ne peut se bloquer.

    🔺 **Les installations existantes ne reçoivent pas automatiquement les nouveaux fichiers de phase.** Les fichiers de `addons/AOneBlock/phases/` ne sont jamais écrasés. En 1.26.0, vous deviez copier vous-même `15000_sulfur_caves.yml` et `15000_sulfur_caves_chests.yml` depuis le jar ; à partir de la 1.26.1, la réconciliation les restaure pour vous.

    🔡 **De nouvelles clés de locale** ont été ajoutées pour l'éditeur d'ordre des phases — régénérez ou mettez à jour les fichiers de locale traduits.

    [Release v1.26.0](https://github.com/BentoBoxWorld/AOneBlock/releases/tag/1.26.0)

!!! warning "Nouveautés dans v1.26.1 — le dossier phases fait désormais autorité"
    **Publié :** 21 juillet 2026

    Une version de correction pour l'index des phases de la 1.26.0. En 1.26.0, les serveurs en cours de mise à niveau recevaient le `phases_index.yml` *d'origine*, qui référence les noms de fichiers du jar actuel — mais les dossiers `phases/` existants contiennent des dispositions plus anciennes ou personnalisées. Des phases échouaient silencieusement à se charger, Sulfur Caves n'apparaissait jamais sur les serveurs mis à niveau, et `/[admin_command] phases` affichait une configuration prédéfinie au lieu de la réalité du serveur.

    - 🔺 **Index des phases auto-réparateur.** L'index est désormais réconcilié avec le dossier `phases/` à chaque chargement et à chaque enregistrement depuis le panneau : les entrées renommées d'une version de l'addon à l'autre sont repointées vers votre fichier d'après le nom de la phase, les entrées absentes mais fournies dans le jar sont restaurées (donc Sulfur Caves apparaît sur les serveurs 26.2 mis à niveau), les fichiers de phase personnalisés sont ajoutés automatiquement, et les entrées dont les fichiers ont définitivement disparu sont retirées avec un avertissement. Là où une réparation a été nécessaire, les longueurs sont recalculées d'après les clés de bloc de départ historiques de vos fichiers, ce qui préserve la disposition que votre serveur exécutait réellement.
    - 🔡 **Définir les longueurs de phase dans le panneau.** Maj + clic gauche sur une phase pour définir sa longueur via une invite dans le chat. La première modification de longueur écrit `adminLengths: true` dans `phases_index.yml`, après quoi la réconciliation ne recalcule plus jamais les longueurs.
    - **Les nombres dans les noms de fichiers de phase sont désormais facultatifs.** Un `desert.yml` personnalisé avec une section `desert:` fonctionne ; les fichiers de coffres sont toujours appariés par nom de fichier.
    - 🔡 **Finitions du panneau.** Les icônes de phase retombent sur le premier bloc de la phase au lieu de la pierre, le livre « Comment utiliser » se répartit sur quatre lignes, et la description par phase est plus courte pour les petits écrans.

    🔺 **Votre `phases_index.yml` sera probablement réécrit au premier démarrage** pour correspondre aux fichiers de votre dossier phases. Surveillez dans le journal les lignes commençant par `Phase index:` — elles indiquent exactement ce qui a été repointé, restauré, ajouté ou retiré. Les phases qui avaient disparu après la mise à niveau en 1.26.0 reviennent d'elles-mêmes.

    🔺 **Pour retirer une phase définitivement, supprimez ses fichiers,** ou désactivez-la dans le panneau. Supprimer uniquement son entrée d'index ne fonctionne plus — la réconciliation réajoute tout fichier de phase qu'elle trouve.

    🔡 **Clés de locale nouvelles et modifiées** pour l'invite de longueur et le texte remanié du panneau.

    [Release v1.26.1](https://github.com/BentoBoxWorld/AOneBlock/releases/tag/1.26.1)

??? note "Nouveautés dans v1.26.2"
    **Publié :** 25 juillet 2026

    Version de correction pour une régression du butin introduite en 1.26.0. **Si vous êtes en 1.26.0 ou 1.26.1, mettez à jour.**

    - 🐛 **Les objets des coffres conservent à nouveau leurs métadonnées.** Depuis la 1.26.0, les fichiers de coffres sont lus avec SnakeYAML brut plutôt qu'avec `YamlConfiguration`, afin qu'un objet inconnu de votre version de serveur puisse être ignoré individuellement au lieu de faire tomber tout le fichier de coffres. L'effet secondaire était que rien n'était désérialisé à l'entrée : la section `meta` d'un objet arrivait sous forme de simple map, et le désérialiseur d'objets de Bukkit ignore silencieusement les métadonnées qui ne sont pas déjà un `ItemMeta`. Enchantements, effets de potion et noms étaient perdus sans une ligne dans le journal — de façon la plus visible pour les livres enchantés des coffres de Plains, mais cela s'appliquait à tous les objets de coffres de toutes les phases, y compris les potions, les flèches à effet, les objets renommés, les bannières, les têtes de joueur et les livres écrits.

        Les définitions d'objets de coffres sont désormais parcourues correctement et leurs métadonnées désérialisées avant la construction de l'objet. Le comportement de la 1.26.0 est inchangé — un objet qui n'existe pas dans votre version de Minecraft est toujours ignoré avec une ligne de journal — et une section de métadonnées illisible ne coûte désormais que ses métadonnées, en le signalant dans le journal, au lieu de faire perdre l'objet.

    Aucune modification des fichiers de phase n'est nécessaire : les anciens noms d'enchantements dans le YAML de phase fourni (`PROTECTION_FALL` et compagnie) sont toujours traduits par le serveur, donc les fichiers de coffres personnalisés fonctionnent tels quels. Les objets que les joueurs ont **déjà** récupérés restent en l'état — les métadonnées ont été perdues au moment du remplissage du coffre, il n'y a donc rien à réparer après coup. Tous les coffres générés à partir de maintenant sont corrects.

    [Release v1.26.2](https://github.com/BentoBoxWorld/AOneBlock/releases/tag/1.26.2)

??? note "Nouveautés dans v1.26.3"
    **Publié :** 29 juillet 2026

    Version corrective pour l'interface des phases — remplacement direct, sans changement de configuration, de traduction ni de fichier de phase.

    - 🐛 **« Cliquez pour changer » n'est proposé que lorsque le clic peut aboutir.** Le panneau `/[player_command] phases` décidait de proposer l'action de changement de phase à partir du seul état de l'île et des prérequis de la phase, sans jamais vérifier si le joueur disposait de la permission `aoneblock.island.setcount` que le clic utilise réellement. Sur les serveurs où cette permission est retirée à certains rangs ou à tous, les joueurs voyaient l'infobulle sur chaque phase éligible et obtenaient *« Vous n'avez pas la permission d'exécuter cette commande »* en cliquant. Le panneau vérifie désormais la permission avant de proposer l'action. Si la sous-commande ne peut être résolue pour une raison quelconque, le panneau reste permissif comme auparavant : aucune phase ne devient donc impossible à cliquer à cause de ce changement. Les joueurs qui **détiennent** la permission ne voient aucune différence.

    Compatibilité : BentoBox API 3.15.0+, Minecraft 1.21.5 ou ultérieur (la phase Sulfur Caves elle-même s'active à partir de Minecraft 26.2), Java 21.

    [Release v1.26.3](https://github.com/BentoBoxWorld/AOneBlock/releases/tag/1.26.3)
