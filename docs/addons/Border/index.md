# Border

**Border** peut créer et afficher une bordure autour des îles que les joueurs ne peuvent pas dépasser.
La bordure peut être :

- la bordure du monde vanilla
- une bordure personnalisée qui s'affiche quand le joueur s'en rapproche (les visuels peuvent être configurés).

Créé et maintenu par [tastybento](https://github.com/tastybento).

{{ addon_description("Border") }}

## Installation

1. Redémarrez le serveur (pour activer l'addon et avoir le fichier `config.yml` généré)
2. Placez le fichier jar de l'addon dans le dossier `plugins/BentoBox/addons`
3. Personnalisez les paramètres dans `config.yml` (facultatif)
4. Redémarrez le serveur pour appliquer les nouveaux paramètres

## Commandes

!!! tip
    `[player_command]` est une commande qui diffère selon le mode de jeu que vous exécutez.
    Le fichier `config.yml` des modes de jeu contient des paramètres qui vous permettent de modifier cette valeur.
    Par exemple, sur BSkyBlock, la `[player_command]` par défaut est `island`.

### border
**Commande**: `/[player command] border`
**Description**: Active/désactive la bordure.
**Permission**: `[gamemode].border.toggle`. Défaut: `op`.
**Notes**: Depuis la version 3.0.0, cela nécessite une permission.

### border type {...}
**Commande**: `/[player command] border type {barrier | vanilla}`
**Description**: Définit le type de bordure. Exécutez sans argument pour basculer entre les types disponibles.
**Permission**: `[gamemode].border.type`. Défaut: `true`.
**Exemple**: `/[player command] border type barrier`

### bordertype {...}
**Commande**: `/[player command] bordertype {barrier | vanilla}`  
**Description**: La même commande que `border type`, enregistrée directement sous la commande du mode de jeu.  
**Permission**: `[gamemode].border.bordertype`. Défaut: `false`.  
**Exemple**: `/[player command] bordertype vanilla`  

### border color {red|green|blue}
**Commande**: `/[player command] border color {red | green | blue}` (également disponible sous la forme `/[player command] bordercolor {red | green | blue}`)  
**Description**: Définit la couleur de la bordure monde vanilla pour le joueur. S'applique uniquement avec le type de bordure vanilla.  
**Permission**: `[gamemode].border.color` pour pouvoir exécuter la commande. Défaut: `true`.  
Chaque couleur nécessite ensuite sa propre permission : `[gamemode].border.color.red`, `[gamemode].border.color.green`, `[gamemode].border.color.blue` (ou `[gamemode].border.color.*` pour toutes). Défaut: `op`.  
**Exemple**: `/[player command] border color green`

!!! warning "Changements de permissions en 4.8.5"
    `[gamemode].border.color` n'avait jamais été déclarée avant la 4.8.5 : elle retombait donc silencieusement sur op uniquement, et les joueurs ordinaires ne pouvaient pas du tout utiliser la commande de couleur. Elle est désormais déclarée avec `true` par défaut.

    Le nœud déclaré `[gamemode].bordertype` a également été renommé en `[gamemode].border.bordertype`, qui est le nœud réellement vérifié par la commande. Si vous aviez accordé ou refusé `[gamemode].bordertype` dans LuckPerms (ou équivalent), mettez la règle à jour — l'ancien nœud n'a jamais eu le moindre effet.

!!! tip
    `[gamemode]` est un préfixe qui diffère selon le mode de jeu que vous exécutez.
    Le préfixe est le nom du mode de jeu en minuscules, c'est-à-dire que si vous utilisez BSkyBlock, le préfixe est `bskyblock`.
    De même, si vous utilisez AcidIsland, le préfixe est `acidisland`.

## Configuration

Le fichier `config.yml` contient des paramètres.
La valeur par défaut est généralement la valeur d'exemple, sauf indication contraire.

### Désactiver les modes de jeu
Vous pouvez désactiver l'addon avec ce paramètre.
Par défaut, Border fonctionnera dans tous les mondes des modes de jeu sur le serveur BentoBox.

Vous pouvez désactiver un mode de jeu en écrivant son nom sur une nouvelle ligne qui commence par `-`.
Exemple pour désactiver BSkyBlock:

```yml
disabled-gamemodes:
  - BSkyBlock
```

Valeur par défaut:

```yml
disabled-gamemodes: []
```

### Type de bordure
Le type de bordure par défaut que les nouveaux joueurs reçoivent. Il y a deux choix :

- `VANILLA` — utilise l'effet de bordure de monde natif de Minecraft (le mur tremblotant que vous voyez dans le jeu vanilla). Elle peut être teintée d'une couleur.
- `BARRIER` — utilise des blocs de barrière invisibles et des particules colorées qui n'apparaissent que lorsque vous vous en approchez.

Les joueurs disposant d'une permission peuvent changer leur propre bordure avec `/[player command] border type`. S'ils n'ont pas la permission, ils reçoivent ce que vous avez défini ici.

```yml
type: VANILLA
```

### Couleur de la bordure vanilla
La couleur de la bordure de monde vanilla. Utilisée uniquement lorsque le type de bordure est `VANILLA`.  
Les choix sont `RED`, `GREEN` ou `BLUE`. Les joueurs disposant d'une permission peuvent choisir leur propre couleur avec `/[player command] border color`.

```yml
color: BLUE
```

### Renvoyer les objets
Si `true`, les objets qu'un joueur jette contre la bordure sont renvoyés à l'intérieur au lieu de s'envoler. Définissez sur `false` pour laisser les objets lancés passer à travers.

```yml
bounce-back: true
```

### Retour à la téléportation
Contrôle si les joueurs qui réussissent à passer à travers la bordure (par exemple par téléportation dans le même monde) devraient être téléportés de retour à leurs îles.

Définissez sur `true` si vous souhaitez que les joueurs soient téléportés de retour.

**Attention**: Si vous définissez cette valeur sur `false` avec `use-barrier-blocks` également sur `false`, les joueurs pourront simplement marcher à travers la bordure.

```yml
return-teleport: true
```

!!! tip
    Si vous voulez utiliser cet addon **seulement pour afficher** les bordures pour les joueurs, utilisez les paramètres suivants:
    ```yml
    use-barrier-blocks: false
    return-teleport: false
    ```

### Bloc de sécurité du retour à la téléportation
Utilisé uniquement lorsque `return-teleport` est `true`. Si un joueur est téléporté de retour à l'intérieur de la bordure et se retrouve quelque part sans sécurité (par exemple au-dessus d'une chute ou dans la lave), ceci place un bloc sécurisé sous ses pieds pour qu'il ne se fasse pas mal.

```yml
return-teleport-safety-block: true
```

### Utiliser des blocs de barrière.
S'applique uniquement aux joueurs qui n'utilisent **pas** le type de bordure vanilla.

- `true`: la bordure sera composée de blocs de barrière.
- `false`: il n'y aura pas de bordure basée sur les blocs de barrière. Cela signifie que c'est jusqu'au paramètre `return-teleport` si les joueurs sont téléportés de retour lorsqu'ils quittent l'île.

```yml
use-barrier-blocks: true
```

### Comportement de bordure par défaut
Les joueurs peuvent activer et désactiver la bordure avec une commande s'ils disposent de la bonne permission.
Ce paramètre définit le paramètre par défaut activé ou désactivé; définissez-le sur `true` pour l'avoir activé par défaut.

```yml
show-by-default: true
```

### Afficher la bordure de la plage de protection maximale.
S'applique uniquement aux joueurs qui n'utilisent **pas** le type de bordure vanilla.

Définissez sur `true` pour afficher les particules de barrière (🚫) affichées à la plage de protection maximale.
Ceci est utile pour les modes de jeu comme Boxed où la zone de protection du joueur peut se déplacer.

Notez que ce ne sont **pas des blocs de barrière** mais des _particules_, donc l'« air » y _ressemble_.

```yml
show-max-border: true
```

### Afficher les particules
Active/désactive tous les types de particules de mur affichées par l'addon (bordure et particules de plage de protection maximale).

Définissez sur `false` si vous ne voulez **aucune** particule de mur à afficher.

```
show-particles: true
```

### Décalage de la barrière
Applicable uniquement aux joueurs qui n'utilisent **pas** le type de bordure vanilla.

Normalement, la bordure est exactement au bord de la plage de protection du joueur. Ce paramètre pousse la barrière vers l'**extérieur** du nombre de blocs que vous donnez, afin que les joueurs puissent marcher un peu au-delà de leur zone protégée avant de heurter le mur.

Choses importantes à savoir :

- Cela ne rend **pas** la zone protégée plus grande — les joueurs ne peuvent toujours pas construire ni protéger l'espace supplémentaire, ils peuvent seulement s'y tenir.
- La bordure ne dépassera jamais la distance de l'île, peu importe le nombre que vous définissez.
- La valeur minimale (et par défaut) est `0`, ce qui signifie que la bordure se situe exactement sur la plage de protection.

```yml
barrier-offset: 0
```

## Placeholders

| Placeholder | Description | Version |
|---|---|---|
| `%Border_color%` | La couleur de bordure actuelle du joueur (`red`, `green` ou `blue`) | 4.8.0 |

## FAQ

??? question "Comment puis-je modifier la taille de la bordure?"
    La bordure n'a pas sa propre taille — elle est dessinée autour de la **plage de protection** de chaque île. Donc, pour agrandir ou réduire la bordure, vous modifiez la plage de protection.

    - Donnez aux joueurs une plage plus grande avec une permission comme `[gamemode].island.range.<number>` (par exemple `bskyblock.island.range.150`).
    - Les admins peuvent définir la plage sur une île spécifique avec la commande admin de plage, par exemple `/bsbadmin range set <player> <number>`.
    - La plage ne peut jamais être plus grande que **la moitié de la distance entre les îles**, et cette distance est définie une fois à la création du monde et ne peut pas être modifiée ensuite.

    Consultez [Plage d'Île et Espacement](../../BentoBox/About/IslandManagement.md#plage-dile-et-espacement) pour tous les détails.

??? question "Puis-je faire la bordure un peu plus grande que la plage de l'île?"
    Oui ! Utilisez le paramètre `barrier-offset` dans `config.yml`. Il pousse la bordure vers l'extérieur du nombre de blocs que vous choisissez, afin que les joueurs puissent marcher un peu au-delà de leur zone protégée avant de heurter le mur.

    N'oubliez pas que cela déplace uniquement le mur — cela ne donne **pas** aux joueurs de terrain supplémentaire sur lequel ils peuvent construire ou protéger. Consultez le paramètre [Décalage de la barrière](#decalage-de-la-barriere) ci-dessus.

??? question "Quelle est la différence entre les types de bordure barrier et vanilla?"
    - **Vanilla** utilise l'effet de bordure de monde natif de Minecraft — le mur scintillant que vous connaissez déjà du jeu normal. Vous pouvez le teinter en rouge, vert ou bleu.
    - **Barrier** utilise des blocs de barrière invisibles plus des particules colorées qui ne s'affichent que lorsque vous vous approchez du bord.

    Les joueurs disposant d'une permission peuvent basculer entre eux avec `/[player command] border type`.

??? question "Je ne veux pas d'un mur solide — puis-je simplement montrer une ligne que les joueurs peuvent traverser?"
    Oui. Définissez `use-barrier-blocks: false` pour qu'il n'y ait pas de mur solide, et `return-teleport: false` pour que les joueurs ne soient pas tirés en arrière. Cela ne laisse que la bordure visuelle. Mettez ceci dans `config.yml`:

    ```yml
    use-barrier-blocks: false
    return-teleport: false
    ```

??? question "Comment puis-je modifier la couleur de la bordure?"
    Les couleurs ne fonctionnent qu'avec le type de bordure **vanilla**. Définissez une valeur par défaut au niveau du serveur avec le paramètre `color` dans `config.yml` (`RED`, `GREEN` ou `BLUE`). Les joueurs disposant d'une permission peuvent choisir leur propre couleur en jeu avec `/[player command] border color {red|green|blue}`.

??? question "Comment puis-je désactiver la bordure?"
    Les joueurs peuvent basculer leur propre bordure activée ou désactivée avec `/[player command] border` (ils ont besoin de la permission `[gamemode].border.toggle`). Pour l'avoir désactivée pour tout le monde par défaut, définissez `show-by-default: false` dans `config.yml`.

??? question "La bordure ne s'affiche pas — que dois-je vérifier?"
    - Assurez-vous que le mode de jeu n'est pas répertorié dans `disabled-gamemodes` dans `config.yml`.
    - Vérifiez que le joueur a réellement la bordure activée (`/[player command] border`) et que `show-by-default` est `true`.
    - La bordure n'apparaît que autour de la plage de protection de votre propre île, donc vous devez être près d'une arête pour la voir.
    - Si vous utilisez le type **barrier** avec `show-particles: false`, le mur est invisible jusqu'à ce que vous le touchiez — c'est normal.

??? question "Pouvez-vous ajouter une fonctionnalité X?"
    Veuillez la demander sur le [issue tracker](https://github.com/BentoBoxWorld/Border/issues).

## Journal des modifications

??? note "Nouveautés dans v4.7.0 → v4.8.2"
    **Publié :** 16 février 2026 au 4 avril 2026

    - **Sélection de couleur de bordure monde vanilla.** Les joueurs utilisant le type de bordure vanilla peuvent maintenant choisir leur couleur de bordure — rouge, verte ou bleue — via `/[player_command] color {red|green|blue}`.
    - Nouveau placeholder `%Border_color%` retournant la couleur de bordure actuelle du joueur.
    - Nouvelles permissions `[gamemode].color.red`, `[gamemode].color.green`, `[gamemode].color.blue` (ou `[gamemode].color.*` pour toutes). Défaut : op.
    - Correction : contournement de la téléportation de bordure quand un joueur est hors de tous les espaces d'île (4.7.0).
    - Correction : la bordure monde vanilla ne se réinitialisait pas lors d'un téléport entre îles — causait un état restreint pour les joueurs Bedrock/Geyser (4.8.1).
    - Correction : placeholder `%Border_color%` retournant une erreur null dans certaines configurations (4.8.1).
    - Correction : la bordure s'activait incorrectement dans le nether et l'end vanilla (4.8.1).

    [Release v4.7.0](https://github.com/BentoBoxWorld/Border/releases/tag/4.7.0) · [v4.8.0](https://github.com/BentoBoxWorld/Border/releases/tag/4.8.0) · [v4.8.1](https://github.com/BentoBoxWorld/Border/releases/tag/4.8.1) · [v4.8.2](https://github.com/BentoBoxWorld/Border/releases/tag/4.8.2)

??? note "Nouveautés dans v4.8.3"
    **Publié le :** 2026-04-26

    - 🔡 Tous les fichiers de locale convertis des codes couleur `&` hérités vers le format MiniMessage.
    - 🔡 Clés `set-color` manquantes ajoutées à toutes les locales non-anglaises.
    - 🔡 Corrections de bugs dans les fichiers de locale polonais, ukrainien et chinois.
    - 🔺 API BentoBox minimale portée à **3.12.0**.

    🔺 **Si vous maintenez des remplacements de locale personnalisés** sous `plugins/BentoBox/addons/Border/locales/`, migrez les codes couleur du style `&a` vers les balises MiniMessage (ex. `<green>`) avant de redémarrer.

    [Release v4.8.3](https://github.com/BentoBoxWorld/Border/releases/tag/4.8.3)

??? note "Nouveautés dans v4.8.4"
    **Publié le :** 2026-05-26

    - 🐛 **Correction de `NoSuchMethodError: WorldBorder.changeSize` sur Paper/Purpur 1.21.10.** Le build 4.8.3 était compilé contre Paper 1.21.11, qui a renommé la méthode de bordure de monde, si bien que le type de bordure vanilla plantait sur les serveurs 1.21.10 lors de l'utilisation de `/[player_command] bordertype vanilla`. Border utilise désormais l'API `setSize` compatible toutes versions et fonctionne sur **1.21.10 et 1.21.11**.
    - 🐛 Correction du workflow de publication Modrinth (chemin d'artefact incorrect).

    Aucune modification de config ou de locale n'est requise. Si vous contourniez le bug avec `bordertype barrier`, vous pouvez revenir à `vanilla` une fois la 4.8.4 installée.

    [Release v4.8.4](https://github.com/BentoBoxWorld/Border/releases/tag/4.8.4)

??? warning "Nouveautés dans v4.8.5 — changements de permissions"
    **Publié :** 1er août 2026

    Un correctif de compatibilité et de permissions. Aucun changement de configuration ni de traduction n'est nécessaire.

    - 🐛 **Les objets lâchés à la mort ne sont plus détournés des autres plugins.** La protection des objets lâchés ajoutée en 4.7.0 retirait chaque objet de `PlayerDeathEvent`, les faisait apparaître elle-même, puis vidait la liste. Tout plugin qui stocke ces objets — DeathChest, les plugins de tombes, les fonctionnalités de conservation d'inventaire — s'exécute à une priorité ultérieure et voyait un événement vide, alors que les objets jonchaient déjà le sol. Avec `bounce-back: true` par défaut, cela cassait silencieusement tous ces plugins. Border ne touche plus aux objets de l'événement : il s'exécute en priorité MONITOR et ne renvoie à l'intérieur que les objets que le serveur fait lui-même apparaître au tick suivant près du lieu de la mort. Si un autre plugin récupère les objets, rien n'est renvoyé ; s'ils subsistent, ils rebondissent à l'intérieur de la bordure exactement comme avant, en conservant les vitesses et les délais de disparition d'origine.
    - 🔺 **`[gamemode].border.color` est maintenant déclarée avec `true` par défaut,** de sorte que les joueurs ordinaires peuvent utiliser la commande de couleur comme le décrit la documentation. Elle n'avait jamais été déclarée dans `addon.yml` et retombait donc sur op uniquement. Les couleurs individuelles (`.red`, `.green`, `.blue`) restent en `op`. Si vous les accordiez explicitement pour contourner le problème, ces attributions restent valables.
    - 🔺 **`[gamemode].bordertype` renommée en `[gamemode].border.bordertype`,** qui est le nœud réellement vérifié par `BorderTypeCommand`. Sa valeur par défaut `false` est inchangée. Mettez à jour toute règle LuckPerms qui référence l'ancien nœud — il n'avait de toute façon aucun effet.
    - Les versions sont désormais publiées automatiquement sur CurseForge et Hangar en plus de Modrinth, et la fiche Modrinth couvre 1.21.5 – 1.21.11 et 26.1.x.

    Compatibilité : BentoBox API 3.12.0+, Minecraft 1.21.5 – 1.21.11 et 26.1.x, Java 21.

    [Release v4.8.5](https://github.com/BentoBoxWorld/Border/releases/tag/4.8.5)

## Traductions

{{ translations("Border") }}

## Source
Vous voulez contribuer? Voir le code source de cette documentation sur [GitHub](https://github.com/BentoBoxWorld/docs/blob/master/docs/addons/Border/).
