# MagicCobblestoneGenerator

**MagicCobblestoneGenerator** transforme les générateurs de roche plats et ennuyeux en une source géniale et fiable de blocs configurables!

Créé et maintenu par [BONNe](https://github.com/BONNe).

{{ addon_description("MagicCobblestoneGenerator") }}

## Installation

1. Placez le fichier jar de l'addon dans le dossier des addons du plugin BentoBox
2. Redémarrez le serveur
3. Exécutez la commande `/[admincmd] generator` pour configurer l'addon

## Configuration

Par défaut, l'addon tente d'importer toutes les données du fichier modèle, pour simplifier la première configuration. De nombreux paramètres du addon sont exposés dans l'interface graphique Admin, cependant, certains ne le sont pas.
Les dernières options de configuration et leurs explications détaillées se trouvent [ici](https://github.com/BentoBoxWorld/MagicCobblestoneGenerator/blob/develop/src/main/resources/config.yml).

Les fichiers modèles sont principalement pour les utilisateurs qui n'aiment pas utiliser l'interface graphique d'édition en jeu. Cependant, le fichier modèle n'est pas automatiquement importé à chaque modification. Cela nécessite une importation via une commande ou l'interface graphique Admin.

??? question "Structure du fichier modèle"
    ```
    # Commencez à répertorier tous les niveaux de générateur.
    tiers:
      # Id unique pour le générateur. Utilisé dans le stockage interne et l'accès à chaque donnée du générateur.
      generator_unique_id:
        # Nom d'affichage pour les utilisateurs. Supporte les codes de couleur.
        # Valeur par défaut: generator_unique_id sans _
        name: "Something fancy"
        # Description en message de lore. Supporte les codes de couleur.
        # Peut être défini vide en remplaçant tout par [].
        # Valeur par défaut: []
        description: -|
          First Line Of lore Message
          &2Second Line Of lore Message
        # Icône utilisée dans les interfaces graphiques. Le nombre à la fin permet de spécifier la taille de la pile pour l'article.
        # Valeur par défaut: Paper.
        icon: "PAPER:1"
        # Type de générateur: COBBLESTONE, STONE ou BASALT. Auto-explicatif.
        # Valeur par défaut: COBBLESTONE
        type: COBBLESTONE
        # Indique si le générateur est le générateur par défaut. Les générateurs par défaut ignorent la section des conditions.
        # Il est activé pour chaque nouvelle île. Il ne peut y en avoir qu'un par type de générateur.
        # Valeur par défaut: false
        default: false
        # Les utilisateurs sélectionnent les générateurs actifs.
        # La priorité indique quel générateur sera utilisé
        # si plusieurs d'entre eux remplissent les conditions.
        # Valeur par défaut: 1
        priority: 1
        # Il existe plusieurs exigences qui peuvent être définies ici.
        requirements:
          # Peut définir le niveau d'île minimum pour que le générateur fonctionne. Addon de niveau requis.
          # Valeur par défaut: 0
          island-level: 10
          # Liste des permissions requises pour que les utilisateurs sélectionnent ce générateur.
          # Valeur par défaut: []
          required-permissions: []
          # Liste des biomes requis pour que le générateur fonctionne.
          # Vide signifie qu'il n'y a pas de limitation dans quel biome le générateur fonctionne.
          # Valeur par défaut: [].
          required-biomes: []
          # Coût pour acheter ce générateur. Nécessite Vault et n'importe quel plugin d'économie.
          # Actuellement implémenté en cliquant sur l'icône d'achat dans l'interface graphique de visualisation du générateur.
          # Valeur par défaut: 0
          purchase-cost: 5.0
        # Coût pour activer le niveau de générateur actuel. Nécessite Vault et n'importe quel plugin d'économie.
        # Sera payé uniquement lors du changement actif entre les générateurs.
        # Valeur par défaut: 0.
        activation-cost: 0.0
        # Matériaux et leurs chances. Utilisez les blocs réels s'il vous plaît.
        # La chance supporte n'importe quel nombre positif, y compris la valeur double.
        # Tout à la fin sera normalisé.
        # Valeur par défaut: []
        blocks:
          FIRST_BLOCK_NAME_ID: NUMBER
          SECOND_BLOCK_NAME_ID: NUMBER
        # Trésor qui a une chance d'être lâché quand le bloc est généré.
        # SEULEMENT à la génération, pas au cassage de bloc.
        # Valeur par défaut: []
        treasure:
          # Chance de 0 till 1. 0 - ne sera pas possible d'obtenir un trésor.
          # Valeur par défaut: 0
          chance: 0.001
          # Matériaux qui peuvent être lâchés. S'applique aux mêmes règles que la section des blocs.
          # Valeur par défaut: []
          material:
            FIRST_BLOCK_NAME_ID: NUMBER
            SECOND_BLOCK_NAME_ID: NUMBER
          # Montant maximal d'articles lâchés.
          # Il sera de 1 till montant défini.
          # Valeur par défaut: 1
          amount: 1
    
    # Commencez à répertorier tous les bundles
    bundles:
      # bundle_id
      bundle_unique_id:
        # Nom d'affichage pour les utilisateurs
        name: "Something fancy"
        # Description en message de lore. Supporte les codes de couleur.
        # Peut être défini vide en remplaçant tout par [].
        # Valeur par défaut: []
        description: -|
          First Line Of lore Message
          &2Second Line Of lore Message
        # Icône utilisée dans les interfaces graphiques. Le nombre à la fin permet de spécifier la taille de la pile pour l'article.
        # Valeur par défaut: Paper.
        icon: "PAPER:1"
        # Liste des générateurs auxquels le bundle aura accès.
        generators:
          - generator_id_1
          - generator_id_2
    ```

### Épuisement du générateur (limitation du débit)

Depuis **2.8.0** les générateurs peuvent être plafonnés pour ne produire qu'un nombre défini de blocs dans une période donnée avant de passer en cooldown — utile pour décourager les fermes AFK entièrement automatisées. La fonctionnalité est **opt-in et désactivée par défaut** (une limite de `0`), donc les configurations existantes ne sont pas affectées jusqu'à ce que vous l'activiez. Quand un générateur est temporairement en cooldown, les joueurs reçoivent un message `generator-exhausted`.

=== "exhaustion.limit"
    !!! summary "Description"
        Le nombre par défaut de blocs qu'un générateur peut produire au cours d'une seule période d'épuisement. `0` ou moins désactive la limitation (la valeur par défaut). Chaque niveau de générateur peut remplacer ceci via la clé `exhaustion-limit` par niveau (voir ci-dessous).

        Défaut : `0`

=== "exhaustion.period"
    !!! summary "Description"
        La durée de la période d'épuisement, en **minutes**. Le comptage des blocs se réinitialise à la fin de chaque période.

        Défaut : `60`

=== "exhaustion.cooldown"
    !!! summary "Description"
        Combien de temps, en **minutes**, un générateur reste en cooldown après avoir atteint sa limite d'épuisement.

        Défaut : `1440` (24 heures)

=== "exhaustion.notification-cooldown"
    !!! summary "Description"
        Le temps minimum, en **secondes**, entre deux messages d'avertissement d'épuisement affichés au même joueur.

        Défaut : `60`

!!! tip "Limite par niveau"
    Chaque niveau de générateur peut remplacer la limite globale avec une clé `exhaustion-limit` dans le modèle de générateur (et dans l'interface graphique admin), de sorte que différents niveaux peuvent être étranglés indépendamment.

### Plages de hauteur par bloc

Également depuis **2.8.0**, les générateurs — et les blocs individuels au sein d'un générateur — peuvent être limités à un niveau Y minimum et maximum, de sorte que différents matériaux sont produits à différentes hauteurs. De nouveaux boutons de l'interface graphique permettent aux admins de définir et d'effacer la plage, et la lore du générateur montre aux joueurs où chaque générateur opère. Les modèles hérités sans plage de hauteur restent pleinement compatibles.

## Commandes

!!! tip
    `[player_command]` et `[admin_command]` sont les commandes qui diffèrent selon le mode de jeu que vous exécutez.
    Le fichier `config.yml` des Gamemodes contient des options qui vous permettent de modifier ces valeurs.
    Par exemple, sur BSkyBlock, le `[player_command]` par défaut est `island`, et l'`[admin_command]` par défaut est `bsbadmin`.
    Attention, cet addon permet de modifier les alias des commandes joueur dans le fichier `config.yml` de l'addon.

=== "Commandes joueur"
    - `/[player_command] generator`: Accédez à l'interface graphique de sélection du générateur.
    - `/[player_command] generator view <generator>`: Accédez à la vue détaillée d'un générateur spécifique.
    - `/[player_command] generator activate <generator> [false]`: Permet d'activer (ou désactiver) un générateur spécifique.
    - `/[player_command] generator buy <generator>`: Permet d'acheter un générateur spécifique.

=== "Commandes admin"
    - `/[admin_command] generator`: Accédez à l'interface graphique admin de l'addon
    - `/[admin_command] generator import`: Importe le fichier modèle par défaut - `/plugins/BentoBox/addons/MagicCobblestoneGenerator/generatorTemplate.yml`.
    - `/[admin_command] generator database import <file>`: Permet d'importer la base de données exportée <file>.
    - `/[admin_command] generator database export <file>`: Permet d'exporter la base de données dans <file> sauvegardé dans le dossier `/plugins/BentoBox/addons/MagicCobblestoneGenerator/`.
    - `/[admin_command] generator why <player>`: Une commande de débogage qui permet de trouver les problèmes avec les générateurs pour chaque joueur.

## Permissions

!!! tip
    `[gamemode]` est un préfixe qui diffère selon le mode de jeu que vous exécutez.
    Le préfixe est le nom du mode de jeu en minuscules, c'est-à-dire si vous utilisez BSkyBlock, le préfixe est `bskyblock`.
    De même, si vous utilisez AcidIsland, le préfixe est `acidisland`.

=== "Permissions joueur"
    - `[gamemode].stone-generator` - Permet au joueur d'utiliser la commande '/[player_command] generator' et ses sous-commandes.
    - `[gamemode].stone-generator.active-generators.3` - Définit le nombre maximum de générateurs actifs que le propriétaire de l'île peut avoir. 3 peut être remplacé par n'importe quel entier positif. Ceci n'est qu'un exemple.
    - `[gamemode].stone-generator.max-range.30` - Définit la distance maximale du générateur pour qu'il continue de fonctionner. 30 peut être remplacé par n'importe quel entier positif. Ceci n'est qu'un exemple.
    - `[gamemode].stone-generator.bundle.[bundle_id]` - Spécifie quel bundle sera utilisé pour l'île possédée par l'utilisateur.
    
=== "Permissions admin"
    - `[gamemode].admin.stone-generator` - Permet au joueur d'utiliser la commande '/[admin_command] generator' et ses sous-commandes.
    - `[gamemode].admin.stone-generator.why` - Permet au joueur d'utiliser la commande de débogage '/[admin_command] why generator <player>'.
    - `[gamemode].admin.stone-generator.database` - Permet au joueur d'utiliser la commande '/[admin_command] generator database' et ses sous-commandes.
    
??? question "Quelque chose manque?"
    Vous pouvez trouver la liste complète des permissions dans le fichier [addon.yml](https://github.com/BentoBoxWorld/MagicCobblestoneGenerator/blob/develop/src/main/resources/addon.yml) de cet addon.  
    Si quelque chose manque effectivement à la liste ci-dessous, veuillez nous le signaler!


## Placeholders

{{ placeholders_source(source="MagicCobblestoneGenerator") }}


## FAQ

??? question "Pouvez-vous ajouter une fonctionnalité X?"
    Veuillez l'ajouter à la liste [ici](https://github.com/BentoBoxWorld/MagicCobblestoneGenerator/issues).

??? question "Comment puis-je ajouter un nouveau niveau de générateur?"
    Actuellement, l'addon supporte 3 façons d'ajouter un nouveau générateur:
    
    - En utilisant l'interface graphique en jeu disponible via la commande `/[admin] generator`.
    - En ajoutant le générateur au fichier modèle.
    - En ajoutant le générateur au fichier de base de données exporté.

??? question "J'ai ajouté un générateur au fichier modèle/base de données, mais il n'apparaît pas en jeu."
    Pour faciliter la configuration avec plusieurs modes de jeu, les générateurs sont stockés dans la base de données interne. Après avoir modifié le fichier modèle ou de base de données, vous devez les importer dans cette mémoire. Vous pouvez le faire via l'interface graphique Admin en cliquant sur les boutons `Import Template` ou `Import Database`.
    
    ![modèle](resources/import_template.png){: loading=lazy }
    ![base de données](resources/import_database.png){: loading=lazy }

??? question "J'ai un générateur qui s'affiche dans l'interface graphique Admin, mais les joueurs ne le voient pas."
    C'est probablement dû au statut de "déploiement". Pour éviter les problèmes quand les joueurs commencent à activer les générateurs tandis qu'un admin les ajoute, les générateurs ne sont pas déployés et personne ne peut les utiliser. Vous pouvez les activer en modifiant le générateur via l'interface graphique Admin et en cliquant sur le levier dans l'interface graphique Editer le Générateur.
    ![déployé](resources/deployed.png){: loading=lazy }

??? question "Qu'est-ce que les trésors?"
    Les trésors sont des choses qui sont lâchées lors de la génération de bloc. Cela permet de donner une personnalisation supplémentaire pour chaque générateur.

??? question "Qu'est-ce que les bundles?"
    Les bundles sont une fonctionnalité qui permet de personnaliser davantage l'expérience pour chaque île. Si un bundle est attribué à une île, alors les joueurs de cette île ne pourront utiliser que les générateurs de ce bundle.

??? question "Puis-je désactiver l'affichage des permissions requises dans la description du générateur?"
    Oui, l'addon fournit beaucoup d'options de personnalisation pour afficher chaque générateur. Il est situé dans le fichier de locales:
    ```
          # Générateur de message de lore de générateur. Tous les éléments de la lore du générateur sont générés
          # basé sur la section ci-dessous.
          generator:
            # Contenu du principal élément de lore. Si vous ne voulez pas afficher les trésors du tout,
            # supprimez-les simplement de la section [treasures].
            # [description] provient de chaque niveau de générateur.
            # Lore ne supporte pas les codes de couleur. Chaque objet supporte séparément.
            lore: |-
              [description]
              [blocks]
              [treasures]
              [type]
              [requirements]
              [status]
            # Génère la section [blocks]
            blocks:
              # Première ligne dans la section des blocs. La ligne vide ne s'affichera pas.
              title: "&7&l Blocks:"
              # Chaque bloc et sa valeur sous le titre. Ne peut pas être vide.
              # Supporte [number], [#.#], [#.##], [#.###], [#.####], [#.#####]
              value: "&8 [material] - [#.##]%"
            # Génère la section [treasures]
            treasures:
              # Première ligne dans la section des blocs. La ligne vide ne s'affichera pas.
              title: "&7&l Treasures:"
              # Chaque trésor et sa valeur sous le titre. Ne peut pas être vide.
              # Supporte [number], [#.#], [#.##], [#.###], [#.####], [#.#####]
              value: "&8 [material] - [#.####]%"
            # Génère la section [requirements]
            requirements:
              # Permet de modifier l'ordre et le contenu du message des exigences.
              description: |-
                [biomes]
                [level]
                [missing-permissions]
              # Génère le message [level].
              level: "&c&l Required Level: &r&c [number]"
              # Génère le titre du message [missing-permission].
              permission-title: "&c&l Missing Permissions:"
              # Génère les valeurs du message [missing-permission].
              permission: "&c  -[permission]"
              # Génère le titre du message [biomes].
              biome-title: "&7&l Operates in:"
              # Génère les valeurs du message [biomes].
              biome: "&8 [biome]"
              # Génère le message [biomes] pour Tous les Biomes.
              any: "&7&l Operates in &e&o all &r&7&l biomes"
            # Génère la section [status]
            status:
              # Message affiché pour les générateurs verrouillés.
              locked: "&c Locked!"
              # Message affiché pour les générateurs qui ne sont pas déployés.
              undeployed: "&c Not Deployed!"
              # Message affiché pour les générateurs actifs.
              active: "&2 Active"
              # Message affiché pour les générateurs qui nécessitent un achat.
              purchase-cost: "&e Purchase Cost: $[number]"
              # Message affiché pour les générateurs qui ont un coût d'activation.
              activation-cost: "&e Activation Cost: $[number]"
            # Génère la section [type]
            type:
              title: "&7&l Supports:"
              cobblestone: "&8 Cobblestone Generators"
              stone: "&8 Stone Generators"
              basalt: "&8 Basalt Generators"
              any: "&7&l Supports &e&o all &r&7&l generators"
    ```

## Journal des modifications

!!! warning "Nouveautés dans v2.8.0 — nécessite BentoBox 3.14.0 / Java 21"
    **Publié :** 3 juillet 2026

    - ⚙️ **Épuisement du générateur.** Limitation optionnelle du nombre de blocs qu'un générateur produit par période, avec un cooldown une fois la limite atteinte. Configurable globalement (`exhaustion.*` dans `config.yml`) et par niveau de générateur (`exhaustion-limit` dans le modèle). Opt-in et désactivé par défaut. Voir la section Configuration ci-dessus.
    - **Plages de hauteur par bloc.** Limitez les générateurs et les blocs individuels à un niveau Y minimum/maximum, avec de nouveaux contrôles de l'interface graphique et une lore de face utilisateur.
    - 🔡 **Nouveaux placeholders** `[gamemode]_magiccobblestonegenerator_generator_exhaustion_status` et `[gamemode]_magiccobblestonegenerator_exhausted_generator_names` exposent l'état d'épuisement.
    - 🔡 🔺 **Locales MiniMessage + 13 nouvelles langues.** Chaque fichier de locale a été converti des codes couleur `&` legacy vers MiniMessage (que BentoBox 3.14 rend nativement), et des traductions ont été ajoutées pour cs, hr, hu, id, it, ja, ko, lv, nl, pt, pt-BR, ro et zh-HK — 24 locales au total, correspondant à BentoBox core. Si vous avez conservé vos propres modifications à n'importe quel fichier `locales/*.yml`, réappliquez-les au format MiniMessage (ou supprimez le fichier pour régénérer un frais).
    - 🔺 **Modernisé pour BentoBox 3.14 / Java 21.** Mis à jour vers l'API BentoBox et Paper actuels, avec la suite de tests migrée vers MockBukkit. Cette version ne se chargera pas sur les anciennes versions de BentoBox ou Java — mettez d'abord à jour BentoBox.

    [Release v2.8.0](https://github.com/BentoBoxWorld/MagicCobblestoneGenerator/releases/tag/2.8.0)

## Traductions

{{ translations("MagicCobblestoneGenerator") }}

## API

Depuis MagicCobblestoneGenerator 2.4.0 et BentoBox 1.17, d'autres plugins peuvent accéder directement aux données du addon MagicCobblestoneData. Cependant, les demandes d'addon restent toujours une bonne solution pour les plugins qui ne veulent pas utiliser trop de dépendances.

### Dépendance Maven
MagicCobblestoneGenerator fournit une API pour les autres plugins. Cela couvre la version 2.5.0 et ultérieures.

!!! note
    Ajoutez la dépendance MagicCobblestoneGenerator à votre Maven POM.xml:

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
                <artifactId>magiccobblestonegenerator</artifactId>
                <version>2.5.0</version>
                <scope>provided</scope>
            </dependency>
        </dependencies>
    ```
Utilisez la dernière version de MagicCobblestoneGenerator.

La JavaDoc pour MagicCobblestoneGenerator peut être trouvée [ici](https://ci.codemc.io/job/BentoBoxWorld/job/MagicCobblestoneGenerator/ws/target/apidocs/index.html).

### Événements

=== "GeneratorActivationEvent"
    !!! summary "Description"
        Événement qui est déclenché quand un joueur active/désactive un générateur sur son île.
        Cet événement est annulable.

        Lien vers la classe: [GeneratorActivationEvent](https://github.com/BentoBoxWorld/MagicCobblestoneGenerator/blob/develop/src/main/java/world/bentobox/magiccobblestonegenerator/events/GeneratorActivationEvent.java)

    !!! question "Variables"
        - `String islandUUID` - l'ID de l'île ciblée.
        - `UUID targetPlayer` - l'ID du joueur qui a déclenché l'activation du générateur.
        - `String generator` - le nom du générateur activé.
        - `String generatorID` - l'ID du générateur activé.
        - `boolean activate` - le booléen qui indique si le générateur est activé ou désactivé.

        
    !!! example "Exemple de code"
        ```java
        @EventHandler(priority = EventPriority.LOW)
        public void onGeneratorActivationChange(GeneratorActivationEvent event) {
            UUID user = event.getTargetPlayer();
            String island = event.getIslandUUID();

            String generator = event.getGenerator();
            String generatorID = event.getGeneratorID();
            boolean activate = event.isActivate();
        }
        ```

=== "GeneratorUnlockEvent"
    !!! summary "Description"
        Événement qui est déclenché quand un joueur déverrouille un nouveau générateur sur son île.
        Cet événement est annulable.

        Lien vers la classe: [GeneratorUnlockEvent](https://github.com/BentoBoxWorld/MagicCobblestoneGenerator/blob/develop/src/main/java/world/bentobox/magiccobblestonegenerator/events/GeneratorUnlockEvent.java)

    !!! question "Variables"
        - `String islandUUID` - l'ID de l'île ciblée.
        - `UUID targetPlayer` - l'ID du joueur qui a déclenché le déverrouillage du générateur.
        - `String generator` - le nom du générateur déverrouillé.
        - `String generatorID` - l'ID du générateur déverrouillé.

        
    !!! example "Exemple de code"
        ```java
        @EventHandler(priority = EventPriority.LOW)
        public void onGeneratorUnlock(GeneratorUnlockEvent event) {
            UUID user = event.getTargetPlayer();
            String island = event.getIslandUUID();

            String generator = event.getGenerator();
            String generatorID = event.getGeneratorID();
        }
        ```

=== "GeneratorBuyEvent"
    !!! summary "Description"
        Événement qui est déclenché quand un joueur achète un nouveau générateur sur son île.
        Cet événement n'est PAS annulable.

        Lien vers la classe: [GeneratorBuyEvent](https://github.com/BentoBoxWorld/MagicCobblestoneGenerator/blob/develop/src/main/java/world/bentobox/magiccobblestonegenerator/events/GeneratorBuyEvent.java)

    !!! question "Variables"
        - `String islandUUID` - l'ID de l'île ciblée.
        - `UUID targetPlayer` - l'ID du joueur qui a acheté le générateur.
        - `String generator` - le nom du générateur acheté.
        - `String generatorID` - l'ID du générateur acheté.

        
    !!! example "Exemple de code"
        ```java
        @EventHandler(priority = EventPriority.LOW)
        public void onGeneratorBuy(GeneratorBuyEvent event) {
            UUID user = event.getTargetPlayer();
            String island = event.getIslandUUID();

            String generator = event.getGenerator();
            String generatorID = event.getGeneratorID();
        }
        ```

### Gestionnaires de demandes d'addon

Jusqu'à BentoBox 1.17, nous avions un problème d'accès aux données en dehors de l'environnement BentoBox en raison du chargeur de classe que nous utilisions pour charger les addons.
Cela signifiait que les données n'étaient accessibles que depuis d'autres addons. Mais BentoBox a mis en place la fonctionnalité PlAddon, ce qui signifie que les gestionnaires de demandes
ne sont plus nécessaires.

Plus d'informations sur les gestionnaires de demandes d'addon peuvent être trouvées [ici](/en/latest/BentoBox/Request-Handler-API---How-plugins-can-get-data-from-addons/)

=== "active-generator-names"
    !!! summary "Description"
        Retourne les noms des générateurs actifs pour le joueur.

        Depuis la version 2.4.0.

    !!! question "Entrée"
        - `world-name`: String - le nom du monde.
        - `player`: String - l'UUID du joueur.

    !!! success "Sortie"
        La sortie est une `List<String>` qui contient les noms des générateurs actifs.

    !!! failure
        Ce gestionnaire retournera null si `world-name` n'a pas été fourni ou si `world-name` n'existe pas ou si `player` n'est pas fourni.

    !!! example "Exemple de code"
        ```java
        public List<String> getActiveGeneratorNames(String worldName, UUID playerUUID) {
            return (List<String>) new AddonRequestBuilder()
                .addon("MagicCobblestoneGenerator")
                .label("active-generator-names")
                .addMetaData("world-name", worldName)
                .addMetaData("player", playerUUID)
                .request();
        }
        ```


=== "generator-data"
    !!! summary "Description"
        Retourne les données brutes stockées pour l'objet de générateur demandé. 

        Depuis la version 2.4.0.

    !!! question "Entrée"
        - `generator`: String - l'UUID du générateur.

    !!! success "Sortie"
        La sortie est une `Map<String, Object>` qui contient les données brutes du générateur.
        
        La carte de sortie contient:

        - `uniqueId`: String - l'ID unique du générateur. Devrait être le même que dans l'entrée.
        - `friendlyName`: String - le nom d'affichage du générateur (non formaté).
        - `description`: List<String> - la liste des chaînes pour le message lore (non formaté).
        - `generatorType`: String - le type du générateur. Types disponibles:

            - COBBLESTONE
            - STONE
            - BASALT
            - COBBLESTONE_OR_STONE
            - BASALT_OR_COBBLESTONE
            - BASALT_OR_STONE
            - ANY

        - `generatorIcon`: ItemStack - l'ItemStack de l'icône du générateur.
        - `lockedIcon`: ItemStack - l'ItemStack de l'icône du générateur verrouillé.
        - `defaultGenerator`: boolean - le booléen qui indique si le générateur est par défaut ou non.
        - `priority`: int - la valeur de priorité du générateur.
        - `requiredMinIslandLevel`: int - le niveau d'île minimum pour que le générateur fonctionne.
        - `requiredBiomes`: Set<Biome> - l'ensemble des biomes requis pour que le générateur fonctionne.
        - `requiredPermissions`: Set<String> - l'ensemble des permissions requises pour que le générateur soit achetable.
        - `generatorTierCost`: double - le prix du générateur.
        - `activationCost`: double - le prix d'activation du générateur.
        - `deployed`: boolean - le booléen qui indique si le générateur est disponible pour les joueurs.
        - `blockChanceMap`: TreeMap<Double, Material> - la carte qui contient les données brutes pour les chances de bloc.
        - `treasureItemChanceMap`: TreeMap<Double, ItemStack> - la carte qui contient les données brutes pour les chances de trésor.
        - `treasureChance`: double - la valeur du trésor à lâcher lors de la génération de bloc.
        - `maxTreasureAmount`: int - le montant maximal de trésors à lâcher à la fois.

    !!! failure
        Ce gestionnaire retournera null si `generator` n'a pas été fourni ou une carte vide si `generator` n'existe pas.

    !!! example "Exemple de code"
        ```java
        public Map<String, Object> getGeneratorData(String generatorId) {
            return (List<String>) new AddonRequestBuilder()
                .addon("MagicCobblestoneGenerator")
                .label("generator-data")
                .addMetaData("generator", generatorId)
                .request();
        }
        ```
