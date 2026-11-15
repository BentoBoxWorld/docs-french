# Commandes StrangerRealms

| | Commande | Préfixe d'autorisation |
|---|---|---|
| Joueurs | `/st` (aussi `/strange`) | `strangerrealms.` |
| Administrateurs | `/stranger` | `strangerrealms.` |

Vous pouvez renommer les deux commandes dans le `config.yml` du du mode de jeu.

## Commandes standard

StrangerRealms utilise les commandes standard du joueur et administrateur de BentoBox. Elles sont toutes listées, avec leurs autorisations, dans la [Référence des commandes](../../BentoBox/Commands.md) : remplacez `/[player_command]` par `/st`, `/[admin_command]` par `/stranger` et `[gamemode]` par `strangerrealms`. Par exemple :

```
/st              allez à votre revendication, ou créez-en une
/st team invite <player>
/st settings
/stranger info <player>
/stranger why <player>
```

Pour voir ce qu'elles font, consultez le [Guide du Joueur](../../BentoBox/Player-Guide.md) et les Guides Administrateur, tels que [Équipes et Rangs](../../BentoBox/About/Teams.md) et [Îles](../../BentoBox/About/IslandManagement.md).

## Commandes uniquement dans StrangerRealms

| Commande | Ce qu'il fait | Autorisation | Par défaut |
|---|---|---|---|
| `/st claim` | Revendiquer la terre sur laquelle vous vous tenez | `strangerrealms.claim` | Tout le monde |
| `/st unclaim` | Retirer votre revendication | `strangerrealms.unclaim` | Tout le monde |
| `/st spawn` | Se téléporter au spawn (remplace la commande spawn standard) | `strangerrealms.spawn` | Tout le monde |
| `/stranger worldborder [on\|off\|set\|auto\|info]` | Changer les paramètres de la bordure du monde | `strangerrealms.admin.worldborder` | Opérateurs (non déclaré) |

Stranger Realms, les joueurs revendiquent des terres avec `/st claim` au lieu de créer une île, donc `/st create` n'est pas donné aux joueurs (`strangerrealms.island.create` n'est pas déclaré, ce qui le rend réservé aux opérateurs), et `/st` sans sous-commande envoie les nouveaux joueurs au spawn.

## Commandes des addons

Les addons ajoutent des sous-commandes à `/st` et `/stranger`, par exemple `/st level` de [Level](../../addons/Level/index.md) ou `/st challenges` de [Challenges](../../addons/Challenges/index.md). Consultez la page de chaque addon.
