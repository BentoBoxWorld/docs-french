# Warps

**Warps** permet aux joueurs d'ajouter des panneaux de téléportation personnels à leur île.

Créé et maintenu par [tastybento](https://github.com/tastybento).

{{ addon_description("Warps") }}

## Installation

1. Placez le fichier jar du addon Warps dans le dossier des addons du plugin BentoBox
2. Redémarrez le serveur
3. L'addon créera un dossier de données et à l'intérieur du dossier se trouvera un config.yml
4. Modifiez le config.yml comme vous le souhaitez.
5. Redémarrez le serveur si vous apportez une modification

## Configuration

### config.yml

Une fois l'addon correctement installé, il créera un fichier config.yml. Chaque option dans ce fichier est accompagnée de commentaires. Veuillez vérifier le fichier pour plus d'informations.
Vous pouvez trouver le dernier fichier config : [config.yml](https://github.com/BentoBoxWorld/Warps/blob/develop/src/main/resources/config.yml)

??? question "Qu'est-ce que la restriction de téléportation?"
    Cela limite la création de panneau de téléportation aux joueurs qui ont au moins un certain niveau d'île. Cela nécessite le addon Level
    et le niveau par défaut est 10.

??? question "Qu'est-ce que le texte de bienvenue"
    C'est le texte que le joueur doit mettre sur le panneau pour en faire un panneau de téléportation, par exemple, [Welcome]. Ce n'est pas sensible à la casse!

    Ce texte doit être sur la première ligne.

??? question "Qu'est-ce que les modes de jeu désactivés?"
    Cette liste stocke les modes de jeu dans lesquels le addon Warps ne devrait pas fonctionner.

    Pour désactiver l'addon, il est nécessaire d'écrire son nom sur une nouvelle ligne qui commence par -. Exemple:
    ```
      disabled-gamemodes:
       - BSkyBlock
    ```

??? question "Qu'est-ce que le format de lore?"
    Le format de lore permet de changer la couleur par défaut pour les lignes de description dans le panneau. Les lignes de description sont utilisées dans l'interface graphique.

    Les lignes de description contiennent les lignes de panneau qui sont en dessous du texte [welcome].

??? question "Qu'est-ce que fait le paramètre permettre dans d'autres mondes?"
    Cela permet aux panneaux de téléportation d'être placés dans *n'importe quel* monde, même les mondes non-BentoBox.

    Les joueurs doivent avoir la permission `welcomewarpsigns.warp` pour l'utiliser.

??? question "Qu'est-ce que show-warps-on-map ?"
    Quand défini sur `true`, les emplacements des panneaux de warp sont affichés comme marqueurs sur les plugins de carte web (Dynmap, BlueMap).

    Nécessite un plugin de carte compatible et le hook de carte BentoBox actif. Chaque panneau de warp apparaît comme un marqueur de point avec le texte des lignes du panneau en dessous de `[Welcome]`.

    Défaut : `true`

??? question "Qu'est-ce que le warp et les warps?"
    La commande `warp` nécessite `<player>` vers lequel le téléportation devrait se produire, tandis que `warps` ouvre un menu qui permet de choisir un joueur.

    Si vous avez activé `allow in other worlds` alors ce sera une commande principale `/warp`

    Tandis que pour chaque mode de jeu BentoBox ce sera toujours `/[player_cmd] warp`


### Interfaces graphiques personnalisables

BentoBox 1.17 API a introduit une fonction qui permet de mettre en œuvre des interfaces graphiques personnalisables. Cet addon est l'un des premiers à utiliser cette fonctionnalité. Nous avons essayé d'être aussi simples que possible pour la personnalisation, cependant, certaines fonctionnalités nécessitent une explication.
Vous pouvez trouver plus d'informations sur le fonctionnement des interfaces graphiques personnalisées de BentoBox ici : [Interfaces graphiques personnalisées](/en/latest/Tutorials/generic/Customizable-GUI/)

??? question "Comment puis-je personnaliser les interfaces graphiques"
    Pour personnaliser les interfaces graphiques d'addon, vous devez avoir la version 1.12. C'est la première version qui les a implémentées. L'addon créera un nouveau répertoire sous `/plugins/BentoBox/addons/Warps` portant le nom `panels`

??? question "Que fait le type de bouton `PREVIOUS`|`NEXT`?"
    Les types de bouton PREVIOUS et NEXT permettent de créer une pagination automatique, lorsque vous avez plus d'îles que d'espace dans l'interface graphique.
    Ces types ont des paramètres supplémentaires sous les données :

    - `indexing` - indique si le bouton affichera le numéro de page.

    Exemple :
    ```yaml
        icon: tipped_arrow[potion_contents={custom_color:11546150}]
        title: warps.gui.buttons.previous.name
        description: warps.gui.buttons.previous.description
        data:
          type: PREVIOUS
          indexing: true
        action:
          left:
            action: PREVIOUS
            tooltip: warps.gui.tips.click-to-previous
    ```

??? question "Qu'est-ce que le type de bouton `RANDOM`?"
    Ce bouton permet aux joueurs de se téléporter vers un panneau de téléportation aléatoire.
    Il n'est disponible que s'il y a plus de 1 panneau de téléportation.

    Exemple :
    ```yaml
        icon: DROPPER
        title: warps.gui.buttons.random.name
        description: warps.gui.buttons.random.description
        data:
          type: RANDOM
        actions:
          warp:
            click-type: left
            tooltip: warps.gui.tips.click-to-warp
    ```

??? question "Qu'est-ce que le type de bouton `WARP`?"
    Le bouton WARP crée une entrée dynamique pour un objet warp.

    Spécifier le titre, la description et l'icône remplacera la génération dynamique basée sur les données du panneau et de la base de données. Par défaut, ces valeurs seront générées à partir des entrées de la base de données.

    L'icône PLAYER_HEAD sera remplacée par la tête du joueur propriétaire.

    Exemple :
    ```yaml
        warp_button:
          icon: PLAYER_HEAD
          title: warps.gui.buttons.warp.name
          description: warps.gui.buttons.warp.description
          data:
            type: WARP
          actions:
            warp:
              click-type: left
              tooltip: warps.gui.tips.click-to-warp
    ```


## Commandes

!!! tip
    `[player_command]` est une commande qui diffère selon le mode de jeu que vous exécutez.
    Le fichier `config.yml` des modes de jeu contient des options qui vous permettent de modifier cette valeur.
    Par exemple, sur BSkyBlock, la `[player_command]` par défaut est `island`.

=== "Commandes joueur"
    - `/[player_command] warp <player>`: téléporte le joueur vers le panneau ciblé.
    - `/[player_command] warps`: ouvre l'interface graphique permettant de voir tous les panneaux de téléportation disponibles.

## Permissions

!!! tip
    `[gamemode]` est un préfixe qui diffère selon le mode de jeu que vous exécutez.
    Le préfixe est le nom en minuscules du mode de jeu, c.-à-d. si vous utilisez BSkyBlock, le préfixe est `bskyblock`.
    De même, si vous utilisez AcidIsland, le préfixe est `acidisland`.

=== "Permissions joueur"
    - `[gamemode].island.warp` - Le joueur peut utiliser les commandes `/[player_command] warp` et `/[player_command] warps`. Activé par défaut.
    - `[gamemode].island.addwarp` - Les joueurs peuvent créer des panneaux de téléportation. Activé par défaut.
    - `welcomewarpsigns.warp` - Le joueur peut utiliser les commandes `/warp` et `/warps`. Désactivé par défaut. Nécessite `allow-in-other-worlds`.
    - `welcomewarpsigns.addwarp` - Les joueurs peuvent créer des panneaux de téléportation. Désactivé par défaut. Nécessite `allow-in-other-worlds`.

??? question "Quelque chose manque-t-il ?"
    Vous pouvez trouver la liste complète des permissions dans le fichier [addon.yml](https://github.com/BentoBoxWorld/Warps/blob/develop/src/main/resources/addon.yml) de ce module.
    Si quelque chose manque effectivement de la liste ci-dessous, veuillez nous le faire savoir !

## FAQ

??? question "Pouvez-vous ajouter la fonctionnalité X ?"
    Veuillez l'ajouter à la liste [ici](https://github.com/BentoBoxWorld/Warps/issues).

??? question "J'ai un bug, où dois-je le signaler ?"
    Veuillez l'ajouter à la liste [ici](https://github.com/BentoBoxWorld/Warps/issues).

## Journal des modifications

??? note "Nouveautés dans v1.18.0"
    **Publié :** 5 avril 2026

    - **Support de carte web (Dynmap / BlueMap).** Les panneaux de warp apparaissent maintenant comme marqueurs sur les cartes web quand l'option `show-warps-on-map` est activée (défaut : true). Nécessite un plugin de carte compatible avec BentoBox.
    - ⚙️ Nouvelle option de configuration `show-warps-on-map` (voir Configuration ci-dessus).
    - 🔡 Locale russe mise à jour au format MiniMessage avec une couverture complète des clés.
    - Fichiers de locale supplémentaires ajoutés et mis à jour.
    - Nécessite BentoBox API 3.12.0+.

    🔡 Supprimez `BentoBox/addons/Warps/locales/` pour régénérer les fichiers de locale avec le nouveau format.

    [Release v1.18.0](https://github.com/BentoBoxWorld/Warps/releases/tag/1.18.0)

??? warning "Nouveautés dans v1.19.0 — migration des locales requise"
    **Publié :** 11 avril 2026

    - **Tous les fichiers de locale migrés vers MiniMessage.** Chaque fichier de locale a été converti des codes couleur `&` legacy vers les balises MiniMessage pour être cohérent avec BentoBox 3.14.
    - Nécessite BentoBox API 3.14.0+.
    - Warps est désormais compilé exclusivement contre Paper 1.21.11 (API Spigot supprimée).

    🔺 **BentoBox 3.14.0 requis.** Assurez-vous que votre BentoBox est à jour avant de mettre à jour Warps.

    🔡 **Régénérez les fichiers de locale** — supprimez `BentoBox/locales/Warps/` et redémarrez le serveur. Les codes couleur `&` dans les fichiers de locale personnalisés ne s'afficheront plus.

    [Release v1.19.0](https://github.com/BentoBoxWorld/Warps/releases/tag/1.19.0)

## Traductions

{{ translations("Warps") }}

## Api

### Événements

Depuis que BentoBox 1.17 API a implémenté une fonctionnalité qui a résolu un problème avec les classloaders. Les plugins qui souhaitent utiliser les événements directement peuvent maintenant le faire.

Vous avez juste besoin d'ajouter Warps à votre projet en tant que dépendance. Vous pouvez utiliser Maven pour cela :

```xml
<dependency>
    <groupId>world.bentobox</groupId>
    <artifactId>warps</artifactId>
    <version>1.11.2</version>
    <scope>provided</scope>
</dependency>
```

=== "WarpInitiateEvent"
    !!! summary "Description"
        Événement déclenché après qu'un joueur a créé un nouveau panneau de téléportation.

        Lien vers la classe : [WarpInitiateEvent](https://github.com/BentoBoxWorld/Warps/blob/develop/src/main/java/world/bentobox/warps/event/WarpInitiateEvent.java)

    !!! question "Variables"
        - `UUID player` - id du joueur qui crée le panneau de téléportation.
        - `Location warpLoc` - l'emplacement du panneau de téléportation.

    !!! example "Code example"
        ```java
        @EventHandler(priority = EventPriority.MONITOR)
        public void onWarpInitiate(WarpInitiateEvent event) {
            UUID player = event.getPlayer();
            Location warpLoc = event.getWarpLoc();
        }
        ```

=== "WarpRemoveEvent"
    !!! summary "Description"
        Événement déclenché après qu'un joueur a supprimé un panneau de téléportation.

        Lien vers la classe : [WarpRemoveEvent](https://github.com/BentoBoxWorld/Warps/blob/develop/src/main/java/world/bentobox/warps/event/WarpRemoveEvent.java)

    !!! question "Variables"
        - `UUID owner` - id du joueur qui possède le panneau de téléportation.
        - `UUID remover` - id du joueur qui supprime le panneau de téléportation.
        - `Location warpLoc` - l'emplacement du panneau de téléportation.

    !!! example "Code example"
        ```java
        @EventHandler(priority = EventPriority.MONITOR)
        public void onWarpRemove(WarpRemoveEvent event) {
            UUID owner = event.getOwner();
            UUID remover = event.getRemover();
            Location warpLoc = event.getWarpLocation();
        }
        ```
