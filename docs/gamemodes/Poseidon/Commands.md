# Commandes Poseidon

| | Commande | Préfixe d'autorisation |
|---|---|---|
| Players | `/po` | `poseidon.` |
| Admins | `/padmin` | `poseidon.` |

Vous pouvez renommer les deux commandes dans le `config.yml` du du mode de jeu.

## Commandes standard

Poseidon utilise les commandes standard du joueur et administrateur de BentoBox. Elles sont toutes listées, avec leurs autorisations, dans la [Référence des commandes](../../BentoBox/Commands.md) : replace `/[player_command]` with `/po`, `/[admin_command]` with `/padmin` et `[gamemode]` par `poseidon`. Par exemple :

```
/po              allez à votre île, ou créez-en une
/po team invite <player>
/po settings
/padmin info <player>
/padmin why <player>
```

Pour voir ce qu'elles font, consultez le [Guide du Joueur](../../BentoBox/Player-Guide.md) et les Guides Administrateur, tels que [Équipes et Rangs](../../BentoBox/About/Teams.md) et [Îles](../../BentoBox/About/IslandManagement.md).

## Commandes uniquement dans Poseidon

| Commande | Ce qu'il fait | Autorisation | Par défaut |
|---|---|---|---|
| `/po about` | Afficher les informations de copyright et de licence | `poseidon.island` | Tout le monde |

## Commandes des addons

Addons add subcommands to `/po` and `/padmin`, for example `/po level` from [Level](../../addons/Level/index.md) or `/po challenges` from [Challenges](../../addons/Challenges/index.md). See each addon's page.
