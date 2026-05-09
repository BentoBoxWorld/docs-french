# Biomes

**Biomes** permet à vos joueurs de **changer le biome** sur leur île.

Créé et maintenu par [BONNe](https://github.com/BONNe).

{{ addon_description("Biomes", beta=True) }}

## Installation

1. Placez le fichier jar de l'addon dans le dossier `plugins/BentoBox/addons`.
2. Démarrez et arrêtez le serveur pour laisser Biomes générer ses fichiers de configuration.
3. Modifiez les fichiers [`config.yml`](#config.yml) et [`biomesTemplate.yml`](#Template) (vous pouvez les trouver dans le dossier `plugins/BentoBox/addons/Biomes`).
4. Redémarrez le serveur.
5. Importez les biomes dans le mode de jeu.

## Configuration

### config.yml

Une fois l'addon correctement installé, il créera un fichier config.yml. Chaque option dans ce fichier est accompagnée de commentaires. Veuillez vérifier le fichier pour plus d'informations.
Vous pouvez trouver le dernier fichier config : [config.yml](https://github.com/BentoBoxWorld/Biomes/blob/develop/src/main/resources/config.yml)

### Modèle

!!! warning
    Contrairement aux fichiers de configuration habituels, les modifications que vous apportez au fichier `biomesTemplate.yml` ne sont pas automatiquement prises en compte au démarrage du serveur.
    Vous devez importer manuellement les modifications que vous avez apportées et éventuellement les remplacer si vous en aviez déjà importé une configuration précédente.

Ce fichier contient toutes les informations nécessaires sur les biomes par défaut.
Si vous modifiez les valeurs dans biomes.yml, alors pour les appliquer, vous devez exécuter **/[admin_command] biomes**.

Le fichier modèle par défaut se trouve ici : [biomesTemplate.yml](https://github.com/BentoBoxWorld/Biomes/blob/develop/src/main/resources/biomesTemplate.yml)

!!! info "Ressources utiles sur les biomes"
    - [Liste complète des biomes disponibles sur Spigot](https://hub.spigotmc.org/javadocs/spigot/org/bukkit/block/Biome.html)
    - [Page « Biome » sur le wiki officiel de Minecraft](https://minecraft.gamepedia.com/Biome)

??? Template file Structure
    ```
    biomes:                                      # Internal Data Structure. DO NOT CHANGE!
      <unique_name>:                             # Unique name for the biome. Required!
        biome: <BIOME>                           # Spigot BIOME TYPE. Valid values can be found in link below. Required!
        environment: <ENVIRONMENT>               # Spigot WORLD ENVIRONMENT TYPE. World environment value. Default Normal.
        name: <String>                           # String. Custom name for biome. Default <unique_name>.
        description: <String>                    # String. Some extra description in icon lore. Default empty.
        icon: <Item>                             # BentoBox ItemParser type. Write format can be found in: https://docs.bentobox.world/en/latest/BentoBox/ItemParser/. Default Paper.
        order: <Integer>                         # Integer. Order of current biome. Default -1.
        unlock:                                  # Section that configures biomes unlock/buy options. Not required.
          level: <Long>                          # Minimal island level for biome to be unlockable. Requires Level addon. Default 0.
          permissions: [<String>]                # Set of permissions for biome to be unlockable. Default empty.
          cost: <Double>                         # Purchase cost (once) for biome. Requires Vault and Economy plugins. Default 0.
          items: [<Item>]                        # Set of items for purchasing biome (once). Write format for each item can be found in: https://docs.bentobox.world/en/latest/BentoBox/ItemParser/. Default empty.
        change:                                  # Section that configures cost for each biome usage. Not required.
          mode: <Mode>                           # Mode how cost is applied. Supported values: STATIC - price never changes, PER_BLOCK - cost is applied for each block in area, PER_USAGE - cost increases by [increment] after each usage. Default STATIC.
          cost: <Double>                         # Biome change cost. Requires Vault and Economy plugins. Default 0.
          items: [<Item>]                        # Set of items for changing biome. Write format for each item can be found in: https://docs.bentobox.world/en/latest/BentoBox/ItemParser/. Default empty.
          increment: <Double>                    # Increment for all costs (money and items) if usage is set to PER_USAGE. Default 0. (works as static)
    # Here starts the Bundle List
    bundles:                                     # Internal Data Structure.
      <unique_name>:                             # Unique name for the bundle. Required!
        name: <String>                           # String. Custom name for bundle. Default <unique_name>.
        description: <String>                    # String. Some extra description in icon lore. Default empty.
        icon: <Item>                             # BentoBox ItemParser type. Write format can be found in: https://docs.bentobox.world/en/latest/BentoBox/ItemParser/. Default Paper.
        biomes: [<String>]                       # Set of <unique_names> that you used in biomes section. Default empty.
    ```

### Interfaces graphiques personnalisables

BentoBox 1.17 API a introduit une fonction qui permet de mettre en œuvre des interfaces graphiques personnalisables. Cet addon est l'un des premiers à utiliser cette fonctionnalité. Nous avons essayé d'être aussi simples que possible pour la personnalisation, cependant, certaines fonctionnalités nécessitent une explication.
Vous pouvez trouver plus d'informations sur le fonctionnement des interfaces graphiques personnalisées de BentoBox ici : [Interfaces graphiques personnalisées](/en/latest/Tutorials/generic/Customizable-GUI/)

??? question "Comment puis-je personnaliser les interfaces graphiques"
    Pour personnaliser les interfaces graphiques d'addon, vous devez avoir la version 2.0. C'est la première version qui les a implémentées. L'addon créera un nouveau répertoire sous `/plugins/BentoBox/addons/Biomes` portant le nom `panels`

    Actuellement, vous pouvez personnaliser 3 interfaces graphiques :

    - Panneau principal : `main_panel` - panneau qui contient tous les biomes que les utilisateurs peuvent acheter ou utiliser.
    - Panneau avancé : `advanced_panel` - panneau qui contient différentes façons dont le biome peut être appliqué sur l'île.
    - Panneau d'achat : `buy_panel` - panneau qui contient les biomes que le joueur peut acheter.

    Chaque interface graphique contient des fonctions qui ne sont supportées que par elle-même.

??? question "Que fait le type de bouton `PREVIOUS`|`NEXT`?"
    Les types de bouton PREVIOUS et NEXT permettent de créer une pagination automatique, lorsque vous avez plus de biomes que d'espace dans l'interface graphique.
    Ces types ont des paramètres supplémentaires sous les données :

    - `indexing` - indique si le bouton affichera le numéro de page.

    Exemple :
    ```yaml
        icon: tipped_arrow[potion_contents={custom_color:11546150}]
        title: biomes.gui.buttons.previous.name
        description: biomes.gui.buttons.previous.description
        data:
          type: PREVIOUS
          indexing: true
        action:
          left:
            tooltip: biomes.gui.tips.click-to-previous
    ```

??? question "Qu'est-ce que le type de bouton `RETURN`?"
    Ce bouton est disponible dans tous les panneaux.
    Il crée un bouton qui permet de retourner au menu précédent ou de quitter l'interface graphique. La description est générée par l'addon, cependant, comme pour tous les boutons, vous pouvez spécifier votre propre texte dans le panneau.

    Exemple :
    ```yaml
        data:
          type: RETURN
    ```

??? question "Qu'est-ce que le type de bouton `BIOME`?"
    Ce bouton est disponible dans main_panel et buy_panel.
    Le bouton BIOME crée une entrée dynamique pour un objet biome. Le bouton ne sera rempli que s'il existe un biome. Par exemple, si vous avez seulement 3 biomes, mais que vous avez défini 7 endroits pour eux dans l'interface graphique, alors seulement 3 endroits seront remplis. Les autres endroits seront laissés vides.

    Par défaut, les biomes seront triés par leurs numéros d'ordre, cependant, vous pouvez spécifier un biome spécifique à placer dans un emplacement spécifique avec le paramètre `id` sous les données.

    ```yaml
      data:
        type: BIOME
        id: example_biome
    ```

    Spécifier le titre, la description et l'icône remplacera la génération dynamique basée sur les données de la base de données. Par défaut, ces valeurs seront générées à partir des entrées de la base de données.
    Ce bouton supporte 3 types d'actions différentes :

    - CHANGE - change le biome selon le mode de mise à jour par défaut et les valeurs de plage par défaut. Disponible dans main_panel.
    - ADVANCED_PANEL - ouvre le panneau avancé qui permet de choisir différents modes de mise à jour du biome. Disponible dans main_panel.
    - BUY - achète le biome sélectionné. Disponible dans buy_panel.

    Exemple :
    ```yaml
      data:
        type: BIOME
      actions:
        left:
          type: CHANGE
          # Supports ISLAND | CHUNK:NUMBER | RANGE:NUMBER
          content: ISLAND
          tooltip: biomes.gui.tips.left-click-to-apply
        right:
          type: ADVANCED_PANEL
          tooltip: biomes.gui.tips.right-click-to-open
    ```

??? question "Qu'est-ce que le type de bouton `PURCHASE`?"
    Ce bouton est disponible dans main_panel.
    Il crée un bouton qui ouvre un nouveau panneau contenant les biomes que le joueur peut acheter.

    Exemple :
    ```yaml
        data:
          type: PURCHASE
        action:
          left:
            tooltip: biomes.gui.tips.click-to-view
    ```


??? question "Qu'est-ce que le type de bouton `INCREASE|REDUCE`?"
    Ce bouton est disponible dans advanced_panel.
    Il crée un bouton qui augmente/réduit la « plage » pour changer le biome. Le nombre par lequel il augmente/réduit peut être défini aux côtés du type de bouton.

    Exemple :
    ```yaml
        data:
          type: INCREASE
          value: 5
        actions:
          left:
            tooltip: biomes.gui.tips.click-to-increase
    ```

??? question "Qu'est-ce que le type de bouton `MODE`?"
    Ce bouton est disponible dans advanced_panel.
    Il crée un bouton qui permet de changer le mode de mise à jour du biome entre les modes ISLAND, CHUNK et RANGE. Le mode est défini aux côtés du type de bouton.

    Exemple :
    ```yaml
        data:
          type: MODE
          value: CHUNK
        actions:
          left:
            tooltip: biomes.gui.tips.click-to-choose
    ```

??? question "Qu'est-ce que le type de bouton `ACCEPT`?"
    Ce bouton est disponible dans advanced_panel.
    Il crée un bouton qui permet de démarrer la mise à jour du biome avec les paramètres sélectionnés. Il a deux actions :

       - ACCEPT: démarre la mise à jour du biome
       - INPUT: permet d'entrer manuellement un nombre via le chat.

    Exemple :
    ```yaml
        data:
          type: ACCEPT
        actions:
          left:
            type: ACCEPT
            tooltip: biomes.gui.tips.left-click-to-accept
          right:
            type: INPUT
            tooltip: biomes.gui.tips.right-click-to-write
    ```

## Commandes

!!! tip
    `[player_command]` et `[admin_command]` sont des commandes qui diffèrent selon le mode de jeu que vous exécutez.
    Le fichier `config.yml` des modes de jeu contient des options qui vous permettent de modifier ces valeurs.
    Par exemple, sur BSkyBlock, la `[player_command]` par défaut est `island`, et la `[admin_command]` par défaut est `bsbadmin`.

!!! info
    Les commandes du joueur du addon Biomes sont complètement configurables. Vous pouvez les modifier dans le fichier de configuration du addon Biomes. Ci-dessous se trouvent seulement les noms par défaut de ces commandes.

=== "Commandes du joueur"
    - `/[player_command] biomes`: Cette méthode ouvre une interface graphique qui permet de changer le biome sur l'île de l'utilisateur.
    - `/[player_command] biomes help`: Affiche l'aide pour toutes les commandes
    - `/[player_command] biomes set <biome> [<type>] [<size>]`: Cette commande permet de changer le biome sur l'île sans ouvrir l'interface graphique. Si les paramètres < type> et < size> ne sont pas fournis, la commande utilise les valeurs par défaut de la configuration de l'addon.
    - `/[player_command] biomes buy <biome>`: Cette commande permet d'acheter un biome sans ouvrir l'interface graphique.

    !!! info
        - `<biome>` peut ne pas être le nom réel du biome Minecraft. Il est défini par l'administrateur.
        - `<type>` est l'un des trois types de changement de biome. Il offre de changer le biome sur l'île entière (`ISLAND`), dans le ou les chunks actuels (`CHUNK`) ou par distance autour du joueur (`RANGE`).


=== "Commandes Admin"
    - `/[admin_command] biomes`: ouvre l'interface graphique Admin Biomes.
    - `/[admin_command] biomes help`: affiche l'aide pour tous les commandes liées aux Biomes.
    - `/[admin_command] biomes import [<file>]`: importe les biomes du fichier de configuration `biomesTemplate.yml`, ou du fichier fourni.
    - `/[admin_command] biomes set <player> <biome> [<type>] [<size>]`: fonctionne comme la commande de biome utilisateur, mais il est nécessaire de fournir également le joueur dont l'île sera mise à jour du biome.
    - `/[admin_command] biomes migrate`: migre les données du addon biomes. Généralement utilisé lors de la mise à niveau d'une version plus ancienne à une version plus récente.
    - `/[admin_command] biomes unlock <player> <biome_id> [true]`: déverrouille (et achète si `true` est ajouté à la fin) le biome transmis pour une île du joueur.

## Permissions

!!! tip
    `[gamemode]` est un préfixe qui diffère selon le mode de jeu que vous exécutez.
    Le préfixe est le nom du mode de jeu en minuscules, c'est-à-dire que si vous utilisez BSkyBlock, le préfixe est `bskyblock`.
    De même, si vous utilisez AcidIsland, le préfixe est `acidisland`.

??? question "Quelque chose manque-t-il?"
    Vous pouvez trouver la liste complète des permissions dans le fichier [addon.yml](https://github.com/BentoBoxWorld/Biomes/blob/develop/src/main/resources/addon.yml) de cet addon.
    Si quelque chose manque vraiment de la liste ci-dessous, veuillez nous le faire savoir!

=== "Permissions du joueur"
    - `[gamemode].biomes` (défaut: `true`): le joueur peut utiliser la commande biomes qui ouvre l'interface graphique.
    - `[gamemode].biomes.info` (défaut: `true`): le joueur peut utiliser la commande biomes info.
    - `[gamemode].biomes.set` (défaut: `true`): le joueur peut utiliser la commande biomes set.
    - `[gamemode].biomes.buy` (défaut: `true`): le joueur peut utiliser la commande biomes buy.

=== "Permissions Admin"
    - `[gamemode].admin.biomes` (défaut: `op`): le joueur peut utiliser la commande admin biomes qui ouvre l'interface graphique.

## Journal des modifications

??? warning "Nouveautés dans v2.3.0 — requiert BentoBox 3.14.0+ et Paper"
    **Publié le :** 2026-05-05

    - ⚙️ **Préservation des biomes océan.** Nouvelle option `change-ocean-biomes` dans `config.yml` (défaut : `false`) qui empêche les changements de biome d'écraser les blocs océan (`OCEAN`, `WARM_OCEAN`, `DEEP_OCEAN`, etc.), gardant intacts les rivages et les zones sous-marines de l'île. Mettez à `true` pour rétablir l'ancien comportement.
    - **Type d'action de panneau `COMMAND`.** Les boutons de panneau peuvent désormais exécuter des commandes au clic, à la fois comme type de bouton autonome et comme action sur les boutons biome existants aux côtés de `CHANGE`/`BUY`/`ADVANCED_PANEL`. Pratique pour des boutons « Retour au panneau d'île » ou toute intégration personnalisée.
    - **`biomesTemplate.yml` retravaillé.** 44 biomes (contre ~29), coûts rééquilibrés, 9 nouveaux biomes dont Marais de mangrove, Jardin pâle (avec le mob The Creaking) et Jungle de bambou. 3 bundles de démarrage (Starter, Explorer, Nether & End) et démonstrations du mécanisme de coût `PER_USAGE`.
    - **Notifications de déblocage adaptées au mode de jeu.** Les joueurs dans le bon monde de mode de jeu reçoivent l'invite cliquable « utiliser maintenant » habituelle ; les joueurs ailleurs reçoivent un message simple indiquant le mode de jeu où le biome a été débloqué, évitant la confusion d'une commande exécutée dans le mauvais monde.
    - **Auto-import des biomes par défaut au premier démarrage.** Lorsqu'aucun biome n'est configuré pour un mode de jeu, l'addon importe désormais automatiquement `biomesTemplate.yml`. Plus besoin d'étape `import` manuelle sur les installations neuves.
    - **Annulation de la file de biomes lors de la suppression/réinitialisation d'île.** Les tâches de mise à jour de biome en file d'attente et en cours sont annulées sur `IslandDeleteEvent` et `IslandResettedEvent`, les tâches en cours s'arrêtant à la prochaine limite de chunk grâce à un drapeau `AtomicBoolean`.
    - 🐛 Correction de l'imprécision d'affichage en virgule flottante dans les infobulles GUI admin (par ex. `0.0299999999329447746` → `0.03`).
    - 🐛 Le formateur décimal est désormais figé sur `Locale.ROOT`, ce qui fait que les locales utilisant la virgule décimale (par ex. l'allemand) affichent `0.5` comme `0.5` et non `0,5`.
    - 🐛 Les objets du template de biomes au-dessus de la limite de pile de 99 sont maintenant fractionnés en piles valides au lieu d'échouer au chargement.
    - 🔡 Les 23 fichiers de locale, YAMLs de panneau et chaînes Java codées en dur ont été migrés des codes couleur `&` vers MiniMessage. 14 nouvelles traductions ajoutées (cs, de, hr, hu, id, it, ko, pt, pt-BR, ro, ru, tr, vi, zh-HK).

    🔺 **Rupture :** cette version requiert **BentoBox 3.14.0+**, **Paper** (Spigot n'est plus supporté) et **Java 21**. L'addon ne se chargera pas sur les anciennes versions.

    🔡 **Note locale :** les fichiers de locale personnalisés doivent être mis à jour — convertissez `&c`/`&l`/etc. en balises MiniMessage (`<red>`, `<bold>`), ou supprimez vos personnalisations pour récupérer les valeurs par défaut.

    ⚙️ **Note config :** vérifiez `config.yml` pour la nouvelle option `change-ocean-biomes` (défaut `false`).

    [Release v2.3.0](https://github.com/BentoBoxWorld/Biomes/releases/tag/2.3.0)

## Traductions

{{ translations("Biomes") }}

## API

Depuis Biomes 2.0 et BentoBox 1.17, d'autres plugins peuvent accéder directement aux données du addon Biomes. Cependant, les demandes de addon sont toujours une bonne solution pour les plugins qui ne veulent pas utiliser trop de dépendances.

### Dépendance Maven

Biomes fournit une API pour d'autres plugins. Cela couvre la version 2.1.0 et ultérieures.

!!! note
Ajoutez la dépendance Biomes à votre Maven POM.xml :

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
                <artifactId>biomes</artifactId>
                <version>2.1.0</version>
                <scope>provided</scope>
            </dependency>
        </dependencies>
    ```

Utilisez la dernière version de Biomes.

Les JavaDocs pour Biomes peuvent être trouvés [ici](https://ci.codemc.io/job/BentoBoxWorld/job/Biomes/ws/target/apidocs/index.html).

### Événements

=== "BiomeUnlockedEvent"
    !!! summary "Description"
        Événement déclenché lorsqu'un joueur déverrouille un nouveau biome.

        L'événement est annulable. L'annulation de l'événement empêchera l'utilisateur de déverrouiller l'objet biomesObject.

        Lien vers la classe : [BiomeUnlockedEvent](https://github.com/BentoBoxWorld/Biomes/blob/develop/src/main/java/world/bentobox/biomes/events/BiomeUnlockedEvent.java)

    !!! summary "Depuis"
        L'événement est ajouté dans la version Biomes 2.0.

    !!! question "Variables"
        - `@NotNull BiomesObject biomesObject` - l'objet biomesObject qui est déverrouillé.
        - `@Nullable User user` - l'utilisateur qui déverrouille le biomesObject.
        - `@NotNull Island island` - l'île sur laquelle le biomesObject est déverrouillé.

    !!! example "Exemple de code"
        ```java
        @EventHandler(priority = EventPriority.LOW)
        public void onBiomesUnlock(BiomeUnlockedEvent event) {
            User user = event.getUser();
            BiomesObject biomesOjbect = event.getBiomesObject();
            Island island = event.getIsland();

            // There is also converted methods, that do not use Biomes Addon objects.
            UUID userUUID = event.getUserUUID();
            String islandUUID = event.getIslandUUID();
            String biomeId = event.getBiomeId();
            Biome biome = event.getBiome();

            event.setCancelled(false);
        }
        ```

=== "BiomePurchasedEvent"
    !!! summary "Description"
        Événement déclenché lorsqu'un joueur achète un nouveau biome.

        L'événement est uniquement informatif. Impossible à annuler.

        Lien vers la classe : [BiomePurchasedEvent](https://github.com/BentoBoxWorld/Biomes/blob/develop/src/main/java/world/bentobox/biomes/events/BiomePurchasedEvent.java)

    !!! summary "Depuis"
        L'événement est ajouté dans la version Biomes 2.0.

    !!! question "Variables"
        - `@NotNull BiomesObject biomesObject` - l'objet biomesObject qui est acheté.
        - `@NotNull User user` - l'utilisateur qui achète le biomesObject.
        - `@NotNull Island island` - l'île sur laquelle le biomesObject est acheté.

    !!! example "Exemple de code"
        ```java
        @EventHandler(priority = EventPriority.MONITOR)
        public void onBiomesPurchase(BiomePurchasedEvent event) {
            User user = event.getUser();
            BiomesObject biomesOjbect = event.getBiomesObject();
            Island island = event.getIsland();

            // There is also converted methods, that do not use Biomes Addon objects.
            UUID userUUID = event.getUserUUID();
            String islandUUID = event.getIslandUUID();
            String biomeId = event.getBiomeId();
            Biome biome = event.getBiome();
        }
        ```

=== "BiomePreChangeEvent"
    !!! summary "Description"
        Événement déclenché avant le retrait des éléments et le changement du biome dans la zone.

        L'événement est uniquement informatif. Impossible à annuler.

        Lien vers la classe : [BiomePreChangeEvent](https://github.com/BentoBoxWorld/Biomes/blob/develop/src/main/java/world/bentobox/biomes/events/BiomePreChangeEvent.java)

    !!! summary "Depuis"
        L'événement est ajouté dans la version Biomes 2.0.

    !!! question "Variables"
        - `@NotNull BiomesObject biomesObject` - l'objet biomesObject qui est utilisé.
        - `@Nullable User user` - l'utilisateur qui a déclenché le changement de biome.
        - `@NotNull Island island` - l'île sur laquelle le biome est modifié.
        - `@NotNull BlockVector minCoordinate` - la coordonnée minimale pour le changement de biome.
        - `@NotNull BlockVector maxCoordinate` - la coordonnée maximale pour le changement de biome.

    !!! example "Exemple de code"
        ```java
        @EventHandler(priority = EventPriority.MONITOR)
        public void onBiomesPreChange(BiomePreChangeEvent event) {
            User user = event.getUser();
            BiomesObject biomesOjbect = event.getBiomesObject();
            Island island = event.getIsland();

            BlockVector minCoordinate = event.getMinCoordinate();
            BlockVector maxCoordinate = event.getMaxCoordinate();

            // There is also converted methods, that do not use Biomes Addon objects.
            UUID userUUID = event.getUserUUID();
            String islandUUID = event.getIslandUUID();
            String biomeId = event.getBiomeId();
            Biome biome = event.getBiome();

            int minX = event.getMinX();
            int minY = event.getMinY();
            int minZ = event.getMinZ();

            int maxX = event.getMaxX();
            int maxY = event.getMaxY();
            int maxZ = event.getMaxZ();
        }
        ```


=== "BiomeChangedEvent"
    !!! summary "Description"
        Événement déclenché après que le biome soit modifié sur toute la zone. Il est déclenché même si le changement de biome a échoué.

        L'événement est uniquement informatif. Impossible à annuler.

        Lien vers la classe : [BiomeChangedEvent](https://github.com/BentoBoxWorld/Biomes/blob/develop/src/main/java/world/bentobox/biomes/events/BiomeChangedEvent.java)

    !!! summary "Depuis"
        L'événement est ajouté dans la version Biomes 2.0.

    !!! question "Variables"
        - `@NotNull BiomesObject biomesObject` - l'objet biomesObject qui a été utilisé.
        - `@Nullable User user` - l'utilisateur qui a déclenché le changement de biome.
        - `@NotNull Island island` - l'île sur laquelle le biome a été modifié.
        - `@NotNull BlockVector minCoordinate` - la coordonnée minimale pour le changement de biome.
        - `@NotNull BlockVector maxCoordinate` - la coordonnée maximale pour le changement de biome.
        - `@Nullable Result result` - la valeur du résultat après le changement de biome. Les valeurs du résultat peuvent être :
                                        - FINISHED: le changement de biomes a été réussi.
                                        - TIMEOUT: le changement de biomes a pris plus longtemps que la valeur du délai d'expiration et a échoué.
                                        - FAILED: le changement de biomes a échoué pour une autre raison.

    !!! example "Exemple de code"
        ```java
        @EventHandler(priority = EventPriority.MONITOR)
        public void onBiomeChanged(BiomeChangedEvent event) {
            User user = event.getUser();
            BiomesObject biomesOjbect = event.getBiomesObject();
            Island island = event.getIsland();

            BlockVector minCoordinate = event.getMinCoordinate();
            BlockVector maxCoordinate = event.getMaxCoordinate();

            Result result = event.getResult();

            // There is also converted methods, that do not use Biomes Addon objects.
            UUID userUUID = event.getUserUUID();
            String islandUUID = event.getIslandUUID();
            String biomeId = event.getBiomeId();
            Biome biome = event.getBiome();

            int minX = event.getMinX();
            int minY = event.getMinY();
            int minZ = event.getMinZ();

            int maxX = event.getMaxX();
            int maxY = event.getMaxY();
            int maxZ = event.getMaxZ();

            String resultName = event.getResultName();
        }
        ```

### Gestionnaires de demandes d'addon

Jusqu'à BentoBox 1.17, nous avions un problème pour accéder aux données en dehors de l'environnement BentoBox en raison du chargeur de classe que nous utilisions pour charger les addons.
Cela signifiait que les données n'étaient accessibles que d'autres addons. Mais BentoBox a implémenté la fonctionnalité PlAddon, ce qui signifie que les gestionnaires de demandes ne sont plus nécessaires.


=== "biome-data"
    !!! summary "Description"
        Renvoie une `Map<String, Object>` contenant toutes les informations sur le biome demandé.

    !!! question "Entrée"
        - `biomeId`: String - l'ID unique du biome demandé.

    !!! success "Sortie"
        La sortie est une `Map<String, Object>` avec les clés suivantes :

        - `uniqueId`: String - l'ID unique du biome demandé.
        - `world`: String - le nom du monde où le biome est disponible.
        - `biome`: String - le nom du biome Minecraft correspondant.
        - `name`: String - le nom d'affichage pour le biome.
        - `deployed`: Boolean - `true` si le biome est déployé, `false` sinon.
        - `description`: List&lt;String&gt; - la description pour le biome.
        - `icon`: ItemStack - l'élément qui représente le biome dans les interfaces graphiques.
        - `order`: Integer - le numéro de commande pour le biome donné.
        - `cost`: Integer - le coût d'utilisation du biome.
        - `level`: Long - le niveau d'île minimum requis pour utiliser le biome.
        - `permissions`: Set&lt;String&gt; - la liste des permissions requises pour utiliser le biome.

    !!! failure
        Ce gestionnaire retournera une carte vide si le `biomeId` n'a pas été fourni ou si le `biomeId` n'a pas pu être trouvé dans la base de données.

    !!! example "Exemple de code"
        ```java
        public Map<String, Object> getBiomeData(String biomeId) {
            return (Map<String, Object>) new AddonRequestBuilder()
                .addon("Biomes")
                .label("biome-data")
                .addMetaData("biomeId", biomeId)
                .request();
        }
        ```

=== "biomes-list"
    !!! summary "Description"
        Renvoie une liste de tous les ID uniques des biomes définis dans un monde donné.

    !!! question "Entrée"
        - `world-name`: String - le nom du monde.

    !!! success "Sortie"
        La sortie est une `List<String>` contenant la liste des uniqueIds des biomes définis pour le monde spécifié.

    !!! failure
        Ce gestionnaire retournera une liste vide si le `world-name` n'a pas été fourni ou si le `world-name` n'existe pas ou n'est pas un monde du mode de jeu.

    !!! example "Exemple de code"
        ```java
        public List<String> getBiomesList(String worldName) {
            return (List<String>) new AddonRequestBuilder()
                .addon("Biomes")
                .label("biomes-list")
                .addMetaData("world-name", worldName)
                .request();
        }
        ```

=== "biome-request-change"
    !!! summary "Description"
        Demande un changement de biome avec les paramètres fournis.

    !!! question "Entrée"
        - Paramètres obligatoires :
            - `player`: UUID - l'UUID du joueur ciblé.
            - `world-name`: String - le nom du monde où le biome sera modifié.
            - `biomeId`: String - l'uniqueId du biome.
        - Paramètres optionnels :
            - `updateMode`: String - le mode à utiliser lors de la modification du biome.
                                     Peut être ISLAND, RANGE ou CHUNK.
                                     (Défaut: config)
            - `range`: Integer - la plage dans laquelle le biome sera modifié.
                                 (Défaut: config)
            - `checkRequirements`: Boolean - si `true`, le joueur devra remplir toutes les conditions du biome spécifié.
                                   (Défaut: true)
            - `withdraw`: Boolean - si `true`, l'argent sera retiré du compte bancaire du joueur.
                          (Défaut: true)

    !!! success "Sortie"
        La sortie est une `Map<String, Object>` avec les clés suivantes :

        - `status`: Boolean - `true` si le biome a été modifié avec succès, `false` sinon.
        - `reason`: String - message expliquant ce qui s'est passé (si la modification a réussi ou non).

    !!! failure
        Ce gestionnaire retournera `false` comme son statut avec une raison appropriée s'il a échoué.

    !!! example "Exemple de code"
        ```java
        public Map<String, Object> requestBiomeChange(UUID player, String worldName, String biomeId, String mode, int range, boolean requirements, boolean withdraw) {
            return (Map<String, Object>) new AddonRequestBuilder()
                .addon("Biomes")
                .label("biome-request-change")
                .addMetaData("player", player)
                .addMetaData("world-name", worldName)
                .addMetaData("biomeId", biomeId)
                .addMetaData("updateMode", mode)
                .addMetaData("range", range)
                .addMetaData("checkRequirements", requirements)
                .addMetaData("withdraw", withdraw)
                .request();
        }
        ```
