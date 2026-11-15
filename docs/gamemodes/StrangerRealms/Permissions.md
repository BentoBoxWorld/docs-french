# Autorisations StrangerRealms

Les autorisations de StrangerRealms commencent par `strangerrealms.`. Chaque autorisation est listée dans la [Référence des autorisations](../../BentoBox/Permissions.md) avec `[gamemode]` à la place de `strangerrealms`. Pour les avantages VIP tels que des équipes plus grandes, des îles plus grandes et plus de maisons, consultez [Autorisations et Avantages VIP](../../BentoBox/Permissions-Guide.md).

## Commandes du joueur : qui les a par défaut

Ces valeurs par défaut proviennent de StrangerRealms `addon.yml`. **Tout le monde** signifie que tous les joueurs ont l'autorisation à moins que vous la leur retiriez; **Opérateurs** signifie que vous devez la donner aux joueurs avec votre plugin d'autorisations. Exécutez `/bentobox perms` dans la console pour voir les valeurs par défaut de votre serveur.

| Autorisation | Commandes | Par défaut |
|---|---|---|
| `strangerrealms.island` | La commande du joueur elle-même | Tout le monde |
| `strangerrealms.island.create` | `create` | Opérateurs (non déclaré) |
| `strangerrealms.island.home` | `go` | Tout le monde |
| `strangerrealms.island.homes` | `homes` | Tout le monde |
| `strangerrealms.island.sethome` | `sethome` | Tout le monde |
| `strangerrealms.island.deletehome` | `deletehome` | Tout le monde |
| `strangerrealms.island.renamehome` | `renamehome` | Tout le monde |
| `strangerrealms.island.info` | `info` | Tout le monde |
| `strangerrealms.island.near` | `near` | Tout le monde |
| `strangerrealms.island.reset` | `reset` | Personne |
| `strangerrealms.island.name` | `setname`, `resetname` | Tout le monde |
| `strangerrealms.island.language` | `language` | Tout le monde |
| `strangerrealms.island.settings` | `settings` | Tout le monde |
| `strangerrealms.island.lock` | `lock` | Tout le monde |
| `strangerrealms.island.ban` | `ban`, `unban`, `banlist` | Tout le monde |
| `strangerrealms.island.expel` | `expel` | Tout le monde |
| `strangerrealms.island.team` | `team` | Tout le monde |
| `strangerrealms.island.team.invite` | `team invite` | Tout le monde |
| `strangerrealms.island.team.accept` | `team accept` | Tout le monde |
| `strangerrealms.island.team.reject` | `team reject` | Tout le monde |
| `strangerrealms.island.team.leave` | `team leave` | Tout le monde |
| `strangerrealms.island.team.kick` | `team kick` | Tout le monde |
| `strangerrealms.island.team.promote` | `team promote`, `team demote` | Tout le monde |
| `strangerrealms.island.team.setowner` | `team setowner` | Tout le monde |
| `strangerrealms.island.team.trust` | `team trust`, `team untrust` | Tout le monde |
| `strangerrealms.island.team.coop` | `team coop`, `team uncoop` | Tout le monde |

## Autorisations uniquement dans StrangerRealms

| Autorisation | Allows | Par défaut |
|---|---|---|
| `strangerrealms.claim` | `/st claim` | Tout le monde |
| `strangerrealms.unclaim` | `/st unclaim` | Tout le monde |
| `strangerrealms.spawn` | `/st spawn` | Tout le monde |
| `strangerrealms.admin.worldborder` | `/stranger worldborder` | Opérateurs (non déclaré) |

Les autorisations des administrateurs et modérateurs (`strangerrealms.admin.*`, `strangerrealms.mod.*`) sont pour les opérateurs par défaut. Voir [Autorisations du personnel](../../BentoBox/Permissions-Guide.md#staff-permissions).
