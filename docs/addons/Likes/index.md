# Likes

**Likes** permet aux joueurs d'évaluer les autres îles avec des j'aime, des dislikes ou des étoiles.

Créé et maintenu par [BONNe](https://github.com/BONNe).

{{ addon_description("Likes") }}

## Installation

0. Installez BentoBox et exécutez-le sur le serveur au moins une fois pour créer ses dossiers de données.
1. Placez ce fichier jar dans le dossier des addons du plugin BentoBox.
2. Redémarrez le serveur.
3. L'addon créera un dossier de données et à l'intérieur du dossier se trouvera un config.yml.
4. Arrêtez le serveur.
5. Modifiez config.yml comme vous le souhaitez.
7. Redémarrez le serveur.

## Configuration

Le fichier `config.yml` principal contient les informations de base sur la configuration du addon du mode de jeu.

`panels` permet de personnaliser certains panneaux accessibles aux utilisateurs.


### config.yml

Une fois l'addon correctement installé, il créera un fichier config.yml. Chaque option dans ce fichier est accompagnée de commentaires. Veuillez vérifier le fichier pour plus d'informations.
Vous pouvez trouver le dernier fichier config : [config.yml](https://github.com/BentoBoxWorld/Likes/blob/develop/src/main/resources/config.yml)

Certaines options de configuration peuvent être modifiées via l'interface graphique d'administration en jeu. Cependant, certaines options ne peuvent pas l'être.

L'option de configuration la plus importante est le mode :

!!! summary "Mode Likes"
    mode: permet de changer le mode de fonctionnement du addon

    - LIKES - Permet d'ajouter uniquement Like à l'île.
    - LIKES_DISLIKES - Permet d'ajouter uniquement Like et Dislikes à l'île.
    - STARS - Permet d'ajouter des Stars à l'île.

Vous ne pouvez utiliser qu'un seul mode à la fois.

### Interfaces graphiques personnalisables

BentoBox 1.17 API a introduit une fonction qui permet de mettre en œuvre des interfaces graphiques personnalisables. Cet addon est l'un des premiers à utiliser cette fonctionnalité. Nous avons essayé d'être aussi simples que possible pour la personnalisation, cependant, certaines fonctionnalités nécessitent une explication.
Vous pouvez trouver plus d'informations sur le fonctionnement des interfaces graphiques personnalisées de BentoBox ici : [Interfaces graphiques personnalisées](/en/latest/Tutorials/generic/Customizable-GUI/)

??? question "Comment puis-je personnaliser les interfaces graphiques"
    Pour personnaliser les interfaces graphiques d'addon, vous devez avoir la version 2.2. C'est la première version qui les a implémentées. L'addon créera un nouveau répertoire sous `/plugins/BentoBox/addons/Likes` portant le nom `panels`

    Actuellement, vous pouvez personnaliser 3 interfaces graphiques :

    - Panneau d'affichage : `view_panels` - panneau qui permet de voir qui a aimé l'île du joueur.
    - Panneau supérieur : `top_panel` - panneau qui contient les meilleures îles par certaine valeur.
    - Panneau de gestion : `manage_panels` - panneau qui permet d'ajouter j'aime/dislike ou des étoiles.

    Les panneaux View et Manage contiennent 3 panneaux différents pour chaque mode.


## Commandes

!!! tip
    `[player_command]` et `[admin_command]` sont des commandes qui diffèrent selon le mode de jeu que vous exécutez.
    Le fichier `config.yml` des modes de jeu contient des options qui vous permettent de modifier ces valeurs.
    Par exemple, sur BSkyBlock, la `[player_command]` par défaut est `island`, et la `[admin_command]` par défaut est `bsbadmin`.

=== "Commandes du joueur"
    - `/[player_command] likes`: ouvre l'interface graphique pour ajouter / supprimer des j'aime, dislikes ou des étoiles.
    - `/[player_command] likes top`: ouvre l'interface graphique qui affiche les îles supérieures par Likes, Dislikes ou Stars
    - `/[player_command] likes view <player>`: ouvre l'interface graphique qui montre qui a ajouté des j'aime ou des étoiles à l'île.

=== "Commandes Admin"
    - `/[admin_command] likes`: ouvre l'interface graphique Admin.
    - `/[admin_command] likes settings`: ouvre l'interface graphique Admin Settings.

## Permissions

!!! tip
    `[gamemode]` est un préfixe qui diffère selon le mode de jeu que vous exécutez.
    Le préfixe est le nom du mode de jeu en minuscules, c'est-à-dire que si vous utilisez BSkyBlock, le préfixe est `bskyblock`.
    De même, si vous utilisez AcidIsland, le préfixe est `acidisland`.

=== "Permissions du joueur"
    - `[gamemode].likes` - (défaut: `true`) - Permet au joueur d'utiliser la commande '/[player_command] likes'.
    - `[gamemode].likes.top` - (défaut: `true`) - Permet au joueur d'utiliser la commande '/[player_command] likes top'.
    - `[gamemode].likes.view` - (défaut: `true`) - Permet au joueur d'utiliser la commande '/[player_command] likes top'.
    - `[gamemode].likes.icon.[MATERIAL]` - (défaut: `false`) - Permet de modifier l'icône du propriétaire de l'île dans les interfaces graphiques supérieures.

=== "Permissions Admin"
    - `[gamemode].likes.view.others` - (défaut: `op`) - Permet au joueur d'utiliser la commande '/[player_command] likes view <player>'.
    - `[gamemode].likes.bypass-cost` - (défaut: `op`) - Permet de contourner le coût des opérations dans le addon.
    - `[gamemode].likes.admin` - (défaut: `op`) - Permet d'utiliser la commande '/[admin_command] likes'.
    - `[gamemode].likes.admin.settings` - (défaut: `op`) - Permet d'utiliser la commande '/[admin_command] likes settings'.

??? question "Quelque chose manque-t-il?"
    Vous pouvez trouver la liste complète des permissions dans le fichier [addon.yml](https://github.com/BentoBoxWorld/Likes/blob/develop/src/main/resources/addon.yml) de cet addon.
    Si quelque chose manque vraiment de la liste ci-dessous, veuillez nous le faire savoir!

## Placeholders

{{ placeholders_source(source="Likes") }}

## FAQ

??? question "Pouvez-vous ajouter la fonctionnalité X ?"
    Veuillez l'ajouter à la liste [ici](https://github.com/BentoBoxWorld/Likes/issues).

??? question "Puis-je désactiver les dislikes ?"
    Oui, l'addon Likes supporte 3 modes de fonctionnement :

    - Likes : permet d'ajouter uniquement des j'aime à l'île
    - LikesDislikes : permet d'ajouter des j'aime et des dislikes
    - Stars : permet d'évaluer les îles des joueurs de 1 à 5 étoiles
       
??? question "Puis-je voir les j'aime d'autres joueurs ?"
    Oui, mais vous avez besoin de la permission : `[gamemode].likes.view.others`. 
    
    Avec cette permission, les joueurs peuvent utiliser `/[playercmd] likes view <player>` pour voir les j'aime d'autres joueurs. 
    
??? question "Puis-je changer l'icône affichée juste pour certaines îles ?"
    Oui, c'est possible. 
    
    Il y a 2 façons :
    
    1. En utilisant l'interface graphique Admin, vous pouvez choisir l'île et le bloc qui sera affiché pour elle.
    2. En ajoutant une permission au propriétaire de l'île : `[gamemode].likes.icon.[MATERIAL]`
        
    Sachez que PLAYER_HEAD sera converti à la tête du propriétaire de l'île.

## Traductions

{{ translations("Likes") }}

## API

Depuis Likes 2.2.0 et BentoBox 1.17, les autres plugins peuvent accéder directement aux données de l'addon Likes.

### Dépendance Maven

Likes fournit une API pour les autres plugins. Cela couvre la version 2.2.0 et ultérieures.

!!! note
    Ajoutez la dépendance Likes à votre fichier Maven POM.xml :

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
                <artifactId>likes</artifactId>
                <version>2.2.0</version>
                <scope>provided</scope>
            </dependency>
        </dependencies>
    ```

Utilisez la dernière version de Likes.

Les JavaDocs pour Likes peuvent être trouvés [ici](https://ci.codemc.io/job/BentoBoxWorld/job/Likes/ws/target/apidocs/index.html).

### Évènements

=== "LikeAddEvent"
    !!! summary "Description"
        Évènement qui est déclenché quand un joueur ajoute un nouveau j'aime à l'île.

        Cet évènement est uniquement informatif. Ne peut pas être annulé.

        Lien vers la classe : [LikeAddEvent](https://github.com/BentoBoxWorld/Likes/blob/develop/src/main/java/world/bentobox/likes/events/LikeAddEvent.java)


    !!! question "Variables"
        - `UUID user` - l'identifiant du joueur qui a ajouté le j'aime.
        - `String islandId` - l'identifiant de l'île qui reçoit le j'aime.
        
    !!! example "Exemple"
        ```java
        @EventHandler(priority = EventPriority.MONITOR)
        public void onLike(LikeAddEvent event) {
            UUID user = event.getUser();
            String islandId = event.getIslandId();
        }
        ```  

=== "LikeRemoveEvent"
    !!! summary "Description"
        Évènement qui est déclenché quand un joueur retire son j'aime de l'île.

        Cet évènement est uniquement informatif. Ne peut pas être annulé.

        Lien vers la classe : [LikeRemoveEvent](https://github.com/BentoBoxWorld/Likes/blob/develop/src/main/java/world/bentobox/likes/events/LikeRemoveEvent.java)

    !!! question "Variables"
        - `UUID user` - l'identifiant du joueur qui a retiré le j'aime.
        - `String islandId` - l'identifiant de l'île qui perd le j'aime.
        
    !!! example "Exemple"
        ```java
        @EventHandler(priority = EventPriority.MONITOR)
        public void onLikeRemove(LikeRemoveEvent event) {
            UUID user = event.getUser();
            String islandId = event.getIslandId();
        }
        ```  
   
=== "DislikeAddEvent"
    !!! summary "Description"
        Évènement qui est déclenché quand un joueur ajoute un nouveau dislike à l'île.

        Cet évènement est uniquement informatif. Ne peut pas être annulé.

        Lien vers la classe : [DislikeAddEvent](https://github.com/BentoBoxWorld/Likes/blob/develop/src/main/java/world/bentobox/likes/events/DislikeAddEvent.java)

    !!! question "Variables"
        - `UUID user` - l'identifiant du joueur qui a ajouté le dislike.
        - `String islandId` - l'identifiant de l'île qui reçoit le dislike.

    !!! example "Exemple"
        ```java
        @EventHandler(priority = EventPriority.MONITOR)
        public void onDislike(DislikeAddEvent event) {
            UUID user = event.getUser();
            String islandId = event.getIslandId();
        }
        ```  

=== "DislikeRemoveEvent"
    !!! summary "Description"
        Évènement qui est déclenché quand un joueur retire son dislike de l'île.

        Cet évènement est uniquement informatif. Ne peut pas être annulé.

        Lien vers la classe : [DislikeRemoveEvent](https://github.com/BentoBoxWorld/Likes/blob/develop/src/main/java/world/bentobox/likes/events/DislikeRemoveEvent.java)

    !!! question "Variables"
        - `UUID user` - l'identifiant du joueur qui a retiré le dislike.
        - `String islandId` - l'identifiant de l'île qui perd le dislike.

    !!! example "Exemple"
        ```java
        @EventHandler(priority = EventPriority.MONITOR)
        public void onDislikeRemove(DislikeRemoveEvent event) {
            UUID user = event.getUser();
            String islandId = event.getIslandId();
        }
        ```  

=== "StarsAddEvent"
    !!! summary "Description"
        Évènement qui est déclenché quand un joueur ajoute de nouvelles étoiles à l'île.

        Cet évènement est uniquement informatif. Ne peut pas être annulé.

        Lien vers la classe : [StarsAddEvent](https://github.com/BentoBoxWorld/Likes/blob/develop/src/main/java/world/bentobox/likes/events/StarsAddEvent.java)

    !!! question "Variables"
        - `UUID user` - l'identifiant du joueur qui a ajouté les étoiles.
        - `String islandId` - l'identifiant de l'île qui reçoit les étoiles.
        - `int value` - la valeur des étoiles ajoutées (de 1 à 5)

    !!! example "Exemple"
        ```java
        @EventHandler(priority = EventPriority.MONITOR)
        public void onStarsAdd(StarsAddEvent event) {
            UUID user = event.getUser();
            String islandId = event.getIslandId();
            int value = event.getValue();
        }
        ```  

=== "StarsRemoveEvent"
    !!! summary "Description"
        Évènement qui est déclenché quand un joueur retire ses étoiles de l'île.

        Cet évènement est uniquement informatif. Ne peut pas être annulé.

        Lien vers la classe : [StarsRemoveEvent](https://github.com/BentoBoxWorld/Likes/blob/develop/src/main/java/world/bentobox/likes/events/StarsRemoveEvent.java)

    !!! question "Variables"
        - `UUID user` - l'identifiant du joueur qui a ajouté les étoiles.
        - `String islandId` - l'identifiant de l'île qui perd les étoiles.

    !!! example "Exemple"
        ```java
        @EventHandler(priority = EventPriority.MONITOR)
        public void onStarsRemove(StarsRemoveEvent event) {
            UUID user = event.getUser();
            String islandId = event.getIslandId();
        }
        ```  

### Gestionnaires de Demandes d'Addon

Jusqu'à BentoBox 1.17, nous avions un problème pour accéder aux données en dehors de l'environnement BentoBox en raison du chargeur de classe que nous utilisions pour charger les addons.
Cela signifiait que les données n'étaient accessibles que depuis d'autres addons. Mais BentoBox a implémenté la fonctionnalité PlAddon, ce qui signifie que les gestionnaires de demandes ne sont plus nécessaires.

Plus d'informations sur les gestionnaires de demandes d'addon peuvent être trouvées [ici](/en/latest/BentoBox/Request-Handler-API---How-plugins-can-get-data-from-addons/)

=== "island-likes"
    !!! summary "Description"
        Retourne les données de j'aime de l'île qui sont stockées pour l'île dans le monde donné.

    !!! question "Entrée"
        - `world-name`: String - le nom du monde.
        - `island`: String - l'UUID de l'île.

    !!! success "Sortie"
        La sortie est une `Map<String, Object>` avec les clés suivantes :

        - `likes`: long - le nombre de j'aime définis pour l'île donnée.
        - `dislikes`: long - le nombre de dislikes définis pour l'île donnée.
        - `rank`: long - le nombre de classement pour l'île donnée.
        - `stars`: double - la valeur moyenne des étoiles pour l'île donnée.
        - `placeByLikes`: integer - la place dans le classement par j'aime définis pour l'île donnée.
        - `placeByDislikes`: integer - la place dans le classement par dislikes définis pour l'île donnée.
        - `placeByRank`: integer - la place dans le classement par classement défini pour l'île donnée.
        - `placeByStars`: integer - la place dans le classement par étoiles définis pour l'île donnée.
        - `likedBy`: List&lt;UUID&gt; - la liste des UUID des joueurs qui ont aimé l'île donnée.
        - `dislikedBy`: List&lt;UUID&gt; - la liste des UUID des joueurs qui ont désaimé l'île donnée.
        - `staredBy`: Map&lt;UUID, Integer&gt; - la carte des UUID des joueurs qui ont évalué l'île donnée avec un nombre d'étoiles qu'ils ont ajoutées.


    !!! failure
        Ce gestionnaire retournera une carte vide si le `world-name` n'a pas été fourni ou si le `world-name` n'existe pas ou n'est pas un monde de mode de jeu ou si l'île n'est pas fournie ou si les données pour l'île sont vides.

    !!! example "Exemple de code"
        ```java
        public Map<String, Object> getLikesData(String worldName, String islandUUID) {
            return (Map<String, Object>) new AddonRequestBuilder()
                .addon("Likes")
                .label("island-likes")
                .addMetaData("world-name", worldName)
                .addMetaData("island", islandUUID)
                .request();
        }
        ```

=== "top-ten-likes"
    !!! summary "Description"
        Retourne une `Map<String, Number>` contenant les 10 meilleures UUID d'îles et leurs valeurs dans le classement donné.

    !!! question "Entrée"
        - `world-name`: String - le nom du monde.
        - `type`: String - le type du Classement. Supporte : STARS, LIKES, DISLIKES, RANK.

    !!! success "Sortie"
        Une Map contenant les UUID des îles qui sont dans le Top 10, mappées à la valeur de classement supérieur de leur île.

    !!! failure
        Ce gestionnaire retournera une carte vide si le `world-name` n'a pas été fourni ou si le `world-name` n'existe pas ou n'est pas un monde de mode de jeu ou si le type de classement fourni n'a pas de données.

    !!! example "Exemple de code"
        ```java
        public Map<String, Number> getTopTenLikes(String worldName, String type) {
            return (Map<String, Number>) new AddonRequestBuilder()
                .addon("Likes")
                .label("top-ten-likes")
                .addMetaData("world-name", worldName)
                .addMetaData("type", type)
                .request();
        }
        ```
