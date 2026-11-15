# Commandes AcidIsland { #acidisland-commands }

| | Commande | Préfixe d'autorisation |
|---|---|---|
| Joueurs | `/ai` | `acidisland.` |
| Administrateurs | `/acid` | `acidisland.` |

Vous pouvez renommer les deux commandes dans le `config.yml` du du mode de jeu.

## Commandes standard { #standard-commands }

AcidIsland utilise les commandes standard du joueur et administrateur de BentoBox. Elles sont toutes listées, avec leurs autorisations, dans la [Référence des commandes](../../BentoBox/Commands.md) : remplacez `/[player_command]` par `/ai`, `/[admin_command]` par `/acid` et `[gamemode]` par `acidisland`. Par exemple :

```
/ai              allez à votre île, ou créez-en une
/ai team invite <player>
/ai settings
/acid info <player>
/acid why <player>
```

Pour voir ce qu'elles font, consultez le [Guide du Joueur](../../BentoBox/Player-Guide.md) et les Guides Administrateur, tels que [Équipes et Rangs](../../BentoBox/About/Teams.md) et [Îles](../../BentoBox/About/IslandManagement.md).

## Commandes uniquement dans AcidIsland { #commands-only-in-acidisland }

| Commande | Ce qu'il fait | Autorisation | Par défaut |
|---|---|---|---|
| `/ai about` | Afficher les informations de copyright et de licence | `acidisland.island` | Tout le monde |

## Commandes des addons { #addon-commands }

Les addons ajoutent des sous-commandes à `/ai` et `/acid`, par exemple `/ai level` de [Level](../../addons/Level/index.md) ou `/ai challenges` de [Challenges](../../addons/Challenges/index.md). Consultez la page de chaque addon.
