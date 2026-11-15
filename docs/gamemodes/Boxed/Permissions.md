# Autorisations Boxed { #boxed-permissions }

Les autorisations de Boxed commencent par `boxed.`. Chaque autorisation est listée dans la [Référence des autorisations](../../BentoBox/Permissions.md) avec `[gamemode]` à la place de `boxed`. Pour les avantages VIP tels que des équipes plus grandes, des îles plus grandes et plus de maisons, consultez [Autorisations et Avantages VIP](../../BentoBox/Permissions-Guide.md).

## Commandes du joueur : qui les a par défaut { #player-commands-who-has-them-by-default }

Ces valeurs par défaut proviennent de Boxed `addon.yml`. **Tout le monde** signifie que tous les joueurs ont l'autorisation à moins que vous la leur retiriez; **Opérateurs** signifie que vous devez la donner aux joueurs avec votre plugin d'autorisations. Exécutez `/bentobox perms` dans la console pour voir les valeurs par défaut de votre serveur.

| Autorisation | Commandes | Par défaut |
|---|---|---|
| `boxed.island` | La commande du joueur elle-même | Tout le monde |
| `boxed.island.create` | `create` | Tout le monde |
| `boxed.island.home` | `go` | Tout le monde |
| `boxed.island.homes` | `homes` | Tout le monde |
| `boxed.island.sethome` | `sethome` | Tout le monde |
| `boxed.island.deletehome` | `deletehome` | Tout le monde |
| `boxed.island.renamehome` | `renamehome` | Tout le monde |
| `boxed.island.spawn` | `spawn` | Tout le monde |
| `boxed.island.info` | `info` | Tout le monde |
| `boxed.island.near` | `near` | Tout le monde |
| `boxed.island.reset` | `reset` | Tout le monde |
| `boxed.island.name` | `setname`, `resetname` | Tout le monde |
| `boxed.island.language` | `language` | Tout le monde |
| `boxed.island.settings` | `settings` | Tout le monde |
| `boxed.island.lock` | `lock` | Tout le monde |
| `boxed.island.ban` | `ban`, `unban`, `banlist` | Tout le monde |
| `boxed.island.expel` | `expel` | Tout le monde |
| `boxed.island.team` | `team` | Tout le monde |
| `boxed.island.team.invite` | `team invite` | Tout le monde |
| `boxed.island.team.accept` | `team accept` | Tout le monde |
| `boxed.island.team.reject` | `team reject` | Tout le monde |
| `boxed.island.team.leave` | `team leave` | Tout le monde |
| `boxed.island.team.kick` | `team kick` | Tout le monde |
| `boxed.island.team.promote` | `team promote`, `team demote` | Tout le monde |
| `boxed.island.team.setowner` | `team setowner` | Tout le monde |
| `boxed.island.team.trust` | `team trust`, `team untrust` | Tout le monde |
| `boxed.island.team.coop` | `team coop`, `team uncoop` | Tout le monde |

## Autorisations uniquement dans Boxed { #permissions-only-in-boxed }

| Autorisation | Allows | Par défaut |
|---|---|---|
| `boxed.admin.place` | `/boxadmin place` | Opérateurs |

Les autorisations des administrateurs et modérateurs (`boxed.admin.*`, `boxed.mod.*`) sont pour les opérateurs par défaut. Voir [Autorisations du personnel](../../BentoBox/Permissions-Guide.md#staff-permissions).
