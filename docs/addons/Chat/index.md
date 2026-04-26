# Chat

**Chat** fournit un **Chat d'équipe** et un **Chat d'île** pour permettre à vos joueurs de parler en privé à leurs visiteurs ou aux autres membres de l'équipe de l'île.

Créé et maintenu par [tastybento](https://github.com/tastybento).

{{ addon_description("Chat") }}

## Chat de l'île

Lorsqu'il est activé, le chat est limité aux joueurs sur l'île uniquement, y compris les visiteurs. Les administrateurs ou les modérateurs peuvent écouter les chats d'île en utilisant une commande d'espionnage.

## Chat d'équipe

Lorsqu'il est activé, les chats n'iront qu'aux membres de l'équipe. Les joueurs en équipe peuvent basculer si leur chat ira sur le canal de chat d'équipe ou non. Les administrateurs peuvent écouter tous les chats d'équipe en utilisant une commande d'espionnage.

## Commandes
### Commandes du joueur

* `chat` - bascule le chat de l'île activé et désactivé
* `teamchat` - bascule si le chat du joueur va au canal d'équipe ou non

### Commandes Admin

* `chatspy` - bascule le chat de l'île activé et désactivé
* `teamchatspy` - bascule si le chat du joueur va au canal d'équipe ou non

La configuration a également des paramètres pour enregistrer tous les chats si nécessaire.

## Configuration

```
# Configuration file for Chat
team-chat:
  gamemodes:
  - BSkyBlock
  - AcidIsland
  - CaveBlock
  - SkyGrid
  # Log team chats to console.
  log: false
island-chat:
  # Lists the gamemodes in which you want the Chat addon to be effective.
  gamemodes:
  - BSkyBlock
  - AcidIsland
  - CaveBlock
  - SkyGrid
  # Log island chats to console.
  log: false
chat-listener:
  # Sets priority of AsyncPlayerChatEvent. Change this if Chat addon
  # is conflicting with other plugins which listen to the same event
  # Acceptable values: lowest, low, normal, high, highest, monitor
  priority: normal
```

## Permissions

```
permissions:
  '[gamemode].chat.team-chat':
    description: Le joueur peut utiliser le chat d'équipe
    default: true
  '[gamemode].chat.island-chat':
    description: Le joueur peut utiliser le chat d'île
    default: true
  '[gamemode].chat.spy':
    description: Le joueur peut utiliser l'espionnage du chat d'équipe ou d'île
    default: op

```

## Aimez cet addon?
Vous pouvez [sponsoriser](https://github.com/sponsors/tastybento) pour obtenir plus d'addons comme celui-ci et l'améliorer!

## Changelog

??? note "Nouveautés dans v1.4.1"
    **Publié le :** 2026-04-26

    - 🔡 **Correction de la locale tchèque** — Le fichier `cs.yml` contenait une entrée YAML malformée pour `island-chat-spy` provoquant une `ScannerException` au démarrage du serveur. Supprimez `plugins/BentoBox/addons/Chat/locales/cs.yml` avant de redémarrer pour qu'il soit régénéré depuis la version corrigée.

    [Release v1.4.1](https://github.com/BentoBoxWorld/Chat/releases/tag/1.4.1)

## Traductions

{{ translations("Chat") }}
