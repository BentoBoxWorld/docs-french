# Commandes AOneBlock

| | Commande | Préfixe d'autorisation |
|---|---|---|
| Joueurs | `/ob` (aussi `/oneblock`) | `aoneblock.` |
| Administrateurs | `/obadmin` (aussi `/oneblockadmin`, `/oba`) | `aoneblock.` |

Vous pouvez renommer les deux commandes dans le `config.yml` du du mode de jeu.

## Commandes standard

AOneBlock utilise les commandes standard du joueur et administrateur de BentoBox. Elles sont toutes listées, avec leurs autorisations, dans la [Référence des commandes](../../BentoBox/Commands.md) : remplacez `/[player_command]` par `/ob`, `/[admin_command]` par `/obadmin` et `[gamemode]` par `aoneblock`. Par exemple :

```
/ob              allez à votre île, ou créez-en une
/ob team invite <player>
/ob settings
/obadmin info <player>
/obadmin why <player>
```

Pour voir ce qu'elles font, consultez le [Guide du Joueur](../../BentoBox/Player-Guide.md) et les Guides Administrateur, tels que [Équipes et Rangs](../../BentoBox/About/Teams.md) et [Îles](../../BentoBox/About/IslandManagement.md).

## Commandes uniquement dans AOneBlock

| Commande | Ce qu'il fait | Autorisation | Par défaut |
|---|---|---|---|
| `/ob count` | Afficher votre comptage de blocs et votre phase | `aoneblock.count` | Tout le monde |
| `/ob phases` | Afficher une liste de toutes les phases | `aoneblock.phases` | Opérateurs |
| `/ob setCount <count>` | Définissez votre comptage de blocs à une valeur que vous avez déjà atteinte | `aoneblock.island.setcount` | Opérateurs |
| `/ob respawnBlock` | Faire réapparaître le bloc magique s'il a disparu (alias : check) | `aoneblock.respawn-block` | Tout le monde |
| `/ob bossbar` | Activer ou désactiver la barre de boss de phase | `aoneblock.island.bossbar` | Tout le monde |
| `/ob actionbar` | Activer ou désactiver la barre d'action de phase | `aoneblock.island.actionbar` | Tout le monde |
| `/obadmin setcount <name> <count> [lifetime]` | Définir le comptage de blocs d'un joueur | `aoneblock.admin.setcount` | Opérateurs |
| `/obadmin setchest <phase> <rarity>` | Ajouter le coffre auquel vous regardez à une phase, avec cette rareté | `aoneblock.admin.setchest` | Opérateurs |
| `/obadmin sanity <phase>` | Imprimer une vérification des probabilités de blocs de la phase dans la console | `aoneblock.admin.sanity` | Opérateurs |
| `/obadmin phases` | Ouvrir l'éditeur d'ordre des phases | `aoneblock.admin.phases` | Opérateurs |

The Les étiquettes des commandes du joueur AOneBlock (`count`, `phases`, `setCount`, `respawnBlock`, `bossbar`, `actionbar`) peuvent être renommées dans `config.yml` sous `aoneblock.command`. Les commandes de la barre de boss et de la barre d'action n'existent que lorsque ces fonctionnalités sont activées.

## Commandes des addons

Les addons ajoutent des sous-commandes à `/ob` et `/obadmin`, par exemple `/ob level` de [Level](../../addons/Level/index.md) ou `/ob challenges` de [Challenges](../../addons/Challenges/index.md). Consultez la page de chaque addon.
