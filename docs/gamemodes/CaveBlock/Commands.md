# Commandes CaveBlock { #caveblock-commands }

| | Commande | Préfixe d'autorisation |
|---|---|---|
| Joueurs | `/cave` (aussi `/cb`) | `caveblock.` |
| Administrateurs | `/cbadmin` (aussi `/cba`) | `caveblock.` |

Vous pouvez renommer les deux commandes dans le `config.yml` du du mode de jeu.

## Commandes standard { #standard-commands }

CaveBlock utilise les commandes standard du joueur et administrateur de BentoBox. Elles sont toutes listées, avec leurs autorisations, dans la [Référence des commandes](../../BentoBox/Commands.md) : remplacez `/[player_command]` par `/cave`, `/[admin_command]` par `/cbadmin` et `[gamemode]` par `caveblock`. Par exemple :

```
/cave              go to your cave, or create one
/cave team invite <player>
/cave settings
/cbadmin info <player>
/cbadmin why <player>
```

Pour voir ce qu'elles font, consultez le [Guide du Joueur](../../BentoBox/Player-Guide.md) et les Guides Administrateur, tels que [Équipes et Rangs](../../BentoBox/About/Teams.md) et [Îles](../../BentoBox/About/IslandManagement.md).

## Commandes uniquement dans CaveBlock { #commands-only-in-caveblock }

| Commande | Ce qu'il fait | Autorisation | Par défaut |
|---|---|---|---|
| `/cave about` | Afficher les informations de copyright et de licence | `caveblock.island` | Tout le monde |

## Commandes des addons { #addon-commands }

Les addons ajoutent des sous-commandes à `/cave` et `/cbadmin`, par exemple `/cave level` de [Level](../../addons/Level/index.md) ou `/cave challenges` de [Challenges](../../addons/Challenges/index.md). Consultez la page de chaque addon.
