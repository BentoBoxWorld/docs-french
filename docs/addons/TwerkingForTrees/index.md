# TwerkingForTrees

**TwerkingForTrees** permet à vos joueurs de cultiver les arbres plus rapidement en twerking.

Créé et maintenu par [tastybento](https://github.com/tastybento).

{{ addon_description("TwerkingForTrees") }}

## Installation

1. Placez le fichier jar de l'addon dans le dossier des addons du plugin BentoBox
2. Redémarrez le serveur
3. Plantez des arbres sur votre île
4. Twerk, twerk, twerk...
5. Les arbres poussent!

## Fichier de configuration

```
# Fichier de configuration TwerkingForTrees.
#
# Combien de fois le joueur doit twerker avant que l'arbre ne commence à pousser plus vite.
# Si le joueur n'a pas assez twerké, l'arbre ne poussera pas plus vite.
minimum-twerks: 4
sounds:
  # Basculer le son activé/désactivé.
  enabled: true
  twerk:
    # Son qui joue quand le joueur a assez twerké pour que la pousse commence à pousser plus vite.
    # Les sons disponibles sont les suivants:
    #    https://hub.spigotmc.org/javadocs/spigot/org/bukkit/Sound.html
    sound: BLOCK_NOTE_BLOCK_BASS
    volume: 1.0
    pitch: 2.0
  growing-small-tree:
    # Son qui joue quand un petit arbre (1x1) pousse.
    # Les sons disponibles sont les suivants:
    #    https://hub.spigotmc.org/javadocs/spigot/org/bukkit/Sound.html
    sound: BLOCK_BUBBLE_COLUMN_UPWARDS_AMBIENT
    volume: 1.0
    pitch: 1.0
  growing-big-tree:
    # Son qui joue quand un gros arbre (2x2) pousse.
    # Les sons disponibles sont les suivants:
    #    https://hub.spigotmc.org/javadocs/spigot/org/bukkit/Sound.html
    sound: BLOCK_BUBBLE_COLUMN_UPWARDS_AMBIENT
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
