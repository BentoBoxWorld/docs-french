## Locales Disponibles

{{ translations("BentoBox") }}

## Formatage MiniMessage

BentoBox utilise [MiniMessage](https://docs.advntr.dev/minimessage/format.html) pour toutes les chaînes de locale. Cela signifie que vous pouvez utiliser les balises MiniMessage dans vos traductions pour appliquer un formatage de texte enrichi. Par exemple :

```yaml
my-message: "<green>Bienvenue sur l'île !</green>"
my-message: "<bold><red>Attention !</red></bold> Quelque chose s'est passé."
my-message: "<gradient:gold:yellow>Nom de l'île</gradient>"
```

Les anciens codes de couleur `§` ou `&` sont toujours pris en charge pour la compatibilité ascendante et seront automatiquement convertis au format MiniMessage lors du chargement.

## Balises de Livraison de Message

Les chaînes de locale peuvent contrôler la façon dont les messages sont livrés aux joueurs à l'aide de balises spéciales en ligne. Lorsqu'aucune balise de livraison n'est présente, le message est envoyé dans le chat (comportement par défaut).

### `[actionbar]`

Envoie le message en tant que message de **barre d'action** (le texte affiché au-dessus de la barre rapide).

```yaml
island-go: "[actionbar]Téléportation..."
```

### `[title]` et `[subtitle]`

Envoie le message en tant que **titre** superposé à l'écran. `[title]` affiche le grand texte d'en-tête et `[subtitle]` affiche un texte plus petit en dessous. `[subtitle]` n'est pas un type de livraison autonome — il ne fonctionne que comme séparateur à l'intérieur d'un message `[title]`. Sans `[title]`, il retombe sur le chemin du chat.

```yaml
# Titre avec sous-titre
island-go: "[title]Téléportation...[subtitle]Patientez une seconde."
# Titre uniquement (titre vide, texte en sous-titre)
scooping: "[title][subtitle]Vous avez ramassé la lave !"
```

### `[sound:nom:volume:pitch]`

Joue un **son** pour le joueur. Le volume et le pitch sont optionnels (par défaut `1.0`). Utilisez les noms de son séparés par des underscores depuis la liste des sons Bukkit/Minecraft (par ex. `entity_experience_orb_pickup`). La balise de son peut être combinée avec n'importe quelle balise de type de livraison.

```yaml
island-go: "[sound:entity_experience_orb_pickup:1:1][title]Téléportation...[subtitle]Patientez une seconde."
```

!!! note
    Les expéditeurs non-joueurs (par ex. la console) retomberont sur la sortie chat lorsque les balises de barre d'action ou de titre sont utilisées.

## Directives

* Nous avons maintenant un outil pour permettre les traductions de fichier sur [https://download.bentobox.world/translate.html](https://download.bentobox.world/translate.html). Cela s'exécute localement dans votre navigateur et peut aider la traduction. Soumettez de nouveaux fichiers en tant que PRs sur GitHub.
* Les Traducteurs obtiennent un badge spécial !
* Ne traduisez pas le texte à l'intérieur des crochets car ce sont des placeholders, par ex. [name] devrait rester en anglais
* Testez vos traductions - essayez de vérifier tout ce que vous pouvez avant de la soumettre
* N'incluez pas de publicité, de jurons ou de commentaires dérogatoires dans les traductions. Nous les vérifions avant d'accepter la PR.
* N'hésitez pas à poser des questions sur Discord à propos des traductions.

## Modes de jeu

- [AcidIsland](../gamemodes/AcidIsland/index.md#translations)
- [AOneBlock](../gamemodes/AOneBlock/index.md#translations)
- [Boxed](../gamemodes/Boxed/index.md#translations)
- [BSkyBlock](../gamemodes/BSkyBlock/index.md#translations)
- [CaveBlock](../gamemodes/CaveBlock/index.md#translations)
- [ChunkBlock](../gamemodes/ChunkBlock/index.md#translations)
- [Poseidon](../gamemodes/Poseidon/index.md#translations)
- [SkyGrid](../gamemodes/SkyGrid/index.md#translations)
- [Stranger Realms](../gamemodes/StrangerRealms/index.md#translations)
- [TradeWinds](../gamemodes/TradeWinds/index.md#translations)

## Compléments

- [Bank](../addons/Bank/index.md#translations)
- [Biomes](../addons/Biomes/index.md#translations)
- [Border](../addons/Border/index.md#translations)
- [CauldronWitchery](../addons/CauldronWitchery/index.md#translations)
- [Challenges](../addons/Challenges/index.md#translations)
- [Chat](../addons/Chat/index.md#translations)
- [CheckMeOut](../addons/CheckMeOut/index.md#translations)
- [ControlPanel](../addons/ControlPanel/index.md#translations)
- [DimensionalTrees](../addons/DimensionalTrees/index.md#translations)
- [ExtraMobs](../addons/ExtraMobs/index.md#translations)
- [FarmersDance](../addons/FarmersDance/index.md#translations)
- [Greenhouses](../addons/Greenhouses/index.md#translations)
- [InvSwitcher](../addons/InvSwitcher/index.md#translations)
- [IslandFly](../addons/IslandFly/index.md#translations)
- [Level](../addons/Level/index.md#translations)
- [Likes](../addons/Likes/index.md#translations)
- [Limits](../addons/Limits/index.md#translations)
- [MagicCobblestoneGenerator](../addons/MagicCobblestoneGenerator/index.md#translations)
- [TopBlock](../addons/TopBlock/index.md#translations)
- [TwerkingForTrees](../addons/TwerkingForTrees/index.md#translations)
- [Upgrades](../addons/Upgrades/index.md#translations)
- [Visit](../addons/Visit/index.md#translations)
- [VoidPortals](../addons/VoidPortals/index.md#translations)
- [Warps](../addons/Warps/index.md#translations)
