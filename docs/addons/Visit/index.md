# Addon Visit

**Visit** est un simple addon BentoBox qui permet de visiter les îles d'autres joueurs.
Ceci est une alternative au addon Warps.

Créé et maintenu par [BONNe](https://github.com/BONNe).

{{ addon_description("Visit") }}

## Installation

1. Placez le fichier jar de l'addon dans le dossier des addons du plugin BentoBox
2. Redémarrez le serveur
3. Exécutez la commande `/[admin_cmd] visit` pour configurer l'addon

## Configuration

De nombreux paramètres du addon sont exposés dans l'interface graphique Admin, cependant, certains ne le sont pas.
Modifier les étiquettes des commandes nécessite un redémarrage du serveur.

### config.yml

Une fois l'addon correctement installé, il créera un fichier config.yml. Chaque option dans ce fichier est accompagnée de commentaires. Veuillez vérifier le fichier pour plus d'informations.
Vous pouvez trouver le dernier fichier config : [config.yml](https://github.com/BentoBoxWorld/Visit/blob/develop/src/main/resources/config.yml)

### Interfaces graphiques personnalisables

BentoBox 1.17 API a introduit une fonction qui permet de mettre en œuvre des interfaces graphiques personnalisables. Cet addon est l'un des premiers à utiliser cette fonctionnalité. Nous avons essayé d'être aussi simples que possible pour la personnalisation, cependant, certaines fonctionnalités nécessitent une explication.
Vous pouvez trouver plus d'informations sur le fonctionnement des interfaces graphiques personnalisées de BentoBox ici : [Interfaces graphiques personnalisées](/en/latest/Tutorials/generic/Customizable-GUI/)

??? question "Comment puis-je personnaliser les interfaces graphiques"
    Pour personnaliser les interfaces graphiques d'addon, vous devez avoir la version 1.5. C'est la première version qui les a implémentées. L'addon créera un nouveau répertoire sous `/plugins/BentoBox/addons/Visit` portant le nom `panels`

    Actuellement, vous pouvez personnaliser 2 interfaces graphiques :

    - Panneau principal : `main_panel` - panneau qui contient toutes les îles.
    - Panneau de gestion : `manage_panel` - panneau qui contient certaines options de configuration.

    Chaque interface graphique contient des fonctions qui ne sont supportées que par elle-même.

??? question "Que fait le type de bouton `PREVIOUS`|`NEXT`?"
    Les types de bouton PREVIOUS et NEXT permettent de créer une pagination automatique, lorsque vous avez plus d'îles que d'espace dans l'interface graphique.
    Ces types ont des paramètres supplémentaires sous les données :

    - `indexing` - indique si le bouton affichera le numéro de page.

    Exemple :
    ```yaml
        icon: tipped_arrow[potion_contents={custom_color:11546150}]
        title: visit.gui.buttons.previous.name
        description: visit.gui.buttons.previous.description
        data:
          type: PREVIOUS
          indexing: true
        action:
          left:
            action: PREVIOUS
            tooltip: visit.gui.tips.click-to-previous
    ```

??? question "Qu'est-ce que le type de bouton `SEARCH`?"
    Ce bouton est disponible dans le panneau principal.
    Il crée un bouton qui permet de rechercher une île spécifique.

    Exemple :
    ```yaml
        icon: PAPER
        title: visit.gui.buttons.search.name
        # Deccription is generated dynamically. However, you can set it manualy.
        # description: visit.gui.buttons.search.description
        data:
          type: SEARCH
        actions:
          left:
            type: INPUT
            tooltip: visit.gui.tips.left-click-to-edit
          right:
            type: CLEAR
            tooltip: visit.gui.tips.right-click-to-clear
    ```

??? question "Qu'est-ce que le type de bouton `FILTER`?"
    Ce bouton est disponible dans le panneau principal.
    Il crée un bouton qui permet de filtrer les îles par certaines propriétés.

    Exemple :
    ```yaml
        # Icon is generated dynamically. However, you can set it manualy.
        # icon: SANDSTONE
        title: visit.gui.buttons.filter.name
        # Deccription is generated dynamically. However, you can set it manualy.
        # description: visit.gui.buttons.filter.description
        data:
          type: FILTER
        actions:
          left:
            type: UP
            tooltip: visit.gui.tips.left-click-to-cycle
          right:
            type: DOWN
            tooltip: visit.gui.tips.right-click-to-cycle
    ```

??? question "Qu'est-ce que le type de bouton `ISLAND`?"
    Ce bouton est disponible dans le panneau principal.
    Le bouton ISLAND crée une entrée dynamique pour un objet île.

    Spécifier le titre, la description et l'icône remplacera la génération dynamique basée sur les données de la base de données. Par défaut, ces valeurs seront générées à partir des entrées de la base de données.
    Ce bouton supporte 3 types d'actions différents :

    - Le type `VISIT` permet au joueur de visiter l'île
    - Le type `CONFIRM` permet au joueur de confirmer la visite si ask-payment-confirmation est activé dans la config.
    - Le type `CANCEL` permet au joueur d'annuler la visite si ask-payment-confirmation est activé dans la config.

    Exemple :
    ```yaml
      # Data is generated dynamicaly. However, setting them will overwrite it.
      # icon: PLAYER_HEAD
      # title: visit.gui.buttons.island.name
      # description: visit.gui.buttons.island.description
      data:
        type: ISLAND
      actions:
        - click-type: left
          type: VISIT
          tooltip: visit.gui.tips.click-to-visit
        - click-type: left
          type: CONFIRM
          tooltip: visit.gui.tips.left-click-to-confirm
        - click-type: right
          type: CANCEL
          tooltip: visit.gui.tips.right-click-to-cancel
    ```

??? question "Qu'est-ce que le type de bouton `PAYMENT`?"
    Ce bouton est disponible dans le panneau de gestion.
    Il crée un bouton qui permet de définir la valeur de paiement pour les joueurs visitant l'île.

    Exemple :
    ```yaml
        icon: ANVIL
        title: visit.gui.buttons.payment.name
        # Deccription is generated dynamically. However, you can set it manualy.
        # description: visit.gui.buttons.payment.description
        data:
          type: PAYMENT
        actions:
          left:
            type: CHANGE
            tooltip: visit.gui.tips.click-to-change
    ```

??? question "Qu'est-ce que le type de bouton `OFFLINE`?"
    Ce bouton est disponible dans le panneau de gestion.
    Il crée un bouton qui permet de définir si les joueurs peuvent visiter l'île lorsqu'aucun membre de l'île n'est en ligne.

    Exemple :
    ```yaml
        icon: REDSTONE_LAMP
        title: visit.gui.buttons.offline.name
        # Deccription is generated dynamically. However, you can set it manualy.
        # description: visit.gui.buttons.offline.description
        data:
          type: OFFLINE
        actions:
          left:
            type: TOGGLE
            tooltip: visit.gui.tips.click-to-toggle
    ```

??? question "Qu'est-ce que le type de bouton `ALLOWED`?"
    Ce bouton est disponible dans le panneau de gestion.
    Il crée un bouton qui permet de désactiver les visites en un clic. C'est le raccourci pour modifier la valeur du drapeau `ALLOW_VISITS_FLAG` via les paramètres.

    Exemple :
    ```yaml
        icon: PUMPKIN_PIE
        title: visit.gui.buttons.enabled.name
        # description: visit.gui.buttons.enabled.description
        data:
          type: ALLOWED
        actions:
          left:
            type: TOGGLE
            tooltip: visit.gui.tips.click-to-toggle
    ```

## Commandes

!!! tip
    `[player_command]` et `[admin_command]` sont des commandes qui diffèrent selon le mode de jeu que vous utilisez.
    Le fichier `config.yml` des modes de jeu contient des options qui vous permettent de modifier ces valeurs.
    Par exemple, sur BSkyBlock, la commande `[player_command]` par défaut est `island`, et la commande `[admin_command]` par défaut est `bsbadmin`.
    Soyez conscient que cet addon permet de modifier les alias de commandes du joueur dans le fichier de configuration de l'addon `config.yml`.

=== "Commandes du joueur"
    - `/[player_command] visit <player>`: ouvre l'interface graphique ou visite l'île du joueur ciblé.
    - `/[player_command] visit configure`: ouvre l'interface graphique qui permet de gérer les paramètres de visite.
    - `/[player_command] visit setlocation`: permet de changer le lieu d'apparition des visiteurs.

=== "Commandes Admin"
    - `/[admin_command] visit <player>`: ouvre l'interface graphique qui permet de modifier les paramètres du addon et de configurer les données de l'île.

## Permissions

!!! tip
    `[gamemode]` est un préfixe qui diffère selon le mode de jeu que vous utilisez.
    Le préfixe est le nom du mode de jeu en minuscules, c'est-à-dire que si vous utilisez BSkyBlock, le préfixe est `bskyblock`.
    De même, si vous utilisez AcidIsland, le préfixe est `acidisland`.

=== "Permissions des joueurs"
    - `[gamemode].visit` - Permet au joueur d'utiliser la commande '/[player_command] visit'.
    - `[gamemode].visit.configure` - Permet au joueur d'utiliser la commande '/[player_command] visit configure'.
    - `[gamemode].visit.setlocation` - Permet au joueur d'utiliser la commande '/[player_command] visit setlocation'.
    - `visit.icon.[material]` - Permet de modifier l'icône de l'île appartenant à un joueur dans l'interface graphique Visit.

=== "Permissions Admin"
    - `[gamemode].admin.visit` - Permet au joueur d'utiliser la commande '/[admin_command] visit' et ses sous-commandes.
    
??? question "Quelque chose manque-t-il?"
    Vous pouvez trouver la liste complète des permissions dans le fichier [addon.yml](https://github.com/BentoBoxWorld/Visit/blob/develop/src/main/resources/addon.yml) de cet addon.
    Si quelque chose manque effectivement de la liste ci-dessous, s'il vous plaît, dites-le-nous !
   
## Drapeaux

L'addon introduit 2 drapeaux de protection BentoBox :

- ![pumpkin_pie](https://static.wikia.nocookie.net/minecraft_gamepedia/images/a/ac/Pumpkin_Pie_JE2_BE2.png){: loading=lazy width=16px } ALLOW_VISITS_FLAG: drapeau dans les paramètres de l'île qui permet d'activer/désactiver la visite de l'île.
- ![paper](https://static.wikia.nocookie.net/minecraft_gamepedia/images/f/f2/Paper_JE2_BE2.png){: loading=lazy width=16px } RECEIVE_VISIT_MESSAGE_FLAG: drapeau dans les paramètres de l'île qui permet d'activer/désactiver la réception par les membres de l'île des messages de visite/départ.


## FAQ

??? question "Pouvez-vous ajouter la fonctionnalité X?"
    S'il vous plaît, ajoutez-la à la liste [ici](https://github.com/BentoBoxWorld/Visit/issues).

??? question "Les joueurs peuvent-ils changer le lieu où les visiteurs sont téléportés?"
    Oui, les joueurs peuvent le définir avec la commande : `/[player_cmd] visit setlocation`. Cependant, soyez conscient que les visiteurs ne seront pas téléportés dans des endroits "dangereux", et si le lieu n'est pas sûr, ils seront téléportés dans un lieu plus sûr.

??? question "Les administrateurs peuvent-ils changer le lieu où les visiteurs sont téléportés?"
    Oui, les administrateurs peuvent le définir avec la commande : `/[admin_cmd] setspawnpoint`. Cependant, soyez conscient que les visiteurs ne seront pas téléportés dans des endroits "dangereux", et si le lieu n'est pas sûr, ils seront téléportés dans un lieu plus sûr.

??? question "Les joueurs peuvent-ils avoir des icônes personnalisées?"
    Oui, l'icône de l'île dans le panneau Visit peut être changée en ajoutant les permissions `visit.icon.[material]` au propriétaire de l'île.

??? question "Je ne veux pas utiliser l'économie. Puis-je la désactiver complètement?"
    Oui, l'option de configuration `disable-economy` désactiva complètement toutes les parties de l'économie.

??? question "Comment puis-je autoriser ou interdire aux membres de l'île de modifier les valeurs de visite?"
    Les propriétaires d'île (et les membres avec l'allowance `CHANGE_SETTINGS`) peuvent modifier l'accès `RANKED_COMMANDS` via le panneau Paramètres. Il y aura une commande `/[player_cmd] visit configure` dans la liste.

??? question "Comment puis-je autoriser ou interdire aux membres de l'île de modifier le lieu de visite?"
    Les propriétaires d'île (et les membres avec l'allowance `CHANGE_SETTINGS`) peuvent modifier l'accès `RANKED_COMMANDS` via le panneau Paramètres. Il y aura une commande `/[player_cmd] visit setlocation` dans la liste.

## Traductions

{{ translations("Visit") }}

## API

Depuis Visit 1.4.0 et BentoBox 1.17, d'autres plugins peuvent accéder directement aux données du addon Visit.

### Dépendance Maven

Visit fournit une API pour les autres plugins. Cela couvre la version 1.5.0 et au-delà.

!!! note
    Ajoutez la dépendance Visit à votre POM.xml Maven :

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
                <artifactId>visit</artifactId>
                <version>1.5.0</version>
                <scope>provided</scope>
            </dependency>
        </dependencies>
    ```

Utilisez la dernière version de Visit.

La documentation JavaDoc pour Visit peut être trouvée [ici](https://ci.codemc.io/job/BentoBoxWorld/job/Visit/ws/target/apidocs/index.html).

### Événements

=== "VisitEvent"
    !!! summary "Description"
        Événement qui est déclenché avant que le joueur soit téléporté à l'île, mais après les paiements.

        Peut être annulé. (les paiements ne sont pas retournés lors de l'annulation)

        Lien vers la classe : [VisitEvent](https://github.com/BentoBoxWorld/Visit/blob/develop/src/main/java/world/bentobox/visit/events/VisitEvent.java)

    !!! question "Variables"
        - `User player` - ID du joueur qui essaie de visiter une île.
        - `Island island` - l'île que le joueur essaie de visiter.
        - `boolean cancelled` - le booléen qui indique si l'événement est annulé.
 
    !!! example "Exemple de code"
        ```java
        @EventHandler(priority = EventPriority.MONITOR)
        public void onVisit(VisitEvent event) {
            UUID player = event.getPlayer();
            User user = event.getUser();
            Island island = event.getIsland();

            boolean cancelled = event.isCancelled();
        }
        ```
