# Commandes SkyGrid

| | Commande | Préfixe d'autorisation |
|---|---|---|
| Players | `/skygrid` (also `/sg`) | `skygrid.` |
| Admins | `/sgadmin` (also `/sga`) | `skygrid.` |

Vous pouvez renommer les deux commandes dans le `config.yml` du du mode de jeu.

## Commandes standard

SkyGrid utilise les commandes standard du joueur et administrateur de BentoBox. Elles sont toutes listées, avec leurs autorisations, dans la [Référence des commandes](../../BentoBox/Commands.md) : remplacez `/[player_command]` par `/skygrid`, `/[admin_command]` par `/sgadmin` et `[gamemode]` par `skygrid`. Par exemple :

```
/skygrid              go to your area, or create one
/skygrid team invite <player>
/skygrid settings
/sgadmin info <player>
/sgadmin why <player>
```

Pour voir ce qu'elles font, consultez le [Guide du Joueur](../../BentoBox/Player-Guide.md) et les Guides Administrateur, tels que [Équipes et Rangs](../../BentoBox/About/Teams.md) et [Îles](../../BentoBox/About/IslandManagement.md).

SkyGrid doesn't add any commands of its own.

## Commandes des addons

Les addons ajoutent des sous-commandes à `/skygrid` et `/sgadmin`, par exemple `/skygrid level` de [Level](../../addons/Level/index.md) ou `/skygrid challenges` de [Challenges](../../addons/Challenges/index.md). Consultez la page de chaque addon.
