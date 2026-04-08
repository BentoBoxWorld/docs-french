# IslandFly

**IslandFly** permet aux joueurs de voler sur leur île.

Créé et maintenu par [tastybento](https://github.com/tastybento).

{{ addon_description("IslandFly") }}

## Installation

0. Installez BentoBox et exécutez-le sur le serveur au moins une fois pour créer ses dossiers de données.
1. Placez ce fichier jar dans le dossier des addons du plugin BentoBox.
2. Redémarrez le serveur.
3. L'addon créera un dossier de données et à l'intérieur du dossier se trouvera un config.yml.
4. Arrêtez le serveur.
5. Modifiez config.yml comme vous le souhaitez.
7. Redémarrez le serveur.

## Configuration

Une fois l'addon correctement installé, il créera un fichier config.yml. Chaque option dans ce fichier est accompagnée de commentaires. Veuillez vérifier le fichier pour plus d'informations.
Vous pouvez trouver le dernier fichier config : [config.yml](https://github.com/BentoBoxWorld/IslandFly/blob/develop/src/main/resources/config.yml)

=== "fly-timeout"
    !!! summary "Description"
        Combien de secondes l'addon attendra avant de désactiver le mode vol quand un joueur quitte son île.

=== "logout-disable-fly"
    !!! summary "Description"
        Si le mode vol devrait être désactivé quand un joueur se déconnecte.

=== "disabled-gamemode"
    !!! summary "Description"
        Cette liste stocke les modes de jeu dans lesquels le addon islandFly ne devrait pas fonctionner. Pour désactiver l'addon, il est nécessaire d'écrire son nom sur une nouvelle ligne qui commence par -.

    !!! example "Exemple"
        ```yaml
            disabled-gamemodes:
            - BSkyBlock
        ```

=== "allow-command-outside-protection-range"
    !!! summary "Description"
        Cela permet au joueur d'utiliser la commande en dehors de la plage de protection de l'île.

## Commandes

!!! tip
    `[player_command]` et `[admin_command]` sont des commandes qui diffèrent selon le mode de jeu que vous exécutez.
    Le fichier `config.yml` des modes de jeu contient des options qui vous permettent de modifier ces valeurs.
    Par exemple, sur BSkyBlock, la `[player_command]` par défaut est `island`, et la `[admin_command]` par défaut est `bsbadmin`.

=== "Commandes du joueur"
    - `/[player_command] fly`: bascule le vol activé / désactivé.

## Permissions

!!! tip
    `[gamemode]` est un préfixe qui diffère selon le mode de jeu que vous exécutez.
    Le préfixe est le nom du mode de jeu en minuscules, c'est-à-dire que si vous utilisez BSkyBlock, le préfixe est `bskyblock`.
    De même, si vous utilisez AcidIsland, le préfixe est `acidisland`.

=== "Permissions"
    - `[gamemode].island.fly` - (défaut: `true`) - Permet au joueur d'utiliser la commande '/[player_command] fly'.
    - `[gamemode].island.flyspawn` - (défaut: `op`) - Permet au joueur de voler à l'île de spawn.
    - `[gamemode].island.flybypass` - (défaut: `op`) - Permet au joueur de voler sur les îles d'autres joueurs.

## FAQ

??? question "Pouvez-vous ajouter une fonctionnalité X?"
    Veuillez l'ajouter à la liste [ici](https://github.com/BentoBoxWorld/IslandFly/issues).

??? question "J'ai un bogue, où dois-je le signaler?"
    Veuillez l'ajouter à la liste [ici](https://github.com/BentoBoxWorld/IslandFly/issues).

## Traductions

{{ translations("IslandFly") }}
