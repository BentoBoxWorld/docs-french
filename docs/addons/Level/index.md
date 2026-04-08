# Level

**Level** permet à vos joueurs de rivaliser pour avoir l'île la meilleure ! Placez des blocs et augmentez le niveau de l'île !

Créé et maintenu par [tastybento](https://github.com/tastybento).

{{ addon_description("Level") }}

## Installation

1. Placez le fichier jar du module level dans le dossier addons du plugin BentoBox
2. Redémarrez le serveur
3. Le module créera un dossier de données et dans ce dossier se trouvera un config.yml
4. Modifiez le config.yml comme vous le souhaitez. La configuration spécifie combien les blocs valent (voir ci-dessous)
5. Redémarrez le serveur si vous apportez une modification

## Configuration

Le module level a 3 choses de configuration générale :

- Le fichier config.yml contient les fichiers de configuration par défaut du module.
- Le fichier blockconfig.yml contient la valeur de chaque bloc.
- /panels/ contient les fichiers qui gèrent les interfaces graphiques du joueur

### config.yml

Le fichier de configuration contient les fonctions principales du module.

Le dernier config.yml se trouve [ici](https://github.com/BentoBoxWorld/Level/blob/develop/src/main/resources/config.yml).

Cette section définit un certain nombre de paramètres généraux pour le module.

??? note "disabled-game-modes"
    Permet de spécifier dans quels GameModeAddons le module Level ne doit pas opérer.

    Le module Level ne se connectera PAS à ces modules gamemode.

    Par défaut : `[]`

??? note "log-report-to-console"
    Permet de voir un rapport de niveau si la commande est exécutée depuis la console.

    Par défaut : `true`

??? note "concurrent-island-calcs"
    Permet de spécifier combien de calculs de niveau d'île peuvent se produire à la fois.

    Si votre CPU peut le gérer, vous pouvez exécuter des calculs parallèles d'îles s'il y en a plus d'un dans la file d'attente.

    Par défaut : `1`

??? note "calculation-timeout"
    Permet de spécifier le nombre de minutes après lequel le calcul du niveau doit être arrêté.

    Généralement, le calcul ne devrait prendre que quelques secondes, donc si cela se déclenche jamais, quelque chose ne va pas.

    Par défaut : `5`

??? note "zero-new-island-levels"
    Permet de spécifier si les blocs de démarrage doivent être inclus dans le niveau de l'île.

    Si true, le module Level calculera le niveau de l'île de démarrage et le supprimera de tous les calculs de niveau futurs.
    Le niveau du joueur peut entrer dans des valeurs négatives si tous les blocs de démarrage sont supprimés.

    Si c'est false, les blocs de l'île de démarrage du joueur compteront vers son niveau.

    Par défaut : `true`

??? note "login"
    Permet de définir que le niveau de l'île est calculé à la connexion du joueur.

    Cela calcule silencieusement le niveau de l'île du joueur quand il se connecte.

    Par défaut : `false`

??? note "nether"
    Permet d'inclure l'île du nether dans le calcul du niveau.

    Avertissement : Activer ceci en cours de partie donnera aux joueurs avec une île un niveau d'île supérieur. Les nouvelles îles seront correctement mises à zéro.

    Par défaut : `false`

??? note "end"
    Permet d'inclure l'île de la fin dans le calcul du niveau.

    Avertissement : Activer ceci en cours de partie donnera aux joueurs avec une île un niveau d'île supérieur. Les nouvelles îles seront correctement mises à zéro.

    Par défaut : `false`

??? note "include-chests"
    Permet d'inclure le contenu des coffres dans le calcul du niveau.

    Avertissement : le calcul du niveau sera plus long et les performances du serveur peuvent être affectées.

    Par défaut : `false`

??? note "underwater"
    Permet de spécifier le multiplicateur de bloc sous-marin.

    Si les blocs sont sous le niveau de la mer, ils peuvent avoir une valeur plus élevée. par exemple 2x.
    Favorise le développement sous-marin s'il y a une mer. La valeur peut être fractionnaire.

    Par défaut : `1.0`

??? note "levelcost"
    Permet de spécifier la valeur d'un niveau d'île.

    Par défaut : `100`

    Minimum : `1`

??? note "level-calc"
    Permet de spécifier la formule pour le calcul du niveau.

    * blocks - la somme totale de toutes les valeurs de blocs, moins toute pénalité de mort
    * level_cost - dans une équation linéaire, la valeur d'un niveau

    Cette formule peut inclure +,=,*,/,sqrt,^,sin,cos,tan,log (log naturel).
    Le résultat sera toujours arrondi à un long entier.

    Par exemple, une option non-linéaire alternative pourrait être : `3 * sqrt(blocks / level_cost)`

    Par défaut : `blocks / level_cost`

??? note "levelwait"
    Permet de spécifier le délai entre les demandes de niveau en secondes.

    Par défaut : `60`

??? note "deathpenalty"
    Permet de spécifier la pénalité de mort.

    Combien de valeurs de blocs un joueur perdra par mort.
    La valeur par défaut de 100 signifie que pour chaque mort, le joueur perdra 1 niveau (si levelcost est 100).

    Définir à zéro pour ne pas utiliser cette fonctionnalité.

    Par défaut : `100`

??? note "sumteamdeaths"
    Permet de sommer toutes les morts des membres de l'équipe pour la pénalité de mort.

    Si false, seules les morts du chef comptent.

    Par défaut : `false`

??? note "shorthand"
    Permet d'afficher des numéros de niveau d'île plus courts.

    Affiche les grandes valeurs de niveau arrondies vers le bas, par ex., 10 345 -> 10k

    Par défaut : `false`

### blockconfig.yml

Le fichier de configuration des blocs contient les valeurs des blocs.

Le dernier blockconfig.yml se trouve [ici](https://github.com/BentoBoxWorld/Level/blob/develop/src/main/resources/blockconfig.yml).

Cette section définit les valeurs des blocs et les limites pour ceux-ci.

!!! tip
    Les valeurs dans ce fichier supportent uniquement les entiers -> nombres entiers.

!!! tip
    Les noms de matériaux corrects peuvent être trouvés sur la page des matériaux de Spigot.

    Note : ceci est la dernière liste des matériaux spigot : [MATERIALS](https://hub.spigotmc.org/javadocs/bukkit/org/bukkit/Material.html)

??? note "limits"
    Cette section répertorie les limites pour un bloc particulier.
    Les blocs au-delà de ce montant ne sont pas comptabilisés.
    Cette limite s'applique à tous les gamemodes et n'est pas spécifique au monde.

    Format : `MATERIAL: NUMBER`

??? note "blocks"
    Cette section répertorie la valeur d'un bloc dans tous les gamemodes (mondes).
    Pour spécifier des valeurs spécifiques au monde, utilisez la section suivante.
    Tous les blocs non répertoriés auront une valeur de 0. L'AIR a toujours une valeur de zéro.

    Format : `MATERIAL: NUMBER`

??? note "worlds"
    Répertoriez les blocs qui ont une valeur différente dans un monde spécifique.
    Si un bloc n'est pas répertorié, la valeur par défaut sera utilisée à partir de la section des blocs.
    Préfixez avec le nom du monde. Les valeurs s'appliqueront au nether associé et à la fin s'ils existent.

    Exemple:

    ```
        worlds:
          AcidIsland_world:
            SAND: 0
            SANDSTONE: 0
            ICE: 0
    ```

    Dans cet exemple, AcidIsland utilisera les mêmes valeurs que BSkyBlock pour tous les blocs sauf le sable, la pierre de sable et la glace.

### Interfaces graphiques personnalisables

L'API BentoBox 1.17 a introduit une fonction qui permet d'implémenter des interfaces graphiques personnalisables. Nous avons essayé d'être aussi simple que possible pour la personnalisation, cependant, certaines fonctionnalités nécessitent une explication.
Vous pouvez trouver plus d'informations sur le fonctionnement des interfaces graphiques personnalisées de BentoBox ici : [Custom GUI's](/en/latest/Tutorials/generic/Customizable-GUI/)

??? question "Comment puis-je personnaliser les interfaces graphiques ?"
    Pour personnaliser les interfaces graphiques du module Level, vous devez avoir la version 2.10.0. C'est la première version qui les a implémentées. Le module créera un nouveau répertoire sous `/plugins/bentobox/addons/level` nommé `panels`

    Actuellement, vous pouvez personnaliser 3 interfaces graphiques :

    - Top panel: `top_panel` - permet de voir les 10 meilleures îles.
    - The detail block panel: `detail_panel` - permet de voir une liste détaillée des valeurs de blocs en jeu.
    - The block value panel: `value_panel` - permet de voir chaque valeur de bloc en jeu.

    Chaque interface graphique contient des fonctions qui ne sont supportées que par elle-même.

??? question "Que fait le type de bouton `PREVIOUS`|`NEXT` ?"
    Ce bouton est disponible dans detail_panel et value_panel.
    Les types de bouton PREVIOUS et NEXT permettent de créer une pagination automatique, quand vous avez plus de blocs que d'espaces dans l'interface graphique.
    Ces types ont des paramètres supplémentaires sous data:

    - `indexing` - indique si le bouton affichera le numéro de page.

      Exemple:
      ```yaml
          icon: tipped_arrow[potion_contents={custom_color:11546150}]
          title: level.gui.buttons.previous.name
          description: level.gui.buttons.previous.description
          data:
            type: PREVIOUS
            indexing: true
          action:
            left:
              tooltip: level.gui.tips.click-to-previous
      ```

??? question "Que fait le type de bouton `TOP` ?"
    Ce bouton est disponible dans top_panel. Il montre l'île au top X par niveau d'île.

    L'`icon` par défaut sera `PLAYER_HEAD` avec une skin de joueur appropriée. L'activer remplacera celui-ci par le matériau spécifié.

    L'`index` dans le champ data permet de spécifier quelle place du Top 10 doit être affichée à l'endroit actuel.

    Le panel top a 2 actions implémentées qui nécessitent un module supplémentaire :

    - `warp` - nécessite le module Warps. Sera affiché seulement si un panneau de warp existe sur l'île du joueur.
    - `visit` - nécessite le module Visit. Sera affiché seulement si la visite est autorisée sur l'île du joueur.

    Fallback permet de changer l'icône de fond, quand il n'y a pas de joueur au top spot.

    Exemple:
    ```yaml
        #icon: PLAYER_HEAD
        title: level.gui.buttons.island.name
        description: level.gui.buttons.island.description
        data:
          type: TOP
          index: 1
        actions:
          warp:
            click-type: LEFT
            tooltip: level.gui.tips.click-to-warp
          visit:
            click-type: RIGHT
            tooltip: level.gui.tips.right-click-to-visit
        fallback:
          icon: LIME_STAINED_GLASS_PANE
          title: level.gui.buttons.island.empty
    ```

??? question "Que fait le type de bouton `VIEW` ?"
    Ce bouton est disponible dans top_panel. Il montre le niveau de l'île du spectateur.

    L'`icon` par défaut sera `PLAYER_HEAD` avec une skin de joueur appropriée. L'activer remplacera celui-ci par le matériau spécifié.

    L'action `view` permet de voir un menu détaillé de l'île du joueur.

    Exemple:
    ```yaml
        #icon: PLAYER_HEAD
        title: level.gui.buttons.island.name
        description: level.gui.buttons.island.description
        data:
          type: VIEW
        actions:
          view:
            click-type: unknown
            tooltip: level.gui.tips.click-to-view
    ```

??? question "Que fait le type de bouton `BLOCK` ?"
    Ce bouton est disponible dans detail_panel et value_panel. Ce bouton montre le matériau donné comme icône.

    Exemple:
    ```yaml
      #icon: STONE
      title: level.gui.buttons.value.name
      description: level.gui.buttons.value.description
      data:
        type: BLOCK
    ```

## Commandes

!!! tip
    `[player_command]` et `[admin_command]` sont des commandes qui diffèrent selon le gamemode que vous exécutez.
    Le fichier `config.yml` des Gamemodes contient des options qui vous permettent de modifier ces valeurs.
    Par exemple, sur BSkyBlock, la `[player_command]` par défaut est `island`, et la `[admin_command]` par défaut est `bsbadmin`.

=== "Commandes joueur"
    - `/[player_command] top`: accédez au panel top. Nécessite la permission `[gamemode].island.top`.
    - `/[player_command] level`: déclenche le calcul du niveau pour le joueur. Nécessite la permission `[gamemode].island.level`.
    - `/[player_command] value [material]`: permet de vérifier la valeur du bloc. Nécessite la permission `[gamemode].island.value`.


=== "Commandes admin"
    - `/[admin_command] level <player>`: déclenche le calcul du niveau pour le joueur. Nécessite la permission `[gamemode].admin.level`.
    - `/[admin_command] levelstatus`: affiche combien d'îles sont dans la file d'attente. Nécessite la permission `[gamemode].admin.levelstatus`.
    - `/[admin_command] sethandicap <player> <number>`: permet de définir le numéro initial du niveau de l'île. Nécessite la permission `[gamemode].admin.level.sethandicap`.
    - `/[admin_command] top`: affiche les 10 meilleures îles dans le chat. Nécessite la permission `[gamemode].admin.top`.
    - `/[admin_command] top remove <player>`: permet de retirer un joueur du top. Nécessite la permission `[gamemode].admin.top.remove`.


## Permissions

!!! tip
    `[gamemode]` est un préfixe qui diffère selon le gamemode que vous exécutez.
    Le préfixe est le nom en minuscules du gamemode, c.-à-d. si vous utilisez BSkyBlock, le préfixe est `bskyblock`.
    De même, si vous utilisez AcidIsland, le préfixe est `acidisland`.

=== "Permissions joueur"
    - `[gamemode].intopten` - (défaut : `true`) - Permet au joueur d'être dans le panel top 10.
    - `[gamemode].island.level` - (défaut : `true`) - Permet au joueur d'utiliser la commande `/[player_command] level`.
    - `[gamemode].island.top` - (défaut : `true`) - Permet au joueur d'utiliser la commande `/[player_command] top`.
    - `[gamemode].island.value` - (défaut : `true`) - Permet au joueur d'utiliser la commande `/[player_command] value`.
    - `[gamemode].island.level.details.blocks` - (défaut : `true`) - Permet au joueur de voir une liste détaillée des blocs pour l'île.
    - `[gamemode].island.level.details.spawners` - (défaut : `false`) - Permet au joueur de voir une liste détaillée des spawners pour l'île.
    - `[gamemode].island.level.details.underwater` - (défaut : `false`) - Permet au joueur de voir une liste détaillée des blocs sous-marins pour l'île.
    - `[gamemode].island.level.details.above-sea-level` - (défaut : `false`) - Permet au joueur de voir une liste détaillée des blocs au-dessus du niveau de la mer pour l'île.

=== "Permissions admin"
    - `[gamemode].admin.level` - (défaut : `op`) - Permet au joueur d'utiliser la commande `/[admin_command] level <player>`.
    - `[gamemode].admin.levelstatus` - (défaut : `op`) - Permet au joueur d'utiliser la commande `/[admin_command] levelstatus`.
    - `[gamemode].admin.level.sethandicap` - (défaut : `op`) - Permet au joueur d'utiliser la commande `/[admin_command] sethandicap <player> <number>`.
    - `[gamemode].admin.top` - (défaut : `op`) - Permet l'accès à la commande `/[admin_command] top`.
    - `[gamemode].admin.top.remove` - (défaut : `op`) - Permet l'accès à la commande `/[admin_command] top remove <player>`.

??? question "Quelque chose manque-t-il ?"
    Vous pouvez trouver la liste complète des permissions dans le fichier [addon.yml](https://github.com/BentoBoxWorld/Level/blob/develop/src/main/resources/addon.yml) de ce module.
    Si quelque chose manque effectivement de la liste ci-dessous, veuillez nous le faire savoir !


## Placeholders

{{ placeholders_source(source="Level") }}

## FAQ

??? question "Pouvez-vous ajouter la fonctionnalité X ?"
    Veuillez l'ajouter à la liste [ici](https://github.com/BentoBoxWorld/Level/issues).

??? question "Comment faire que le `level-cost` augmente après chaque niveau ?"
    Le paramètre `level-cost` est une valeur fixe et ne peut pas être configuré pour augmenter de manière itérative niveau par niveau, car BentoBox calcule les niveaux d'île en appliquant une seule formule au nombre total de blocs — et non en itérant niveau par niveau.

    La façon d'obtenir des coûts de niveau croissants est d'utiliser la formule `level-calc`. Par exemple, pour rendre chaque niveau 50 % plus difficile à atteindre que le précédent (c.-à-d. niveau 1 coûte 100 blocs, niveau 2 coûte 150, niveau 3 coûte 225, etc.), la formule est :

    `level-calc: 2.4661 * log(blocks) - (2.4661 * log(level_cost) - 1)`

    où `level_cost` est le nombre de blocs nécessaires pour atteindre le niveau 1.

    Voici le graphique de cette progression :

    ![template](https://user-images.githubusercontent.com/4407265/212771452-edc943fe-c861-4ba1-b581-8ec987e52f94.png){: loading=lazy }

    !!! warning
        Cette formule commence à atteindre une asymptote autour du niveau 25 — atteindre le niveau 26 ou 27 nécessite un nombre extrêmement élevé de blocs, ce qui peut amener la plupart des joueurs à converger vers le même niveau maximum au fil du temps. Tenez-en compte lors du choix de votre courbe de progression.

    **Dériver une formule personnalisée**

    Pour construire une formule adaptée à une courbe de progression spécifique :

    1. Créez un tableau des niveaux cibles et de leurs coûts en blocs correspondants dans un tableur (par ex. Excel ou Google Sheets).
    2. Tracez un graphique X/Y du tableau.
    3. Faites un clic droit sur le graphique et ajoutez une courbe de tendance. Choisissez le type d'approximation (linéaire, logarithmique, exponentielle, etc.) qui correspond le mieux à la courbe, puis activez « Afficher l'équation sur le graphique ».
    4. Dans l'équation obtenue, remplacez `blocks` par `x` et utilisez-la comme valeur de `level-calc`.

    Par exemple, la progression de 50 % ci-dessus a été dérivée de cette manière et donne :

    `level-calc: 2.4661 * log(blocks) - 10.357`

    ![template](https://user-images.githubusercontent.com/4407265/212773894-6f635ed4-f337-4936-b50f-3b616b6bf041.png){: loading=lazy }
    ![template](https://user-images.githubusercontent.com/4407265/212773929-b51ae6b3-5df3-43ae-b35f-bc6fcb42d78f.png){: loading=lazy }



## Translations

{{ translations("Level") }}



## API

Depuis Level 2.7.2 et BentoBox 1.17, d'autres plugins peuvent accéder directement aux données du module Level. Cependant, les demandes d'addon sont toujours une bonne solution pour les plugins qui ne veulent pas utiliser trop de dépendances.

### Maven Dependency
Le module Level fournit une API pour d'autres plugins. Cela couvre Level 2.8.1 et ultérieure.

!!! note
    Ajoutez la dépendance Level à votre POM.xml Maven :

    ```xml
        <repositories>
            <repository>
                <id>codemc-repo</id>
                <url>https://repo.codemc.io/repository/bentoboxworld/</url>
            </repository>
        </repositories>

        <dependencies>
            <dependency>
                <groupId>world.bentobox</groupId>
                <artifactId>level</artifactId>
                <version>2.8.1</version>
                <scope>provided</scope>
            </dependency>
        </dependencies>
    ```
Utilisez la dernière version du module Level.

Ensuite, vous pouvez obtenir le niveau pour un joueur en demandant au module Level une fois que vous avez le monde dans lequel l'île se trouve et en confirmant que le joueur est le propriétaire d'une île dans ce monde.

Les JavaDocs pour Level peuvent être trouvés [ici](https://ci.codemc.io/job/BentoBoxWorld/job/Level/ws/target/apidocs/index.html).

### Events

=== "IslandLevelCalculatedEvent"
    !!! summary "Description"
        Événement déclenché quand le niveau du joueur est calculé.

        Lien vers la classe : [IslandLevelCalculatedEvent](https://github.com/BentoBoxWorld/Level/blob/develop/src/main/java/world/bentobox/level/events/IslandLevelCalculatedEvent.java)

    !!! question "Variables"
        - `Island island` - l'objet île.
        - `UUID targetPlayer` - id du joueur qui a calculé le niveau.
        - `Results results` - les résultats de l'île calculés.

    !!! example "Code example"
        ```java
        @EventHandler(priority = EventPriority.MONITOR)
        public void onLevelCalculated(IslandLevelCalculatedEvent event) {
            UUID user = event.getTargetPlayer();
            Island island = event.getIsland();
            Results results = event.getResults();

            // death handicap from results.
            int deathHandicap = event.getDeathHandicap();

            // the island initial level from results.
            long initialLevel = event.getInitialLevel();

            // the island level from results.
            long level = event.getLevel();

            // this will overwrite island level to 100.
            event.setLevel(100);

            // number of points required to next level
            long pointsToNextLevel = event.getPointsToNextLevel();

            // the report text from results.
            List<String> report = event.getReport();
        }
        ```

=== "IslandPreLevelEvent "
    !!! summary "Description"
        Événement déclenché avant que le niveau du joueur soit calculé.

        Lien vers la classe : [IslandPreLevelEvent](https://github.com/BentoBoxWorld/Level/blob/develop/src/main/java/world/bentobox/level/events/IslandPreLevelEvent.java)

    !!! question "Variables"
        - `Island island` - l'objet île.
        - `UUID targetPlayer` - id du joueur qui a calculé le niveau.

    !!! example "Code example"
        ```java
        @EventHandler(priority = EventPriority.LOW)
        public void beforeLevelCalculated(IslandPreLevelEvent event) {
            UUID user = event.getTargetPlayer();
            Island island = event.getIsland();
        }
        ```

### Addon Request Handlers

***Cette API n'est plus nécessaire*** car le module Level est maintenant chargé en tant que plugin Bukkit, donc ses méthodes peuvent être accédées directement. Les JavaDocs pour Level peuvent être trouvés [ici](https://ci.codemc.io/job/BentoBoxWorld/job/Level/ws/target/apidocs/index.html). Si vous voulez le niveau d'un joueur par exemple, vous pouvez l'obtenir directement à partir des méthodes de la classe LevelsManager. Cependant, cette documentation est conservée pour des raisons de compatibilité descendante.

Plus d'informations sur les handlers de demande d'addon peuvent être trouvées [ici](/en/latest/BentoBox/Request-Handler-API---How-plugins-can-get-data-from-addons/)

=== "island-level"
    !!! summary "Description"
        Retourne le niveau de l'île de ce joueur dans le monde donné.

    !!! question "Input"
        - `world-name`: String - le nom du monde.
        - `player`: UUID - l'UUID du joueur.

    !!! success "Output"
        Le niveau de l'île du joueur ou `0L` si l'entrée n'était pas valide ou si ce joueur n'a pas d'île dans ce monde.

    !!! failure
        Ce handler retournera `0L` si le `world-name` n'a pas été fourni ou si le `world-name` n'existe pas ou n'est pas un monde gamemode.

    !!! example "Code example"
        ```java
            /**
             * Returns the level of this player's island in the given world.
             * @param playerUUID UUID of the player, not null.
             * @param worldName Name of the world (Overworld) the island is in, not null.
             * @return the player's island level or {@code 0L} if the input was invalid or
             *         if this player does not have an island in this world.
             */
            public long getIslandLevel(UUID playerUUID, String worldName) {
                return (Long) new AddonRequestBuilder()
                    .addon("Level")
                    .label("island-level")
                    .addMetaData("world-name", worldName)
                    .addMetaData("player", playerUUID)
                    .request();
            }
        ```

=== "top-ten-level"
    !!! summary "Description"
        Retourne les joueurs dont l'île qu'ils possèdent est dans le Top 10 mappés au niveau de leur île.

    !!! question "Input"
        - `world-name`: String - le nom du monde.

    !!! success "Output"
        `Map<UUID, Long>` contenant les UUID des propriétaires d'îles dont l'île est dans le Top 10, mappés au niveau de leur île.

    !!! failure
        Ce handler retournera une carte vide si le `world-name` n'a pas été fourni ou si le `world-name` n'existe pas ou n'est pas un monde gamemode.

    !!! example "Code example"
        ```java
            /**
             * Returns the players whose island they own is in the Top 10 mapped to the level of their island.
             * @param worldName Name of the world (Overworld) the island is in, not null.
             * @return a Map containing the UUIDs of the island owners whose island is in the Top 10, mapped to the level of their island,
             *         or an empty map if the specified world doesn't exist or doesn't contain islands.
             */
            public Map<UUID, Long> getTopTen(String worldName) {
                return (Map<UUID, Long>) new AddonRequestBuilder()
                    .addon("Level")
                    .label("top-ten-level")
                    .addMetaData("world-name", worldName)
                    .request();
            }
        ```
