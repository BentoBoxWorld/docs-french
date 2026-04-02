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
