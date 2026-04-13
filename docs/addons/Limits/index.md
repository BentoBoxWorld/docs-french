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
* worlds
* entitylimits

### blocklimits

Cette section répertorie le nombre maximum de blocs autorisés pour chaque matériau de bloc. N'utilisez pas de matériaux non-blocs car ils ne fonctionneront pas. Les limites s'appliquent à tous les mondes du jeu.

### worlds

Cette section répertorie les limites de blocs pour des mondes spécifiques. Vous devez nommer le monde spécifiquement, par exemple AcidIsland_world et ensuite répertorier les matériaux et la limite.

### entitylimits

Cette section répertorie les limites d'entité par défaut dans l'espace d'île d'un joueur (zone protégée et limite de l'île). Une limite de 5 permettra jusqu'à 5 entités dans le monde surground. Affecte tous les types de génération de créatures. Inclut également les entités comme MINECARTS. Notez que les limites d'entité ne sont plus supportées dans le Nether et l'End car les limites nécessitent le chargement des chunks pour compter les entités et cela cause trop de lag.

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

Les propriétaires d'îles peuvent avoir des permissions exclusives qui remplacent les paramètres par défaut ou spécifiques au monde. Le format est :

Format est `GAME-MODE-NAME.island.limit.MATERIAL.LIMIT`

exemple : `bskyblock.island.limit.hopper.10`

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

## Traductions

{{ translations("Limits") }}

## Articles qui ne peuvent pas être limités
Certains articles ne peuvent pas être limités (pour l'instant). Les raisons sont généralement parce qu'il y a trop de façons de supprimer l'article sans qu'il soit suivi. Si vous êtes un programmeur et pouvez trouver comment corriger ceux-ci, veuillez soumettre une PR!
