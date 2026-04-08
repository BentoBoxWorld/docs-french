# CheckMeOut

Ceci est un addon de soumission d'île. Cet addon permet aux joueurs de soumettre leur île pour examen par les administrateurs. De cette façon, les administrateurs peuvent mettre en place des défis ou des compétitions à l'échelle du site que les joueurs peuvent faire, puis soumettre leur île pour examen. Les administrateurs reçoivent une interface graphique qui répertorie les soumissions et ils peuvent se téléporter aux îles à partir de là. Une fois qu'une île est examinée par les administrateurs, elle peut être supprimée, ou lorsque toute l'activité est terminée, toutes les soumissions peuvent être effacées.

Créé et maintenu par [tastybento](https://github.com/tastybento).

{{ addon_description("CheckMeOut") }}


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
Vous pouvez trouver le dernier fichier config : [config.yml](https://github.com/BentoBoxWorld/CheckMeOut/blob/develop/src/main/resources/config.yml)

### Interfaces graphiques personnalisables

BentoBox 1.17 API a introduit une fonction qui permet de mettre en œuvre des interfaces graphiques personnalisables. Cet addon est l'un des premiers à utiliser cette fonctionnalité. Nous avons essayé d'être aussi simples que possible pour la personnalisation, cependant, certaines fonctionnalités nécessitent une explication.
Vous pouvez trouver plus d'informations sur le fonctionnement des interfaces graphiques personnalisées de BentoBox ici : [Interfaces graphiques personnalisées](/en/latest/Tutorials/generic/Customizable-GUI/)

??? question "Comment puis-je personnaliser les interfaces graphiques"
    Pour personnaliser les interfaces graphiques d'addon, vous devez avoir la version 1.1. C'est la première version qui les a implémentées. L'addon créera un nouveau répertoire sous `/plugins/BentoBox/addons/CheckMeOut` portant le nom `panels`

    Actuellement, vous pouvez personnaliser 1 interface graphique :

    - Panneau principal : `view_panel` - panneau qui contient les îles soumises.

??? question "Que fait le type de bouton `PREVIOUS`|`NEXT`?"
    Les types de bouton PREVIOUS et NEXT permettent de créer une pagination automatique, lorsque vous avez plus d'îles que d'espace dans l'interface graphique.
    Ces types ont des paramètres supplémentaires sous les données :

    - `indexing` - indique si le bouton affichera le numéro de page.

    Exemple :
    ```yaml
        icon: tipped_arrow[potion_contents={custom_color:11546150}]
        title: checkmeout.gui.buttons.previous.name
        description: checkmeout.gui.buttons.previous.description
        data:
          type: PREVIOUS
          indexing: true
        action:
          left:
            action: PREVIOUS
            tooltip: checkmeout.gui.tips.click-to-previous
    ```

??? question "Qu'est-ce que le type de bouton `RANDOM`?"
    Ce bouton permet aux joueurs de se téléporter à une soumission aléatoire.

    - l'action warp n'est disponible que si vous avez installé le addon Warps et que le joueur a un panneau de téléportation existant.
    - l'action visit n'est disponible que si vous avez installé le addon Visits.
    - l'action check est le mécanisme de téléportation de l'addon par défaut.

    Exemple :
    ```yaml
        icon: DROPPER
        title: checkmeout.gui.buttons.random.name
        description: checkmeout.gui.buttons.random.description
        data:
          type: RANDOM
        actions:
          # Warp action requires WARP addon. If warp addon is not present, warp action will not work.
          warp:
            click-type: UNKNOWN
            tooltip: checkmeout.gui.tips.click-to-warp
          # Visit action requires Visit addon. If Visit addon is not present, visit action will not work.
          visit:
            click-type: UNKNOWN
            tooltip: checkmeout.gui.tips.click-to-visit
          # Check action requires player to have "[gamemode].checkmeout.admin.check" permission.
          check:
            click-type: UNKNOWN
            tooltip: checkmeout.gui.tips.click-to-check
    ```

??? question "Qu'est-ce que le type de bouton `ISLAND`?"
    Ce bouton est disponible dans le panneau principal.
    Le bouton ISLAND crée une entrée dynamique pour un objet île.

    Spécifier le titre, la description et l'icône remplacera la génération dynamique basée sur les données de la base de données. Par défaut, ces valeurs seront générées à partir des entrées de la base de données.
    Ce bouton supporte 3 types d'actions différentes :

    - l'action warp n'est disponible que si vous avez installé le addon Warps et que le joueur a un panneau de téléportation existant.
    - l'action visit n'est disponible que si vous avez installé le addon Visits.
    - l'action check est le mécanisme de téléportation de l'addon par défaut.

    Exemple :
    ```yaml
      # icon: PLAYER_HEAD
      title: checkmeout.gui.buttons.island.name
      description: checkmeout.gui.buttons.island.description
      data:
        type: ISLAND
      actions:
        # Warp action requires WARP addon. If warp addon is not present, warp action will not work.
        warp:
          # Click type UNKNOWN means that it accept any click type.
          click-type: UNKNOWN
          tooltip: checkmeout.gui.tips.click-to-warp
        # Visit action requires Visit addon. If Visit addon is not present, visit action will not work.
        visit:
          # Click type UNKNOWN means that it accept any click type.
          click-type: UNKNOWN
          tooltip: checkmeout.gui.tips.click-to-visit
        # Check action requires player to have "[gamemode].checkmeout.admin.check" permission.
        check:
          # Click type UNKNOWN means that it accept any click type.
          click-type: UNKNOWN
          tooltip: checkmeout.gui.tips.click-to-check
    ```

## Commandes

!!! tip
    `[player_command]` et `[admin_command]` sont des commandes qui diffèrent selon le mode de jeu que vous exécutez.
    Le fichier `config.yml` des modes de jeu contient des options qui vous permettent de modifier ces valeurs.
    Par exemple, sur BSkyBlock, la `[player_command]` par défaut est `island`, et la `[admin_command]` par défaut est `bsbadmin`.
    Soyez conscient que cet addon permet de modifier les alias des commandes du joueur dans le fichier `config.yml` du addon.

=== "Commandes du joueur"
    - `/[player_command] checkmeout`: soumet l'île pour révision.
    - `/[player_command] checkmeout view`: ouvre l'interface graphique qui permet de voir les autres îles soumises.

=== "Commandes Admin"
    - `/[admin_command] checkmeout`: commande admin principale.
    - `/[admin_command] checkmeout check <player>`: téléporte le joueur vers une île soumise.
    - `/[admin_command] checkmeout clearall`: supprime toutes les îles soumises.
    - `/[admin_command] checkmeout delete <player>`: supprime l'île soumise de <player>.
    - `/[admin_command] checkmeout seesubs`: ouvre un menu pour voir toutes les îles soumises.


## Permissions

!!! tip
    `[gamemode]` est un préfixe qui diffère selon le mode de jeu que vous exécutez.
    Le préfixe est le nom du mode de jeu en minuscules, c'est-à-dire que si vous utilisez BSkyBlock, le préfixe est `bskyblock`.
    De même, si vous utilisez AcidIsland, le préfixe est `acidisland`.

=== "Permissions du joueur"
    - `[gamemode].checkmeout` - Permet au joueur d'utiliser la commande '/[player_command] checkmeout' pour soumettre l'île. Par défaut, true.
    - `[gamemode].checkmeout.view` - Permet au joueur d'utiliser la commande '/[admin_command] checkmeout view' pour voir toutes les îles soumises. Par défaut, true.
    - `checkmeout.icon.[material]` - Permet de modifier l'icône de l'île possédée par un joueur dans View GUI. Par défaut, false.

=== "Permissions Admin"
    - `[gamemode].checkmeout.admin.check` - Permet au joueur d'utiliser la commande '/[admin_command] checkmeout check'. Par défaut, OP.
    - `[gamemode].checkmeout.admin.delete` - Permet au joueur d'utiliser la commande '/[admin_command] checkmeout delete'. Par défaut, OP.
    - `[gamemode].checkmeout.admin.clearsubmissions` - Permet au joueur d'utiliser la commande '/[admin_command] checkmeout clearall'. Par défaut, OP.
    - `[gamemode].checkmeout.admin.seesubs` - Permet au joueur d'utiliser la commande '/[admin_command] checkmeout seesubs'. Par défaut, OP.

??? question "Quelque chose manque-t-il?"
    Vous pouvez trouver la liste complète des permissions dans le fichier [addon.yml](https://github.com/BentoBoxWorld/Visit/blob/develop/src/main/resources/addon.yml) de cet addon.
    Si quelque chose manque vraiment de la liste ci-dessous, veuillez nous le faire savoir!

## FAQ

??? question "Pouvez-vous ajouter une fonctionnalité X?"
    Veuillez l'ajouter à la liste [ici](https://github.com/BentoBoxWorld/CheckMeOut/issues).

## Api

### Événements

Depuis que BentoBox 1.17 API a implémenté une fonctionnalité qui a résolu un problème avec les chargeurs de classes. Les plugins qui veulent utiliser les événements directement, maintenant ils peuvent le faire.

Vous devez juste ajouter CheckMeOut à votre projet en tant que dépendance. Vous pouvez utiliser Maven pour cela :

```xml
<dependency>
    <groupId>world.bentobox</groupId>
    <artifactId>checkmeout</artifactId>
    <version>1.1.0</version>
    <scope>provided</scope>
</dependency>
```

=== "IslandSubmittedEvent"
    !!! summary "Description"
        Événement déclenché après que le joueur ait soumis son île pour révision.

        Lien vers la classe : [IslandSubmittedEvent](https://github.com/BentoBoxWorld/CheckMeOut/blob/develop/src/main/java/world/bentobox/checkmeout/events/IslandSubmittedEvent.java)

    !!! question "Variables"
        - `UUID uuid` - id du joueur qui a soumis l'île.
        - `Location location` - l'emplacement de la soumission.

    !!! example "Exemple de code"
        ```java
        @EventHandler(priority = EventPriority.MONITOR)
        public void onSubmittion(IslandSubmittedEvent event) {
            UUID player = event.getUUID();
            Location location = event.getLocation();
        }
        ```

## Traductions

{{ translations("CheckMeOut") }}
