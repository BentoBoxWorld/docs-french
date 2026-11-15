# Permissions

Chaque permission BentoBox, générée à partir de la source BentoBox. Pour savoir comment les utiliser (rangs VIP, rôles du personnel, erreurs courantes), voir [Permissions & Avantages VIP](Permissions-Guide.md).

Les permissions du mode de jeu commencent par le préfixe du mode de jeu, écrit `[gamemode].` ici : `bskyblock.`, `aoneblock.`, `acidisland.`, `caveblock.`, etc. Les permissions des addons sont répertoriées sur la page de chaque [addon](../addons/Bank/index.md).

!!! tip "Voir les valeurs par défaut sur votre serveur"
    Les valeurs par défaut (tout le monde, opérateurs uniquement, ou personne) sont définies par chaque mode de jeu et diffèrent entre eux. Exécutez `/bentobox perms` dans la console pour imprimer chaque permission de commande avec sa valeur par défaut sur votre serveur.

## BentoBox

| Permission | Défaut | Permet |
|---|---|---|
| `bentobox.about` | Tout le monde | `/bentobox about` |
| `bentobox.version` | Opérateurs | `/bentobox version` |
| `bentobox.admin` | Opérateurs | `/bentobox` et ses sous-commandes administrateur |
| `bentobox.admin.reload` | Opérateurs | `/bentobox reload` et `reload locales` |
| `bentobox.admin.manage` | Opérateurs | `/bentobox manage` |
| `bentobox.admin.catalog` | Opérateurs | `/bentobox catalog` |
| `bentobox.admin.locale` | Opérateurs | `/bentobox locale` |
| `bentobox.admin.migrate` | Opérateurs | `/bentobox migrate` |
| `bentobox.admin.perms` | Opérateurs | `/bentobox perms` |
| `bentobox.admin.rank` | Opérateurs | `/bentobox rank` |
| `bentobox.admin.placeholders` | Opérateurs | `/bentobox placeholders` |
| `bentobox.admin.dump-placeholders` | Opérateurs | `/bentobox dump-placeholders` |

## Mode de jeu : commandes du joueur { #game-mode-player-commands }

La plupart de celles-ci sont accordées à tout le monde par le mode de jeu. Vérifiez avec `/bentobox perms` ; dans certains modes de jeu, `island.homes`, `island.deletehome` et `island.renamehome` sont opérateurs uniquement par défaut.

| Permission | Permet |
|---|---|
| `[gamemode].island` | La commande du joueur elle-même et `help` |
| `[gamemode].island.ban` | `ban`, `banlist`, `unban` |
| `[gamemode].island.create` | `create` |
| `[gamemode].island.deletehome` | `deletehome` |
| `[gamemode].island.expel` | `expel` |
| `[gamemode].island.home` | `go` |
| `[gamemode].island.homes` | `homes` |
| `[gamemode].island.info` | `info` |
| `[gamemode].island.language` | `language` |
| `[gamemode].island.lock` | `lock` |
| `[gamemode].island.name` | `resetname`, `setname` |
| `[gamemode].island.near` | `near` |
| `[gamemode].island.renamehome` | `renamehome` |
| `[gamemode].island.reset` | `reset` |
| `[gamemode].island.sethome` | `sethome` |
| `[gamemode].island.settings` | `settings` |
| `[gamemode].island.spawn` | `spawn` |
| `[gamemode].island.team` | `team` |
| `[gamemode].island.team.accept` | `team accept` |
| `[gamemode].island.team.coop` | `team coop`, `team uncoop` |
| `[gamemode].island.team.invite` | `team invite` |
| `[gamemode].island.team.kick` | `team kick` |
| `[gamemode].island.team.leave` | `team leave` |
| `[gamemode].island.team.promote` | `team demote`, `team promote` |
| `[gamemode].island.team.reject` | `team reject` |
| `[gamemode].island.team.setowner` | `team setowner` |
| `[gamemode].island.team.trust` | `team trust`, `team untrust` |

## Mode de jeu : commandes administrateur et modérateur

Opérateurs uniquement par défaut.

| Permission | Permet `/[admin_command]` |
|---|---|
| `[gamemode].admin` | La commande administrateur elle-même et `help` |
| `[gamemode].admin.blueprint` | `blueprint` |
| `[gamemode].admin.blueprint.copy` | `blueprint copy` |
| `[gamemode].admin.blueprint.delete` | `blueprint delete` |
| `[gamemode].admin.blueprint.list` | `blueprint list` |
| `[gamemode].admin.blueprint.load` | `blueprint load` |
| `[gamemode].admin.blueprint.origin` | `blueprint origin` |
| `[gamemode].admin.blueprint.paste` | `blueprint paste` |
| `[gamemode].admin.blueprint.pos1` | `blueprint pos1` |
| `[gamemode].admin.blueprint.pos2` | `blueprint pos2` |
| `[gamemode].admin.blueprint.rename` | `blueprint rename` |
| `[gamemode].admin.blueprint.save` | `blueprint save` |
| `[gamemode].admin.blueprint.sink` | `blueprint sink` |
| `[gamemode].admin.deaths` | `deaths` |
| `[gamemode].admin.deaths.add` | `deaths add` |
| `[gamemode].admin.deaths.remove` | `deaths remove` |
| `[gamemode].admin.deaths.reset` | `deaths reset` |
| `[gamemode].admin.deaths.set` | `deaths set` |
| `[gamemode].admin.delete` | `delete` |
| `[gamemode].admin.getrank` | `getrank` |
| `[gamemode].admin.purge` | `purge` |
| `[gamemode].admin.purge.age-regions` | `purge age-regions` |
| `[gamemode].admin.purge.deleted` | `purge deleted` |
| `[gamemode].admin.purge.protect` | `purge protect` |
| `[gamemode].admin.purge.unowned` | `purge unowned` |
| `[gamemode].admin.range` | `range` |
| `[gamemode].admin.range.add` | `range add` |
| `[gamemode].admin.range.display` | `range display` |
| `[gamemode].admin.range.purgebonus` | `range purgebonus` |
| `[gamemode].admin.range.remove` | `range remove` |
| `[gamemode].admin.range.removebonus` | `range removebonus` |
| `[gamemode].admin.range.reset` | `range reset` |
| `[gamemode].admin.range.set` | `range set` |
| `[gamemode].admin.register` | `register` |
| `[gamemode].admin.reload` | `reload` |
| `[gamemode].admin.resetflags` | `resetflags` |
| `[gamemode].admin.resets` | `resets` |
| `[gamemode].admin.resets.add` | `resets add` |
| `[gamemode].admin.resets.remove` | `resets remove`, `resets reset` |
| `[gamemode].admin.resets.set` | `resets set` |
| `[gamemode].admin.setprotectionlocation` | `setprotectionlocation` |
| `[gamemode].admin.setrank` | `setrank` |
| `[gamemode].admin.setspawn` | `setspawn` |
| `[gamemode].admin.setspawnpoint` | `setspawnpoint` |
| `[gamemode].admin.settings` | `settings` |
| `[gamemode].admin.tp` | `tp`, `tpend`, `tpnether` |
| `[gamemode].admin.tpuser` | `tpuser`, `tpuserend`, `tpusernether` |
| `[gamemode].admin.undelete` | `undelete` |
| `[gamemode].admin.unregister` | `unregister` |
| `[gamemode].admin.version` | `version` |
| `[gamemode].admin.why` | `why` |
| `[gamemode].mod.deletehomes` | `deletehomes` |
| `[gamemode].mod.info` | `info` |
| `[gamemode].mod.maxhomes` | `maxhomes` |
| `[gamemode].mod.resethome` | `resethome` |
| `[gamemode].mod.resetname` | `resetname` |
| `[gamemode].mod.switch` | `switch` |
| `[gamemode].mod.team` | `team` |
| `[gamemode].mod.team.add` | `team add` |
| `[gamemode].mod.team.disband` | `team disband` |
| `[gamemode].mod.team.disbandall` | `team disbandall` |
| `[gamemode].mod.team.kick` | `team kick` |
| `[gamemode].mod.team.maxsize` | `team maxsize` |
| `[gamemode].mod.team.setowner` | `team setowner` |

## Mode de jeu : limites et avantages

Ceux-ci se terminent par un nombre, qui remplace la valeur de configuration pour ce joueur. Le nombre le plus élevé qu'un joueur a gagne. Voir [Permissions & Avantages VIP](Permissions-Guide.md#perks-with-a-number) pour les règles.

| Permission | Définit | Valeur du config qu'il remplace |
|---|---|---|
| `[gamemode].team.maxsize.<n>` | Taille de l'équipe, y compris le propriétaire (permission du propriétaire de l'île) | `island.max-team-size` |
| `[gamemode].coop.maxsize.<n>` | Joueurs en coopération (permission du propriétaire de l'île) | `island.max-coop-size` |
| `[gamemode].trust.maxsize.<n>` | Joueurs confiants (permission du propriétaire de l'île) | `island.max-trusted-size` |
| `[gamemode].island.range.<n>` | Plage de protection de l'île (permission du propriétaire de l'île) | `world.protection-range` |
| `[gamemode].island.maxhomes.<n>` | Nombre de foyers (permission du propriétaire de l'île) | `island.max-homes` |
| `[gamemode].island.number.<n>` | Nombre d'îles qu'un joueur peut posséder | `world.concurrent-islands` |
| `[gamemode].ban.maxlimit.<n>` | Joueurs qu'ils peuvent bannir à la fois | `world.ban-limit` |

| Permission | Permet |
|---|---|
| `[gamemode].island.create.<bundle>` | Choisir une île de démarrage (paquet de plan) qui nécessite une permission |
| `[gamemode].island.name.format` | Codes couleur dans les noms d'île |

## Mode de jeu : paramètres de l'île

| Permission | Permet |
|---|---|
| `[gamemode].settings.<FLAG_ID>` | Modifier ce paramètre dans `/[player_command] settings` |
| `[gamemode].settings.*` | Modifier chaque paramètre |
| `[gamemode].admin.settings.<FLAG_ID>` | Modifier ce drapeau dans `/[admin_command] settings` |
| `[gamemode].admin.world.settings.<FLAG_ID>` | Modifier ce paramètre mondial ou cette protection mondiale |
| `[gamemode].admin.set-world-defaults` | L'onglet Protections Mondiales des paramètres administrateur |

Voir [Protection, Drapeaux et Rangs](Island-Protection,-Flags-&-Ranks.md) pour les ID des drapeaux.

## Mode de jeu : contournements de modérateur

| Permission | Effet |
|---|---|
| `[gamemode].mod.bypassprotect` | Ignorer tous les drapeaux de protection partout |
| `[gamemode].mod.bypass.<FLAG_ID>.everywhere` | Ignorer un drapeau de protection partout |
| `[gamemode].mod.bypass.<FLAG_ID>.island` | Ignorer un drapeau de protection sur les îles |
| `[gamemode].mod.bypasslock` | Entrer les îles verrouillées |
| `[gamemode].mod.bypassban` | Entrer les îles dont ils sont bannis |
| `[gamemode].mod.bypassexpel` | Ne peut pas être expulsé |
| `[gamemode].mod.bypasscooldowns` | Ignorer les refroidissements de commande |
| `[gamemode].mod.bypassdelays` | Ignorer les délais de téléportation |
| `[gamemode].admin.noban` | Ne peut pas être banni des îles |
| `[gamemode].admin.noexpel` | Ne peut pas être expulsé des îles |

`/[admin_command] switch` désactive et active les permissions de contournement d'un modérateur. Voir [Contourner la protection](Island-Protection,-Flags-&-Ranks.md#bypass-the-protection).
