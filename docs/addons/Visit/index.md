# Addon Visit

**Visit** est un simple addon BentoBox qui permet de visiter les îles d'autres joueurs.
Ceci est une alternative au addon Warps.

Créé et maintenu par [BONNe](https://github.com/BONNe).

{{ addon_description("Visit") }}

## Installation

1. Placez le fichier jar de l'addon dans le dossier des addons du plugin BentoBox
2. Redémarrez le serveur
3. Exécutez la commande `/[admin_cmd] visit` pour configurer l'addon

## Configuration

De nombreux paramètres du addon sont exposés dans l'interface graphique Admin, cependant, certains ne le sont pas.
Modifier les étiquettes des commandes nécessite un redémarrage du serveur.

### config.yml

Une fois l'addon correctement installé, il créera un fichier config.yml. Chaque option dans ce fichier est accompagnée de commentaires. Veuillez vérifier le fichier pour plus d'informations.
Vous pouvez trouver le dernier fichier config : [config.yml](https://github.com/BentoBoxWorld/Visit/blob/develop/src/main/resources/config.yml)

### Interfaces graphiques personnalisables

BentoBox 1.17 API a introduit une fonction qui permet de mettre en œuvre des interfaces graphiques personnalisables. Cet addon est l'un des premiers à utiliser cette fonctionnalité. Nous avons essayé d'être aussi simples que possible pour la personnalisation, cependant, certaines fonctionnalités nécessitent une explication.
Vous pouvez trouver plus d'informations sur le fonctionnement des interfaces graphiques personnalisées de BentoBox ici : [Interfaces graphiques personnalisées](/en/latest/Tutorials/generic/Customizable-GUI/)

??? question "Comment puis-je personnaliser les interfaces graphiques"
    Pour personnaliser les interfaces graphiques d'addon, vous devez avoir la version 1.5. C'est la première version qui les a implémentées. L'addon créera un nouveau répertoire sous `/plugins/BentoBox/addons/Visit` portant le nom `panels`

    Actuellement, vous pouvez personnaliser 2 interfaces graphiques :

    - Panneau principal : `main_panel` - panneau qui contient toutes les îles.
    - Panneau de gestion : `manage_panel` - panneau qui contient certaines options de configuration.

    Chaque interface graphique contient des fonctions qui ne sont supportées que par elle-même.

??? question "Que fait le type de bouton `PREVIOUS`|`NEXT`?"
    Les types de bouton PREVIOUS et NEXT permettent de créer une pagination automatique, lorsque vous avez plus d'îles que d'espace dans l'interface graphique.
    Ces types ont des paramètres supplémentaires sous les données :

    - `indexing` - indique si le bouton affichera le numéro de page.

    Exemple :
    ```yaml
        icon: tipped_arrow[potion_contents={custom_color:11546150}]
        title: visit.gui.buttons.previous.name
        description: visit.gui.buttons.previous.description
        data:
          type: PREVIOUS
          indexing: true
        action:
          left:
            action: PREVIOUS
            tooltip: visit.gui.tips.click-to-previous
    ```

??? question "Qu'est-ce que le type de bouton `SEARCH`?"
    Ce bouton est disponible dans le panneau principal.
    Il crée un bouton qui permet de rechercher une île spécifique.

    Exemple :
    ```yaml
        icon: PAPER
        title: visit.gui.buttons.search.name
        # Deccription is generated dynamically. However, you can set it manualy.
        # description: visit.gui.buttons.search.description
        data:
          type: SEARCH
        actions:
          left:
            type: INPUT
            tooltip: visit.gui.tips.left-click-to-edit
          right:
            type: CLEAR
            tooltip: visit.gui.tips.right-click-to-clear
    ```

??? question "Qu'est-ce que le type de bouton `FILTER`?"
    Ce bouton est disponible dans le panneau principal.
    Il crée un bouton qui permet de filtrer les îles par certaines propriétés.

    Exemple :
    ```yaml
        # Icon is generated dynamically. However, you can set it manualy.
        # icon: SANDSTONE
        title: visit.gui.buttons.filter.name
        # Deccription is generated dynamically. However, you can set it manualy.
        # description: visit.gui.buttons.filter.description
        data:
          type: FILTER
        actions:
          left:
            type: UP
            tooltip: visit.gui.tips.left-click-to-cycle
          right:
            type: DOWN
