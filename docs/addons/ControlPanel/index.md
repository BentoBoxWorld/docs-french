# ControlPanel

**ControlPanel** donne à vos joueurs un menu interface graphique cliquable pour exécuter leurs commandes d'île les plus utilisées - aucune saisie requise. Les administrateurs du serveur construisent des panneaux entièrement personnalisables en utilisant un simple fichier YAML, avec support pour plusieurs actions de clic, des icônes personnalisées et des placeholders en direct.

Créé et maintenu par [BONNe](https://github.com/BONNe).

{{ addon_description("ControlPanel") }}

## Installation

1. Placez le fichier jar du addon ControlPanel dans le dossier `addons` du plugin BentoBox.
2. Redémarrez le serveur. ControlPanel créera un `controlPanelTemplate.yml` par défaut dans `plugins/BentoBox/addons/ControlPanel/`.
3. Modifiez `controlPanelTemplate.yml` pour construire vos panneaux (voir [Configuration](#configuration) ci-dessous).
4. Importez les panneaux avec la commande admin :
```
/{admin} cp import
```

!!! tip
    Remplacez `{admin}` par l'étiquette de la commande admin de votre mode de jeu, par exemple `bsb` pour BSkyBlock, `oa` pour AOneBlock, `acid` pour AcidIsland.

## Commandes

### Commande du joueur

| Commande | Description | Permission |
|---|---|---|
| `/[label] controlpanel` | Ouvre le panneau de contrôle assigné au joueur | `[gamemode].controlpanel` |
| `/[label] cp` | Alias raccourci de la commande ci-dessus | `[gamemode].controlpanel` |

Remplacez `[label]` par la commande du joueur du mode de jeu, par exemple `island` pour BSkyBlock ou `ob` pour AOneBlock.

Le panneau affiché dépend des permissions du joueur. Les joueurs sans une permission de panneau spécifique voient le panneau marqué `defaultPanel: true`. Si un joueur a la permission pour un panneau particulier via `[gamemode].controlpanel.panel.<suffix>`, ce panneau est affiché à la place.

### Commande Admin

| Commande | Description | Permission |
|---|---|---|
| `/{admin} cp import` | Importe les panneaux de `controlPanelTemplate.yml` | `[gamemode].controlpanel.admin` |
| `/{admin} cp import <filename>` | Importe les panneaux d'un fichier YAML personnalisé | `[gamemode].controlpanel.admin` |

Le nom du fichier n'a pas besoin de l'extension `.yml` — il est ajouté automatiquement. Le fichier doit être situé dans `plugins/BentoBox/addons/ControlPanel/`.

!!! warning
    Si les panneaux existent déjà pour le mode de jeu, l'importation demandera une confirmation avant de les remplacer.

## Permissions

| Permission | Défaut | Description |
|---|---|---|
| `[gamemode].controlpanel` | `true` | Permet au joueur d'ouvrir le panneau de contrôle |
| `[gamemode].controlpanel.admin` | `op` | Permet l'utilisation de la commande admin d'importation |
| `[gamemode].controlpanel.panel.default` | `true` | Accordez l'accès au panneau par défaut |
| `[gamemode].controlpanel.panel.<suffix>` | — | Accordez l'accès à un panneau personnalisé avec le suffixe donné |

Remplacez `[gamemode]` par le nom du mode de jeu en minuscules, par exemple `bskyblock`, `acidisland`, `aoneblock`, `caveblock`, `skygrid`.

!!! note
    Si un joueur a plusieurs permissions de panneau, le premier panneau marqué `defaultPanel: true` parmi ceux auxquels il a accès est affiché. Si le joueur a des permissions de caractère générique `*`, le premier panneau par défaut défini est utilisé.

## Configuration

ControlPanel utilise deux fichiers :

- `config.yml` — paramètres généraux du addon
- `controlPanelTemplate.yml` — définit les panneaux et les boutons

Les deux sont situés dans `plugins/BentoBox/addons/ControlPanel/`.

### config.yml

Le fichier de configuration principal a un paramètre :

??? note "disabled-gamemodes"
    Une liste des noms du addon GameMode où ControlPanel ne devrait pas fonctionner. ControlPanel ne se connectera pas à ces modes de jeu.

    Défaut: `[]`

    Exemple:
    ```yaml
    disabled-gamemodes:
      - BSkyBlock
      - AcidIsland
    ```

### controlPanelTemplate.yml

Ce fichier définit tous les panneaux de contrôle et leurs boutons. Après l'avoir modifié, exécutez `/{admin} cp import` pour charger vos modifications.

#### Structure du panneau

```yaml
panel-list:
  <panel-key>:
    defaultPanel: true|false
    panelName: '<title>'
    permission: '<suffix>'
    buttons:
      <slot>:
        name: '<display name>'
        material: MATERIAL_NAME
        icon: 'namespace:item_id'
        itemsadder: 'namespace:item_id'
        description: |-
          line one
          line two
        command: '<left-click command>'
        right_click_command: '<right-click command>'
        shift_click_command: '<shift+left-click command>'
```

#### Champs du panneau

| Champ | Type | Description |
|---|---|---|
| `defaultPanel` | booléen | Définissez sur `true` pour afficher ce panneau aux joueurs sans permission de panneau spécifique. |
| `panelName` | chaîne | Titre de l'interface graphique d'inventaire. Supporte les codes de couleur `&`. |
| `permission` | chaîne | Le suffixe ajouté à `[gamemode].controlpanel.panel.<suffix>`. Les joueurs avec cette permission voient ce panneau. |

#### Champs du bouton

| Champ | Requis | Description |
|---|---|---|
| `slot` | Oui | Numéro d'emplacement d'inventaire (0–53). Utilisez une plage entre guillemets comme `"0-8"` pour remplir plusieurs emplacements avec le même bouton. |
| `name` | Oui | Nom d'affichage du bouton. Supporte les codes de couleur `&`. |
| `material` | Non | Matériel Minecraft vanille, par exemple `GRASS_BLOCK`. Utilisé comme icône de secours. |
| `icon` | Non | Format BentoBox `ItemParser`, par exemple `minecraft:diamond_block`. Prend priorité sur `material`. |
| `itemsadder` | Non | ID d'élément personnalisé [ItemsAdder](https://github.com/LoneDev6/ItemsAdder), par exemple `iasurvival:ruby`. Nécessite l'installation d'ItemsAdder. Revient à du papier s'il ne l'est pas. |
| `description` | Non | Lignes de lore affichées sous le nom du bouton. Supporte les codes de couleur `&`, multi-lignes avec `|-`, PlaceholderAPI `%placeholders%`, et substitution `[gamemode]`. |
| `command` | Non | Commande exécutée au clic gauche (et comme secours pour tous les autres types de clic). |
| `right_click_command` | Non | Commande exécutée au clic droit ou shift+clic droit. Revient à `command` si omis. |
| `shift_click_command` | Non | Commande exécutée au shift+clic gauche. Revient à `command` si omis. |

!!! info "Priorité de l'icône"
    Si plusieurs champs d'icône sont spécifiés, la priorité est : `itemsadder` > `icon` > `material`. Si aucun n'est défini, le bouton utilise par défaut `PAPER`.

#### Types de clic

Chaque bouton peut répondre différemment selon la façon dont le joueur le clique :

| Action de clic | Commande utilisée |
|---|---|
| Clic gauche | `command` |
| Clic droit | `right_click_command` (revient à `command`) |
| Shift + Clic gauche | `shift_click_command` (revient à `command`) |
| Shift + Clic droit | `right_click_command` (revient à `command`) |
| Tout autre clic | `command` |

#### Placeholders de commande

Ces placeholders peuvent être utilisés dans les champs `command`, `right_click_command`, et `shift_click_command` :

| Placeholder | Remplacé par |
|---|---|
| `[label]` | L'étiquette de la commande du joueur du mode de jeu, par exemple `island`, `ob` |
| `[player]` | Le nom d'utilisateur du joueur qui a cliqué |
| `[server]` | Fait exécuter la commande par la console du serveur au lieu du joueur |

#### Placeholders de description

Ces placeholders peuvent être utilisés dans le champ `description` :

| Placeholder | Remplacé par |
|---|---|
| `[gamemode]` | Nom du mode de jeu en minuscules, par exemple `bskyblock`, `aoneblock` |
| `%placeholder%` | Tout placeholder PlaceholderAPI enregistré |

#### Disposition des emplacements

L'interface graphique est un inventaire de coffre. Chaque ligne a 9 emplacements (0–8), et le maximum est un coffre de 6 lignes avec 54 emplacements (0–53):

```
Ligne 1:  0  1  2  3  4  5  6  7  8
Ligne 2:  9 10 11 12 13 14 15 16 17
Ligne 3: 18 19 20 21 22 23 24 25 26
Ligne 4: 27 28 29 30 31 32 33 34 35
Ligne 5: 36 37 38 39 40 41 42 43 44
Ligne 6: 45 46 47 48 49 50 51 52 53
```

Utilisez une plage entre guillemets comme `"0-8"` pour placer le même bouton sur toute une ligne. Ceci est utile pour les bordures décoratives.

## Exemple: Panneaux par défaut et VIP

Ci-dessous se trouve un exemple pratique montrant deux panneaux — un panneau par défaut pour tous les joueurs et un panneau VIP pour les donateurs. Il démontre les plages d'emplacements, les actions de clic multiples, les commandes de console, les placeholders PlaceholderAPI, et les icônes ItemsAdder.

```yaml
panel-list:

  # Default panel — shown to all players
  default:
    defaultPanel: true
    panelName: '&0&l Control Panel'
    permission: 'default'
    buttons:

      # Decorative top border using a slot range
      "0-8":
        name: ' '
        material: BLACK_STAINED_GLASS_PANE
        description: ''
        command: ''

      # Go to island with multiple click actions
      9:
        name: '&a&l Go to Island'
        icon: minecraft:grass_block
        description: |-
          &7 Left-click: teleport to your island
          &7 Right-click: go to nether
          &7 Shift-click: set home
          &7 Island level: &e%Level_[gamemode]_island_level%
        command: '[label] go'
        right_click_command: '[label] go nether'
        shift_click_command: '[label] sethome'

      10:
        name: '&e&l Set Home'
        icon: minecraft:white_bed
        description: |-
          &7 Set your island home
          &7 to your current location.
        command: '[label] sethome'

      11:
        name: '&b&l Team'
        icon: minecraft:player_head
        description: |-
          &7 View and manage
          &7 your island team.
        command: '[label] team'

      13:
        name: '&6&l Settings'
        icon: minecraft:anvil
        description: |-
          &7 Configure your island
          &7 protection settings.
        command: '[label] settings'

      # Console command — runs as server, not player
      17:
        name: '&c&l Report Bug'
        icon: minecraft:writable_book
        description: |-
          &7 Opens a support ticket.
        command: '[server] ticket create [player] bug-report'

  # VIP panel — players need bskyblock.controlpanel.panel.vip
  vip:
    defaultPanel: false
    panelName: '&d&l VIP Control Panel'
    permission: 'vip'
    buttons:

      "0-8":
        name: ' '
        material: PURPLE_STAINED_GLASS_PANE
        description: ''
        command: ''

      9:
        name: '&a&l Go to Island'
        icon: minecraft:grass_block
        description: |-
          &7 Teleport to your island.
        command: '[label] go'

      # VIP exclusive — grants a kit via console
      13:
        name: '&d&l VIP Kit'
        icon: minecraft:chest
        description: |-
          &d VIP exclusive!
          &7 Claim your weekly VIP kit.
        command: '[server] kit vipweekly [player]'

      # ItemsAdder custom icon example
      14:
        name: '&6&l VIP Perks'
        itemsadder: 'iasurvival:vip_star'
        description: |-
          &7 Browse all your VIP perks.
        command: 'vipperks'
```

## Conseils

??? tip "Créer des bordures décoratives"
    Utilisez des plages d'emplacements avec des vitres teintées pour créer des bordures nettes autour de votre panneau. Définissez `command: ''` et `name: ' '` pour rendre le bouton non interactif :
    ```yaml
    "0-8":
      name: ' '
      material: BLACK_STAINED_GLASS_PANE
      description: ''
      command: ''
    ```

??? tip "Exécuter les commandes en tant que console"
    Préfixez une commande avec `[server]` pour l'exécuter en tant que console du serveur. Cela vous permet d'accorder des kits, d'exécuter des commandes d'économie, ou d'effectuer des actions admin que le joueur n'aurait pas la permission d'exécuter directement :
    ```yaml
    command: '[server] give [player] diamond 64'
    ```

??? tip "Utiliser plusieurs panneaux pour les rangs"
    Créez des panneaux séparés pour différents groupes de joueurs tels que par défaut, VIP ou staff. Assignez-les en utilisant des permissions comme `bskyblock.controlpanel.panel.vip` ou `bskyblock.controlpanel.panel.staff`. Chaque groupe voit un panneau adapté aux boutons appropriés.

??? tip "Utiliser PlaceholderAPI dans les descriptions"
    Les descriptions des boutons sont traitées par PlaceholderAPI au moment où le panneau est ouvert, donc elles affichent toujours des données en direct. Utilisez `[gamemode]` dans les noms des placeholders afin que le même modèle fonctionne dans les modes de jeu :
    ```yaml
    description: |-
      &7 Level: &e%Level_[gamemode]_island_level%
      &7 Rank: &6%Level_[gamemode]_island_rank%
      &7 Balance: &a%vault_balance%
    ```

??? tip "Recharger après les modifications"
    Après avoir modifié `controlPanelTemplate.yml`, exécutez `/{admin} cp import` pour recharger. Si vous avez apporté des modifications à `config.yml`, utilisez la commande de rechargement de BentoBox à la place : `/{admin} bentobox reload`.

## FAQ

??? question "Comment puis-je modifier le ControlPanel?"
    ControlPanel stocke les panneaux dans la base de données, mais vous les modifiez via le fichier modèle. Après avoir apporté des modifications à `controlPanelTemplate.yml`, importez-les en exécutant `/{admin} controlpanel import`. Vous pouvez également créer des fichiers modèles supplémentaires et les importer par nom : `/{admin} controlpanel import myPanels`.

??? question "Puis-je avoir différents panneaux pour différents utilisateurs?"
    Oui. Définissez plusieurs panneaux dans le fichier modèle, chacun avec un suffixe `permission` différent. Assignez ensuite aux joueurs la permission correspondante, par exemple `bskyblock.controlpanel.panel.vip`. Les joueurs sans une permission de panneau spécifique voient le panneau marqué `defaultPanel: true`.

??? question "Quels types d'icônes sont supportés?"
    ControlPanel supporte trois types d'icônes, vérifiés dans cet ordre de priorité : éléments personnalisés ItemsAdder (champ `itemsadder`), format BentoBox ItemParser (champ `icon`), et matériaux Minecraft vanille (champ `material`). Si aucun n'est spécifié, le bouton utilise par défaut du papier.

??? question "Puis-je exécuter une commande en tant que console du serveur?"
    Oui. Préfixez la commande avec `[server]` et elle sera exécutée par la console au lieu du joueur. Vous pouvez également utiliser `[player]` dans la chaîne de commande pour insérer le nom du joueur qui a cliqué. Par exemple : `[server] give [player] diamond 64`.

??? question "Un seul bouton peut-il faire différentes choses selon la façon dont je le clique?"
    Oui. Chaque bouton supporte jusqu'à trois commandes différentes : `command` pour le clic gauche, `right_click_command` pour le clic droit, et `shift_click_command` pour shift+clic gauche. Si une commande de clic spécifique n'est pas définie, elle revient à la `command` régulière.

??? question "Pouvez-vous ajouter une fonctionnalité X?"
    Veuillez l'ajouter à la liste [ici](https://github.com/BentoBoxWorld/ControlPanel/issues).

## Traductions

{{ translations(3135, ["cs", "de", "es", "fr", "lv", "zh-CN", "zh-TW", "ko", "pl", "ru", "id", ]) }}
