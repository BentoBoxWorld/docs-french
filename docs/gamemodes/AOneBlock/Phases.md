# Personnaliser les phases d'AOneBlock

Tout ce qu'un joueur extrait du bloc magique provient d'un **fichier de phase**. Cette page explique comment ces fichiers fonctionnent, ce que chaque chiffre signifie, et comment créer vos propres phases.

!!! tip "La réponse courte"
    Les chiffres après un matériau ou une entité — `COBBLESTONE: 900` — sont des **poids**, pas des quantités ni des pourcentages. Une phase additionne tous ses poids et en choisit une entrée au hasard proportionnellement à son poids. `blocks:`, `mobs:` et `custom-blocks:` tirent tous du même pool unique.

## Où se trouvent les fichiers

Une fois que le module a fonctionné une première fois, les fichiers se trouvent dans :

```
plugins/BentoBox/addons/AOneBlock/
├── config.yml
├── phases_index.yml          ← quelles phases charger, dans quel ordre, et la durée de chacune
└── phases/
    ├── 0_plains.yml          ← les blocs, mobs, hologrammes et paramètres d'une phase
    ├── 0_plains_chests.yml   ← les tables de butin de cette phase
    ├── 700_underground.yml
    ├── 700_underground_chests.yml
    └── ...
```

Chaque phase est une paire de fichiers : `<nom>.yml` et `<nom>_chests.yml`. Le fichier coffre est appairé **par nom de fichier**, donc si vous renommez l'un, vous devez renommer l'autre.

!!! info "`0_plains.yml` est le fichier de référence"
    Le fichier `0_plains.yml` fourni est très commenté et documente chaque option. Si vous ne lisez qu'un seul fichier, lisez celui-ci. Cette page couvre le même terrain avec des exemples concrets.

Après avoir modifié l'un de ces fichiers, rechargez le module (`/bbox reload`) ou redémarrez le serveur.

---

## Les trois types de chiffres

C'est la partie qui pose problème aux gens. Un fichier de phase contient trois types de chiffres complètement différents, et le type dépend entièrement de **la section dans laquelle il se trouve**.

| Où | Ce que le chiffre est |
|---|---|
| `blocks:`, `mobs:`, `custom-blocks:` | Un **poids** — la part de ce résultat dans le pool aléatoire. |
| Clés dans `fixedBlocks:` et `holograms:` | Une **position** — combien de blocs dans *cette phase*, en comptant à partir de 0. |
| La clé de niveau supérieur du fichier (`'0':`, `'2500':`) | Le **nom de la section** de la phase, historiquement son bloc de départ. L'ordre et la durée des phases proviennent maintenant de `phases_index.yml`. |

---

## Poids — les sections `blocks:` et `mobs:`

### Comment fonctionne le tirage

Chaque fois qu'un joueur casse le bloc magique, AOneBlock :

1. Additionne **tous** les poids de la phase actuelle — tous les `blocks:`, tous les `mobs:`, et tous les `custom-blocks:`.
2. Choisit un nombre aléatoire dans cette plage et retourne l'entrée sur laquelle il atterrit.

Donc :

```
chance d'une entrée = son poids ÷ total de tous les poids de la phase
```

Un poids n'est pas une quantité. `STONE: 1000` ne signifie pas qu'une mille pierre seront générées pendant la phase — cela signifie que la pierre obtient 1000 tickets dans la tombola, et il est tiré à nouveau à chaque casse de bloc.

### Exemple concret

```yaml
'2500':
  name: Winter
  firstBlock: SNOW_BLOCK
  biome: SNOWY_TAIGA
  blocks:
    COBBLESTONE: 900
    SAND: 100
    DIRT: 200
    STONE: 1000
    SPRUCE_LEAVES: 500
```

Les poids totalisent `900 + 100 + 200 + 1000 + 500 = 2700`, donc :

| Bloc | Poids | Chance par casse |
|---|---:|---:|
| `STONE` | 1000 | 1000 / 2700 = **37,0%** |
| `COBBLESTONE` | 900 | 900 / 2700 = **33,3%** |
| `SPRUCE_LEAVES` | 500 | 500 / 2700 = **18,5%** |
| `DIRT` | 200 | 200 / 2700 = **7,4%** |
| `SAND` | 100 | 100 / 2700 = **3,7%** |

Sur une phase de 1000 blocs, vous *attendriez* environ 370 pierres, mais chaque casse est un tirage indépendant, donc le compte réel varie autour de ce chiffre.

### Seul le ratio importe

```yaml
blocks:
  STONE: 1000
  DIRT: 200
```

se comporte **de manière identique** à

```yaml
blocks:
  STONE: 10
  DIRT: 2
```

Les fichiers fournis utilisent intentionnellement de grands chiffres : avec un total en milliers, vous pouvez ajouter une entrée rare au poids `5` sans avoir à redimensionner tout le reste pour garder les pourcentages sensés.

### Les blocs et les mobs partagent un seul pool

!!! warning "Les poids des mobs comptent pour le même total que les poids des blocs"
    `mobs:` n'est pas un tirage séparé. Une entrée de mob est juste un autre ticket dans la même tombola, donc `CHICKEN: 200` est exactement aussi probable qu'un bloc avec un poids de 200 — et ajouter des mobs rend chaque bloc un peu moins rare.

La phase Plains fournie le rend concret. Ses poids `blocks:` totalisent 11450 et ses poids `mobs:` totalisent 665, pour un total de phase de **12115** :

| Entrée | Poids | Chance par casse |
|---|---:|---:|
| `GRASS_BLOCK` | 2000 | 16,5% |
| `OAK_LOG` | 2000 | 16,5% |
| `CHEST` | 200 | 1,7% |
| `CHICKEN` *(mob)* | 200 | 1,7% |
| `COW` *(mob)* | 150 | 1,2% |
| `DIAMOND_ORE` | 30 | 0,25% |
| `VILLAGER` *(mob)* | 15 | 0,12% |
| `EMERALD_ORE` | 10 | 0,08% |

### Recettes d'ajustement

| Vous voulez… | Faites ceci |
|---|---|
| Rendre quelque chose deux fois plus courant | Doubler son poids |
| Supprimer quelque chose | Supprimer la ligne (ou la commenter) |
| Ajouter un bloc à environ *X*% | Poids ≈ `X/100 × total actuel ÷ (1 − X/100)` — ou prenez simplement le total actuel, et pour ~1% ajoutez une entrée de poids ≈ total/100 |
| Rééquilibrer une phase entière | Changer un poids à la fois — chaque changement décale tous les autres pourcentages, car le total change |
| Rendre les mobs moins courants sans toucher aux blocs | Baisser les poids `mobs:` ; les pourcentages des blocs augmentent automatiquement |

### Règles et pièges

- Un poids doit être un **nombre entier de 1 ou plus**. `0`, une valeur négative ou un nombre décimal est rejeté et enregistré comme `Bad item weight for <phase>: <material>`.
- Le matériau doit être un vrai Bukkit [Material](https://hub.spigotmc.org/javadocs/bukkit/org/bukkit/Material.html) **qui est un bloc**. Les articles comme `DIAMOND` seront enregistrés comme `Bad block material`.
- Les mobs doivent être un [EntityType](https://hub.spigotmc.org/javadocs/bukkit/org/bukkit/entity/EntityType.html) vivant et spawnable. Les noms invalides enregistrent la liste complète des noms valides au démarrage.
- Si une phase n'a aucun poids valide du tout, elle enregistre `has zero probability of generating blocks` et revient à un seul type de bloc — vérifiez l'orthographe du nom de section.

### `CHEST` est un cas particulier

Quand `CHEST` est tiré du pool, AOneBlock la remplit à partir du fichier `_chests.yml` de cette phase. Le poids `CHEST` est donc la chance d'obtenir **un** coffre ; quel coffre vous obtenez est un **deuxième tirage séparé sur la rareté** :

| Rareté | Chance |
|---|---:|
| `COMMON` | 62% |
| `UNCOMMON` | 25% |
| `RARE` | 9% |
| `EPIC` | 4% |

Ces chances de rareté sont fixes dans le code et ne sont pas configurables. Si une rareté n'a pas de coffres définis pour la phase, la liste `COMMON` est utilisée à la place ; s'il n'y a pas de coffres du tout, un coffre vide ordinaire est placé.

### Mobs

Quand un mob est tiré, le bloc magique devient `STONE` s'il était vide et le mob apparaît dessus. Avec `clear-blocks: true` dans `config.yml`, les blocs au chemin sont supprimés pour que les gros mobs s'adaptent.

```yaml
mobs:
  COW: 150
  SPIDER: 75
  SHEEP: 75
  PIG: 150
  VILLAGER: 15
  CHICKEN: 200
```

---

## Positions — `fixedBlocks` et `holograms`

Les clés dans ces deux sections sont des **positions au sein de la phase**, en comptant à partir de 0. La position `0` est le premier bloc de la phase, `1` le deuxième, et ainsi de suite. Ce ne sont *pas* le nombre total de blocs du joueur, et une position plus grande que la durée de la phase n'est tout simplement jamais atteinte.

### `fixedBlocks`

Les blocs fixes sont garantis — ils contournent complètement le pool pondéré. Utilisez-les pour les moments scripted.

```yaml
fixedBlocks:
  0: GRASS_BLOCK
  1: GRASS_BLOCK
  2: GRASS_BLOCK
  3: OAK_LOG
  4: OAK_LOG
  5: OAK_LOG
  700: CHEST_WITH_WATER_BUCKET
```

- Définir la position `0` ici remplace `firstBlock`, qui n'est alors plus nécessaire.
- `CHEST_WITH_<ITEM>` est un raccourci qui place un coffre contenant un seul article de ce matériau — pratique pour donner aux joueurs un seau d'eau avant la phase Océan.
- Préférez les blocs qui n'ont pas besoin de support. Une torche, un rail ou un semis placé comme bloc magique saute simplement.
- Une entrée de bloc fixe peut aussi être une définition de [bloc personnalisé](#custom-blocks).

### `holograms`

Même numérotation, mais la valeur est le texte à flotter au-dessus du bloc magique. Les codes couleur `&` fonctionnent.

```yaml
holograms:
  0: "&aFirst block is grass!"
  1: "&aSecond block is grass!"
  3: "&aGood Luck!"
```

Le tout premier hologramme — celui affiché avant le début de la phase 1 — vit dans le fichier de locale du module, pas ici.

---

## Ordre et durée des phases — `phases_index.yml`

!!! new "Depuis AOneBlock 1.26.0"
    L'ordre et la durée des phases ne sont **plus** pris à partir des noms de fichiers ou des clés de niveau supérieur. `phases_index.yml` est la source de vérité.

```yaml
phases:
  - file: 0_plains
    section: '0'
    name: Plains
    length: 700
  - file: 700_underground
    section: '700'
    name: Underground
    length: 1300
gotoAtEnd: 0
```

| Champ | Signification |
|---|---|
| `file` | Nom de base du fichier de phase, sans `.yml`. Le fichier coffre est `<file>_chests.yml`. |
| `section` | La clé de niveau supérieur à l'intérieur de ce fichier de phase. |
| `name` | Nom d'affichage, utilisé dans les journaux et dans `/[admin_command] phases`. |
| `length` | Combien de blocs cette phase dure. |
| `enabled` | Optionnel, par défaut `true`. Définissez sur `false` pour exclure complètement la phase. |
| `requiredMinecraftVersion` | Optionnel. La phase est ignorée sur les serveurs plus anciens, ne prenant pas d'espace du tout. |

Les blocs de départ sont **calculés** : chaque phase commence au total cumulatif des durées des phases activées au-dessus, en commençant par 0. Réorganisez les phases librement ; une phase désactivée ou ignorée s'effondre de la progression. Après la dernière phase, le nombre de blocs saute à `gotoAtEnd`.

Le moyen le plus facile de changer tout cela est en jeu avec `/[admin_command] phases`, qui édite l'index pour vous. Consultez les notes de l'[éditeur d'ordre de phase](index.md#commands). Une fois que vous modifiez une durée là, `adminLengths: true` est écrit dans l'index et vos durées ne sont jamais recalculées.

!!! tip "Le chiffre dans un nom de fichier n'est qu'un indice"
    `0_plains`, `2500_winter` et ainsi de suite sont historiques. Une phase personnalisée peut être `my_phase.yml` avec une clé de niveau supérieur `my_phase:` et aucun chiffre nulle part. Les chiffres sont toujours utiles pour un nouveau fichier : ils disent au réconciliateur d'index où la phase appartient dans l'ordre cumulatif.

---

## Anatomie d'un fichier de phase

```yaml
'0':                          # section name (see phases_index.yml)
  name: Plains                # display name
  icon: GRASS_BLOCK           # icon in the phases GUI (BentoBox ItemParser)
  firstBlock: GRASS_BLOCK     # the block for position 0 (optional)
  biome: PLAINS               # biome at the magic block location
  requiredMinecraftVersion: '1.21.6'   # optional version gate

  fixedBlocks: { ... }        # guaranteed blocks at positions
  holograms: { ... }          # text at positions

  blocks: { ... }             # weighted pool of blocks
  mobs: { ... }               # weighted pool of mobs — same pool
  custom-blocks: [ ... ]      # weighted pool of custom entries — same pool

  start-commands: [ ... ]
  end-commands: [ ... ]
  end-commands-first-time: [ ... ]
  requirements: { ... }
```

=== "name"
    Le nom d'affichage, affiché dans l'interface graphique des phases, la barre de boss, les lignes de journal et l'espace réservé de la commande `[phase]`.

=== "icon"
    L'icône utilisée uniquement dans l'interface graphique des phases. Analysée avec le [BentoBox ItemParser](../../BentoBox/ItemParser.md), donc les têtes de joueur personnalisées et tout article affichable fonctionnent. Une phase sans icône revient à son premier bloc.

=== "firstBlock"
    Le bloc placé à la position 0 de la phase. Optionnel — définir `0:` sous `fixedBlocks` fait le même travail et a la priorité.

=== "biome"
    Change le biome à l'**emplacement du bloc magique uniquement**, pas l'île entière. Pour rébioter une île entière lors d'un changement de phase, appelez le module Biomes à partir d'une entrée `start-commands`. Un nom de biome invalide enregistre la liste complète des biomes valides au démarrage.

=== "requirements"
    Limite l'accès à la phase. Jusqu'à ce que tous les critères soient remplis, le joueur est maintenu à la fin de la phase précédente.

    - `economy-balance` — solde minimal du joueur (nécessite Vault et un module économique)
    - `bank-balance` — solde minimal de la banque de l'île (nécessite le module Bank)
    - `level` — niveau d'île minimal (nécessite le module Level)
    - `permission` — une permission que le joueur doit avoir
    - `cooldown` — secondes qui doivent s'écouler depuis le dernier démarrage de la phase

    ```yaml
    requirements:
      bank-balance: 10000
      level: 10
      permission: ready.for.battle
      cooldown: 60
    ```

---

## Commandes lors du changement de phase

Les commandes s'exécutent en tant que **console** sauf si elles sont préfixées par `[SUDO]`, auquel cas elles s'exécutent en tant que joueur qui les a déclenchées.

| Section | Quand elle s'exécute |
|---|---|
| `start-commands` | Quand la phase commence |
| `end-commands` | Chaque fois que la phase est complétée |
| `end-commands-first-time` | Seulement la **première** fois que cette île complète la phase |

Espaces réservés substitués à la chaîne de commande :

| Espace réservé | Valeur |
|---|---|
| `[island]` | Nom de l'île |
| `[owner]` | Nom du propriétaire de l'île |
| `[player]` | Nom du joueur qui a cassé le bloc |
| `[phase]` | Nom de cette phase |
| `[blocks]` | Nombre de blocs cassés |
| `[level]` | Niveau de l'île (nécessite le module Level) |
| `[bank-balance]` | Solde de la banque de l'île (nécessite le module Bank) |
| `[eco-balance]` | Solde d'économie du joueur (nécessite Vault et un module économique) |

```yaml
start-commands:
- 'give [player] WOODEN_AXE 1'
- 'broadcast [player] just started OneBlock!'
end-commands-first-time:
- 'broadcast &c&l[!] &b[player] &fhas completed the &d&n[phase]&f phase for the first time.'
```

---

## Coffres

Les coffres vivent dans le fichier `_chests.yml` de la phase, sous la même clé de niveau supérieur :

```yaml
'0':
  chests:
    '1':
      rarity: COMMON
      contents:
        0: ==: org.bukkit.inventory.ItemStack ...
    '2':
      rarity: EPIC
      contents:
        ...
```

- Le chiffre clé de chaque coffre (`'1'`, `'2'`) est juste un **id unique** — ce n'est ni un poids ni une position. Quand un coffre d'une rareté donnée est dû, l'un des coffres de cette rareté est choisi au hasard avec une probabilité égale.
- Les clés `contents` sont des **numéros d'emplacements d'inventaire**.
- `rarity` est `COMMON`, `UNCOMMON`, `RARE` ou `EPIC`.

!!! tip "Construire les coffres en jeu, pas à la main"
    Remplissez un vrai coffre avec ce que vous voulez, regardez-le, et exécutez `/[admin_command] setchest <phase> <rarity>`. Le coffre est sérialisé directement dans le fichier de coffre de la phase, correctement, la première fois. L'édition manuelle du YAML d'objet sérialisé est sujette aux erreurs ; utilisez `/[admin_command] sanity [<phase>]` après pour vérifier vos tables de butin. La suppression d'un coffre signifie toujours éditer le fichier et recharger.

---

## Blocs personnalisés

`custom-blocks:` est une liste d'entrées qui ne sont pas des matériaux ordinaires. Chaque entrée a un champ `probability:` qui — malgré son nom — est un **poids**, dans exactement le même pool que `blocks:` et `mobs:`. `probability: 10` est aussi probable qu'un bloc avec un poids `10`.

```yaml
custom-blocks:
  - type: block-data
    data: minecraft:chest[waterlogged=true]
    probability: 10
  - type: mob
    mob: ZOMBIE
    underlying-block: STONE
    probability: 5
  - type: itemsadder
    id: mypack:ruby_ore
    probability: 10
```

| `type` | Ce qu'il fait | Nécessite |
|---|---|---|
| `block` / `block-data` | Exécute `/setblock` avec les données de bloc complètes — états de bloc, NBT, et un mode optionnel `destroy`\|`keep`\|`replace`. Préférez `block` quand vous utilisez NBT. | — |
| `mob` | Génère une entité vanilla en utilisant l'API Spawn Entity. | `mob` ; optionnel `underlying-block` (par défaut `STONE`) |
| `mob-data` | Exécute `/summon` avec NBT/composants vanilla. Les blocs à l'intérieur de la boîte englobante (mis à l'échelle) du mob sont supprimés une tick après l'apparition pour qu'il s'adapte. | `data` |
| `mythic-mob` | Génère un MythicMob via le hook de BentoBox. | Plugin MythicMobs |
| `itemsadder` | Bloc de [ItemsAdder](https://itemsadder.devs.beer/). | Plugin ItemsAdder |
| `nexo` | Bloc de [Nexo](https://polymart.org/resource/nexo.6901). | Plugin Nexo |
| `craftengine` | Bloc de [CraftEngine](https://github.com/Xiao-MoMi/craft-core). | Plugin CraftEngine, BentoBox 3.15.0+ |

Les blocs personnalisés peuvent aussi être utilisés dans `fixedBlocks`, en tant qu'objet au lieu d'un nom de matériau :

```yaml
fixedBlocks:
  0:
    type: block-data
    data: minecraft:chest[waterlogged=true]
  1: GRASS_BLOCK
```

!!! warning "Citez vos chaînes de données"
    Les chaînes `data` de bloc personnalisé contiennent `{`, `}`, `[`, `]` et des guillemets doubles. Enveloppez toute la valeur entre **guillemets simples** pour que les guillemets doubles internes ne s'opposent pas aux délimiteurs de chaîne de YAML.

    ```yaml
    - type: mob-data
      data: 'breeze{CustomName:[{text:"Breezy",color:"#f90606"}],Glowing:1b}'
      underlying-block: STONE
      probability: 10
    ```

!!! tip "Piège du spawner"
    Un `spawner` placé sans les champs de timing est inactif dans vanilla 1.21 (`Delay:-1` signifie "ne jamais tick"). Définissez explicitement `Delay`, `MinSpawnDelay`, `MaxSpawnDelay` et autres, ou le spawner apparaît et ne fait rien. `Delay:0` rend le premier spawn à la tick suivante.

Si le plugin d'un bloc personnalisé n'est pas installé, le bloc revient à `STONE` et une ligne est écrite dans le journal.

---

## Portail de version

Une phase, un bloc individuel ou un mob individuel peut déclarer la version Minecraft minimale dont il a besoin. Tout ce que le serveur est trop vieux pour est ignoré avec une ligne d'information dans le journal au lieu d'une erreur `Tried to load invalid item`.

**Phase entière** — mettez `requiredMinecraftVersion` dans `phases_index.yml` pour que le fichier ne soit pas même analysé sur un ancien serveur. La phase ne prend alors aucun espace et les phases après s'effondrent.

**Un bloc ou un mob unique** — utilisez la forme d'objet, qui échange le poids nu pour un champ `weight:`:

```yaml
blocks:
  NETHERRACK: 300
  DRIED_GHAST:
    weight: 25
    requiredMinecraftVersion: '1.21.6'

mobs:
  ZOMBIFIED_PIGLIN: 100
  HAPPY_GHAST:
    weight: 5
    requiredMinecraftVersion: '1.21.6'
```

Les fichiers de coffre sont lus élément par élément, donc un article que votre version de serveur ne connaît pas est ignoré de lui-même et le reste du coffre se charge toujours.

---

## Construire une nouvelle phase

1. **Copier une paire de fichiers existants** dans le dossier `phases` — par exemple `4000_jungle.yml` et `4000_jungle_chests.yml` — vers `volcano.yml` et `volcano_chests.yml`.
2. **Changez la clé de niveau supérieur** dans les deux fichiers vers quelque chose d'unique, par ex. `volcano:`. Il doit correspondre dans les deux.
3. **Définissez `name:` et `icon:`**, puis modifiez `blocks:` et `mobs:` avec les poids que vous voulez. N'oubliez pas que les pourcentages sont relatifs au total de la *phase*.
4. **Redémarrez ou rechargez.** Le module remarque le nouveau fichier, l'ajoute à `phases_index.yml` à la fin de l'ordre avec la durée par défaut de 500, et enregistre :
   `Phase index: added Volcano from volcano.yml at the end of the phase order. Move it with the admin phases GUI.`
5. **Positionnez-le** avec `/[admin_command] phases` — clic gauche pour le prendre, clic où il devrait aller, clic gauche+décalage pour définir sa durée.
6. **Testez-le** avec `/[admin_command] setcount <player> <number>` pour sauter directement au bloc de départ de la phase.

!!! tip "Testez sur une île de travail"
    Cassez quelques centaines de blocs et voyez ce qui en sort réellement. Les poids se lisent très différemment sur papier qu'ils ne jouent. `/[player_command] count` montre où vous êtes dans la phase.

---

## Dépannage

| Symptôme | Cause probable |
|---|---|
| `Bad block material in <phase>: X` | `X` n'est pas un matériau Bukkit, ou est un article plutôt qu'un bloc |
| `Bad item weight for <phase>: X. Must be positive number above 1` | Le poids est 0, négatif ou pas un nombre entier |
| `Bad entity type in <phase>: X` | Pas un `EntityType` valide ; le journal en liste les valides |
| `<phase> has zero probability of generating blocks` | La section `blocks:` manque, est vide, ou sous la mauvaise clé de section |
| `Phase name trying to be set to X but already set to Y. Duplicate phase file?` | Deux fichiers utilisent la même clé de section de niveau supérieur |
| Une phase ne semble jamais | Elle est `enabled: false` dans `phases_index.yml`, ou son `requiredMinecraftVersion` est plus récent que le serveur |
| Les coffres sont vides | La clé de niveau supérieur du fichier coffre ne correspond pas à celle du fichier de phase, ou ses articles n'ont pas pu se charger — exécutez `/[admin_command] sanity` |
| Les modifications ne font rien | Le module n'a pas été rechargé, ou vous avez modifié le fichier dans `src/main/resources` dans le jar au lieu de `plugins/BentoBox/addons/AOneBlock/phases/` |

Regardez le journal du serveur au démarrage. Chaque fichier de phase chargé est enregistré, tout comme chaque bloc, mob et article rejeté, et chaque changement que le réconciliateur d'index effectue (les lignes commençant par `Phase index:`).
