# Limits

**Limits** vous permet de limiter les blocs et les entités de l'île dans les modes de jeu comme BSkyBlock et AcidIsland.

Cet addon a été créé pour aider à limiter les entités ou les blocs causant du lag, par exemple les entonnoirs. Il peut être utilisé pour limiter les blocs et les entités réguliers, mais pas tous peuvent être limités.

Créé et maintenu par [tastybento](https://github.com/tastybento).

{{ addon_description("Limits") }}

## Installation

1. Placez le fichier jar du addon Limits dans le dossier des addons du plugin BentoBox
2. Redémarrez le serveur
3. L'addon créera un dossier de données et à l'intérieur du dossier se trouvera un config.yml
4. Modifiez le config.yml comme vous le souhaitez.
5. Redémarrez le serveur si vous apportez une modification

## Commandes
Il existe une commande d'utilisateur et une commande admin appelées « limits ». Les administrateurs peuvent vérifier les limites d'un propriétaire d'île spécifique. Les deux affichent un panneau GUI avec les limites et le nombre actuel.

## Setup - Config.yml

Le config.yml a les sections suivantes :

* blocklimits
* blocklimits-nether
* blocklimits-end
* blockgrouplimits *(1.29.0+)*
* blockgrouplimits-nether / blockgrouplimits-end *(1.29.0+)*
* worlds
* entitylimits
* entitylimits-nether
* entitylimits-end
* entitygrouplimits

Il possède également ces commutateurs de premier niveau (tous ajoutés en **1.29.0** sauf mention contraire) : `apply-member-limit-perms`, `show-limit-messages`, `stacked-plants-count-as-one` et `log-limits-on-join`.

!!! info "Limites par dimension (1.28.2+)"
    Depuis la version **1.28.2**, les comptages de blocs, les comptages d'entités, les limites et les offsets sont suivis **indépendamment pour l'Overworld, le Nether et l'End**. Une limite unique définie dans `blocklimits` ou `entitylimits` s'applique séparément à chaque dimension — par exemple `HOPPER: 10` autorise 10 entonnoirs dans l'Overworld, 10 dans le Nether et 10 dans l'End (30 au total sur l'île). Utilisez les sections optionnelles `-nether` / `-end` pour remplacer une seule dimension.

    Au premier chargement après la mise à jour, vos données existantes à dimension unique sont automatiquement migrées vers l'emplacement **Overworld**. Le format sur disque change, alors faites une sauvegarde avant la mise à jour ; notez que le retour à une version antérieure n'est pas pris en charge.

### blocklimits

Cette section répertorie le nombre maximum de blocs autorisés pour chaque matériau de bloc. N'utilisez pas de matériaux non-blocs car ils ne fonctionneront pas. Les limites s'appliquent indépendamment dans chaque dimension (Overworld, Nether, End).

Les variantes de croissance et d'endommagement sont normalisées vers leur bloc canonique — `BAMBOO_SAPLING` compte comme `BAMBOO`, et depuis **1.30.0** `KELP_PLANT` compte comme `KELP` — de sorte qu'un nom de variante utilisé comme clé de limite (par ex. `KELP_PLANT` ou `CHIPPED_ANVIL`) configure la limite du bloc canonique.

### blocklimits-nether / blocklimits-end

Sections optionnelles qui remplacent les valeurs par défaut de `blocklimits` respectivement pour le Nether ou l'End. Elles sont commentées dans la configuration par défaut ; décommentez-les et ajoutez des entrées pour définir des limites de blocs spécifiques à une dimension.

### worlds

Cette section répertorie les limites de blocs pour des mondes spécifiques. Vous devez nommer le monde spécifiquement, par exemple AcidIsland_world et ensuite répertorier les matériaux et la limite. Les limites nommées par monde remplacent la limite par défaut de la dimension ci-dessus pour ce monde spécifique.

### entitylimits

Cette section répertorie les limites d'entité par défaut dans l'espace d'île d'un joueur (zone protégée et limite de l'île). Une limite de 5 permettra jusqu'à 5 entités. Affecte tous les types de génération de créatures. Inclut également les entités comme MINECARTS. Depuis la version **1.28.2**, les limites d'entité s'appliquent indépendamment par dimension, de sorte que le Nether et l'End sont désormais comptés et limités correctement (cela corrige le bug de longue date où les comptages du Nether/End étaient remis à zéro au déchargement des chunks).

### entitylimits-nether / entitylimits-end

Sections optionnelles qui remplacent les valeurs par défaut de `entitylimits` respectivement pour le Nether ou l'End. Elles sont commentées dans la configuration par défaut ; décommentez-les et ajoutez des entrées pour définir des limites d'entité spécifiques à une dimension.

Remarque : Seuls les 49 premiers blocs et entités limités sont affichés dans l'interface graphique de limites.

### entitygrouplimits

!!! note "Fonctionnalité expérimentale"
    La fonctionnalité suivante n'est disponible que dans les builds de développement, que vous pouvez trouver sur ci.codemc.io.

```yaml
entitygrouplimits:
  friendly:
    limit: 2
    entities:
      - COW
      - SHEEP
  monsters:
    limit: 4
    entities:
      - ZOMBIE
      - CREEPER
```

### blockgrouplimits

!!! info "Depuis la 1.29.0"
    Le pendant côté blocs de `entitygrouplimits` : une limite partagée sur un ensemble de matériaux de blocs. Les comptages de chaque membre sont additionnés et vérifiés par rapport à la limite du groupe, de sorte que les joueurs ne peuvent pas contourner une limite en convertissant des blocs apparentés (par exemple herbe → terre) ou en les répartissant entre variantes (piston / piston collant). Les `blocklimits` individuelles s'appliquent toujours par-dessus si les deux sont définies.

Définissez un groupe nommé avec une `icon`, une `limit` partagée et une liste de `materials` :

```yaml
blockgrouplimits:
  Pistons:
    icon: PISTON
    limit: 10
    materials:
    - PISTON
    - STICKY_PISTON
  Soil:
    icon: GRASS_BLOCK
    limit: 200
    materials:
    - GRASS_BLOCK
    - DIRT
    - DIRT_PATH
    - FARMLAND
```

Les remplacements par environnement sont pris en charge via `blockgrouplimits-nether` / `blockgrouplimits-end`, qui remplacent uniquement la limite numérique d'un groupe déjà défini dans `blockgrouplimits` :

```yaml
blockgrouplimits-nether:
  Pistons: 5
```

!!! warning "Lancez un recomptage après avoir modifié les groupes"
    Après avoir ajouté un groupe de blocs (ou modifié `stacked-plants-count-as-one` ci-dessous), lancez `/[player_command] limits recount` pour que les comptages stockés correspondent aux nouvelles règles de comptage.

### Blocs personnalisés ItemsAdder & Oraxen

!!! info "Depuis la 1.29.0"
    Les blocs personnalisés d'**ItemsAdder** et d'**Oraxen** peuvent être limités en utilisant leurs identifiants directement dans la section `blocklimits` existante (et ses remplacements `-nether`/`-end` et `worlds:`). L'application utilise les propres événements de pose/casse de chaque plugin via les hooks BentoBox, enregistrés uniquement lorsque le plugin est installé. Mettez entre guillemets les clés contenant deux-points.

```yaml
blocklimits:
  "iafestivities:christmas/christmas_tree/green_orb": 5
  "oraxen:caveblock": 10
```

### Autres commutateurs

=== "apply-member-limit-perms"
    !!! summary "Description"
        (**1.29.0+**) Lorsque `true`, les permissions `<gamemode>.island.limit.*` d'un membre de l'équipe sont fusionnées dans les limites de l'île lors de sa connexion — la valeur la plus élevée l'emporte. Les joueurs coopérants et de confiance ne sont pas membres de l'équipe et leurs permissions ne s'appliquent jamais.

        Par défaut : `false`

=== "show-limit-messages"
    !!! summary "Description"
        (**1.29.0+**) Lorsque `false`, les limites sont appliquées silencieusement — les poses et apparitions sont toujours bloquées, mais les joueurs ne reçoivent aucun message de limite atteinte.

        Par défaut : `true`

=== "stacked-plants-count-as-one"
    !!! summary "Description"
        (**1.29.0+**) Lorsque `true`, une tige de `SUGAR_CANE`, `BAMBOO` ou `KELP` (kelp depuis **1.30.0**) compte comme une seule plante quelle que soit sa hauteur — seul le segment de base est compté. Lancez un recomptage après avoir modifié cette option.

        Par défaut : `false`

=== "log-limits-on-join"
    !!! summary "Description"
        Journalise les limites d'une île dans la console lorsque son propriétaire se connecte. Depuis la **1.29.0**, cette option est **par défaut à `false`** (elle était auparavant à `true`) car elle inondait la console sur les serveurs comportant de nombreuses limites basées sur les permissions. Remettez-la à `true` si vous vous appuyiez sur cette sortie pour le débogage.

        Par défaut : `false`

## Permissions

Les propriétaires d'îles peuvent avoir des permissions exclusives qui remplacent les paramètres par défaut ou spécifiques au monde. Deux formats sont pris en charge :

1. `GAME-MODE-NAME.island.limit.MATERIAL.LIMIT` — appliqué à toutes les dimensions.

    exemple : `bskyblock.island.limit.hopper.10`

2. `GAME-MODE-NAME.island.limit.ENV.MATERIAL.LIMIT` — appliqué à une seule dimension, où `ENV` est l'un de `overworld`, `nether` ou `end` (1.28.2+).

    exemple : `bskyblock.island.limit.nether.hopper.5`

Les permissions s'activent quand le joueur se connecte.

Les permissions d'utilisation sont (mettez le nom du mode de jeu, par exemple acidisland à l'avant):

```
  GAMEMODE_NAME.limits.player.limits:
    description: Le joueur peut utiliser la commande des limites
    default: true
  GAMEMODE_NAME.mod.bypass:
    description: Le joueur peut contourner les limites
    default: op
  GAMEMODE_NAME.limits.admin.limits:
    description: Le joueur peut utiliser la commande des limites admin
    default: op
```

Les permissions complètes sont listées [ici](Permissions).

## Placeholders

{{ placeholders_source(source="Limits") }}


## Journal des modifications

??? warning "Nouveautés dans v1.30.0 — recomptage de varech recommandé"
    **Publié :** 15 août 2026

    Deux corrections de précision de comptage. Compatibilité : API BentoBox 2.7.1 · Paper Minecraft 1.21.11 – 26.2 · Java 21. Aucune modification de configuration ou locale.

    - 🐛 **Les abeilles peuvent toujours quitter leurs ruches.** Une abeille quittant une ruche n'est pas une nouvelle abeille — son décompte a déjà été soustrait quand elle est entrée — mais la sortie était toujours vérifiée par limite. Sur une île à sa limite d'abeilles, la libération était annulée, le serveur réessayait chaque quelques ticks, les joueurs à proximité étaient spammés avec « La reproduction des abeilles est limitée à … » et les abeilles stockées restaient piégées pour toujours. Les sorties de ruche sont maintenant exemptes de la vérification tout en restant comptées, de sorte que le cycle d'entrée/sortie reste net-zéro. Un élément de ruche placé transportant des abeilles jamais comptées peut laisser l'île légèrement au-dessus de sa limite ; cela bloque simplement les apparitions supplémentaires et l'élevage jusqu'à ce que la population chute.
    - 🔺 🐛 **Les colonnes de varech comptent correctement.** La croissance du varech convertit le `KELP` tip en segment de tige `KELP_PLANT` sans événement Bukkit, de sorte que l'ancien bloc n'a jamais été décrémenté et les comptages de varech ne faisaient que croître, bloquant finalement la pose à totaux fantômes. `KELP_PLANT` est maintenant normalisé à `KELP` (comme `BAMBOO_SAPLING`/`BAMBOO`) : la croissance est neutre pour le comptage, casser la base d'une colonne décrémente chaque segment, `KELP` participe à `stacked-plants-count-as-one`, et les noms de variantes tels que `KELP_PLANT` ou `CHIPPED_ANVIL` utilisés comme clés de limite configurent la limite canonique.

    🔺 **Si vous limitez le varech, lancez un recomptage.** Les comptages de varech stockés peuvent avoir dérivé vers le haut sous les versions précédentes. Lancez `/[admin_command] limits calc <joueur>` sur les îles affectées — ou laissez les joueurs exécuter `/[player_command] limits recount` — pour que les décomptes correspondent à la réalité.

    [Release v1.30.0](https://github.com/BentoBoxWorld/Limits/releases/tag/1.30.0)

??? note "Nouveautés dans v1.29.1"
    **Publié :** 23 juillet 2026

    Compatibilité : API BentoBox 2.7.1 · Paper Minecraft 1.21.11 – 26.2 · Java 21. Aucun changement de configuration ni de locale — c'est un remplacement direct.

    - 🐛 **La reproduction naturelle respecte désormais les limites d'entités.** La reproduction qui se produit sans intervention d'un joueur (abeilles, renards, reproducteurs gérés par des villageois, et similaires) contournait entièrement la vérification des limites, donc les décomptes pouvaient dépasser la limite configurée. Toute reproduction est désormais vérifiée. Les joueurs op ou disposant de la permission de contournement restent exemptés.
    - 🐛 **Les reproducteurs automatiques ne réessaient plus à chaque tick.** Quand une tentative de reproduction est refusée à la limite, les deux parents sont mis en temps de recharge de reproduction, et aucun message de limite atteinte n'est envoyé aux joueurs proches sauf si un joueur a réellement nourri les animaux.
    - 🐛 **Les entrées de joueurs ne fuient plus dans la carte de suivi des entités.** Les joueurs étaient ajoutés à la carte de suivi entité-île sans jamais en être retirés.
    - 🐛 **Les bateaux sont désormais inclus dans `recount`.** Le recomptage admin comptait les wagonnets mais ignorait les bateaux, ce qui mettait à zéro des décomptes de bateaux que le suivi en direct ne pouvait ensuite pas récupérer.

    Merci à [@daniel-skopek](https://github.com/daniel-skopek) pour les correctifs.

    [Release v1.29.1](https://github.com/BentoBoxWorld/Limits/releases/tag/1.29.1)

??? note "Nouveautés dans v1.29.0"
    **Publié :** 10 juillet 2026

    Compatibilité : API BentoBox 2.7.1 · Paper Minecraft 1.21.11 – 26.2 · Java 21.

    - ⚙️ **Limites de groupes de blocs.** Une limite partagée sur un ensemble de matériaux de blocs (par exemple pistons + pistons collants, ou herbe/terre/terre labourée), afin que les joueurs ne puissent pas contourner une limite en convertissant des blocs apparentés. Configuré sous `blockgrouplimits`, avec des remplacements `-nether`/`-end`. Voir la section Configuration ci-dessus.
    - ⚙️ **Limites de blocs personnalisés ItemsAdder & Oraxen.** Limitez les blocs personnalisés directement depuis `blocklimits` en utilisant leurs identifiants avec espace de noms.
    - ⚙️ **Permissions de limite des membres de l'équipe (optionnel).** Avec `apply-member-limit-perms: true`, les permissions `island.limit.*` des membres de l'équipe peuvent contribuer aux limites de l'île, et pas seulement celles du propriétaire.
    - 🔡 **Placeholders et API des limites atteintes.** De nouveaux placeholders `%Limits_<gamemode>_island_reached_limits%` (plus `_overworld`/`_nether`/`_end`) listent quelles limites sont au maximum, soutenus par une nouvelle API `Limits#getReachedLimits(...)`. Clôt le plus ancien ticket ouvert du suivi (déposé en 2018).
    - ⚙️ **Les plantes empilables peuvent compter comme une seule.** Comptez optionnellement toute une tige de canne à sucre ou de bambou comme une seule plante (`stacked-plants-count-as-one`).
    - ⚙️ **Option d'application silencieuse.** `show-limit-messages: false` désactive les messages de chat de limite atteinte tout en maintenant les limites appliquées.
    - 🔡 **Traductions manuelles des noms de matériaux/entités.** Les fichiers de locale peuvent désormais traduire les noms de blocs/entités affichés dans l'interface graphique et les messages de limite atteinte.
    - **Les cadres, cadres lumineux et peintures peuvent désormais être limités** sous `entitylimits`.
    - 🐛 **Correction : comptages d'entités fantômes provenant de mobs passés par un portail** (par exemple `Chicken 10/10` sans aucune poule sur l'île) et un golem de cuivre contournant la limite `COPPER_CHEST` en construisant.
    - ⚙️ **`log-limits-on-join` est désormais par défaut à `false`** — remettez-le à `true` si vous vous appuyiez sur cette sortie console.

    !!! warning "Les nouvelles options de configuration ne sont pas ajoutées automatiquement"
        Les nouvelles clés n'apparaissent **pas** dans un `config.yml` existant — ajoutez celles que vous voulez depuis la liste ci-dessus, ou supprimez la config pour la régénérer. Après avoir ajouté un groupe de blocs ou modifié `stacked-plants-count-as-one`, lancez un recomptage pour que les comptages stockés correspondent aux nouvelles règles de comptage.

    [Release v1.29.0](https://github.com/BentoBoxWorld/Limits/releases/tag/1.29.0)

??? note "Nouveautés dans v1.28.4"
    **Publié :** 6 juillet 2026

    Version de maintenance axée sur la précision et la persistance fiable des comptages d'entités. Aucune modification de configuration ou locale n'est requise.

    - 🐛 **Les comptages d'entités ne dérivent plus au-dessus de la réalité.** Dans certaines séquences d'apparition/suppression, le comptage d'entités suivi pouvait dépasser le nombre d'entités réellement présentes sur l'île, bloquant finalement les apparitions qui auraient dû être autorisées. Les comptages restent maintenant synchronisés avec la population réelle de l'île. [[#273](https://github.com/BentoBoxWorld/Limits/pull/273)]
    - 🐛 **Persistance du comptage d'entités centralisée.** Toutes les mutations de comptage d'entités passent maintenant par `BlockLimitsListener`, afin que les modifications soient intégrées dans le cycle de sauvegarde par lot normal au lieu d'être écrites uniquement à la désactivation du addon. Cela prévient la perte de comptages lors d'un arrêt anormal ou d'un crash. [[#274](https://github.com/BentoBoxWorld/Limits/pull/274)]

    [Release v1.28.4](https://github.com/BentoBoxWorld/Limits/releases/tag/1.28.4)

??? note "Nouveautés dans v1.28.3"
    **Publié :** 29 juin 2026

    Version de correction de bugs — pas de changement de données, de configuration ou de locale ; un remplaçable direct qui rend les comptages d'entités par île fiables après les redémarrages du serveur.

    - 🐛 **Les comptages d'entités ne dérivent plus après un redémarrage.** La carte reliant chaque entité à son île était conservée uniquement en mémoire et perdue à chaque redémarrage. Les entités rechargeées depuis les chunks ne réentraient jamais dedans, donc quand elles mouraient ou disparaissaient plus tard **hors de l'île**, leur comptage n'était jamais décrémenté et augmentait lentement. Les entités sont maintenant réenregistrées au chargement de leurs chunks, donc les suppressions hors île décrémentent correctement à nouveau.
    - 🩹 **Pas plus de croissance de map au déchargement des chunks.** La correspondance en mémoire est maintenant libérée quand un chunk se décharge (et reconstruite au rechargement), empêchant la croissance illimitée sur les serveurs de longue durée.

    [Release v1.28.3](https://github.com/BentoBoxWorld/Limits/releases/tag/1.28.3)

??? warning "Nouveautés dans v1.28.0 — Java 21 requis"
    **Publié :** 1er avril 2026

    - **Les fermes de duplication de Shulker sont maintenant correctement limitées sur Paper.** Utilise le `ShulkerDuplicateEvent` de Paper pour appliquer les limites avant la duplication, corrigeant un contournement où les Shulkers se téléportaient hors de l'île avant la vérification.
    - **Les limites de coffres en cuivre ne peuvent plus être contournées.** Toutes les variantes de coffres en cuivre (oxydés, cirés, grattés, créés par golem) sont maintenant normalisées vers un seul matériau suivi. Les transitions d'état de bloc sont correctement comptées.
    - **Les entrées de configuration invalides sont gérées proprement.** Les clés d'espace de noms malformées, les matériaux non-blocs et les matériaux incomptables (lave, eau, air) dans `blocklimits` produisent maintenant des messages d'avertissement clairs au lieu d'erreurs NPE.
    - 🔺 **Java 21 est maintenant requis** (précédemment Java 17). Assurez-vous que votre serveur utilise Java 21 avant de mettre à jour.
    - Cible Spigot mise à jour vers 1.21.11.

    [Release v1.28.0](https://github.com/BentoBoxWorld/Limits/releases/tag/1.28.0)

??? note "Nouveautés dans v1.28.1"
    **Publié :** 7 avril 2026

    Correctif pour deux régressions dans 1.28.0 :

    - **Les bases de données existantes se chargent à nouveau.** Dans 1.28.0, les champs de map `IslandBlockCount` ont changé de `Map<Material, Integer>` vers `Map<NamespacedKey, Integer>`, cassant la lecture des fichiers JSON pré-1.28.0. Un `TypeAdapter` Gson rétrocompatible lit maintenant les noms d'enum legacy, les chaînes avec espace de noms et la forme tableau complexe. **Aucune migration manuelle requise** — les anciens fichiers se chargent tels quels.
    - **Les noms de blocs dans l'interface des limites sont à nouveau lisibles.** Les items s'affichaient comme `Minecraft:hopper` à cause d'un formatage de clé incorrect.

    [Release v1.28.1](https://github.com/BentoBoxWorld/Limits/releases/tag/1.28.1)

??? warning "Nouveautés dans v1.28.2 — Limites par dimension (migration de données)"
    **Publié :** 13 juin 2026

    - 🔺⚙️ **Limites par dimension.** Les comptages de blocs et d'entités, les limites et les offsets sont désormais suivis indépendamment pour l'Overworld, le Nether et l'End, corrigeant le bug de longue date où les comptages du Nether/End étaient remis à zéro au déchargement des chunks ([#43](https://github.com/BentoBoxWorld/Limits/issues/43)). Une valeur unique de `blocklimits`/`entitylimits` s'applique désormais séparément à chaque dimension, avec les nouvelles sections optionnelles de remplacement `blocklimits-nether`, `blocklimits-end`, `entitylimits-nether` et `entitylimits-end`.
    - 🔺 **Migration de données.** Les données existantes à dimension unique sont migrées vers l'emplacement **Overworld** au premier chargement. Le format sur disque change, alors faites une sauvegarde avant la mise à jour ; le retour à une version antérieure n'est pas pris en charge.
    - 🔺 **Permissions par dimension.** Un nouveau format à 6 segments, `<gamemode>.island.limit.<overworld|nether|end>.<KEY>.<NUMBER>`, limite une limite à une seule dimension. Le format à 5 segments existant s'applique toujours à toutes les dimensions.
    - 🐛 Corrections de précision du comptage : lits/portes comptés en double ([#86](https://github.com/BentoBoxWorld/Limits/issues/86)), retrait de blocs des golems/bonshommes de neige ancré sur la citrouille plutôt que sur le bloc de génération ([#127](https://github.com/BentoBoxWorld/Limits/issues/127)), trois bugs de comptage d'entités, œufs d'apparition qui ne sont plus consommés à la limite ([#134](https://github.com/BentoBoxWorld/Limits/issues/134)), et fuites de comptage lors du recomptage.
    - 🩹 Résout un crash `NoSuchFieldError` sur Minecraft 1.21.8 et antérieur causé par la référence à des blocs de cuivre de 1.21.9 ; ceux-ci sont maintenant résolus par nom.
    - 🔡 Tous les fichiers de localisation fournis ont été convertis des anciens codes couleur `&` vers MiniMessage, et les clés manquantes ont été synchronisées dans les 21 langues. Vérifiez vos chaînes de localisation personnalisées par rapport aux nouveaux fichiers.

    Compatibilité : BentoBox API 2.7.1 · Minecraft 1.21.5 – 26.1.2 · Java 21.

    [Release v1.28.2](https://github.com/BentoBoxWorld/Limits/releases/tag/1.28.2)

## Traductions

{{ translations("Limits") }}

## Articles qui ne peuvent pas être limités
Certains articles ne peuvent pas être limités (pour l'instant). Les raisons sont généralement parce qu'il y a trop de façons de supprimer l'article sans qu'il soit suivi. Si vous êtes un programmeur et pouvez trouver comment corriger ceux-ci, veuillez soumettre une PR!

* Primed TNT
* Evoker Fangs
* Llama Spit
* Dragon Fireball
* Area Effect Cloud
* Ender signal
* Small fireball
* Fireball
* Thrown Exp Bottle
* Shulker Bullet
* Wither Skull
* Tridents
* Arrows
* Spectral Arrows
* Snowballs
* Eggs
* Leashes
* Ender crystals
* Ender pearls
* Ender dragon

!!! tip "Les cadres et peintures peuvent désormais être limités (1.29.0)"
    Les cadres, cadres lumineux et peintures figuraient auparavant sur cette liste. Depuis la **1.29.0**, le comptage des entités est persistant et piloté par événements, donc les trois peuvent maintenant être configurés sous `entitylimits` comme n'importe quelle autre entité.
