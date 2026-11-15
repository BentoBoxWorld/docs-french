# Autorisations AOneBlock

Les autorisations d'AOneBlock commencent par `aoneblock.`. Chaque autorisation est listée dans la [Référence des autorisations](../../BentoBox/Permissions.md) avec `[gamemode]` à la place de `aoneblock`. Pour les avantages VIP tels que des équipes plus grandes, des îles plus grandes et plus de maisons, consultez [Autorisations et Avantages VIP](../../BentoBox/Permissions-Guide.md).

## Commandes du joueur : qui les a par défaut

Ces valeurs par défaut proviennent d'AOneBlock `addon.yml`. **Tout le monde** signifie que tous les joueurs ont l'autorisation à moins que vous la leur retiriez; **Opérateurs** signifie que vous devez la donner aux joueurs avec votre plugin d'autorisations. Exécutez `/bentobox perms` dans la console pour voir les valeurs par défaut de votre serveur.

| Autorisation | Commandes | Par défaut |
|---|---|---|
| `aoneblock.island` | La commande du joueur elle-même | Tout le monde |
| `aoneblock.island.create` | `create` | Tout le monde |
| `aoneblock.island.home` | `go` | Tout le monde |
| `aoneblock.island.homes` | `homes` | Tout le monde |
| `aoneblock.island.sethome` | `sethome` | Tout le monde |
| `aoneblock.island.deletehome` | `deletehome` | Tout le monde |
| `aoneblock.island.renamehome` | `renamehome` | Tout le monde |
| `aoneblock.island.spawn` | `spawn` | Tout le monde |
| `aoneblock.island.info` | `info` | Tout le monde |
| `aoneblock.island.near` | `near` | Tout le monde |
| `aoneblock.island.reset` | `reset` | Tout le monde |
| `aoneblock.island.name` | `setname`, `resetname` | Tout le monde |
| `aoneblock.island.language` | `language` | Tout le monde |
| `aoneblock.island.settings` | `settings` | Tout le monde |
| `aoneblock.island.lock` | `lock` | Tout le monde |
| `aoneblock.island.ban` | `ban`, `unban`, `banlist` | Tout le monde |
| `aoneblock.island.expel` | `expel` | Tout le monde |
| `aoneblock.island.team` | `team` | Tout le monde |
| `aoneblock.island.team.invite` | `team invite` | Tout le monde |
| `aoneblock.island.team.accept` | `team accept` | Tout le monde |
| `aoneblock.island.team.reject` | `team reject` | Tout le monde |
| `aoneblock.island.team.leave` | `team leave` | Tout le monde |
| `aoneblock.island.team.kick` | `team kick` | Tout le monde |
| `aoneblock.island.team.promote` | `team promote`, `team demote` | Tout le monde |
| `aoneblock.island.team.setowner` | `team setowner` | Tout le monde |
| `aoneblock.island.team.trust` | `team trust`, `team untrust` | Tout le monde |
| `aoneblock.island.team.coop` | `team coop`, `team uncoop` | Tout le monde |

## Autorisations uniquement dans AOneBlock

| Autorisation | Allows | Par défaut |
|---|---|---|
| `aoneblock.count` | `/ob count` | Tout le monde |
| `aoneblock.phases` | `/ob phases` | Opérateurs |
| `aoneblock.island.setcount` | `/ob setCount` | Opérateurs |
| `aoneblock.respawn-block` | `/ob respawnBlock` | Tout le monde |
| `aoneblock.island.bossbar` | `/ob bossbar` | Tout le monde |
| `aoneblock.island.actionbar` | `/ob actionbar` | Tout le monde |
| `aoneblock.admin.setcount` | `/obadmin setcount` | Opérateurs |
| `aoneblock.admin.setchest` | `/obadmin setchest` | Opérateurs |
| `aoneblock.admin.sanity` | `/obadmin sanity` | Opérateurs |
| `aoneblock.admin.phases` | `/obadmin phases` | Opérateurs |

Les autorisations des administrateurs et modérateurs (`aoneblock.admin.*`, `aoneblock.mod.*`) sont pour les opérateurs par défaut. Voir [Autorisations du personnel](../../BentoBox/Permissions-Guide.md#staff-permissions).
