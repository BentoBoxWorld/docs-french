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
* worlds
* entitylimits
* entitylimits-nether
* entitylimits-end

!!! info "Limites par dimension (1.28.2+)"
    Depuis la version **1.28.2**, les comptages de blocs, les comptages d'entités, les limites et les offsets sont suivis **indépendamment pour l'Overworld, le Nether et l'End**. Une limite unique définie dans `blocklimits` ou `entitylimits` s'applique séparément à chaque dimension — par exemple `HOPPER: 10` autorise 10 entonnoirs dans l'Overworld, 10 dans le Nether et 10 dans l'End (30 au total sur l'île). Utilisez les sections optionnelles `-nether` / `-end` pour remplacer une seule dimension.

    Au premier chargement après la mise à jour, vos données existantes à dimension unique sont automatiquement migrées vers l'emplacement **Overworld**. Le format sur disque change, alors faites une sauvegarde avant la mise à jour ; notez que le retour à une version antérieure n'est pas pris en charge.

### blocklimits

Cette section répertorie le nombre maximum de blocs autorisés pour chaque matériau de bloc. N'utilisez pas de matériaux non-blocs car ils ne fonctionneront pas. Les limites s'appliquent indépendamment dans chaque dimension (Overworld, Nether, End).

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
