## Interfaces utilisateur personnalisables

BentoBox 1.17 a introduit une API pour la personnalisation de l'interface utilisateur. Cependant, en raison du nombre de modifications requises, tout n'est pas encore personnalisable, et seulement quelques addons ont implémenté cette fonctionnalité.

Exemple d'interface utilisateur personnalisable :
```yaml
# Le nom du panneau. Il doit être le même que le nom du fichier.
panel_name:
  # Titre du panneau
  title: "The Panel Title"
  # Type de panneau :
  # INVENTORY - type d'interface utilisateur du coffre
  # HOPPER - type d'interface utilisateur du silo
  # DROPPER - type d'interface utilisateur du distributeur/dropper.
  type: INVENTORY
  # Élément d'arrière-plan pour les emplacements vides
  background:
    # Icône pour l'élément.
    # Le format d'écriture peut être trouvé dans : https://docs.bentobox.world/en/latest/BentoBox/ItemParser/
    icon: BLACK_STAINED_GLASS_PANE
    # Titre de l'élément
    title: "&b&r" # Texte vide
    # Description de l'élément
    description: "I am background"
  # Élément de bordure pour les emplacements de bordure non vides
  border:
    # Icône pour l'élément.
    # Le format d'écriture peut être trouvé dans : https://docs.bentobox.world/en/latest/BentoBox/ItemParser/
    icon: BLACK_STAINED_GLASS_PANE
    # Titre de l'élément
    title: "&b&r" # Texte vide
    # Description de l'élément
    description: "I am border"
  # Lignes qui doivent toujours être visibles
  force-shown: [2,4]
  # Contenu de l'interface utilisateur.
  content:
    # Numéro de ligne de 1 à 6
    2:
      # Numéro de colonne
      2: reusable_button_one
      3: reusable_button_one
      4: reusable_button_one
      5: reusable_button_one
      6: reusable_button_one
      7: reusable_button_one
      8: reusable_button_one
    3:
      1:
        # Icône pour l'élément.
        # Le format d'écriture peut être trouvé dans : https://docs.bentobox.world/en/latest/BentoBox/ItemParser/
        icon: tipped_arrow[potion_contents={custom_color:11546150}]
        # Titre de l'élément.
        title: "Button One"
        # Description de l'élément
        description: "Button description"
        # Les données sont utilisées pour définir certaines fonctions utilisées par les addons.
        # Son contenu dépend de l'implémentation de l'addon/interface utilisateur.
        data:
          type: ADDON_THING
        # Les actions permettent de spécifier ce que le bouton devrait faire. Les addons peuvent spécifier des paramètres supplémentaires.
        action:
          # les options disponibles peuvent être trouvées ici : [ClickType](https://hub.spigotmc.org/javadocs/spigot/org/bukkit/event/inventory/ClickType.html)
          left:
            # Les addons peuvent définir un type de clic.
            type: ADDON_THING
            # Les infobulles sont un texte qui sera ajouté à la description du bouton à la fin.
            tooltip: "Tooltip for a button"
      9:
        # Icône pour l'élément.
        # Le format d'écriture peut être trouvé dans : https://docs.bentobox.world/en/latest/BentoBox/ItemParser/
        icon: STONE
        # Titre de l'élément.
        title: "Button Twi"
        # Description de l'élément
        description: "Button description"
        # Les données sont utilisées pour définir certaines fonctions utilisées par les addons.
        # Son contenu dépend de l'implémentation de l'addon/interface utilisateur.
        data:
          type: ADDON_THING
        # Les actions permettent de spécifier ce que le bouton devrait faire. Les addons peuvent spécifier des paramètres supplémentaires.
        action:
          # les options disponibles peuvent être trouvées ici : [ClickType](https://hub.spigotmc.org/javadocs/spigot/org/bukkit/event/inventory/ClickType.html)
          left:
            # Les addons peuvent définir un type de clic.
            type: ADDON_THING
            # Les infobulles sont un texte qui sera ajouté à la description du bouton à la fin.
            tooltip: "Tooltip for a button"
    5:
      2: reusable_button_two
      3: reusable_button_two
      4: reusable_button_two
      5: reusable_button_two
      6: reusable_button_one
      7: reusable_button_two
      8: reusable_button_two
  # Les boutons réutilisables qui sont utilisés dans la partie contenu plusieurs fois.
  reusable:
    # L'id du réutilisable
    reusable_button_one:
      # Icône pour l'élément.
      # Le format d'écriture peut être trouvé dans : https://docs.bentobox.world/en/latest/BentoBox/ItemParser/
      icon: GLASS
      # Titre de l'élément.
      title: "Reusable Button One"
      # Description de l'élément
      description: "Button description"
      # Les données sont utilisées pour définir certaines fonctions utilisées par les addons.
      # Son contenu dépend de l'implémentation de l'addon/interface utilisateur.
      data:
        type: ADDON_THING
      # Les actions permettent de spécifier ce que le bouton devrait faire. Les addons peuvent spécifier des paramètres supplémentaires.
      action:
        # les options disponibles peuvent être trouvées ici : [ClickType](https://hub.spigotmc.org/javadocs/spigot/org/bukkit/event/inventory/ClickType.html)
        left:
          # Les addons peuvent définir un type de clic.
          type: ADDON_THING
          # Les infobulles sont un texte qui sera ajouté à la description du bouton à la fin.
          tooltip: "Tooltip for a button"
    reusable_button_two:
      # Icône pour l'élément.
      # Le format d'écriture peut être trouvé dans : https://docs.bentobox.world/en/latest/BentoBox/ItemParser/
      icon: DIRT
      # Titre de l'élément.
      title: "Reusable Button Two"
      # Description de l'élément
      description: "Button description"
      # Les données sont utilisées pour définir certaines fonctions utilisées par les addons.
      # Son contenu dépend de l'implémentation de l'addon/interface utilisateur.
      data:
        type: ADDON_THING
      # Les actions permettent de spécifier ce que le bouton devrait faire. Les addons peuvent spécifier des paramètres supplémentaires.
      action:
        # les options disponibles peuvent être trouvées ici : [ClickType](https://hub.spigotmc.org/javadocs/spigot/org/bukkit/event/inventory/ClickType.html)
        left:
          # Les addons peuvent définir un type de clic.
          type: ADDON_THING
          # Les infobulles sont un texte qui sera ajouté à la description du bouton à la fin.
          tooltip: "Tooltip for a button"
```

### FAQ

??? question "Puis-je définir un titre et une description multilingues ?"
    Oui, vous pouvez. Chaque texte dans l'interface utilisateur essaiera toujours d'utiliser la localisation BentoBox. Cela signifie que si vous spécifiez un texte qui se réfère à une traduction, il l'utilisera.
    Par exemple :
    ```yaml
    tooltip: panels.tooltips.left
    ```
    essaiera d'obtenir la chaîne de traduction de l'une des locales de BentoBox :
    ```yaml
    panels:
      tooltips:
        left: "Left Click Tooltip"
    ```

??? question "Qu'est-ce que le type ?"
    Dans les plugins Spigot, vous pouvez spécifier 3 types d'inventaires avec lesquels les joueurs peuvent interagir :
    - `INVENTORY` - inventaire simple comme les coffres avec 27 à 54 emplacements.
    - `HOPPER` - inventaire du silo avec 5 emplacements.
    - `DROPPER` - inventaire du distributeur avec 9 emplacements.

    D'autres inventaires, comme l'enchantement et l'enclume, ne sont pas supportés par Spigot et nécessitent des plugins supplémentaires. C'est la raison pour laquelle BentoBox ne les supporte actuellement pas.

??? question "Qu'est-ce que l'arrière-plan ?"
    L'élément d'arrière-plan permet de définir un élément unifié pour tous les espaces vides qui seront laissés dans l'interface utilisateur.
    Il faut avoir une icône et un titre. Si vous ne voulez pas l'avoir, supprimez simplement les lignes `background`.
    La seule chose requise sous `background` est l'icône. `title` et `description` peuvent être supprimés.
    ```yaml
        icon: BLACK_STAINED_GLASS_PANE
        title: "The title of background item"
        description: "The description of background item"
    ```

??? question "Qu'est-ce que la bordure ?"
    L'élément de bordure permet de définir un élément unifié tout autour de l'interface utilisateur. Il remplacera uniquement les espaces vides.
    Il faut avoir une icône et un titre. Si vous ne voulez pas l'avoir, supprimez simplement les lignes `border`.
    La seule chose requise sous `background` est l'icône. `title` et `description` peuvent être supprimés.
    ```yaml
        icon: BLACK_STAINED_GLASS_PANE
        title: "The title of border item"
        description: "The description of border item"
    ```

??? question "Puis-je définir un texte vide et masquer l'infobulle ?"
    Malheureusement, les serveurs Minecraft ne peuvent pas désactiver le rendu du texte et de l'infobulle pour les clients. Ce n'est que pour les clients modifiés (comme fabric ou forge) que cela peut être fait.
    Le plus proche que vous pouvez obtenir est de définir un texte vide avec : `&b&r`


??? question "Qu'est-ce que `force-shown` ?"
    Dans les interfaces utilisateur des inventaires, nous essayons de supprimer toutes les lignes complètement vides. Cela permet de définir la taille dynamique des interfaces utilisateur pour différents nombres d'éléments disponibles en eux. Cependant, parfois vous voulez toujours voir une ligne spécifique. L'option force-show permet de le faire, et vous pouvez lister les entiers avec les lignes (de 0-6).

??? question "Qu'est-ce que réutilisable ?"
    Dans certaines interfaces utilisateur, vous auriez beaucoup d'éléments répétés que vous devriez spécifier, comme les défis ou les biomes. Le réutilisable permet de créer un seul élément qui sera remplacé partout où l'objet est requis à partir de la partie contenu.

??? question "Comment remplir correctement `contenu` ?"
    Le contenu nécessite de spécifier d'abord le numéro de la ligne (de 1 à 6) et le numéro de la colonne pour chaque bouton (de 1 à 9). Cela ne nécessite pas de spécifier chaque emplacement, juste ceux que vous voulez remplir. Tout le reste sera soit vide, arrière-plan ou bordure.

    Notez que certains types d'interface utilisateur n'ont pas plusieurs lignes ou moins de colonnes.

??? question "À quoi sert `data` pour les boutons ?"
    Les données sont un moyen par lequel nous avons implémenté une fonctionnalité permettant aux addons d'utiliser des fonctions personnalisées. Comme l'addon Challenges a deux types de données : CHALLENGE et LEVEL. Chaque addon a ses propres données, et il peut contenir plus de choses qu'un type.

??? question "À quoi servent les `actions` pour les boutons ?"
    `Actions` permet d'implémenter différentes choses qui se produiront si le joueur utilise différentes options de clic sur les boutons.
    Toutes les options de clic peuvent être trouvées ici : [ClickType](https://hub.spigotmc.org/javadocs/spigot/org/bukkit/event/inventory/ClickType.html)
    Soyez conscient que toutes les options ne sont pas utilisables par les joueurs.

    `action` supporte la génération d'infobulles. Les infobulles seront toujours ajoutées à la fin de la description du bouton et dans l'ordre des actions.
