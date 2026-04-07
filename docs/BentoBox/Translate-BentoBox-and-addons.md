## Locales Disponibles

{{ translations(2855, ["cs", "de", "es", "fr", "hu", "id", "it", "ja", "lv", "pl", "pt", "ro", "ru", "tr", "vi", "zh-CN", "zh-HK", "zh-TW", "hr", "ko", "uk", "nl"]) }}

## Directives

* Nous avons maintenant un outil pour permettre les traductions de fichier sur [https://download.bentobox.world/translate.html](https://download.bentobox.world/translate.html). Cela s'exécute localement dans votre navigateur et peut aider la traduction. Soumettez de nouveaux fichiers en tant que PRs sur GitHub.
* Les Traducteurs obtiennent un badge spécial !
* Ne traduisez pas le texte à l'intérieur des crochets car ce sont des placeholders, par ex. [name] devrait rester en anglais
* Testez vos traductions - essayez de vérifier tout ce que vous pouvez avant de la soumettre
* N'incluez pas de publicité, de jurons ou de commentaires dérogatoires dans les traductions. Nous les vérifions avant d'accepter la PR.
* N'hésitez pas à poser des questions sur Discord à propos des traductions.

## Formatage MiniMessage

BentoBox utilise [MiniMessage](https://docs.advntr.dev/minimessage/format.html) pour toutes les chaînes de localisation. Cela signifie que vous pouvez utiliser les balises MiniMessage dans vos traductions pour appliquer une mise en forme de texte enrichi. Par exemple :

```
my-message: ""
my-message: "<bold><red>Warning!</red></bold> Something happened."
my-message: "<gradient:gold>Island Name"
```

Les codes couleur `§` ou `&` hérités sont toujours pris en charge pour la rétrocompatibilité et seront automatiquement convertis au format MiniMessage lors du chargement.

## Balises de Livraison des Messages

Les chaînes de localisation peuvent contrôler la manière dont les messages sont envoyés aux joueurs en utilisant des balises spéciales. En l'absence de balise de livraison, le message est envoyé dans le chat (comportement par défaut).

### `[actionbar]`

Envoie le message sous forme de message dans la **barre d'action** (le texte affiché au-dessus de la barre de raccourcis).

```yaml
island-go: "[actionbar]Teleporting..."
```

### `[title]` et `[subtitle]`

Envoie le message sous forme de superposition de **titre** à l'écran. `[title]` affiche le grand texte de titre et `[subtitle]` affiche un texte plus petit en dessous. `[subtitle]` n'est pas un type de livraison autonome — il doit toujours être associé à `[title]`.

```yaml
# Title with subtitle
island-go: "[title]Teleporting...[subtitle]Wait a second."
# Title only (empty title, text as subtitle)
scooping: "[title][subtitle]You scooped the lava!"
```

### `[sound:name:volume:pitch]`

Joue un **son** pour le joueur. Le volume et la hauteur sont optionnels (valeur par défaut `1.0`). Utilisez des noms de sons séparés par des underscores provenant de la liste de sons Bukkit/Minecraft (par ex. `entity_experience_orb_pickup`). Le son est joué à l'emplacement du joueur.

```yaml
island-go: "[sound:entity_experience_orb_pickup:1:1][title]Teleporting...[subtitle]Wait a second."
```

!!! note
    Les expéditeurs non-joueurs (par ex. la console) basculeront vers la sortie dans le chat lorsque des balises de barre d'action ou de titre sont utilisées.

## Compléments
- [AcidIsland](/gamemodes/AcidIsland/#translations)
- [BSkyBlock](/gamemodes/BSkyBlock/#translations)
- [CaveBlock](/gamemodes/CaveBlock/#translations)
- [SkyGrid](/gamemodes/SkyGrid/#translations)
- [Biomes](/addons/Biomes/#translations)
- [Border](/addons/Border/#translations)
- [CauldronWitchery](/addons/CauldronWitchery/#translations)
- [Challenges](/addons/Challenges/#translations)
- [Chat](/addons/Chat/#translations)
- [ControlPanel](/addons/ControlPanel/#translations)
- [DimensionalTrees](/addons/DimensionalTrees/#translations)
- ~~[ExtraMobs](Addons)~~
- [Greenhouses](/addons/Greenhouses/#translations)
- [IslandFly](/addons/IslandFly/#translations)
- ~~[InvSwitcher](Addons)~~
- [Level](/addons/Level/#translations)
- [Likes](/addons/Likes/#translations)
- [Limits](/addons/Limits/#translations)
- [MagicCobblestoneGenerator](/addons/MagicCobblestoneGenerator/#translations)
- ~~[TwerkingForTrees](Addons)~~
- [VoidPortals](/addons/VoidPortals/#translations)
