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
**Description**: Définit le type de bordure.
**Permission**: `[gamemode].border.set-type`. Défaut: `true`.
**Exemple**: `/[player command] border type barrier`

### couleur {red|green|blue}
**Commande**: `/[player command] color {red | green | blue}`  
**Description**: Définit la couleur de la bordure monde vanilla pour le joueur. S'applique uniquement avec le type de bordure vanilla.  
**Permission**: `[gamemode].color.red`, `[gamemode].color.green`, `[gamemode].color.blue` (ou `[gamemode].color.*` pour toutes). Défaut: `op`.  
**Exemple**: `/[player command] color green`

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

### Afficher les warps sur la carte
Contrôle si la fonctionnalité de couleur de bordure monde vanilla est disponible. Les couleurs par joueur sont définies avec la commande `/[player_command] color`. Nécessite un plugin de carte web (Dynmap ou BlueMap) et le hook de carte BentoBox.

```yml
show-warps-on-map: true
```

## Placeholders

| Placeholder | Description | Version |
|---|---|---|
| `%Border_color%` | La couleur de bordure actuelle du joueur (`red`, `green` ou `blue`) | 4.8.0 |

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

## Traductions

{{ translations("Border") }}

## Source
Vous voulez contribuer? Voir le code source de cette documentation sur [GitHub](https://github.com/BentoBoxWorld/docs/blob/master/docs/addons/Border/).
