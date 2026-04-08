# CauldronWitchery

**CauldronWitchery** permet à vos joueurs de **invoquer n'importe quel type de mob ou d'objet en utilisant un chaudron** rempli d'eau, de lave ou de neige et un bâton magique.

Créé et maintenu par [BONNe](https://github.com/BONNe).

{{ addon_description("CauldronWitchery", beta=True) }}

## Installation

1. Placez le fichier jar de l'addon dans le dossier des addons du plugin BentoBox
2. Démarrez le serveur
3. Exécutez la commande admin, par exemple `/[admin_cmd] witchery` pour configurer l'addon

## Configuration

Similaire aux défis, aux biomes et aux générateurs, Cauldron Witchery stocke toutes les données dans la base de données. Le fichier de configuration contient les options génériques sur l'addon et comment il doit fonctionner, tandis que tout le reste, comme les bâtons magiques et les données des joueurs sont stockés dans la base de données.

### config.yml

Le dernier config.yml se trouve [ici](https://github.com/BentoBoxWorld/CauldronWitchery/blob/develop/src/main/resources/config.yml).

### Modèle

Le addon CauldronWitchery contient un fichier modèle qui peut être utilisé pour importer des bâtons magiques dans la base de données. Ce fichier est utile pour l'ajout de données en masse pour les personnes qui n'aiment pas utiliser l'interface graphique en jeu. Cependant, soyez conscient que toutes les fonctions ne sont pas disponibles pour le fichier modèle, et certains articles/options ne peuvent être ajoutés que via l'interface graphique.
Vous pouvez avoir autant de fichiers modèles que vous le souhaitez. L'interface graphique Admin vous permettra de choisir lequel vous souhaitez importer.
Le fichier modèle d'exemple : [template.yml](https://github.com/BentoBoxWorld/CauldronWitchery/blob/develop/src/main/resources/template.yml)

!!! tip
    Le fichier modèle doit contenir `magic-sticks`.

??? question "Puis-je spécifier un enchantement pour le bâton magique?"
    Malheureusement, Spigot n'a pas de mécaniques générales d'analyse d'éléments. Ainsi, les auteurs de plugins doivent créer les leurs. Le addon CauldronWitchery utilise le [Item Parser](/en/latest/BentoBox/ItemParser/) de BentoBox. Si la fonction n'est pas supportée par elle, alors vous ne pouvez pas.

    Cependant, vous pouvez toujours utiliser l'interface graphique admin en jeu pour définir tous les éléments que vous souhaitez. Il n'y a aucune limitation.

??? question "La recette que j'ai ajoutée n'est pas capturée. Quelle pourrait être la raison?"
    Il pourrait y avoir plusieurs raisons à cela. S'il y a une erreur évidente, le fichier journal devrait contenir le message d'erreur avec celui-ci.

    Cependant, vous pouvez commencer par vérifier que toutes les recettes commencent par `- ` et que chaque élément (ingrédient, chaudron, niveau, etc) est aligné par le côté gauche.

    Une autre raison pourrait être que l'entité, l'élément ou le livre n'existe pas. Vous devriez vérifier si l'entrée pour eux est correcte.

### Livres

Les livres sont le moyen pour les joueurs de trouver des recettes. Les livres sont très personnalisables, cependant, soyez conscient que le titre, l'auteur et les pages ont une limitation de caractères. Je suggère d'essayer de créer un livre en jeu avec un livre écrit, et seulement après cela de le mettre dans les fichiers de traduction.

??? question "Puis-je ajouter mes propres traductions pour les livres?"
    Oui, bien sûr, vous pouvez le faire. Vous pouvez l'ajouter via [book_id]-[locale_code].yml ou en modifiant un existant.

??? question "Puis-je désactiver la génération automatique de recettes?"
    Oui, supprimez simplement la section `recipe` du livre.

??? question "Puis-je ajouter plus de livres?"
    Oui, créez simplement un nouveau fichier dans le répertoire `books`. Le fichier doit être nommé `[book_id]-[locale_code].yml` et doit commencer par `[book_id]:`.

## Interfaces graphiques personnalisables

BentoBox 1.17 API a introduit une fonction qui permet de mettre en œuvre des interfaces graphiques personnalisables. Cet addon est l'un des premiers à utiliser cette fonctionnalité. Nous avons essayé d'être aussi simples que possible pour la personnalisation, cependant, certaines fonctionnalités nécessitent une explication.
Vous pouvez trouver plus d'informations sur le fonctionnement des interfaces graphiques personnalisées de BentoBox ici : [Interfaces graphiques personnalisées](/en/latest/Tutorials/generic/Customizable-GUI/)

??? question "Comment puis-je personnaliser les interfaces graphiques"
    Pour personnaliser les interfaces graphiques d'addon, vous devez avoir la version 2.0. C'est la première version qui les a implémentées. L'addon créera un nouveau répertoire sous `/plugins/BentoBox/addons/CauldronWitchery` portant le nom `panels`

    Actuellement, vous pouvez personnaliser 2 interfaces graphiques :

    - Panneau des bâtons : `stick_panel` - panneau qui contient tous les bâtons magiques et les utilisateurs peuvent les acheter ou les obtenir.
    - Panneau des recettes : `recipe_panel` - panneau qui contient toutes les recettes disponibles pour le bâton magique.

    Chaque interface graphique contient des fonctions qui ne sont supportées que par elle-même.

??? question "Que fait le type de bouton `PREVIOUS`|`NEXT`?"
    Les types de bouton PREVIOUS et NEXT permettent de créer une pagination automatique, lorsque vous avez plus de bâtons ou de recettes que d'espace dans l'interface graphique.
    Ces types ont des paramètres supplémentaires sous les données :

    - `indexing` - indique si le bouton affichera le numéro de page.

    Exemple :
    ```yaml
        icon: tipped_arrow[potion_contents={custom_color:11546150}]
        title: cauldron-witchery.gui.buttons.previous.name
        description: cauldron-witchery.gui.buttons.previous.description
        data:
          type: PREVIOUS
          indexing: true
        action:
          left:
            tooltip: cauldron-witchery.gui.tips.click-to-previous
    ```

??? question "Que fait le type de bouton `RETURN`?"
    Le type de bouton RETURN est disponible dans recipe_panel. Il permet de revenir au panneau des bâtons.

    Exemple :
    ```yaml
        icon: OAK_DOOR
        title: cauldron-witchery.gui.buttons.return.name
        description: cauldron-witchery.gui.buttons.return.description
        data:
          type: RETURN
        action:
          left:
            tooltip: cauldron-witchery.gui.tips.click-to-return
    ```

??? question "Qu'est-ce que le type de bouton `STICK`?"
    Ce bouton est disponible dans stick_panel.
    Le bouton STICK crée une entrée dynamique pour un bâton magique. Le bouton ne sera rempli que s'il existe un bâton magique. Par exemple, si vous avez seulement 3 bâtons magiques, mais que vous avez défini 7 endroits pour eux dans l'interface graphique, alors seulement 3 endroits seront remplis. Les autres endroits seront laissés vides.

    Par défaut, les bâtons seront triés par leurs numéros de commande, cependant, vous pouvez spécifier un bâton spécifique à placer dans un emplacement spécifique avec le paramètre `id` sous les données.

    ```yaml
      data:
        type: STICK
        id: example_stick
    ```

    Spécifier le titre, la description et l'icône remplacera la génération dynamique basée sur les données de la base de données. Par défaut, ces valeurs seront générées à partir des entrées de la base de données.
    Ce bouton supporte 2 types d'actions différentes :

    - RECIPES - ouvre un panneau d'affichage de recettes
    - PURCHASE - achète ou donne le bâton magique à un joueur.

    Exemple :
    ```yaml
      data:
        type: STICK
      actions:
        left:
          type: RECIPES
          tooltip: cauldron-witchery.gui.tips.left-click-to-view
        right:
          type: PURCHASE
          tooltip: cauldron-witchery.gui.tips.right-click-to-buy
    ```


??? question "Qu'est-ce que le type de bouton `RECIPE`?"
    Ce bouton est disponible dans recipe_panel.
    Le bouton RECIPE crée une entrée dynamique pour une recette. Le bouton ne sera rempli que s'il existe une recette. Par exemple, si vous avez seulement 3 recettes, mais que vous avez défini 7 endroits pour le niveau dans l'interface graphique, alors seulement 3 endroits seront remplis. Les autres endroits seront laissés vides.

    Par défaut, les recettes seront triées par leur numéro d'ordre puis par leur nom d'élément de récompense.
    Spécifier le titre, la description et l'icône remplacera la génération dynamique basée sur les données de la base de données. Par défaut, ces valeurs seront générées à partir des entrées de la base de données.

    Exemple :
    ```yaml
      data:
        type: RECIPE
    ```

## FAQ

??? question "Comment fonctionnent les recettes?"
    Toutes les recettes nécessitent 3 choses :

    - Bâton magique dans la main principale du joueur
    - Ingrédient principal dans la main secondaire du joueur
    - Ingrédients supplémentaires

    Les ingrédients supplémentaires doivent être jetés dans le chaudron ou conservés dans l'inventaire. Cela dépend de l'option de configuration de l'addon: `mix-in-cauldron`. Si l'option est désactivée, les articles doivent être dans l'inventaire du joueur.

    Si rien ne manque, la recette fonctionnera.

??? question "Puis-je ajouter un article de bâton magique personnalisé?"
    Oui, tant que Spigot les supporte. Cependant, vous ne pourrez pas le faire via le fichier modèle. Seule l'interface graphique Admin supporte l'ajout d'articles personnalisés.

??? question "Comment les joueurs peuvent-ils obtenir des bâtons magiques?"
    Les joueurs peuvent acheter des bâtons magiques en utilisant la commande `/[player_cmd] witchery`.

    Les administrateurs peuvent aussi créer leur propre façon de distribuer les bâtons. Il existe une commande admin pour les générer :

    `/[admin_cmd] witchery get stick <stick_id>`

??? question "Quelle est la différence entre l'ingrédient principal et l'ingrédient supplémentaire?"
    L'ingrédient principal est toujours l'élément « dernier » dont le joueur a besoin pour la recette. C'est toujours un article dans la main secondaire du joueur.

    Les ingrédients supplémentaires sont des articles qui doivent être soit dans l'inventaire du joueur, soit jetés dans le chaudron (selon la configuration).

??? question "Les articles ne brûlent pas dans un chaudron de lave, et ils ne disparaissent pas?"
    Si l'option `mix-in-cauldron` est activée dans les paramètres de l'addon, alors aucun article ne brûlera dans le chaudron de lave et ils ne disparaîtront pas.
    C'est nécessaire pour le fonctionnement de l'addon, car il peut y avoir des recettes qui nécessitent un chaudron de lave. Ces recettes ne seraient pas possibles
    à réaliser si les articles brûlaient. La disparition des articles à l'intérieur du chaudron est désactivée juste comme mesure de protection.

??? question "N'importe qui sur mon île peut utiliser des bâtons magiques. Puis-je l'empêcher?"
    Oui, vous pouvez limiter les groupes d'utilisateurs qui peuvent utiliser les bâtons en utilisant les indicateurs de protection d'île.
    CauldronWitchery ajoute `CAULDRON_WITCHERY_ISLAND_PROTECTION` qui peut être basculé d'un visiteur d'île au propriétaire.

    Les utilisateurs en dehors du groupe des membres ne pourront pas utiliser les bâtons magiques sur l'île.

??? question "Pouvez-vous ajouter une fonctionnalité X?"
    Veuillez l'ajouter à la liste [ici](https://github.com/BentoBoxWorld/CauldronWitchery/issues).


## Traductions

{{ translations("CauldronWitchery") }}
