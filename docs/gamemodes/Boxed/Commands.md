# Commandes Boxed { #boxed-commands }

| | Commande | Préfixe d'autorisation |
|---|---|---|
| Players | `/boxed` (also `/bx`, `/box`) | `boxed.` |
| Admins | `/boxadmin` | `boxed.` |

Vous pouvez renommer les deux commandes dans le `config.yml` du du mode de jeu.

## Commandes standard { #standard-commands }

Boxed utilise les commandes standard du joueur et administrateur de BentoBox. Elles sont toutes listées, avec leurs autorisations, dans la [Référence des commandes](../../BentoBox/Commands.md) : replace `/[player_command]` with `/boxed`, `/[admin_command]` with `/boxadmin` et `[gamemode]` par `boxed`. Par exemple :

```
/boxed              go to your box, or create one
/boxed team invite <player>
/boxed settings
/boxadmin info <player>
/boxadmin why <player>
```

Pour voir ce qu'elles font, consultez le [Guide du Joueur](../../BentoBox/Player-Guide.md) et les Guides Administrateur, tels que [Équipes et Rangs](../../BentoBox/About/Teams.md) et [Îles](../../BentoBox/About/IslandManagement.md).

## Commandes uniquement dans Boxed { #commands-only-in-boxed }

| Commande | Ce qu'il fait | Autorisation | Par défaut |
|---|---|---|---|
| `/boxadmin place <x> <y> <z> <rotation> <mirror> <no mobs>` | Place a structure at a location | `boxed.admin.place` | Opérateurs |

## Commandes des addons { #addon-commands }

Addons add subcommands to `/boxed` and `/boxadmin`, for example `/boxed level` from [Level](../../addons/Level/index.md) or `/boxed challenges` from [Challenges](../../addons/Challenges/index.md). See each addon's page.
