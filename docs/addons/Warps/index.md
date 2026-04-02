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
