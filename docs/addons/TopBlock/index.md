# TopBlock

Addon pour BentoBox qui produit un classement Top Ten pour les modes de jeu à blocs magiques. Les classements sont déterminés par le nombre de blocs magiques qui ont été minés - le nombre.

TopBlock supporte [**AOneBlock**](../../gamemodes/AOneBlock/index.md) et [**ChunkBlock**](../../gamemodes/ChunkBlock/index.md). Vous pouvez installer l'un ou l'autre ou les deux — quand les deux sont présents, chaque mode de jeu obtient son propre classement Top Ten entièrement séparé, sa propre commande `topblock`, et son propre ensemble d'espaces réservés. Le classement d'un joueur dans AOneBlock n'a aucune effet sur son classement dans ChunkBlock.

Créé et maintenu par [tastybento](https://github.com/tastybento).

{{ addon_description("TopBlock") }}

## Installation

1. Placez le fichier jar du addon top block dans le dossier des addons du plugin BentoBox
2. Redémarrez le serveur
3. L'addon créera un dossier de données et à l'intérieur du dossier se trouvera un config.yml
4. Modifiez le config.yml comme vous le souhaitez.
5. Redémarrez le serveur si vous apportez une modification

!!! note "TopBlock n'est pas autonome"
    TopBlock nécessite **au moins un** de [AOneBlock](../../gamemodes/AOneBlock/index.md) ou [ChunkBlock](../../gamemodes/ChunkBlock/index.md) soit installé avec. Si aucun n'est trouvé, TopBlock enregistre une erreur et se désactive. Il se branche à celui des deux qu'il trouve au démarrage, donc installer ou supprimer un mode de jeu plus tard n'a d'effet qu'après un redémarrage.

## Configuration

L'addon TopBlock a 2 choses de configuration générale :

- fichier config.yml contient les fichiers de configuration du addon par défaut.
- /panels/ contient les fichiers qui gèrent les interfaces graphiques du joueur

### config.yml

Le fichier de configuration contient les principales fonctions du addon.

Le dernier config.yml se trouve [ici](https://github.com/BentoBoxWorld/TopBlock/blob/develop/src/main/resources/config.yml).

Cette section définit un certain nombre de paramètres généraux pour l'addon. Ces paramètres sont globaux — ils s'appliquent à chaque mode de jeu auquel TopBlock s'est branché. Il n'y a pas de configuration par mode de jeu.

??? note "refresh-time"
    À quelle fréquence le Top Ten devrait être actualisé en minutes. Le minimum est 1 minute, le défaut est 5.
    Chaque actualisation nécessite la lecture de chaque île de chaque mode de jeu auquel le addon s'est branché à partir de la base de données, donc cela ne devrait pas être fait trop souvent (depuis 2.1.1 cette lecture s'exécute en dehors du thread principal, donc elle ne provoque plus de pics de lag). Si vous utilisez à la fois AOneBlock et ChunkBlock, chaque actualisation lit les deux ensembles d'îles, donc envisagez de laisser ceci à la valeur par défaut ou de l'augmenter.

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
    - `/[player_command] topblock`: accès au panneau supérieur. Nécessite la permission `island.topblock` pour ce mode de jeu (`aoneblock.island.topblock` ou `chunkblock.island.topblock`).

TopBlock enregistre la sous-commande `topblock` sur **chaque** mode de jeu auquel il se branche, donc avec les deux installés vous obtenez `/ob topblock` pour AOneBlock et l'équivalent sous la commande joueur de ChunkBlock. Chacun ouvre le panneau pour le mode de jeu du monde dans lequel vous l'avez exécuté — les deux classements sont entièrement séparés.

## Permissions

=== "Permissions du joueur"
    - `aoneblock.island.topblock` - (défaut: `true`) - Permet au joueur d'utiliser la commande `/[player_command] topblock` dans AOneBlock.
    - `aoneblock.intopten` - (défaut: `true`) - Contrôle si l'île du joueur apparaît dans le top ten d'AOneBlock. Supprimez d'un admin ou testeur pour le exclure du classement.
    - `chunkblock.island.topblock` - (défaut: `true`) - Permet au joueur d'utiliser la commande `/[player_command] topblock` dans ChunkBlock.
    - `chunkblock.intopten` - (défaut: `true`) - Contrôle si l'île du joueur apparaît dans le top ten de ChunkBlock.

??? question "Comment masquer un joueur du classement?"
    Supprimez (ou niez) la permission `intopten` pour le mode de jeu dont vous voulez le masquer — `aoneblock.intopten` ou `chunkblock.intopten`. Parce que le préfixe est par mode de jeu, vous pouvez masquer quelqu'un d'un classement tout en le laissant visible dans l'autre.

    Deux choses à connaître :

    - La permission est uniquement vérifiée pendant que le propriétaire de l'île **est en ligne**. Les propriétaires hors ligne sont toujours inclus, car Bukkit ne peut pas évaluer de manière fiable les permissions pour un joueur qui n'est pas connecté. Donc supprimez la permission du compte qui se connecte réellement, pas d'un alt.
    - Seule la permission du **propriétaire de l'île** est vérifiée. Les permissions des membres de l'équipe n'ont aucune importance.

    Le changement prend effet à la prochaine actualisation, donc accordez jusqu'à `refresh-time` minutes pour que l'île disparaisse de la liste.

??? question "Quelque chose manque-t-il?"
    Vous pouvez trouver la liste complète des permissions dans le fichier [addon.yml](https://github.com/BentoBoxWorld/TopBlock/blob/develop/src/main/resources/addon.yml) de cet addon.
    Si quelque chose manque vraiment de la liste ci-dessous, veuillez nous le faire savoir!


## Placeholders

Les espaces réservés sont enregistrés séparément pour chaque mode de jeu auquel TopBlock s'est branché, en utilisant le propre préfixe de ce mode de jeu. L'ensemble `chunkblock_` n'existe que si ChunkBlock est installé, et rapporte le propre classement de ChunkBlock — les deux ne se mélangent jamais.

{{ placeholders_source(source="TopBlock") }}

## FAQ

??? question "Pouvez-vous ajouter une fonctionnalité X?"
    Veuillez l'ajouter à la liste [ici](https://github.com/BentoBoxWorld/TopBlock/issues).

## Changelog

??? note "Nouveautés dans v2.1.1"
    **Publié :** 27 août 2026

    Version de correctif — aucun changement de configuration, locale ou format de données ; un remplacement direct pour 2.1.0.

    - 🐛 **L'actualisation du top ten n'immobilise plus le thread principal.** La tâche d'actualisation (tous les `refresh-time` minutes, défaut 5) lisait la base de données complète de l'île du mode de jeu de manière synchrone sur le thread principal — jusqu'à ~1 seconde par cycle sur les serveurs avec de nombreuses îles, et deux fois quand à la fois AOneBlock et ChunkBlock étaient branchés — causant des pics de lag périodiques. La lecture de la base de données s'exécute maintenant de manière asynchrone ; seules les recherches bon marché d'île et de permission restent sur le thread principal.

    [Release v2.1.1](https://github.com/BentoBoxWorld/TopBlock/releases/tag/2.1.1)

??? note "Nouveautés dans v2.1.0 — Support de ChunkBlock"
    **Publié :** 21 août 2026

    TopBlock n'est plus réservé à AOneBlock. Il supporte maintenant **ChunkBlock** aussi, et l'un ou l'autre mode de jeu — ou les deux ensemble — peut être installé. Compatibilité : API BentoBox 3.14.0+ · AOneBlock 1.18.0+ et/ou ChunkBlock 1.0.1+ · Paper Minecraft 1.21.x · Java 21.

    - ✨ **Support de ChunkBlock.** TopBlock se branche à celui d'AOneBlock et ChunkBlock qu'il trouve au démarrage. Avec les deux installés, chacun garde un top ten entièrement séparé, une commande `topblock`, et un ensemble d'espaces réservés.
    - ✨ **Nouveaux espaces réservés** — l'ensemble complet `%chunkblock_island_*_top_<number>%`, reflétant les existants `aoneblock_` et rapportant le propre classement de ChunkBlock.
    - ✨ **Nouvelles permissions** — `chunkblock.island.topblock` et `chunkblock.intopten`, tous deux par défaut `true`, reflétant les équivalents AOneBlock. Parce que le préfixe est par mode de jeu, vous pouvez masquer un joueur d'un classement tout en le laissant visible dans l'autre.
    - 🔺 **AOneBlock est maintenant une dépendance souple.** TopBlock refusait auparavant de charger sans AOneBlock ; il se désactive maintenant uniquement si *ni* l'un ni l'autre mode de jeu pris en charge n'est présent. Les configurations existantes d'AOneBlock uniquement ne sont pas affectées et n'ont besoin d'aucune modification.
    - 🐛 **Chaque top ten affiche uniquement les îles de son propre mode de jeu.** AOneBlock et ChunkBlock stockent tous deux les îles sous `database/OneBlockIslands/`, donc une actualisation ChunkBlock chargeait aussi les enregistrements AOneBlock et les mauvais joueurs apparaissaient. Les îles sont maintenant filtrées par le monde du mode de jeu.
    - 🐛 **Les têtes Steve dans le panneau top ten corrigées.** Si `top_panel.yml` avait `icon: PLAYER_HEAD` décommenté, la résolution de skin n'a jamais été déclenchée et chaque tête s'est affichée comme Steve. Le panneau tombe maintenant dans le chemin basé sur le nom.

    ℹ️ C'est une mise à jour plug-and-play pour les serveurs AOneBlock — aucune configuration, panneau, ou modification de locale n'est nécessaire.

    [Release v2.1.0](https://github.com/BentoBoxWorld/TopBlock/releases/tag/2.1.0)

??? warning "Nouveautés dans v2.0.0 — mise à jour de plateforme requise"
    **Publié le :** 2026-04-26

    - 🐛 **Panneau Top Dix corrigé.** Un bug persistant faisait que le panneau top dix n'affichait que des espaces verts vides. Le gestionnaire d'événements était `private`, ce qui amenait Bukkit à le ignorer silencieusement. Corrigé — le panneau affiche désormais correctement les têtes des joueurs et leurs statistiques.
    - ✨ **Permission `aoneblock.intopten`.** Les admins et testeurs peuvent être exclus du top dix en leur retirant cette permission (accordée à tous les joueurs par défaut).
    - 🔡 **22 nouvelles locales** — cs, de, es, fr, hr, hu, id, it, ja, ko, lv, nl, pl, pt, pt-BR, ro, ru, tr, uk, vi, zh-CN, zh-HK.
    - 🔺 Requiert désormais **Paper 1.21.x**, **Java 21**, **BentoBox 3.14.0+** et **AOneBlock 1.18.0+**. Spigot n'est plus supporté.

    🔺 **Supprimez `addons/TopBlock/panels/top_panel.yml`** avant de redémarrer pour que le nouveau modèle de panneau soit extrait. Réappliquez vos personnalisations de mise en page après.

    🔡 Exécutez `/bentobox reload` après la mise à jour pour que BentoBox fusionne les nouvelles clés de locale dans vos fichiers existants.

    [Release v2.0.0](https://github.com/BentoBoxWorld/TopBlock/releases/tag/2.0.0)

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
