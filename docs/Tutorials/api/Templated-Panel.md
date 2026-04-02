# Documentation BentoBox TemplatedPanel

La TemplatedPanel de BentoBox est un outil puissant pour les développeurs Minecraft, permettant la création d'interfaces utilisateur (UI) personnalisables basées sur l'inventaire avec facilité. En définissant les mises en page des panneaux en YAML, les développeurs peuvent ajuster rapidement les éléments de l'interface utilisateur sans avoir besoin de modifier le code de base. Voici une ventilation détaillée de comment configurer une TemplatedPanel en utilisant YAML.

## Définition du panneau

### Identification du panneau
- `detail_panel` : Définissez le nom unique du panneau pour la référence dans le code.

### Titre du panneau
- `title` : Définissez le titre d'affichage du panneau. Ce titre peut être localisé via une référence dans le fichier de locale.

### Type de panneau
- `type` : Choisissez le type d'inventaire à afficher. Les options incluent `INVENTORY`, `HOPPER` et `DROPPER`.

### Arrière-plan et bordure
- `background` : Personnalisez l'arrière-plan du panneau à l'aide d'objets Minecraft. Par exemple, `BLACK_STAINED_GLASS_PANE` peut être utilisé pour un effet esthétique.
- `border` : Définissez l'apparence de la bordure du panneau, à nouveau en utilisant des objets Minecraft. Cela aide à contraster les éléments du panneau.

### Configuration de l'affichage
- `force-shown` : Spécifiez les lignes du panneau qui doivent être affichées, affectant la taille verticale du panneau.

## Configuration du contenu

### Disposition et fonctionnalité des boutons
- `content` : Dans cette section, détaillez chaque élément ou bouton du panneau. Utilisez les numéros de ligne et de colonne pour positionner chaque élément.
  - `icon` : Définissez l'objet Minecraft à utiliser comme icône du bouton.
  - `title` : Fournissez un titre pour le bouton, qui peut être localisé.
  - `description` : Ajoutez une description pour le bouton, également localisable.
  - `data` : Incluez les données pertinentes à la fonction du bouton, telles que le type d'action qu'il déclenche.
  - `actions` : Définissez les actions qui se produisent lors de l'interaction avec le bouton, en spécifiant le type de clic et les infobulles.

### Boutons réutilisables
- `reusable` : Définissez des modèles pour les boutons qui sont utilisés plusieurs fois dans le panneau.
  - Dans cette section, spécifiez les détails tels que l'icône du bouton, le titre, la description et les données associées.

## Configuration des boutons exemple
- Pour un bouton à la ligne 1, colonne 2 :
  ```yaml
  1:
    2:
      icon: STONE
      title: level.gui.buttons.all_blocks.name
      description: level.gui.buttons.all_blocks.description
      data:
        type: TAB
        tab: ALL_BLOCKS
      actions:
        view:
          click-type: unknown
          tooltip: level.gui.tips.click-to-view
  ```

- Pour un bouton réutilisable nommé `material_button` :
  ```yaml
  reusable:
    material_button:
      title: level.gui.buttons.material.name
      description: level.gui.buttons.material.description
      data:
        type: BLOCK
  ```

Ce système TemplatedPanel offre aux développeurs BentoBox un moyen rationalisé et flexible de concevoir et de mettre en œuvre des éléments d'interface utilisateur interactifs dans le jeu, améliorant l'engagement et la fonctionnalité de l'utilisateur.

# Documentation TemplatedPanelBuilder

La classe `TemplatedPanelBuilder` fait partie de l'API BentoBox, conçue pour faciliter la création d'objets `TemplatedPanel`. Elle fournit une interface fluide pour construire des panneaux avec diverses options de personnalisation, telles que des modèles, le contexte de l'utilisateur, le contexte du monde et les écouteurs. Voici un aperçu de sa fonctionnalité et de son utilisation.

## Aperçu de la classe

`TemplatedPanelBuilder` est utilisé pour construire des instances de `TemplatedPanel`. Il permet de définir divers paramètres et configurations nécessaires au fonctionnement du panneau dans le monde Minecraft, spécifiquement dans le cadre de BentoBox.

## Méthodes

### Méthodes de modèle

- `template(String guiName, File dataFolder)` : Définit le modèle du panneau en fonction du nom de l'interface utilisateur et du dossier de données. Retourne l'instance `TemplatedPanelBuilder` pour le chaînage.
- `template(String panelName, String templateName, File dataFolder)` : Définit le modèle du panneau en fonction du nom du panneau, du nom du modèle et du dossier de données. Introduit dans la version 1.20.0. Retourne l'instance `TemplatedPanelBuilder` pour le chaînage.

### Méthode utilisateur

- `user(User user)` : Définit l'utilisateur pour lequel le panneau est construit. Retourne l'instance `TemplatedPanelBuilder` pour le chaînage.

### Méthode monde

- `world(World world)` : Définit le contexte du monde pour le panneau. Retourne l'instance `TemplatedPanelBuilder` pour le chaînage.

### Méthode de paramètres

- `parameters(@NonNull String... parameters)` : Définit les paramètres du titre du panneau. Retourne l'instance `TemplatedPanelBuilder` pour le chaînage. Disponible à partir de la version 1.20.0.
- Exemple : `panelBuilder.parameters("[name]", this.user.getName());` place le nom de l'utilisateur dans le titre du panneau

### Méthode d'écouteur

- `listener(PanelListener listener)` : Ajoute un `PanelListener` au panneau pour gérer les interactions utilisateur. Retourne l'instance `TemplatedPanelBuilder` pour le chaînage.
- Les écouteurs ne sont pas obligatoires car la fonctionnalité de passage à un autre onglet, ou la réaction à un clic est gérée dans l'API.
- Vous n'aurez peut-être besoin d'un écouteur que si vous avez besoin d'une fonctionnalité personnalisée.

### Enregistrement du générateur de type

- `registerTypeBuilder(String type, BiFunction<ItemTemplateRecord, TemplatedPanel.ItemSlot, PanelItem> buttonCreator)` : Enregistre un nouveau générateur de type de bouton pour le panneau. Retourne l'instance `TemplatedPanelBuilder` pour le chaînage.
- Exemple :
```
        panelBuilder.registerTypeBuilder("NEXT", this::createNextButton);
        panelBuilder.registerTypeBuilder("PREVIOUS", this::createPreviousButton);
        panelBuilder.registerTypeBuilder("BLOCK", this::createMaterialButton);
```
- Lorsque le bouton avec le nom associé est cliqué, la méthode appropriée sera appelée. On lui passe le ItemTemplateRecord, l'ItemSlot et le PanelItem.

### Méthode de construction

- `build()` : Construit et retourne une instance `TemplatedPanel` basée sur la configuration fournie.

## Getters

- `getPanelTemplate()` : Récupère le `PanelTemplateRecord` actuel.
- `getUser()` : Obtient l'objet `User` associé au panneau.
- `getWorld()` : Retourne le contexte `World` du panneau.
- `getParameters()` : Récupère la liste des paramètres définis pour le titre du panneau.
- `getListener()` : Retourne le `PanelListener` attaché au panneau.
- `getObjectCreatorMap()` : Fournit l'accès à la carte reliant les objets à leurs créateurs d'éléments de panneau.

## Variables

- `panelTemplate` : Stocke l'enregistrement du modèle d'interface utilisateur.
- `user` : Détient la référence à l'utilisateur qui ouvre l'interface utilisateur.
- `world` : Représente le monde où l'interface utilisateur opère.
- `listener` : Stocke le `PanelListener` pour gérer les interactions de l'interface utilisateur.
- `parameters` : Une liste pour stocker les paramètres pour l'objet titre.
- `objectCreatorMap` : Une carte reliant les types d'objets à leurs créateurs respectifs d'éléments de panneau.

## Utilisation

Pour utiliser le `TemplatedPanelBuilder`, instanciez-le et chaînez ses méthodes pour configurer le panneau selon vos besoins. Une fois toutes les configurations définies, appelez la méthode `build()` pour créer une instance `TemplatedPanel`.

Exemple :

```
        // Commencez à construire le panneau.
        TemplatedPanelBuilder panelBuilder = new TemplatedPanelBuilder();
        panelBuilder.user(this.user);
        panelBuilder.world(this.user.getWorld());

        panelBuilder.template("detail_panel", new File(this.addon.getDataFolder(), "panels"));

        panelBuilder.parameters("[name]", this.user.getName());

        panelBuilder.registerTypeBuilder("NEXT", this::createNextButton);
        panelBuilder.registerTypeBuilder("PREVIOUS", this::createPreviousButton);
        panelBuilder.registerTypeBuilder("BLOCK", this::createMaterialButton);

        panelBuilder.registerTypeBuilder("FILTER", this::createFilterButton);

        // Enregistrer les onglets
        panelBuilder.registerTypeBuilder("TAB", this::createTabButton);

        // Enregistrer le générateur de type inconnu.
        panelBuilder.build();
```
