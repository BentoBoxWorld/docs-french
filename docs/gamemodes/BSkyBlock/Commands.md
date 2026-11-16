# Commandes BSkyBlock { #bskyblock-commands }

| | Commande | Préfixe d'autorisation |
|---|---|---|
| Joueurs | `/island` (aussi `/is`, `/skyblock`, `/sb`) | `bskyblock.` |
| Administrateurs | `/bsbadmin` (aussi `/bsb`, `/skyblockadmin`, `/sbadmin`, `/sba`) | `bskyblock.` |

Vous pouvez renommer les deux commandes dans le `config.yml` du du mode de jeu.

## Commandes standard { #standard-commands }

BSkyBlock utilise les commandes standard du joueur et administrateur de BentoBox. Elles sont toutes listées, avec leurs autorisations, dans la [Référence des commandes](../../BentoBox/Commands.md) : remplacez `/[player_command]` par `/island`, `/[admin_command]` par `/bsbadmin` et `[gamemode]` par `bskyblock`. Par exemple :

```
/island              allez à votre île, ou créez-en une
/island team invite <player>
/island settings
/bsbadmin info <player>
/bsbadmin why <player>
```

Pour voir ce qu'elles font, consultez le [Guide du Joueur](../../BentoBox/Player-Guide.md) et les Guides Administrateur, tels que [Équipes et Rangs](../../BentoBox/About/Teams.md) et [Îles](../../BentoBox/About/IslandManagement.md).

## Commandes uniquement dans BSkyBlock { #commands-only-in-bskyblock }

| Commande | Ce qu'il fait | Autorisation | Par défaut |
|---|---|---|---|
| `/island about` | Afficher les informations de copyright et de licence | `bskyblock.island` | Tout le monde |

## Commandes des addons { #addon-commands }

Les addons ajoutent des sous-commandes à `/island` et `/bsbadmin`, par exemple `/island level` de [Level](../../addons/Level/index.md) ou `/island challenges` de [Challenges](../../addons/Challenges/index.md). Consultez la page de chaque addon.
