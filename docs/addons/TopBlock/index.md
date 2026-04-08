# TopBlock

Addon pour BentoBox pour calculer les niveaux des îles pour AOneBlock spécifiquement. Les classements sont déterminés par le nombre de blocs magiques qui ont été minés - le nombre.

Créé et maintenu par [tastybento](https://github.com/tastybento).

{{ addon_description("TopBlock") }}

## Installation

1. Placez le fichier jar du addon top block dans le dossier des addons du plugin BentoBox
2. Redémarrez le serveur
3. L'addon créera un dossier de données et à l'intérieur du dossier se trouvera un config.yml
4. Modifiez le config.yml comme vous le souhaitez.
5. Redémarrez le serveur si vous apportez une modification

## Configuration

L'addon TopBlock a 2 choses de configuration générale :

- fichier config.yml contient les fichiers de configuration du addon par défaut.
- /panels/ contient les fichiers qui gèrent les interfaces graphiques du joueur

### config.yml

Le fichier de configuration contient les principales fonctions du addon.

Le dernier config.yml se trouve [ici](https://github.com/BentoBoxWorld/TopBlock/blob/develop/src/main/resources/config.yml).

Cette section définit un certain nombre de paramètres généraux pour l'addon.

??? note "refresh-time"
    À quelle fréquence le Top Ten devrait être actualisé en minutes. Le minimum est 1 minute, le défaut est 5.
    Chaque actualisation nécessite la lecture de chaque île à partir de la base de données, donc cela ne devrait pas être fait trop souvent.

    Par défaut: `5`

??? note "shorthand"
    Permet d'afficher des numéros de niveau d'île plus courts.

    Affiche les grandes valeurs de niveau arrondies vers le bas, par exemple, 10 345 -> 10k

    Par défaut: `false`

### Interfaces graphiques personnalisables

BentoBox 1.17 API a introduit une fonction qui permet de mettre en œuvre des interfaces graphiques personnalisables. Nous avons essayé d'être aussi simples que possible pour la personnalisation, cependant, certaines fonctionnalités nécessitent une explication.
Vous pouvez trouver plus d'informations sur le fonctionnement des interfaces graphiques personnalisées de BentoBox ici : [Interfaces graphiques personnalisées](/en/latest/Tutorials/generic/Customizable-GUI/)

??? question "Comment puis-je personnaliser les interfaces graphiques"
     L'addon créera un nouveau répertoire sous `/plugins/bentobox/addons/topblock` portant le nom `panels`

    Actuellement, vous pouvez personnaliser les interfaces graphiques :

    - Panneau supérieur : `top_panel` - permet de voir les 10 meilleures îles.

??? question "Que fait le type de bouton `TOP`?"
    Ce bouton est disponible dans top_panel. Il affiche l'île au sommet X par le haut de l'île.

    L'`icon` par défaut sera `PLAYER_HEAD` avec une peau de joueur appropriée. L'activer le remplacera par le matériau spécifié.

    `index` dans le champ data permet de spécifier quel endroit du Top 10 devrait être affiché à la place actuelle.

    Le panneau supérieur a 2 actions implémentées dont la fonction nécessite un addon supplémentaire :

    - `warp` - nécessite l'addon Warps. Ne sera affiché que si un panneau de téléportation existe sur l'île des joueurs.
    - `visit` - nécessite l'addon Visit. Ne sera affiché que si la visite est autorisée sur l'île des joueurs.

    Fallback permet de changer l'icône de fond, quand il n'y a pas de joueur au sommet.

    Exemple:
    ```yaml
        #icon: PLAYER_HEAD
        title: topblock.gui.buttons.island.name
        description: topblock.gui.buttons.island.description
        data:
          type: TOP
          index: 1
        actions:
          warp:
            click-type: LEFT
            tooltip: topblock.gui.tips.click-to-warp
          visit:
            click-type: RIGHT
            tooltip: topblock.gui.tips.right-click-to-visit
        fallback:
          icon: LIME_STAINED_GLASS_PANE
          title: topblock.gui.buttons.island.empty
    ```

??? question "Que fait le type de bouton `VIEW`?"
    Ce bouton est disponible dans top_panel. Il affiche la valeur topblock de l'île du spectateur.

    L'`icon` par défaut sera `PLAYER_HEAD` avec une peau de joueur appropriée. L'activer le remplacera par le matériau spécifié.

    L'action `view` permet de voir le menu détaillé de l'île du joueur.

    Exemple:
    ```yaml
        #icon: PLAYER_HEAD
        title: topblock.gui.buttons.island.name
        description: topblock.gui.buttons.island.description
        data:
          type: VIEW
        actions:
          view:
            click-type: unknown
            tooltip: topblock.gui.tips.click-to-view
    ```

## Commandes

!!! tip
    `[player_command]` et `[admin_command]` sont des commandes qui diffèrent selon le mode de jeu que vous exécutez.
    Le fichier `config.yml` des modes de jeu contient des options qui vous permettent de modifier ces valeurs.
    Par exemple, sur BSkyBlock, la `[player_command]` par défaut est `island`, et la `[admin_command]` par défaut est `bsbadmin`.

=== "Commandes du joueur"
    - `/[player_command] topblock`: accès au panneau supérieur. Nécessite la permission `aoneblock.island.topblock`.

## Permissions

=== "Permissions du joueur"
    - `aoneblock.island.topblock` - (défaut: `true`) - Permet au joueur d'utiliser la commande `/[player_command] top`.

??? question "Quelque chose manque-t-il?"
    Vous pouvez trouver la liste complète des permissions dans le fichier [addon.yml](https://github.com/BentoBoxWorld/TopBlock/blob/develop/src/main/resources/addon.yml) de cet addon.
    Si quelque chose manque vraiment de la liste ci-dessous, veuillez nous le faire savoir!


## Placeholders

{{ placeholders_source(source="TopBlock") }}

## FAQ

??? question "Pouvez-vous ajouter une fonctionnalité X?"
    Veuillez l'ajouter à la liste [ici](https://github.com/BentoBoxWorld/TopBlock/issues).

## Traductions

{{ translations("TopBlock") }}

## API

### Dépendance Maven
TopBlock fournit une API pour d'autres plugins.

!!! note
    Ajoutez la dépendance TopBlock à votre Maven POM.xml :

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
                <artifactId>topblock</artifactId>
                <version>1.0.1</version>
                <scope>provided</scope>
            </dependency>
        </dependencies>
    ```

Les JavaDocs pour TopBlock peuvent être trouvés [ici](https://ci.codemc.io/job/BentoBoxWorld/job/TopBlock/ws/target/apidocs/index.html).
