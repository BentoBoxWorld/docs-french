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
  finale: { ... }             # optional boss that ends the phase (1.29.0+)
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

## Commandes lors du changement de phase { #commands-on-phase-change }

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

## Finales de phase — le boss qui termine une phase { #phase-finales-the-boss-that-ends-a-phase }

*Ajouté dans AOneBlock 1.29.0.*

Une phase dotée d'une section `finale:` se termine par un combat de boss. Quand le dernier bloc de la phase est miné, le bloc magique se scelle et le boss apparaît dessus. La phase ne change pas tant que le boss n'est pas mort. Une phase sans section `finale:` se termine comme elle l'a toujours fait.

```yaml
  finale:
    boss: GIANT
    name: '<dark_green>The Colossus'
    health: 100
    scale: 0.5
    damage: 4
    speed: 0.25
    minions:
      ZOMBIE: 2
    drops:
      IRON_INGOT: 8
      BREAD: 8
```

### Déroulement d'un combat

- **L'avertissement.** Pendant les 20 derniers blocs de la phase, un battement de cœur retentit, de plus en plus aigu, et une cloche sonne à cinq blocs de la fin. La barre de phase affiche le nom du boss dès qu'il est en attente.
- **Le combat.** Le boss apparaît sur le bloc magique au son d'une corne de raid et dans un éclair. Le bloc magique ne peut pas être miné tant que le boss n'est pas mort, et la barre de phase cède la place à la barre de vie du boss.
- **Équitable pour l'île.** Seuls les joueurs peuvent blesser le boss : corps à corps, projectiles et animaux de compagnie. Le boss et ses acolytes ne peuvent ni casser, ni brûler, ni faire exploser de blocs, et le boss est ramené s'il quitte l'île.
- **Projections hors de l'île.** Les joueurs peuvent toujours être projetés hors de l'île. Un boss projeté dans le vide revient au bloc magique, sauf si `void-respawn` vaut `false`.
- **Défaite.** Si tout le monde meurt ou s'en va, le boss se retire au bout d'une dizaine de secondes. Frapper le bloc magique l'invoque de nouveau. Chaque combat perdu rend la tentative suivante 10 % plus facile, jusqu'à la moitié de la vie.
- **Équipes.** La vie du boss augmente de 50 % pour chaque joueur supplémentaire présent sur l'île, jusqu'à quatre joueurs.
- **Récompenses.** Le boss lâche ses `drops`, puis les `commands` s'exécutent à chaque victoire et les `first-time-commands` uniquement la première fois que l'île le bat.

Les finales sont ignorées en difficulté Paisible, car le boss ne pourrait pas apparaître.

### Options

| Option | Effet | Par défaut |
|---|---|---|
| `boss` | `EntityType` du boss. `GIANT` n'a pas d'IA dans le jeu vanilla ; AOneBlock lui en donne une, ce qui nécessite Paper. Avec `mythic-boss`, c'est la solution de repli facultative | Obligatoire, sauf si `mythic-boss` est défini |
| `mythic-boss` | Un type de mob [MythicMobs](#mythicmobs-bosses-and-minions) à utiliser comme boss à la place (1.30.0+) | Aucun |
| `mythic-level` | Niveau du boss MythicMobs et des `mythic-minions` (1.30.0+) | `1` |
| `name` | Nom d'affichage. MiniMessage ou anciens codes `&`. Définissez-le aussi pour un `mythic-boss`, sinon la barre de boss affiche son identifiant de type | Le nom du mob |
| `health` | Vie maximale de base. `0` conserve la vie propre au mob (1.30.0+). La limite du serveur est de 1024, sauf si vous augmentez `settings.attribute.maxHealth` dans `spigot.yml` | `100`, ou `0` pour un `mythic-boss` |
| `scale` | Multiplicateur de taille. `1` est la taille normale | `1`, ou la taille propre au mob pour un `mythic-boss` |
| `damage` | Dégâts d'attaque. Omettez-le ou utilisez `0` pour garder ceux du mob | Ceux du mob |
| `speed` | Vitesse de déplacement. Omettez-le ou utilisez `0` pour garder celle du mob | Celle du mob |
| `void-respawn` | `true` : un boss projeté dans le vide revient au bloc magique. `false` : le vide le tue, et cela compte comme une victoire | `true` |
| `warning` | Nombre de blocs avant la fin auquel l'avertissement commence. `0` pour aucun avertissement | `20` |
| `minions` | Mobs qui apparaissent avec le boss, sous la forme `TYPE: count` | Aucun |
| `mythic-minions` | Mobs MythicMobs qui apparaissent avec le boss, sous la forme `type: count`. Ils utilisent `mythic-level` (1.30.0+) | Aucun |
| `drops` | Objets lâchés à la mort du boss, sous la forme `MATERIAL: amount` | Aucun |
| `commands` | Commandes exécutées chaque fois que le boss est vaincu. Mêmes préfixes et placeholders que [`end-commands`](#commands-on-phase-change) | Aucun |
| `first-time-commands` | Commandes exécutées seulement la première fois que l'île vainc le boss | Aucun |

Le fichier [`0_plains.yml`](https://github.com/BentoBoxWorld/AOneBlock/blob/master/src/main/resources/phases/0_plains.yml) fourni documente chaque option dans ses commentaires. La copie de votre serveur conserve les commentaires avec lesquels elle a été créée : consultez donc le fichier fourni pour les options ajoutées dans les versions ultérieures.

### Boss et acolytes MythicMobs { #mythicmobs-bosses-and-minions }

*Ajouté dans AOneBlock 1.30.0.*

Si le plugin MythicMobs est installé, une finale peut utiliser l'un de vos mobs MythicMobs comme boss, et des mobs MythicMobs comme acolytes. BentoBox se connecte automatiquement à MythicMobs ; il n'y a rien à activer.

```yaml
  finale:
    mythic-boss: SkeletonKing      # MythicMobs mob type
    mythic-level: 3                # optional, default 1
    boss: WITHER_SKELETON          # optional fallback if the MythicMob can't spawn
    name: '<gold>The Skeleton King'
    mythic-minions:                # MythicMobs type: count
      SkeletalMinion: 3
    minions:                       # vanilla minions still work too
      ZOMBIE: 2
    drops:
      DIAMOND: 4
```

- **Mêmes règles de combat.** Un boss MythicMobs est maintenu sur l'île, a une barre de boss, ne subit de dégâts que de la part des joueurs, gagne de la vie pour chaque joueur supplémentaire et en perd après un combat perdu. Ses compétences, son IA et ses drops MythicMobs fonctionnent toujours. Les `drops` et les commandes de la finale sont également donnés.
- **Santé et taille.** Le boss conserve la santé et la taille de sa config MythicMobs sauf si le fichier de phase définit `health` ou `scale`.
- **Acolytes.** `mythic-minions` fonctionne avec un boss vanilla ou un boss MythicMobs. Comme les acolytes vanilla, ils ne peuvent pas modifier les blocs et sont supprimés à la fin du combat. Pour l'instant, ils affichent leur identifiant de type en guise de nom.
- **Solution de repli.** Si MythicMobs n'est pas installé ou ne connaît pas le mob, le type `boss` est utilisé. Sans `boss`, la phase passe à la suivante sans combat. Un type d'acolyte inconnu est signalé dans le journal et ignoré.

### Activer et désactiver les finales { #turning-finales-on-and-off }

- **Toutes les finales :** réglez `island.phase-finales: false` dans le `config.yml` d'AOneBlock.
- **Une phase :** supprimez la section `finale:` du fichier de cette phase.

!!! warning "Les serveurs mis à niveau depuis une version antérieure à la 1.29.0 n'ont pas de boss"
    Une mise à niveau n'écrase jamais les fichiers de phase de `plugins/BentoBox/addons/AOneBlock/phases/` : ils n'ont donc pas de section `finale:`. Copiez la section `finale:` de chaque [fichier de phase fourni](https://github.com/BentoBoxWorld/AOneBlock/tree/master/src/main/resources/phases) dans votre propre fichier et redémarrez. Les nouvelles installations les ont dès le départ.

### Les boss fournis

| Phase | Boss | Mob |
|---|---|---|
| Plains | The Colossus | Giant |
| Underground | The Broodmother | Spider |
| Winter | The Frostbitten | Stray |
| Ocean | The Drowned King | Drowned |
| Jungle | The Temple Guardian | Iron golem |
| Swamp | The Bog Witch | Witch |
| Dungeon | The Jailer | Wither skeleton |
| Desert | The Pharaoh | Husk |
| The Nether | The Warlord | Piglin brute |
| Plenty | The Harvest Beast | Ravager |
| Desolation | The Last Titan | Giant |
| Deep Dark | The Warden | Warden |
| The End | The Void Walker | Enderman |
| Lush Caves | The Mossback | Bogged |
| Dripstone Caves | The Burrower | Silverfish |
| Mangrove Swamp | The Mire Lurker | Cave spider |
| Meadow | The Summoner | Evoker |
| Cherry Grove | The Petal Phantom | Illusioner |
| Jagged Peaks | The Gale | Breeze |
| Sulfur Caves | Brimstone | Blaze |
| Dappled Forest | The Woodcutter | Vindicator |

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
  - type: mob-data
    data: breeze{Glowing:1b,attributes:[{id:scale,base:2f}]}
    underlying-block: STONE
    probability: 15
  - type: itemsadder
    id: mypack:ruby_ore
    probability: 10
  - type: mythic-mob
    mob: SkeletalKnight      # MythicMob type id (required)
    level: 3                 # optional, default 1
    power: 1.0               # optional, default 0
    display-name: "Boss"     # optional
    stance: ""               # optional
    underlying-block: STONE  # optional
    probability: 5
  - type: nexo
    id: custom_block
    probability: 10
  - type: craftengine
    id: craftengine:custom_block
    probability: 25
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
| Une phase se termine sans boss | Le fichier de phase n'a pas de section `finale:` (les serveurs mis à niveau depuis une version antérieure à la 1.29.0 doivent [les ajouter](#turning-finales-on-and-off)), `island.phase-finales` vaut `false`, ou le monde est en difficulté Paisible. Avec `mythic-boss` et sans repli `boss`, MythicMobs n'est pas installé ou ne connaît pas ce type de mob |
| Les modifications ne font rien | Le module n'a pas été rechargé, ou vous avez modifié le fichier dans `src/main/resources` dans le jar au lieu de `plugins/BentoBox/addons/AOneBlock/phases/` |

Regardez le journal du serveur au démarrage. Chaque fichier de phase chargé est enregistré, tout comme chaque bloc, mob et article rejeté, et chaque changement que le réconciliateur d'index effectue (les lignes commençant par `Phase index:`).
