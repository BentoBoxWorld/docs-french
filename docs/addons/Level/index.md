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

    Les blocs personnalisés CraftEngine sont également pris en charge (requiert BentoBox 3.15.0+). Utilisez leur ID namespacé comme clé :

    ```yaml
    blocks:
      mynamespace:my_block: 50
      mynamespace:custom_ore: 3
    ```

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
    - `/[player_command] donate`: ouvre une interface de style coffre pour donner des blocs directement au niveau de votre île. Les points donnés survivent aux futurs recalculs de niveau. Nécessite la permission `[gamemode].island.level.donate`.
    - `/[player_command] donate hand [amount]`: donne l'objet actuellement tenu dans la main du joueur (ou le montant spécifié) directement au niveau de l'île sans ouvrir l'interface. Nécessite la permission `[gamemode].island.level.donate`.
    - `/[player_command] donate inv`: répertorie chaque bloc donnable dans l'inventaire du joueur avec les valeurs par matériau et un total, puis sur confirmation donne tout et exécute un recalcul de niveau. Les objets sans valeur configurée et non-blocs restent dans l'inventaire. Nécessite la permission `[gamemode].island.level.donate`.


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
    - `[gamemode].island.level.donate` - (défaut: `true`) - Permet au joueur d'utiliser la commande `/[player_command] donate`.

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



## Journal des modifications

??? note "Nouveautés dans v2.23.0"
    **Publié :** 21 février 2026

    - **Support des meubles/blocs personnalisés Oraxen et Nexo.** Level peut maintenant compter les mécaniques de meubles Oraxen et les blocs/meubles personnalisés Nexo dans le niveau de l'île. Ces intégrations sont en bêta — activez-les si vous avez l'un de ces plugins installé.
    - Nouveaux placeholders par bloc : `[gamemode]_island_count_<block>` (nombre d'un bloc spécifique sur l'île), `[gamemode]_island_value_<block>` (valeur d'un type de bloc), et `[gamemode]_island_limit_<block>` (limite de bloc configurée). Les clés de bloc utilisent des underscores, ex. `_island_count_minecraft_stone`.

    [Release v2.23.0](https://github.com/BentoBoxWorld/Level/releases/tag/2.23.0)

??? warning "Nouveautés dans v2.24.0 — action requise"
    **Publié :** 12 avril 2026

    - **Système de don de blocs.** Les joueurs peuvent maintenant donner des blocs de façon permanente au niveau de leur île via `/[player_command] donate` (interface) ou `/[player_command] donate hand [amount]` (don rapide depuis la main). Les points donnés sont stockés par île et rajoutés après chaque recalcul de niveau.
    - Nouveau flag de protection `ISLAND_BLOCK_DONATION` contrôlant qui peut donner. Par défaut propriétaire uniquement ; peut être étendu jusqu'au rang Membre.
    - Nouvel onglet **DONATED** dans `detail_panel.yml` montrant l'historique des dons de l'île.
    - Nouvelle variable `island_members` disponible dans la formule `level-cost` pour handicaper les équipes plus grandes.
    - Le rapport de niveau admin inclut maintenant un résumé des blocs donnés.
    - Tous les fichiers de locale migrés vers le formatage MiniMessage.
    - 🆕 Locale russe (`ru.yml`) ajoutée.
    - Correction du classement top dix sous les écritures concurrentes.
    - Les icônes de blocs pour les panneaux suspendus, les vignes et les vignes de grotte s'affichent maintenant correctement.

    🔺 **Supprimez `plugins/BentoBox/addons/Level/panels/detail_panel.yml`** avant de redémarrer pour que le nouveau template d'onglet DONATED soit généré. Le fichier n'est pas écrasé lors de la mise à jour.

    🔡 **Régénérez les fichiers de locale** si vous avez des personnalisations — les anciens codes couleur `&` ne sont plus valides.

    [Release v2.24.0](https://github.com/BentoBoxWorld/Level/releases/tag/2.24.0)

??? note "Nouveautés dans v2.25.0"
    **Publié le :** 2026-04-26

    - **Support des blocs personnalisés CraftEngine.** Les blocs CraftEngine sont désormais comptés dans le calcul du niveau d'île. Ajoutez-les dans `blockconfig.yml` avec leurs IDs namespacés (ex. `mynamespace:my_block: 50`). Requiert BentoBox 3.15.0+. CraftEngine peut être désactivé avec `disabled-plugin-hooks: [CraftEngine]` dans `config.yml`.
    - **Mot-clé `hand` localisable.** L'argument `hand` dans `/island donate` et `/island value` est désormais traduisible via la nouvelle clé de locale `island.donate.hand.keyword`. L'anglais `hand` est toujours accepté comme solution de repli.
    - 🔡 Les 16 fichiers de locale non-anglais mis à jour pour inclure les clés manquantes.
    - 🔡 La locale ukrainienne est désormais entièrement traduite.

    🔡 **Régénérez les fichiers de locale** pour récupérer la nouvelle clé `island.donate.hand.keyword`.

    [Release v2.25.0](https://github.com/BentoBoxWorld/Level/releases/tag/2.25.0)

??? note "Nouveautés dans v2.26.0"
    **Publié le :** 2026-05-04

    - **Panneau de don configurable.** Le GUI de don est désormais entièrement piloté par un nouveau template `panels/donation_panel.yml`, à l'image des panneaux de valeur, de détail et du top-ten. Les administrateurs peuvent redimensionner le panneau de 1 à 6 lignes, repositionner les quatre boutons nommés (`INFO`, `CANCEL`, `PREVIEW`, `CONFIRM`), changer leurs icônes et ajouter des objets décoratifs. La grille de don remplit automatiquement toutes les cellules qui ne sont ni bordure ni bouton nommé.
    - `force-shown: [1,2,3,4]` contrôle le nombre de lignes utilisées par le panneau (1 à 6 supportées). Les quatre boutons requis sont placés selon leur `data.type`. Si le template est manquant ou si l'un des boutons requis est absent, le panneau revient à l'ancienne disposition codée en dur sur 4 lignes.
    - 🐛 Les objets décoratifs du template s'affichent maintenant réellement dans l'inventaire ; le `title:` personnalisé du panneau de don est désormais respecté ; `force-shown` est maintenant lu comme une liste (cohérent avec les autres YAMLs de panneau).
    - Pas de rupture d'API, pas de changement de locale, pas de migration `config.yml`.

    ⚙️ **Disposition du panneau de don.** Un nouveau `panels/donation_panel.yml` est livré au premier démarrage — laissez-le tel quel pour garder la disposition de 2.25.0, ou éditez-le pour la personnaliser.

    [Release v2.26.0](https://github.com/BentoBoxWorld/Level/releases/tag/2.26.0)

??? warning "Nouveautés dans v2.27.0 — action requise"
    **Publié le :** 13 mai 2026

    🔺 **Requiert BentoBox 3.16.0 ou ultérieur.** Cette version relève le `api-version` dans `addon.yml` à `3.16.0` et dépend des nouveaux helpers `CraftEngineHook.getItemId` / `getItemStack`. Les versions plus anciennes de BentoBox refuseront de charger l'addon.

    - ⚙️ **Mode donations uniquement.** Nouvelle option `donations-only` dans `config.yml` (défaut `false`). Quand `true`, l'analyse de chunk par recalcul est entièrement ignorée et le niveau d'île est calculé à partir des points donnés seuls en utilisant la formule `level-calc` configurée. `/island detail` n'est pas enregistré dans ce mode et le bouton de spectateur top-ten cesse d'ouvrir le panneau de détail. Le `initialCount` stocké est ignoré au moment de `/island level`, donc basculer le mode pour un serveur avec des îles existantes ne pousse pas les joueurs à des niveaux sauvagement négatifs.
    - 💎 **`/island donate inv` — donner tout de l'inventaire.** Nouvelle sous-commande confirmable `inv` : répertorie chaque bloc donnable dans l'inventaire du joueur avec les valeurs par matériau et un total, puis sur confirmation donne tout et exécute un recalcul de niveau. Les objets sans valeur configurée et non-blocs restent dans l'inventaire. La complète onglet suggère maintenant `hand` / `inv` pour le premier arg, et le nombre d'objets tenus après `hand`.
    - 🧱 **Support des blocs personnalisés dans les menus de valeur, détail et don.** Les blocs personnalisés Oraxen, Nexo, ItemsAdder et CraftEngine ne sont plus filtrés de `/level value` ou rendus comme des icônes PAPER anonymes dans `/level detail`. La valeur et les panneaux de détail recherchent l'`ItemStack` de bloc personnalisé réel à partir du registre de chaque plugin, donc la texture/données du modèle configurées et le nom d'affichage sont préservés. `/island value hand` sur un objet personnalisé tenu signale maintenant la valeur configurée et le nom d'affichage. Les chemins de don (`/island donate hand`, `/island donate inv`, le panneau de don) acceptent les objets de bloc personnalisé et enregistrent les dons sous l'ID personnalisé.
    - 🐛 **Correction de la progression négative.** Les formules non-linéaires de `level-calc` (par ex. `3 * sqrt(blocks / level_cost)`) ne descendent plus en dessous de zéro entre les niveaux. Merci @msmith-codes!
    - ⚡ **Performance.** `tidyUp()` ne marche plus jusqu'à 10M de points linéairement sur le thread principal lors du calcul des limites de points — les analyses avant et arrière utilisent maintenant la recherche binaire (~23 itérations au lieu de millions).

    🔡 **Locales mises à jour.** Les 18 locales expédiées ont gagné de nouvelles clés `island.donate.inv.*` (`keyword`, `confirm-header`, `confirm-line`, `confirm-total`). Si vous avez des fichiers de locale personnalisés dans `plugins/BentoBox/addons/Level/locales/`, copiez le nouveau bloc `donate.inv` dedans ou le nouveau flux `/island donate inv` montrera des clés brutes.

    [Release v2.27.0](https://github.com/BentoBoxWorld/Level/releases/tag/2.27.0)

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
