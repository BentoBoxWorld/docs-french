# Format de Fichier Blueprint

**Version de spécification 2**

Cette page documente le format JSON sur disque qu'utilise BentoBox pour les blueprints d'île (fichiers `.blueprint`) et les bundles de blueprints (fichiers bundle `.json`). C'est le compagnon lisible par l'humain aux [JSON Schemas](https://github.com/BentoBoxWorld/BentoBox/tree/develop/schemas) lisibles par la machine livrés dans le dépôt BentoBox, qui peuvent être utilisés pour valider les fichiers dans les éditeurs ou CI.

Si vous voulez *faire* des blueprints dans le jeu, voir la page [Blueprints](Blueprints.md). Cette page est pour les développeurs et utilisateurs avancés qui génèrent, modifient ou valident les fichiers blueprint directement.

## Historique de révision

| Version | Date | Version BentoBox | Description |
|---|---|---|---|
| 1 | 2019-06-09 | [1.5.0](https://github.com/BentoBoxWorld/BentoBox/releases/tag/1.5.0) | Version initiale, dérivée du format Schem de BentoBox |
| 1.1 | 2026 | 2.x | Stockage changé de binaire zippé à JSON simple ; `.blueprint` est devenu l'extension primaire |
| 2 | 2026-08-14 | 3.22.x | Spécification complète au niveau des champs générée à partir du code source ; JSON Schemas publiés |

## Types de fichiers

| Extension | Format | Statut |
|---|---|---|
| `.blueprint` | JSON UTF-8 simple contenant un seul objet [Blueprint](#blueprint) | Actuel |
| `.blu` | Archive ZIP contenant une seule entrée du même JSON | Hérité — toujours chargeable, jamais écrit |
| `<uniqueId>.json` | JSON UTF-8 simple contenant un seul objet [BlueprintBundle](#blueprintbundle) | Actuel |

Les deux types de fichiers se trouvent dans le dossier `blueprints/` d'un addon de mode de jeu, par exemple `plugins/BentoBox/addons/BSkyBlock/blueprints/`. Un bundle référence ses blueprints par `name`, et les fichiers `.blueprint` référencés doivent se trouver dans le même dossier.

## Règles de sérialisation

Les blueprints sont écrits avec Gson. Ces règles s'appliquent partout et expliquent les formes que vous verrez ci-dessous :

- Seuls les champs listés dans cette spécification sont émis ; les producteurs ne doivent pas ajouter d'autres clés.
- **Vecteurs** (`org.bukkit.util.Vector`) sont un tableau JSON à 3 éléments de nombres : `[x, y, z]`. Les positions de bloc contiennent généralement des entiers, mais le type sous-jacent est double.
- **Maps indexées par un Vecteur** utilisent la forme de clé de map complexe de Gson : un *tableau de paires* JSON — `[[<vecteur>, <valeur>], ...]` — **pas** un objet JSON. Cela s'applique à `blocks`, `attached` et `entities`.
- **Maps indexées par une énumération** (par exemple, la map `blueprints` d'un bundle) sont des objets JSON ordinaires avec le nom de l'énumération comme clé.
- **Maps indexées par un entier** (slot d'inventaire → article) sont des objets JSON avec des clés entières stringifiées (`"0"`, `"13"`, …).
- **ItemStacks** sont sérialisés en YAML Bukkit (via `ConfigurationSerializable`) et stockés comme une chaîne JSON *string*. Traitez la valeur comme un document YAML opaque analysable par `YamlConfiguration#loadFromString`.
- **Enumerations** sont sérialisées par leur Java `name()`.
- **Couleurs** (`org.bukkit.Color`) sont sérialisées comme `{"ALPHA": int, "RED": int, "GREEN": int, "BLUE": int}`.
- Les fichiers sont jolis-imprimés par l'écrivain ; les consommateurs ne doivent pas se fier aux espaces.
- Tous les noms de champs sont **sensibles à la casse**.

## Blueprint

L'objet au niveau supérieur d'un fichier `.blueprint`. Il décrit un volume de bloc, des blocs attachés et des entités relatifs à une ancre (`bedrock`).

| Champ | Type | Description |
|---|---|---|
| `name` | string | Identifiant unique, utilisé pour rechercher le blueprint dans un bundle. Conventionnellement correspond à la tige du nom de fichier. |
| `displayName` | string | Nom lisible par l'humain montré dans les interfaces utilisateur. Peut contenir des codes de couleur `§` hérités ou des balises MiniMessage. |
| `icon` | string | Matériau d'icône : un nom `Material` Bukkit (`DIAMOND`), une clé vanilla (`minecraft:diamond`), ou une clé de modèle personnalisé de pack de ressources. Défaut `PAPER`. |
| `description` | string[] | Lignes de lore affichées sous l'icône dans les interfaces de sélection. |
| `bedrock` | Vector | Point d'ancrage. Quand collé, le blueprint `(0,0,0)` est traduit pour que `bedrock` atterrisse sur la cible de collage. S'il est omis, BentoBox en auto-crée un à `(xSize/2, ySize/2, zSize/2)` au moment du chargement. |
| `xSize`, `ySize`, `zSize` | integer | Dimensions de la boîte englobante en blocs. |
| `sink` | boolean | Si true, le blueprint descend jusqu'à ce qu'il trouve une surface au moment du collage au lieu de coller à l'Y exact de l'ancre. |
| `blocks` | Vector-keyed map | Blocs primaires, indexés par position relative à l'origine du blueprint (`0..size-1` sur chaque axe). Voir [BlueprintBlock](#blueprintblock). |
| `attached` | Vector-keyed map | Blocs collés **après** `blocks` parce qu'ils s'attachent à un support : torches, échelles, rails, lits, portes, panneaux, etc. Mêmes conventions de coordonnées que `blocks`. |
| `entities` | Vector-keyed map of lists | Entités à apparaître par position de bloc. Plusieurs entités peuvent partager une clé ; les fins de décalage fin en bloc se trouvent sur [BlueprintEntity](#blueprintentity). |

Un exemple minimal :

```json
{
  "name": "island",
  "displayName": "&aStarter island",
  "icon": "GRASS_BLOCK",
  "description": ["A tiny island"],
  "bedrock": [2.0, 1.0, 2.0],
  "xSize": 5, "ySize": 3, "zSize": 5,
  "blocks": [
    [[2.0, 1.0, 2.0], {"blockData": "minecraft:bedrock"}],
    [[2.0, 2.0, 2.0], {"blockData": "minecraft:grass_block[snowy=false]"}]
  ],
  "attached": [
    [[2.0, 3.0, 2.0], {"blockData": "minecraft:oak_sign[rotation=0,waterlogged=false]", "signLines": ["[spawn_here]", "", "", ""]}]
  ],
  "entities": [
    [[1.0, 2.0, 1.0], [{"type": "COW", "adult": true}]]
  ]
}
```

## BlueprintBlock

Une cellule de bloc. Seul `blockData` est obligatoire ; tous les autres champs ne sont appliqués que quand le type de bloc les supporte.

| Champ | Type | Description |
|---|---|---|
| `blockData` | string | **Obligatoire.** Chaîne `BlockData` Bukkit, c'est-à-dire la sortie de `BlockData#getAsString()` — par exemple `minecraft:chest[facing=north,type=single,waterlogged=false]`. |
| `signLines` | string[] (≤4) | Lignes du panneau du côté avant. Codes de couleur `§` hérités soutenus. Déprécié depuis 1.24.0 en faveur de champs spécifiques aux côtés mais toujours écrit et lu. |
| `signLines2` | string[] (≤4) | Lignes du panneau du côté arrière (panneaux à deux faces, ajoutés dans 1.24.0). |
| `glowingText` | boolean | Le côté avant du panneau a du texte brillant. |
| `glowingText2` | boolean | Le côté arrière du panneau a du texte brillant. |
| `inventory` | slot map | Contenu du conteneur (coffres, tonneaux, entonnoirs, shulkers, fourneaux, supports de brassage, …). Les clés sont des indices de slot stringifiés ; les valeurs sont des ItemStacks codés en YAML. |
| `bannerPatterns` | object[] | Couches de motif de bannière, appliquées dans l'ordre. Chaque entrée a `pattern` (code court hérité, par exemple `bri`) et `color` (un nom de `DyeColor`). |
| `biome` | string | Remplacement de biome pour cette cellule de bloc (nom de `Biome` Bukkit). |
| `creatureSpawner` | object | Présent uniquement quand `blockData` est un spawner. Voir [BlueprintCreatureSpawner](#blueprintcreaturespawner). |
| `trialSpawner` | object | Présent uniquement quand `blockData` est un spawner d'essai (1.21+, ajouté dans BentoBox 3.4.2). Mutuellement exclusif avec `creatureSpawner`. Voir [BlueprintTrialSpawner](#blueprinttrialspawner). |
| `itemsAdderBlock` | string | Id de bloc personnalisé ItemsAdder (par exemple `myserver:custom_ore`). Significatif uniquement quand ItemsAdder est installé ; sinon le bloc revient à `blockData`. |

### BlueprintCreatureSpawner

Configuration du spawner de mob vanilla (non-essai).

| Champ | Type | Description |
|---|---|---|
| `spawnedType` | string | Nom de type d'entité Bukkit. |
| `delay` | integer | Compte à rebours actuel (ticks) jusqu'à la prochaine tentative de spawn. |
| `maxNearbyEntities` | integer | Le spawn se met en pause pendant que au moins ce nombre du type spawnéé se trouve dans la plage de suivi. |
| `minSpawnDelay`, `maxSpawnDelay` | integer | Limites (ticks) du délai randomisé choisi après chaque spawn. |
| `requiredPlayerRange` | integer | Distance maximale du joueur (blocs) qui garde le spawner actif. |
| `spawnRange` | integer | Rayon (blocs) dans lequel les mobs peuvent apparaître. |

### BlueprintTrialSpawner

Configuration du spawner d'essai (Minecraft 1.21+). Utilisez `spawnedType` **ou** `potentialSpawns`, pas les deux.

| Champ | Type | Description |
|---|---|---|
| `ominous` | boolean | Si le spawner est dans son état de mauvaise augure (maudit). |
| `spawnedType` | string | Seul `EntityType` à faire apparaître. |
| `potentialSpawns` | object[] | Candidats de spawn pondérés. Chaque entrée : `snapshot` (valeur opaque `EntitySnapshot#getAsString`), `spawnrule` (objet Bukkit `SpawnRule` ; les clés varient par version de serveur), et obligatoire `spawnWeight` (entier ≥ 1). |
| `delay` | integer | Délai de spawn. |
| `baseSimEnts` / `addSimulEnts` | number | Entités simultanées de base gardées en vie / supplémentaire par joueur supplémentaire. |
| `baseSpawnsB4Cool` / `addSpawnsB4Cool` | number | Total de spawns de base avant refroidissement / supplémentaire par joueur supplémentaire. |
| `spawnRange`, `requiredPlayerRange`, `playerRange` | integer | Plages en blocs. |
| `lootTableMap` | array of pairs | Tables de butin de récompense candidates avec poids relatifs : `[[{"nameSpace": "minecraft", "key": "chests/trial_chambers/reward"}, 1], ...]`. |

## BlueprintEntity

Une entité à faire apparaître. Seul `type` est obligatoire. Les champs non définis signifient « laisser Bukkit par défaut seul » ; chaque champ ne s'applique que quand la classe d'entité le supporte.

**Général**

| Champ | Type | Description |
|---|---|---|
| `type` | string | **Obligatoire.** Nom du type d'entité Bukkit (`VILLAGER`, `ARMOR_STAND`, `ITEM_FRAME`, …). |
| `customName` | string | Nom d'affichage ; codes de couleur `§` hérités soutenus. |
| `x`, `y`, `z` | number | Fin de décalage dans la cellule de position (généralement `0.0 ≤ v < 1.0`). |
| `glowing` | boolean | Effet de brillance. |
| `gravity` | boolean | Si la gravité s'applique. |
| `visualFire` | boolean | Rendre le feu indépendamment de `fireTicks`. |
| `silent` | boolean | Supprimer les sons ambiants. |
| `invulnerable` | boolean | Immunisé à tous les dégâts. |
| `fireTicks` | integer | Durée du feu restante (ticks). |

**Mobs**

| Champ | Type | Description |
|---|---|---|
| `adult` | boolean | Entités vieillissantes — `false` fait apparaître un bébé. |
| `color` | string | Nom de `DyeColor`, pour les entités coloriables (moutons, shulkers, collier de loup, …). |
| `tamed` | boolean | Entités apprivoisables ; le propriétaire n'est pas restauré. |
| `chest` | boolean | Chevaux/lamas porteurs de coffre. |
| `domestication` | integer (0–100) | Niveau de domestication du cheval. |
| `inventory` | slot map | Inventaire du cheval/lama. |
| `style` | string | Style de robe de cheval : `WHITE`, `WHITEFIELD`, `WHITE_DOTS`, `BLACK_DOTS`, `NONE`. |
| `profession` | string | Profession du villageois (nom d'énumération ou clé avec espace de noms). |
| `level` | integer (1–5) | Niveau du villageois. |
| `experience` | integer | Expérience du villageois. |
| `villagerType` | string | Variante biome du villageois (nom d'énumération ou clé avec espace de noms). |

**Intégrations de plugins** (significatif uniquement quand le plugin est installé)

| Champ | Type | Description |
|---|---|---|
| `npc` | string | Id du NPC de Citizens. |
| `MMtype`, `MMLevel`, `MMpower`, `MMStance` | string / number | Type, niveau, puissance et stance de MythicMobs. |

**Entités d'affichage et cadres d'article**

| Champ | Type | Description |
|---|---|---|
| `displayRec` | object | Propriétés communes à toutes les entités d'affichage — voir [DisplayRec](#displayrec). |
| `blockDisp` | object | Charge de BlockDisplay : le bloc affiché, comme un [BlueprintBlock](#blueprintblock). |
| `itemDisp` | object | Charge de ItemDisplay : `item` (ItemStack codé en YAML) et `itemDispTrans` (un nom `ItemDisplayTransform` : `NONE`, `HEAD`, `GUI`, `GROUND`, `FIXED`, `THIRDPERSON_LEFTHAND`, …). |
| `textDisp` | object | Charge de TextDisplay — voir ci-dessous. |
| `itemFrame` | object | Charge de ItemFrame (depuis 3.2.6) : `item` (ItemStack codé en YAML), `rotation` (nom de Bukkit `Rotation`), `isFixed`, `isVisible`, `dropChance` (0.0–1.0). |

Champs de charge de TextDisplay : `text` (codes `§` hérités acceptés), `alignment` (`CENTER`/`LEFT`/`RIGHT`), `bgColor` (objet Couleur), `face` (un nom de `BlockFace`), `lWidth` (largeur de renvoi de ligne en pixels), `opacity` (octet signé, −1 = défaut), `isShadowed`, `isSeeThrough`, `isDefaultBg`.

### DisplayRec

| Champ | Type | Description |
|---|---|---|
| `billboard` | string | `FIXED`, `VERTICAL`, `HORIZONTAL` ou `CENTER` — comment l'affichage fait face au spectateur. |
| `brightness` | object | Bukkit `Display.Brightness`, généralement `{"block": int, "sky": int}`. |
| `width`, `height` | number | Taille d'affichage. |
| `glowColorOverride` | Color | Couleur de contour de brillance. |
| `interpolationDelay`, `interpolationDuration`, `teleportDuration` | integer | Synchronisation d'animation. |
| `shadowRadius`, `shadowStrength` | number | Rendu d'ombre. |
| `transformation` | object | Bukkit `Transformation` (traduction, rotations, mise à l'échelle). Opaque. |
| `range` | number | Plage de vue. |

## BlueprintBundle

Un bundle regroupe jusqu'à trois blueprints — un par environnement du monde — en une seule option dans l'interface de création d'île, et contrôle le coût, la permission, le slot d'interface, le plafond d'utilisation et les commandes post-création de cette option. Persisté sous forme de `<uniqueId>.json` dans le dossier `blueprints/` du mode de jeu ; la tige du nom de fichier **doit** égaler `uniqueId`.

| Champ | Type | Description |
|---|---|---|
| `uniqueId` | string | **Obligatoire.** Id unique ; aussi le suffixe de permission quand `requirePermission` est true. |
| `displayName` | string | Nom montré dans l'interface de sélection. |
| `icon` | string | Matériau d'icône, mêmes formes qu'une icône de blueprint. Défaut `PAPER`. |
| `description` | string[] | Lignes de lore sous l'icône. |
| `blueprints` | object | Map de l'environnement (`NORMAL`, `NETHER`, `THE_END`, `CUSTOM`) au `name` d'un blueprint dans le même dossier. Les environnements sans entrée ne sont pas générés. |
| `requirePermission` | boolean | Si true, les joueurs ont besoin de `<gamemode>.island.create.<uniqueId>`. |
| `slot` | integer | Slot d'interface préféré 0-indexé ; limité au moment du runtime. |
| `times` | integer | Îles maximales qu'un seul joueur peut créer avec ce bundle ; `0` = illimité. |
| `cost` | number | Coût d'économie Vault ; `0` = gratuit. Requiert un plugin d'économie. |
| `commands` | string[] | Commandes exécutées quand une île est créée avec ce bundle (ajouté dans 2.6.0). `[player]` et `[owner]` sont substitués ; les entrées préfixées `[SUDO]` s'exécutent comme le joueur, d'autres en tant que console. |

Exemple `default.json` :

```json
{
  "uniqueId": "default",
  "displayName": "Default Island",
  "icon": "GRASS_BLOCK",
  "description": ["A standard island", "with grass and dirt"],
  "blueprints": {
    "NORMAL": "island",
    "NETHER": "nether",
    "THE_END": "end"
  },
  "requirePermission": false,
  "slot": 0,
  "times": 0,
  "cost": 0.0,
  "commands": ["[SUDO] me has arrived!"]
}
```

## Validation des fichiers

Le dépôt BentoBox publie deux JSON Schemas (draft 2020-12) :

- [`schemas/blueprint.schema.json`](https://github.com/BentoBoxWorld/BentoBox/blob/develop/schemas/blueprint.schema.json) — valide un fichier `.blueprint` ou un bundle
- [`schemas/blueprint-bundle.schema.json`](https://github.com/BentoBoxWorld/BentoBox/blob/develop/schemas/blueprint-bundle.schema.json) — valide un fichier bundle seul

Pointez votre éditeur ou validateur CI dessus, par exemple avec [ajv](https://ajv.js.org/) :

```bash
ajv validate --spec=draft2020 -s blueprint.schema.json -d island.blueprint
```

Notez que les chaînes ItemStack codées en YAML et quelques objets Bukkit `ConfigurationSerializable` (transformations, règles de spawn) sont opaques pour le schéma — un fichier valide pour le schéma peut toujours ne pas charger si ces documents intégrés sont mal formés.
