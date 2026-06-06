# TwerkingForTrees

**TwerkingForTrees** permet à vos joueurs de cultiver les arbres plus rapidement en twerking.

Créé et maintenu par [tastybento](https://github.com/tastybento).

{{ addon_description("TwerkingForTrees") }}

!!! info "Compatibilité"
    Nécessite **BentoBox 3.14.0** ou plus récent, **Minecraft 1.21.3 – 1.21.4**, et **Java 21**.

## Installation

1. Placez le fichier jar de l'addon dans le dossier des addons du plugin BentoBox
2. Redémarrez le serveur
3. Plantez des arbres sur votre île
4. Twerk, twerk, twerk...
5. Les arbres poussent!

## Arbres

La plupart des arbres poussent à partir d'une seule pousse twerkée. Le **Chêne noir** et le **Chêne pâle** font exception : comme dans Minecraft vanilla, ce sont des arbres géants uniquement en 2x2, vous devez donc disposer quatre pousses en grille 2x2 et twerker à côté — une seule pousse ne poussera pas.

## Fichier de configuration

```
# Fichier de configuration TwerkingForTrees.
#
# Combien de fois le joueur doit twerker avant que l'arbre ne commence à pousser plus vite.
# Si le joueur n'a pas assez twerké, l'arbre ne poussera pas plus vite.
minimum-twerks: 4
# Maintenir pour twerker. Fonctionnalité d'accessibilité. Au lieu d'appuyer continuellement sur la touche d'accroupissement, maintenez-la enfoncée.
hold-for-twerk: false
# Utiliser le sprint pour faire pousser les arbres au lieu de twerker.
sprint-to-grow: false
# Portée de recherche des pousses lors du twerk. Une portée de 5 cherchera +/- 5 blocs dans toutes les directions autour du joueur.
# Une valeur trop grande ralentira votre serveur.
range: 5
sounds:
  # Basculer le son activé/désactivé.
  enabled: true
  twerk:
    # Son qui joue quand le joueur a assez twerké pour que la pousse commence à pousser plus vite.
    # Les sons disponibles sont les suivants:
    #    https://hub.spigotmc.org/javadocs/spigot/org/bukkit/Sound.html
    sound: block.note_block.bass
    volume: 1.0
    pitch: 2.0
  growing-small-tree:
    # Son qui joue quand un petit arbre (1x1) pousse.
    # Les sons disponibles sont les suivants:
    #    https://hub.spigotmc.org/javadocs/spigot/org/bukkit/Sound.html
    sound: block.bubble_column.upwards_ambient
    volume: 1.0
    pitch: 1.0
  growing-big-tree:
    # Son qui joue quand un gros arbre (2x2) pousse.
    # Les sons disponibles sont les suivants:
    #    https://hub.spigotmc.org/javadocs/spigot/org/bukkit/Sound.html
    sound: block.bubble_column.upwards_ambient
    volume: 1.0
    pitch: 1.0
effects:
  # Basculer les effets de particules activé/désactivé.
  enabled: true
  # Effet qui joue à chaque fois que le joueur twerke.
  # Les effets disponibles sont les suivants:
  #    https://hub.spigotmc.org/javadocs/spigot/org/bukkit/Effect.html
  twerk: MOBSPAWNER_FLAMES

```

## Traductions

{{ translations("TwerkingForTrees") }}

??? warning "Nouveautés de la v1.6.0 — Changements majeurs"
    **Publié le :** 2026-06-01

    Une grande version de modernisation. Voir les notes complètes de la [Release v1.6.0](https://github.com/BentoBoxWorld/TwerkingForTrees/releases/tag/1.6.0).

    - 🔺 **Nécessite BentoBox 3.14.0** (Java 21, Paper 1.21.11, Minecraft 1.21.3 – 1.21.4). L'addon ne se chargera pas sur des serveurs plus anciens.
    - 🌳 Ajout de la prise en charge du **Chêne pâle**, y compris sa variante géante 2x2. Comme le Chêne noir, le Chêne pâle est un arbre uniquement en 2x2 — une seule pousse ne poussera pas.
    - ⚙️ **Le format de configuration des sons a changé.** Les identifiants de son dans config.yml utilisent désormais la forme en minuscules avec points (par exemple `block.note_block.bass`). Rafraîchissez votre config.yml si vous en conservez un depuis la 1.5.2 pour que les sons de twerk et de croissance continuent de fonctionner.
    - Ajout de nouvelles options de configuration : `hold-for-twerk` (accessibilité — maintenir l'accroupissement au lieu de tapoter), `sprint-to-grow` (faire pousser les arbres en sprintant) et `range` (rayon de recherche des pousses).
    - Livre désormais un `Pladdon` et un `plugin.yml` pour un chargement moderne et tenant compte des dépendances sur Paper.
    - Correction des pousses de Chêne noir poussant à partir d'une seule pousse, restauration de l'application de la limite d'île bloc par bloc (les bûches et les feuilles ne peuvent plus déborder du bord de l'île), et correction d'une fuite de ressources lors de la croissance des arbres.
    - Ajout d'une suite de tests JUnit 5 / MockBukkit.
