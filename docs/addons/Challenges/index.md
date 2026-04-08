# Challenges

**Challenges** permet à vos joueurs de **compléter divers défis personnalisables et de recevoir des récompenses** !

Créé et maintenu par [BONNe](https://github.com/BONNe).

{{ addon_description("Challenges") }}

## Installation

1. Placez le fichier jar du module dans le dossier addons du plugin BentoBox
2. Redémarrez le serveur
3. Exécutez la commande challenges admin, par exemple `/bsbadmin challenges` pour configurer le module

## Configuration

Par défaut, le module challenges ne contient aucun défi ni niveau. À la première exécution, seule l'interface graphique Admin sera accessible.
Les administrateurs peuvent créer leurs propres défis ou charger un ensemble de défis par défaut. Les défis par défaut contiennent 5 niveaux et 57 défis.
Il existe également une bibliothèque Web où les administrateurs peuvent télécharger des défis publics. Elle est accessible via l'interface graphique Admin en cliquant sur l'icône Web.

### config.yml

Le fichier de configuration contient les fonctions principales du module.

Le dernier config.yml se trouve [ici](https://github.com/BentoBoxWorld/Challenges/blob/develop/src/main/resources/config.yml).

### Template

Le module challenges contient un fichier template qui peut être utilisé pour importer des défis dans la base de données. Ce fichier est utile pour ajouter en masse des défis pour ceux qui n'aiment pas utiliser l'interface graphique en jeu. Cependant, soyez conscient que toutes les fonctions ne sont pas disponibles pour le fichier template, et certains éléments/options ne peuvent être ajoutés que via l'interface graphique.
Vous pouvez avoir autant de fichiers template que vous le souhaitez. L'interface graphique Admin vous permettra de choisir lequel vous voulez importer.
Le fichier template d'exemple : [template.yml](https://github.com/BentoBoxWorld/Challenges/blob/develop/src/main/resources/template.yml)

!!! tip
    Le fichier template doit contenir à la fois : défis et niveaux. Sans eux, il ne fonctionnera pas.

??? question "Quel est le type de défi ?"
    Le module challenges a 4 types différents de défis. Chaque type offre différentes choses à tester pour que le défi soit marqué comme complété. Ces types sont :

    - Inventory Challenge (`INVENTORY_TYPE`) - défi qui nécessite des éléments dans l'inventaire du joueur pour être complété.
    - Island Challenge (`ISLAND_TYPE`) - défi qui nécessite des blocs ou des entités sur l'île du joueur pour être complété.
    - Other Challenge (`OTHER_TYPE`) - défi qui nécessite l'XP du joueur, l'argent ou le niveau de l'île pour être complété.
    - Statistic Challenge (`STATISTIC_TYPE`) - défi qui nécessite une certaine valeur de la statistique du joueur pour être complété.

??? question "Puis-je spécifier un enchantement sur les éléments requis/récompensés ?"
    Malheureusement, Spigot n'a pas de mécanique d'analyse d'éléments générale. Les auteurs de plugins doivent créer la leur. Le module challenges utilise le [Item Parser](/en/latest/BentoBox/ItemParser/) de BentoBox. Si la fonction n'est pas supportée par celui-ci, alors vous ne pouvez pas. Cependant, vous pouvez toujours utiliser l'interface graphique admin en jeu pour définir les éléments que vous voulez. Il n'y a pas de limitation.

??? question "Comment puis-je savoir quelles valeurs je peux mettre dans le type de défi statistique ?"
    Le type de statistique que vous pouvez trouver ici : [Statistic](https://hub.spigotmc.org/javadocs/spigot/org/bukkit/Statistic.html).

    Certaines informations peuvent être trouvées sur le site fandom : [minecraft.fandom](https://minecraft.fandom.com/wiki/Statistics)

    Cependant, il n'y a pas d'endroit où vous pouvez découvrir ce que vous pouvez spécifier. Je recommanderais d'utiliser l'interface graphique admin en jeu pour créer des défis de statistique, car elle offre plus d'options pour détecter quels champs peuvent être remplis.

### Interface graphique personnalisable

L'API BentoBox 1.17 a introduit une fonction qui permet d'implémenter des interfaces graphiques personnalisables. Le module challenges est l'un des premiers à utiliser cette fonctionnalité. Nous avons essayé d'être aussi simple que possible pour la personnalisation, cependant, certaines fonctionnalités nécessitent une explication.
Vous pouvez trouver plus d'informations sur le fonctionnement des interfaces graphiques personnalisées de BentoBox ici : [Custom GUI's](/en/latest/Tutorials/generic/Customizable-GUI/)

??? question "Comment puis-je personnaliser les interfaces graphiques ?"
    Pour personnaliser les interfaces graphiques du module Challenges, vous devez avoir la version 1.0. C'est la première version qui les a implémentées. Le module créera un nouveau répertoire sous `/plugins/bentobox/addons/challenges` nommé `panels`

    Actuellement, vous pouvez personnaliser 3 interfaces graphiques :

    - Main Challenges Panel: `main_panel` - panel qui s'ouvre quand le joueur peut voir la liste des défis.
    - Multiple Completion Panel: `multiple_panel` - panel qui s'ouvre quand le joueur veut spécifier le nombre de fois que le défi doit être complété.
    - Gamemode Selection Panel: `gamemode_panel` - panel qui s'ouvre quand `commands.global-command` est activé dans les paramètres et qu'il y a plusieurs gamemodes installés.

    Chaque interface graphique contient des fonctions qui ne sont supportées que par elle-même.

??? question "Que fait le type de bouton `PREVIOUS`|`NEXT` ?"
    Ce bouton est disponible dans main_panel et gamemode_panel.
    Les types de bouton PREVIOUS et NEXT permettent de créer une pagination automatique, quand vous avez plus de défis que d'espaces dans l'interface graphique.
    Ces types ont des paramètres supplémentaires sous data:
    - `target` - indique si le bouton basculera `LEVEL` ou `CHALLENGE` dans main_panel et `GAMEMODE` dans gamemode_panel.
    - `indexing` - indique si le bouton affichera le numéro de page.

    Exemple:
    ```yaml
        icon: tipped_arrow[potion_contents={custom_color:11546150}]
        title: challenges.gui.buttons.previous.name
        description: challenges.gui.buttons.previous.description
        data:
          type: PREVIOUS
          target: CHALLENGE
          indexing: true
        action:
          left:
            tooltip: challenges.gui.tips.click-to-previous
    ```

??? question "Que fait le type de bouton `CHALLENGE` ?"
    Ce bouton est disponible dans main_panel.
    Le bouton CHALLENGE crée une entrée dynamique pour un défi. Le bouton ne sera rempli que s'il existe un défi. Par exemple, si vous avez seulement 3 défis, mais que vous avez défini 7 emplacements pour les défis dans l'interface graphique, alors seulement 3 emplacements seront remplis. Les autres emplacements resteront vides.

    Par défaut, les défis seront ordonnés par leurs numéros d'ordre, cependant, vous pouvez spécifier un défi spécifique pour être dans un emplacement spécifique avec le paramètre `id` sous data.

    ```yaml
      data:
        type: CHALLENGE
        id: example_challenge
    ```

    Spécifier le titre, la description et l'icône remplacera la génération dynamique basée sur les données de la base de données. Par défaut, ces valeurs seront générées à partir des entrées de la base de données.
    Ce bouton supporte 3 types d'action différents :

    - COMPLETE - complète simplement un défi une fois.
    - COMPLETE_MAX - complète un défi autant que possible.
    - MULTIPLE_PANEL - ouvre le panel de complétion multiple qui permet de sélectionner combien de fois le défi doit être complété.

    Exemple:
    ```yaml
      data:
        type: CHALLENGE
      actions:
        left:
          type: COMPLETE
          tooltip: challenges.gui.tips.click-to-complete
        right:
          type: MULTIPLE_PANEL
          tooltip: challenges.gui.tips.right-click-multiple-open
        shift_left:
          type: COMPLETE_MAX
          tooltip: challenges.gui.tips.shift-left-click-to-complete-all
    ```


??? question "Que fait le type de bouton `LEVEL` ?"
    Ce bouton est disponible dans main_panel.
    Le bouton LEVEL crée une entrée dynamique pour un niveau de défi. Le bouton ne sera rempli que s'il existe un niveau. Par exemple, si vous avez seulement 3 niveaux, mais que vous avez défini 7 emplacements pour les niveaux dans l'interface graphique, alors seulement 3 emplacements seront remplis. Les autres emplacements resteront vides.

    Par défaut, les niveaux seront ordonnés selon leur progression, cependant, vous pouvez spécifier un niveau spécifique pour être dans un emplacement spécifique avec le paramètre `id` sous data.

    ```yaml
      data:
        type: LEVEL
        id: example_level
    ```

    Spécifier le titre, la description et l'icône remplacera la génération dynamique basée sur les données de la base de données. Par défaut, ces valeurs seront générées à partir des entrées de la base de données.

    Exemple:
    ```yaml
      data:
        type: LEVEL
      actions:
        left:
          tooltip: challenges.gui.tips.click-to-select
    ```

??? question "Que fait le type de bouton `UNASSIGNED_CHALLENGES` ?"
    Ce bouton est disponible dans main_panel.
    Le bouton UNASSIGNED_CHALLENGES permet de sélectionner un bouton pour les défis gratuits.
    Il n'a pas de fonctions supplémentaires ou de générations dynamiques.

??? question "Que fait le type de bouton `GAMEMODE` ?"
    Ce bouton est disponible dans gamemode_panel
    Il génère un bouton pour chaque module GameMode qui a Challenges installé.

??? question "Que fait le type de bouton `INCREASE`|`REDUCE` ?"
    Ce bouton est disponible dans multiple_panel.
    Ces types permettent d'augmenter/réduire le nombre de complétion de défi.

    Spécifier `value: <number>` sous `data` permet de définir un nombre d'incrément/décrement personnalisé différent.

??? question "Que fait le type de bouton `ACCEPT` ?"
    Ce bouton est disponible dans multiple_panel.
    Ce type permet d'accepter le numéro d'entrée et de compléter le défi ce nombre de fois.

    Spécifier `type: ACCEPT` sous action permet de compléter le défi.
    Spécifier `type: INPUT` sous action permet de demander au joueur d'écrire un numéro dans le chat.

## Commandes

!!! tip
    `[player_command]` et `[admin_command]` sont des commandes qui diffèrent selon le gamemode que vous exécutez.
    Le fichier `config.yml` des Gamemodes contient des options qui vous permettent de modifier ces valeurs.
    Par exemple, sur BSkyBlock, la `[player_command]` par défaut est `island`, et la `[admin_command]` par défaut est `bsbadmin`.

=== "Commandes joueur"
    - `/challenges`: Accédez à l'interface graphique Player Challenges. Contient soit les défis du monde actuel, soit une liste de mondes où les défis sont activés. Ceci doit être activé dans la configuration.
    - `/[player_command] challenges [challenge] [number]`: Accédez à l'interface graphique Player Challenges de BSkyBlock. Si le nom du défi est fourni, cette méthode complétera ce défi une fois. Si un nombre est fourni, il complétera le défi de 0 à plusieurs fois.

=== "Commandes admin"
    - `/challengesadmin`: Accédez à l'interface graphique Admin Challenges. Contient une liste des mondes où les défis sont activés. Ceci doit être activé dans la configuration.
    - `/[admin_command] challenges`: Accédez à l'interface graphique Admin Challenges de BSkyBlock
    - `/[admin_command] challenges reload [hard]`: Capacité à recharger la configuration du module Challenges. Cette méthode efface également les données en cache. Le paramètre hard permet de réinitialiser la connexion à la base de données.

## Permissions

!!! tip
    `[gamemode]` est un préfixe qui diffère selon le gamemode que vous exécutez.
    Le préfixe est le nom en minuscules du gamemode, c.-à-d. si vous utilisez BSkyBlock, le préfixe est `bskyblock`.
    De même, si vous utilisez AcidIsland, le préfixe est `acidisland`.

=== "Permissions joueur"
    - `[gamemode].challenges` - (défaut : `true`) - Permet au joueur d'utiliser la commande '/[player_command] challenges'.
    - `[gamemode].challenges.multiple` - (défaut : `true`) - Permet au joueur de compléter un défi plusieurs fois à la fois.
    - `[gamemode].challenges.complete` - (défaut : `false`) - Permet au joueur d'utiliser la commande '/[player_command] challenges complete <challenge> <number>'.
    - `addon.challenges` - (défaut : `true`) - Permet l'accès à la commande '/challenges' si elle est activée dans la config.
    - `[gamemode].command.challengeexempt` - (défaut : `false`) - Permet de bloquer l'exécution de la commande de récompense pour le joueur.

=== "Permissions admin"
    - `[gamemode].admin.challenges` - (défaut : `op`) - Permet au joueur d'utiliser la commande '/[admin_command] challenges'.
    - `[gamemode].admin.challenges.complete` - (défaut : `op`) - Permet au joueur d'utiliser la commande '/[admin_command] challenges complete'.
    - `[gamemode].admin.challenges.reset` - (défaut : `op`) - Permet au joueur d'utiliser la commande '/[admin_command] challenges reset'.
    - `addon.admin.challenges` - (défaut : `op`) - Permet l'accès à la commande '/challengesadmin' si elle est activée dans la config.

??? question "Quelque chose manque-t-il ?"
    Vous pouvez trouver la liste complète des permissions dans le fichier [addon.yml](https://github.com/BentoBoxWorld/Challenges/blob/develop/src/main/resources/addon.yml) de ce module.
    Si quelque chose manque effectivement de la liste ci-dessous, veuillez nous le faire savoir !


## Placeholders

{{ placeholders_source(source="Challenges") }}

## FAQ

??? question "Pouvez-vous ajouter la fonctionnalité X ?"
    Veuillez l'ajouter à la liste [ici](https://github.com/BentoBoxWorld/Challenges/issues).

??? question "Comment puis-je ajouter un nouveau défi ?"
    La manière officielle est d'ajouter un défi via l'interface graphique Admin ou le fichier Template.
    Soyez conscient que le fichier template n'est importé qu'après utilisation de l'icône appropriée dans l'interface graphique Admin ("Import Template"). L'interface graphique vous permettra de choisir quel template vous voulez importer dans le gamemode.

    Cependant, il existe une option pour éditer le fichier de base de données exporté. Cela peut être fait en exportant vers un fichier via : `/[admin_command] challenges` et en cliquant sur le bouton "Export Database".

??? question "Puis-je activer les défis par île ? Donc tous les membres de l'île ont les mêmes défis ?"
    Oui, vous pouvez le faire via le fichier de configuration du module : `store-island-data: true`

??? question "Puis-je activer les défis par joueur ?"
    Oui, vous pouvez le faire via le fichier de configuration du module : `store-island-data: false`

??? question "Les commandes de récompense ne fonctionnent pas. Pourquoi ?"
    Très probablement, les commandes de récompense ne fonctionnent pas en raison d'une définition incorrecte. La commande ne nécessite pas de symbole `/` avant elle.

    Si vous voulez appeler une commande du point de vue du joueur, vous devez ajouter `[SELF]` avant l'appel de commande, par ex. `[SELF] kill` entraînera l'appel de la commande `/kill` par le joueur.

    Cela pourrait également être causé par les permissions. `[gamemode].command.challengeexempt` empêchera le joueur d'exécuter les commandes. Vérifiez que le joueur n'a pas cette permission.

??? question "Comment ajouter des placeholders dans les commandes de récompense ?"
    Actuellement, le module ne supporte pas les placeholders dans les commandes de récompense. Si c'est nécessaire, vous pouvez les demander sur gitHub.

    Le seul placeholder actuellement supporté dans les commandes de récompense est `[player]` qui retourne le nom du joueur qui a complété le défi.

??? question "Je n'aime pas l'ordre des éléments dans la description du défi. Puis-je le changer ?"
    Oui, l'ordre des éléments est défini dans le fichier de locale du module.

    [Challenge Description](https://github.com/BentoBoxWorld/Challenges/blob/develop/src/main/resources/locales/en-US.yml#L852-L994)
    [Level Description](https://github.com/BentoBoxWorld/Challenges/blob/develop/src/main/resources/locales/en-US.yml#L995-L1042)

    L'échange ou la suppression de parties de lore changera l'ordre des éléments affichés dans celui-ci.

    ```yaml
        lore: |-
            [description]
            [status]
            [cooldown]
            [requirements]
            [rewards]
    ```

    Chacune de ces parties est générée par les balises ci-dessous, et vous pouvez les changer aussi. Par ex. la partie [status] est générée à partir de :

    ```yaml
    status:
        # Status message for completed unrepeatable challenge
        completed: "&2&l Completed"
        # Status message that contains number of completions for unlimited repeatable challenge
        completed-times: "&2 Completed &7&l [number] &r&2 time(-s)"
        # Status message that contains number of completions from max available for repeatable challenge
        completed-times-of: "&2 Completed &7&l [number] &r&2 out of &7&l [max] &r&2 times"
        # Status message that indicates that max completion count reached for repeatable challenge
        completed-times-reached: "&2&l Completed all &7 [max] &2 times"
    ```

## Translations

!!! info "Translations for challenges"
    Les traductions ne couvrent pas les défis.
    Chaque défi a son propre "display name" et "description" qui ne sont pas localisés pour garder le processus de configuration aussi simple que possible pour l'utilisateur final.
    Vous pouvez cependant trouver ou fournir des traductions pour divers défis sur notre [Challenges Library en ligne](https://github.com/BentoBoxWorld/weblink/tree/master/challenges/library) sur GitHub.

    Il existe également une option pour traduire des parties via le fichier [locales](https://github.com/BentoBoxWorld/Challenges/blob/develop/src/main/resources/locales/en-US.yml#L1248-L1270)

{{ translations("Challenges") }}

## API

Depuis Challenges 1.0 et BentoBox 1.17, d'autres plugins peuvent accéder directement aux données du module Challenges. Cependant, les demandes d'addon sont toujours une bonne solution pour les plugins qui ne veulent pas utiliser trop de dépendances.

### Maven Dependency

Challenges fournit une API pour d'autres plugins. Cela couvre la version 1.1.0 et ultérieure.

!!! note
    Ajoutez la dépendance Challenges à votre POM.xml Maven :

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
                <artifactId>challenges</artifactId>
                <version>1.1.0</version>
                <scope>provided</scope>
            </dependency>
        </dependencies>
    ```

Utilisez la dernière version de Challenges.

Les JavaDocs pour Challenges peuvent être trouvés [ici](https://ci.codemc.io/job/BentoBoxWorld/job/Challenges/ws/target/apidocs/index.html).

### Events

Depuis l'API BentoBox 1.17 a implémenté une fonctionnalité qui a résolu un problème avec les class loaders. Les plugins qui veulent utiliser les événements directement peuvent maintenant le faire.

=== "ChallengeCompletedEvent"
    !!! summary "Description"
        Événement déclenché quand un joueur complète un défi.

        L'événement est informatif uniquement. Ne peut pas être annulé.

        Lien vers la classe : [ChallengeCompletedEvent](https://github.com/BentoBoxWorld/Challenges/blob/develop/src/main/java/world/bentobox/challenges/events/ChallengeCompletedEvent.java)


    !!! question "Variables"
        - `String challengeId` - id du défi qui a été complété.
        - `UUID user` - id du joueur qui a complété le défi.
        - `Boolean admin` - indique si le défi a été complété par un admin.
        - `Integer completionCount` - nombre de fois que le défi a été complété.

    !!! example "Code example"
        ```java
        @EventHandler(priority = EventPriority.MONITOR)
        public void onLevelCompletion(ChallengeCompletedEvent event) {
            UUID user = event.getPlayerUUID();
            String challenge = event.getChallengeID();
            boolean isAdmin = event.isAdmin();
            int count = event.getCompletionCount();
        }
        ```

=== "LevelCompletedEvent"
    !!! summary "Description"
        Événement déclenché quand un joueur complète un niveau.

        L'événement est informatif uniquement. Ne peut pas être annulé.

        Lien vers la classe : [LevelCompletedEvent](https://github.com/BentoBoxWorld/Challenges/blob/develop/src/main/java/world/bentobox/challenges/events/LevelCompletedEvent.java)


    !!! question "Variables"
        - `String levelId` - id du niveau qui a été complété.
        - `UUID user` - id du joueur qui a complété le niveau.
        - `Boolean admin` - indique si le niveau a été complété par un admin.

    !!! example "Code example"
        ```java
        @EventHandler(priority = EventPriority.MONITOR)
        public void onLevelCompletion(LevelCompletedEvent event) {
            UUID user = event.getPlayerUUID();
            String levelId = event.getLevelID();
            boolean isAdmin = event.isAdmin();
        }
        ```

=== "ChallengeResetAllEvent"
    !!! summary "Description"
        Événement déclenché quand tous les défis sont réinitialisés pour un joueur. Il inclut les données de niveau des défis.

        L'événement est informatif uniquement. Ne peut pas être annulé.

        Lien vers la classe : [ChallengeResetAllEvent](https://github.com/BentoBoxWorld/Challenges/blob/develop/src/main/java/world/bentobox/challenges/events/ChallengeResetAllEvent.java)

    !!! question "Variables"
        - `String worldName` - nom du monde où les défis ont été réinitialisés.
        - `UUID playerUUID` - id du joueur qui a été ciblé.
        - `Boolean admin` - indique si la réinitialisation a été faite par un admin.
        - `String reason` - contient la raison de la réinitialisation.

    !!! warning "Constant Values"
        - `reason` - est défini à "ISLAND_RESET" si effectué par le joueur ou "RESET_ALL" si effectué par un admin.

    !!! example "Code example"
        ```java
        @EventHandler(priority = EventPriority.MONITOR)
        public void onLevelCompletion(ChallengeResetAllEvent event) {
            UUID user = event.getPlayerUUID();
            String worldName = event.getWorldName();
            boolean isAdmin = event.isAdmin();
            String reason = event.getReason();
        }
        ```

=== "ChallengeResetEvent"
    !!! summary "Description"
        Événement déclenché quand un défi est réinitialisé par un admin.

        L'événement est informatif uniquement. Ne peut pas être annulé.

        Lien vers la classe : [ChallengeResetEvent](https://github.com/BentoBoxWorld/Challenges/blob/develop/src/main/java/world/bentobox/challenges/events/ChallengeResetEvent.java)

    !!! question "Variables"
        - `String challengeID` - id du défi qui a été réinitialisé.
        - `UUID playerUUID` - id du joueur qui a été ciblé.
        - `Boolean admin` - indique si le défi a été réinitialisé par un admin.
        - `String reason` - contient la raison de la réinitialisation.

    !!! warning "Constant Values"
        - `admin` - est défini à true. La réinitialisation non-admin pour un seul défi n'est pas encore implémentée.
        - `reason` - est défini à "RESET".

    !!! example "Code example"
        ```java
        @EventHandler(priority = EventPriority.MONITOR)
        public void onLevelCompletion(ChallengeResetEvent event) {
            UUID user = event.getPlayerUUID();
            String challengeId = event.getChallengeID();
            boolean isAdmin = event.isAdmin();
            String reason = event.getReason();
        }
        ```

### Addon Request Handlers

Jusqu'à BentoBox 1.17, nous avions un problème avec l'accès aux données en dehors de l'environnement BentoBox en raison du class loader que nous utilisions pour charger les addons.
Cela signifiait que les données n'étaient accessibles que depuis d'autres addons. Mais BentoBox a implémenté la fonctionnalité PlAddon, ce qui signifie que les handlers de demande
ne sont plus nécessaires.

Plus d'informations sur les handlers de demande d'addon peuvent être trouvées [ici](/en/latest/BentoBox/Request-Handler-API---How-plugins-can-get-data-from-addons/)

=== "challenge-list"
    !!! summary "Description"
        Retourne une liste de tous les uniqueIds des défis qui sont définis dans un monde donné.

    !!! question "Input"
        - `world-name`: String - le nom du monde.

    !!! success "Output"
        La sortie est une `List<String>` contenant la liste des uniqueIds des défis qui sont définis pour le monde spécifié.

    !!! failure
        Ce handler retournera une liste vide si le `world-name` n'a pas été fourni ou si le `world-name` n'existe pas ou n'est pas un monde gamemode.

    !!! example "Code example"
        ```java
        public List<String> getChallenges(String worldName) {
            return (List<String>) new AddonRequestBuilder()
                .addon("Challenges")
                .label("challenge-list")
                .addMetaData("world-name", worldName)
                .request();
        }
        ```

=== "challenge-data"
    !!! summary "Description"
        Retourne une `Map<String, Object>` contenant toutes les informations sur le défi demandé.

    !!! question "Input"
        - `challenge-name`: String - l'ID unique du défi demandé.

    !!! success "Output"
        La sortie est une `Map<String, Object>` avec les clés suivantes :

        - `uniqueId`: String - l'ID unique du défi demandé.
        - `name`: String - le nom d'affichage du défi.
        - `icon`: ItemStack - l'élément qui représente le défi dans les interfaces graphiques.
        - `levelId`: String - l'uniqueId du niveau auquel le défi demandé est assigné.
        - `order`: Integer - le numéro d'ordre pour le défi donné.
        - `deployed`: Boolean - `true` si le défi est déployé, `false` sinon.
        - `description`: List&lt;String&gt; - la description du défi.
        - `type`: String - le nom du type de défi demandé.
        - `repeatable`: Boolean - `true` si le défi est répétable, `false` sinon.
        - `maxTimes`: Integer - le nombre maximal de complétion pour le défi demandé.

    !!! failure
        Ce handler retournera une carte vide si le `challengeId` n'a pas été fourni ou si le `challengeId` n'a pas pu être trouvé dans la base de données.

    !!! example "Code example"
        ```java
        public Map<String, Object> getChallengeDataMap(String challengeId) {
            return (Map<String, Object>) new AddonRequestBuilder()
                .addon("Challenges")
                .label("challenge-data")
                .addMetaData("challenge-name", challengeId)
                .request();
        }
        ```

=== "level-list"
    !!! summary "Description"
        Retourne une liste de tous les uniqueIds des niveaux qui sont définis dans un monde donné.

    !!! question "Input"
        - `world-name`: String - le nom du monde.

    !!! success "Output"
        La sortie est une `List<String>` contenant la liste des uniqueIds des niveaux qui sont définis pour le monde spécifié.

    !!! failure
        Ce handler retournera une liste vide si le `world-name` n'a pas été fourni ou si le `world-name` n'existe pas ou n'est pas un monde gamemode.

    !!! example "Code example"
        ```java
        public List<String> getChallengeLevels(String worldName) {
            return (List<String>) new AddonRequestBuilder()
                .addon("Challenges")
                .label("level-list")
                .addMetaData("world-name", worldName)
                .request();
        }
        ```

=== "level-data"
    !!! summary "Description"
        Retourne une `Map<String, Object>` contenant toutes les informations sur le niveau demandé.

    !!! question "Input"
        - `level-name`: String - l'ID unique du niveau demandé.

    !!! success "Output"
        La sortie est une `Map<String, Object>` avec les clés suivantes :

        - `uniqueId`: String - l'ID unique du niveau demandé.
        - `name`: String - le nom d'affichage du niveau.
        - `icon`: ItemStack - l'élément qui représente le niveau dans les interfaces graphiques.
        - `world`: String - le nom du monde où le niveau opère.
        - `order`: Integer - le numéro d'ordre pour le niveau donné.
        - `message`: String - le message de déverrouillage pour le niveau donné.
        - `waiveramount`: Integer - le nombre de défis qui peuvent rester non complétés, avant déverrouillage.
        - `challenges`: List&lt;String&gt; - la liste des ids des défis assignés.

    !!! failure
        Ce handler retournera une carte vide si le `levelId` n'a pas été fourni ou si le `levelId` n'a pas pu être trouvé dans la base de données.

    !!! example "Code example"
        ```java
        public Map<String, Object> getChallengeLevelData(String levelId) {
            return (Map<String, Object>) new AddonRequestBuilder()
                .addon("Challenges")
                .label("level-data")
                .addMetaData("level-name", levelId)
                .request();
        }
        ```

=== "completed-challenges"
    !!! summary "Description"
        Retourne une liste des uniqueIds des défis complétés qui sont définis dans un monde donné et complétés par un joueur donné.

    !!! question "Input"
        - `player`: UUID - l'UUID du joueur.
        - `world-name`: String - le nom du monde.

    !!! success "Output"
        La sortie est un `Set<String>` contenant l'ensemble des uniqueIds des défis qui sont complétés par le joueur pour le monde spécifié.

    !!! failure
        Ce handler retournera un ensemble vide si le `world-name` n'a pas été fourni ou si le `world-name` n'existe pas ou n'est pas un monde gamemode.
        Ce handler retournera un ensemble vide si le `player` n'a pas été fourni ou si le `player` n'existe pas.

    !!! example "Code example"
        ```java
        public List<String> getCompletedChallenges(UUID playerUUID, String worldName) {
            return (List<String>) new AddonRequestBuilder()
                .addon("Challenges")
                .label("completed-challenges")
                .addMetaData("player", playerUUID)
                .addMetaData("world-name", worldName)
                .request();
        }
        ```
