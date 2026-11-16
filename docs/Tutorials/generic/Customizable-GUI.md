# Personnaliser les Menus { #customizing-menus }

La plupart des menus que les joueurs voient dans BentoBox (le menu d'équipe, les paramètres de l'île, le menu Créer une Île, les maisons, la langue et bien d'autres) sont construits à partir de **modèles de panneaux** : des fichiers YAML que vous pouvez modifier. Vous pouvez changer le titre, la taille du menu, l'arrière-plan, l'icône que chaque bouton utilise, son texte et sa position.

Vous ne pouvez pas inventer de nouveaux types de boutons. Chaque menu ne comprend que les types de boutons que son code fournit. Pour un menu personnel avec des boutons qui exécutent des commandes, utilisez l'addon [ControlPanel](../../addons/ControlPanel/index.md).

## Où se trouvent les fichiers de menu { #where-the-menu-files-are }

| Menus de | Dossier |
|---|---|
| BentoBox | `plugins/BentoBox/panels/` |
| Un mode de jeu, pour ce mode de jeu uniquement | `plugins/BentoBox/addons/<GameMode>/panels/` |
| Un addon (Level, Challenges, Warps…) | `plugins/BentoBox/addons/<Addon>/panels/` |

BentoBox écrit ses modèles dans `plugins/BentoBox/panels/` la première fois que chaque menu est utilisé. Les addons écrivent les leurs dans leur propre dossier.

### Les menus de BentoBox { #bentoboxs-menus }

| Fichier | Menu | Un mode de jeu peut-il avoir sa propre copie ? |
|---|---|---|
| `island_creation_panel.yml` | Choisir une île lors de la création ou de la réinitialisation | Oui |
| `island_homes_panel.yml` | `/island homes` | Oui |
| `language_panel.yml` | `/island language` | Oui |
| `settings_panel.yml` | `/island settings` | Oui |
| `admin_settings_panel.yml` | `/bsbadmin settings` | Oui |
| `command_ranks_panel.yml` | Page Rangs de Commandes dans le menu des paramètres | Oui |
| `team_panel.yml` | `/island team` | Non |
| `team_invite_panel.yml` | L'écran d'invitation dans le menu d'équipe | Non |
| `placeholder_panel.yml`, `placeholder_list_panel.yml` | Le navigateur de placeholders | Non |

**Menus différents par mode de jeu :** copiez le fichier de `plugins/BentoBox/panels/` dans le dossier `panels` du mode de jeu (créez le dossier s'il n'existe pas) et modifiez la copie. Par exemple, `plugins/BentoBox/addons/AOneBlock/panels/island_creation_panel.yml` change le menu Créer une Île pour AOneBlock uniquement. Les autres modes de jeu continuent d'utiliser la version de BentoBox.

### Les menus des addons { #addon-menus }

Les addons qui utilisent des modèles incluent Level (`top_panel`, `value_panel`, `detail_panel`, `donation_panel`), Challenges, Biomes, Warps, Upgrades, Likes, Visit, TopBlock, CheckMeOut, MagicCobblestoneGenerator, AOneBlock (`phases_panel`) et CauldronWitchery. Regardez dans le dossier `panels` de chaque addon. Ils utilisent le même format que celui présenté ci-dessous.

## Effectuer une modification { #making-a-change }

1. Empêchez les joueurs d'ouvrir le menu, ou faites-le sur un serveur de test en premier.
2. Modifiez le fichier `.yml`. Gardez une copie de l'original.
3. Exécutez `/bentobox reload`. Ceci ferme les menus ouverts et recharge les modèles.
4. Ouvrez le menu en jeu et vérifiez-le.

Si un menu ne s'ouvre pas ou n'affiche rien, le YAML est probablement invalide. Vérifiez la console du serveur pour une erreur et collez le fichier dans un vérificateur YAML. **Pour récupérer la version par défaut**, supprimez le fichier. BentoBox copiera sa version par défaut la prochaine fois que le menu s'ouvrira. Pour un fichier d'addon, redémarrez le serveur.

## Modifications courantes { #common-changes }

### Changer le titre ou le texte des boutons { #change-the-title-or-button-text }

Le texte peut être soit du texte brut, soit une **clé de locale**. Les modèles par défaut utilisent des clés de locale pour que les menus soient traduits :

```yaml
team_panel:
  title: commands.island.team.gui.titles.team-panel
```

- **Changer le texte dans toutes les langues :** modifiez cette clé dans les fichiers de locale (`plugins/BentoBox/locales/`, ou le dossier `locales` de l'addon). Voir [Langues et Messages](../../BentoBox/About/Multilingual.md).
- **Utiliser le même texte pour tout le monde :** remplacez la clé par votre propre texte, par exemple `title: "&6Mon Équipe"`.

### Changer l'arrière-plan ou la bordure { #change-the-background-or-border }

```yaml
  background:
    icon: GRAY_STAINED_GLASS_PANE
    title: "&b&r"     # n'affiche pas de nom
  border:
    icon: LIGHT_BLUE_STAINED_GLASS_PANE
    title: "&b&r"
```

Supprimez la section `background` ou `border` pour laisser ces emplacements vides. `"&b&r"` est la façon habituelle d'afficher un objet sans nom ; Minecraft affiche toujours une infobulle, elle ne peut donc pas être complètement masquée.

### Changer l'icône d'un bouton { #change-a-buttons-icon }

Réglez `icon` sur le bouton. N'importe quel objet fonctionne, y compris les objets avec des données, les couleurs de potion et les têtes de joueurs. Voir [Format d'Élément](../../BentoBox/ItemParser.md).

```yaml
      icon: DIAMOND
      icon: tipped_arrow[potion_contents={custom_color:11546150}]
```

Certains boutons choisissent leur propre icône si vous laissez `icon` vide. Par exemple, le menu d'équipe affiche la tête du joueur et le menu Créer une Île affiche l'icône de l'île.

### Déplacer un bouton { #move-a-button }

Les boutons sont placés par **ligne** (1–6) et **colonne** (1–9) sous `content`. Pour en déplacer un, changez son numéro de ligne ou de colonne :

```yaml
  content:
    1:        # ligne 1
      1:      # colonne 1
        data:
          type: STATUS
```

### Agrandir un menu { #make-a-menu-taller }

Les menus se réduisent pour s'adapter aux lignes qui ont des boutons. Pour conserver les lignes même quand elles sont vides, utilisez `force-shown` :

```yaml
  force-shown: 6        # toujours afficher les lignes 1 à 6
  force-shown: [2, 4]   # toujours afficher les lignes 2 et 4
```

Cela n'ajoute que des lignes vides. Pour afficher **plus d'éléments par page** (plus d'îles, plus de maisons), ajoutez aussi plus de boutons répétables. La page [Agrandir le Menu Créer une Île](Bigger-Create-Island-Menu.md) vous explique comment faire.

### Supprimer un bouton { #remove-a-button }

Supprimez le bouton de `content`. L'emplacement affichera alors l'arrière-plan. Certains boutons sont nécessaires pour que le menu fonctionne : gardez les boutons `NEXT`/`PREVIOUS` dans les menus qui peuvent avoir plusieurs pages.

## Comment un modèle est organisé { #how-a-template-is-laid-out }

Chaque modèle a les mêmes parties. Cet exemple raccourci est basé sur le menu Créer une Île :

```yaml
island_creation_panel:          # doit correspondre au nom du fichier
  title: panels.island_creation.title
  type: INVENTORY               # INVENTORY (coffre), HOPPER (5 emplacements) ou DROPPER (9 emplacements)
  background:
    icon: BLACK_STAINED_GLASS_PANE
    title: "&b&r"
  border:
    icon: BLACK_STAINED_GLASS_PANE
    title: "&b&r"
  force-shown: []
  content:
    2:
      2: blueprint_bundle_button    # un nom fait référence à un bouton dans `reusable`
      3: blueprint_bundle_button
    3:
      9:                            # ou définissez le bouton directement ici
        icon: ARROW
        title: panels.buttons.next.name
        description: panels.buttons.next.description
        data:
          type: NEXT
        actions:
          next:
            click-type: UNKNOWN
            tooltip: panels.tips.click-to-next
  reusable:
    blueprint_bundle_button:
      title: panels.island_creation.buttons.bundle.name
      description: panels.island_creation.buttons.bundle.description
      data:
        type: BUNDLE
      actions:
        select:
          click-type: UNKNOWN
          tooltip: panels.tips.click-to-choose
```

### Paramètres des boutons { #button-settings }

| Paramètre | Ce qu'il fait |
|---|---|
| `icon` | L'objet affiché. Voir [Format d'Élément](../../BentoBox/ItemParser.md) |
| `title` | Le nom de l'objet : texte ou une clé de locale |
| `description` | Les lignes sous le nom : texte ou une clé de locale |
| `data` | **Ce qu'est le bouton.** `type` choisit le type de bouton (voir ci-dessous). Certains types prennent des paramètres supplémentaires, par exemple `tab` sur un bouton d'onglet de paramètres |
| `actions` | Ce que chaque clic fait et la ligne d'infobulle ajoutée pour lui |
| `fallback` | Un autre bouton à afficher quand celui-ci ne peut pas être affiché, par exemple quand il n'y a rien pour remplir un emplacement sur la dernière page. Il peut être un bouton complet ou le nom d'un bouton `reusable`. Nécessite BentoBox 3.23.0 ou ultérieur |

### Boutons répétables (`reusable`) { #repeating-buttons-reusable }

Les menus qui énumèrent des choses (îles, maisons, membres d'équipe, langues, drapeaux) utilisent un design de bouton pour chaque entrée. Définissez-le une fois sous `reusable` et mettez son nom dans chaque emplacement où une entrée peut apparaître. Le menu remplit ces emplacements dans l'ordre et parcourt le reste.

### Actions de clic { #click-actions }

Chaque action a un nom, un type de clic et une infobulle :

```yaml
        actions:              # le bouton de membre du menu d'équipe
          kick:
            click-type: SHIFT_RIGHT
            tooltip: commands.island.team.gui.tips.SHIFT_RIGHT.kick
          setowner:
            click-type: SHIFT_LEFT
            tooltip: commands.island.team.gui.tips.SHIFT_LEFT.setowner
```

- `click-type` est un clic Minecraft : `LEFT`, `RIGHT`, `SHIFT_LEFT`, `SHIFT_RIGHT`, `MIDDLE`, `DROP` et ainsi de suite. `UNKNOWN` signifie n'importe quel clic.
- Le nom de l'action (`kick`, `setowner`) est ce que le menu fait. Utilisez les noms déjà dans le fichier par défaut. Vous pouvez changer quel clic déclenche une action, ou supprimer une action que vous ne voulez pas que les joueurs utilisent du menu.
- Les infobulles sont ajoutées sous la description, dans l'ordre où les actions sont énumérées.

### Types de boutons dans les menus de BentoBox { #button-types-in-bentoboxs-menus }

| Menu | Types de boutons (`data: type:`) |
|---|---|
| Créer une Île | `BUNDLE`, `NEXT`, `PREVIOUS` |
| Maisons | `ISLAND`, `NEXT`, `PREVIOUS` |
| Langue | `LOCALE`, `NEXT`, `PREVIOUS` |
| Équipe | `STATUS`, `MEMBER`, `RANK`, `INVITE`, `INVITED` |
| Invitation d'équipe | `PROSPECT`, `SEARCH`, `BACK`, `NEXT`, `PREVIOUS` |
| Paramètres / paramètres administrateur | `FLAG`, `TAB`, `MODE`, `RESET`, `NEXT`, `PREVIOUS` |
| Rangs de Commandes | `COMMAND`, `NEXT`, `PREVIOUS` |
| Placeholders | `BENTOBOX`, `ADDON`, `PLACEHOLDER`, `BACK`, `NEXT`, `PREVIOUS` |

Les fichiers par défaut ont des commentaires expliquant chacun. Les menus de paramètres sont couverts en détail dans [Protection, Drapeaux et Rangs](../../BentoBox/Island-Protection,-Flags-&-Ranks.md#customizing-the-settings-panel).

## Dépannage { #troubleshooting }

**Ma modification ne s'affiche pas.**
Exécutez `/bentobox reload`, puis rouvrez le menu. Si le mode de jeu a sa propre copie dans `addons/<GameMode>/panels/`, cette copie est utilisée à la place de celle dans `plugins/BentoBox/panels/`.

**Le menu est vide ou ne s'ouvre pas après la modification.**
Le YAML est invalide ou le nom du niveau supérieur ne correspond plus au nom du fichier. Vérifiez la console, corrigez le fichier, ou supprimez-le pour récupérer la version par défaut.

**J'ai ajouté des lignes mais rien n'apparaît dedans.**
`force-shown` ajoute seulement de l'espace. Ajoutez le bouton répétable (par exemple `blueprint_bundle_button`) aux nouveaux emplacements.

**Le texte s'affiche comme `commands.island.…` au lieu de mots.**
Cette clé est manquante du fichier de locale pour la langue du joueur. Ajoutez-la, ou utilisez du texte brut à la place.

**Je veux un bouton qui exécute une commande.**
Les modèles ne peuvent pas faire cela. Utilisez l'addon [ControlPanel](../../addons/ControlPanel/index.md).

## Voir aussi { #see-also }

- [Agrandir le Menu Créer une Île](Bigger-Create-Island-Menu.md) : un exemple complet travaillé
- [Format d'Élément](../../BentoBox/ItemParser.md) : écrire des icônes
- [Langues et Messages](../../BentoBox/About/Multilingual.md) : changer le texte du menu
- [API du Panneau Modélisé](../api/Templated-Panel.md) : pour les développeurs ajoutant des modèles à leurs propres addons
