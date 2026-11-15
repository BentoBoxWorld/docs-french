# Autorisations et Avantages VIP { #permissions-vip-perks }

BentoBox fonctionne avec n'importe quel plugin d'autorisations (LuckPerms est le plus courant). Cette page explique comment les autorisations de BentoBox sont nommées, lesquelles les joueurs ont déjà et comment donner aux rangs ou VIP des équipes plus grandes, des îles plus grandes, plus de maisons et d'autres avantages.

!!! info "Exemples sur cette page"
    Les exemples utilisent BSkyBlock, dont les autorisations commencent par `bskyblock.`, et les commandes LuckPerms. Chaque mode de jeu a son propre préfixe, par exemple `aoneblock.`, `acidisland.` ou `caveblock.`, donc un avantage doit être donné une fois pour chaque mode de jeu.

## Comment les autorisations sont nommées { #how-the-permissions-are-named }

| L'autorisation commence par | Utilisée pour | Qui l'a par défaut |
|---|---|---|
| `bentobox.` | La commande `/bentobox` | Les opérateurs (`bentobox.about` est pour tout le monde) |
| `<gamemode>.island.` | Les commandes du joueur, comme `bskyblock.island.team.invite` | Les joueurs, principalement. Voir [ci-dessous](#check-what-players-have-by-default) |
| `<gamemode>.admin.` | Les commandes d'administrateur, comme `bskyblock.admin.delete` | Les opérateurs |
| `<gamemode>.mod.` | Les commandes de modérateur et les contournements de protection, comme `bskyblock.mod.info` | Les opérateurs |
| `<gamemode>.settings.` | Changer les paramètres de l'île dans `/island settings` | Les joueurs |
| `<gamemode>.<thing>.<number>` | Les limites, comme `bskyblock.team.maxsize.8` | Personne : la valeur de configuration est utilisée |

Les add-ons ajoutent leurs propres autorisations. Elles sont listées sur la page de chaque [add-on](../addons/Bank/index.md).

### Vérifier ce que les joueurs ont par défaut { #check-what-players-have-by-default }

Exécutez **`/bentobox perms`** dans la console. Elle imprime chaque autorisation de commande BentoBox et mode de jeu avec sa valeur par défaut (`TRUE` pour tout le monde, `OP` pour les opérateurs, `FALSE` pour personne), dans un format que vous pouvez coller dans un plugin d'autorisations.

!!! warning "Certaines commandes de joueur ne sont que pour les opérateurs par défaut"
    Dans BSkyBlock, AOneBlock et AcidIsland, `island.deletehome` et `island.renamehome` ne sont que pour les opérateurs par défaut. Dans AOneBlock et AcidIsland, il en va de même pour `island.homes`. Si vous donnez aux joueurs plus d'une maison, donnez-leur aussi celles-ci :

    ```
    /lp group default permission set bskyblock.island.homes true
    /lp group default permission set bskyblock.island.deletehome true
    /lp group default permission set bskyblock.island.renamehome true
    ```

## Avantages avec un nombre { #perks-with-a-number }

Ces autorisations se terminent par un nombre. Le nombre remplace la valeur dans le `config.yml` du mode de jeu pour ce joueur.

| Avantage | Autorisation | Valeur par défaut de la configuration | Vérifiée pour |
|---|---|---|---|
| Taille de l'équipe (y compris le propriétaire) | `bskyblock.team.maxsize.<n>` | `island.max-team-size` | Propriétaire de l'île |
| Joueurs en coopération | `bskyblock.coop.maxsize.<n>` | `island.max-coop-size` | Propriétaire de l'île |
| Joueurs de confiance | `bskyblock.trust.maxsize.<n>` | `island.max-trusted-size` | Propriétaire de l'île |
| Taille de l'île (étendue de protection) | `bskyblock.island.range.<n>` | `world.protection-range` | Propriétaire de l'île |
| Nombre de maisons | `bskyblock.island.maxhomes.<n>` | `island.max-homes` | Propriétaire de l'île |
| Nombre d'îles | `bskyblock.island.number.<n>` | `world.concurrent-islands` | Le joueur |
| Joueurs qu'ils peuvent bannir | `bskyblock.ban.maxlimit.<n>` | `world.ban-limit` (`-1` = pas de limite) | Le joueur |

Comment le nombre est déterminé :

- **Le nombre le plus élevé gagne.** Un joueur avec à la fois `team.maxsize.6` et `team.maxsize.10` obtient 10. Les rangs peuvent s'empiler sans conflits.
- **Le nombre remplace la valeur de configuration, même s'il est inférieur.** `team.maxsize.2` donne une équipe de 2 même si la configuration dit 4. Ne donnez ces autorisations que pour augmenter les limites.
- **`.*` est ignoré.** Un joueur avec `bskyblock.team.maxsize.*` (par exemple via un wildcard ou un plugin d'opérateurs) obtient la valeur de configuration, pas l'illimité. Utilisez un nombre élevé à la place.
- **Les avantages de l'île suivent le propriétaire.** La taille de l'équipe, la portée et les maisons viennent des autorisations du **propriétaire** de l'île, pas de chaque membre. Ils sont mis à jour quand le propriétaire se connecte, et la portée est aussi fixée quand l'île est créée.
- **La taille de l'île est limitée** à `distance-between-islands` ; demander plus n'a aucun effet. Voir [Îles](About/IslandManagement.md#island-size-protection-range).

## Autres avantages { #other-perks }

| Avantage | Autorisation |
|---|---|
| Une île de démarrage VIP dans le menu Créer une île | `bskyblock.island.create.<bundle-name>`, après avoir défini ce bundle pour exiger une autorisation dans `/bsbadmin blueprint`. Voir [Îles](About/IslandManagement.md#creating-islands) |
| Codes de couleur dans les noms d'îles | `bskyblock.island.name.format` |
| Ignorer les refroidissements de commande (réinitialisations, invitations) | `bskyblock.mod.bypasscooldowns` |
| Ignorer le délai de téléportation | `bskyblock.mod.bypassdelays` |
| Ne peut pas être banni ou expulsé des îles | `bskyblock.admin.noban`, `bskyblock.admin.noexpel` |
| Ne peut pas changer un paramètre d'île particulier | Supprimer `bskyblock.settings.<FLAG_ID>`. Voir [Protection, Drapeaux et Rangs](Island-Protection,-Flags-&-Ranks.md#settings-tab) |

Les choses qui ne sont **pas** des autorisations : les réinitialisations d'îles supplémentaires (utilisez `/bsbadmin resets`, voir [Îles](About/IslandManagement.md#resetting-islands)), et le droit d'inviter, d'expulser ou de bannir sur l'île de quelqu'un d'autre (les propriétaires d'îles contrôlent cela avec les rangs, voir [Équipes et Rangs](About/Teams.md#letting-members-manage-the-team)).

## Exemple : un rang VIP { #example-a-vip-rank }

Un groupe VIP dans BSkyBlock avec une équipe de 8, une île plus grande, trois maisons et une île de démarrage VIP :

```
/lp creategroup vip
/lp group vip permission set bskyblock.team.maxsize.8 true
/lp group vip permission set bskyblock.island.range.100 true
/lp group vip permission set bskyblock.island.maxhomes.3 true
/lp group vip permission set bskyblock.island.homes true
/lp group vip permission set bskyblock.island.deletehome true
/lp group vip permission set bskyblock.island.renamehome true
/lp group vip permission set bskyblock.island.create.vip true
/lp user <player> parent add vip
```

Le joueur doit **se déconnecter et se reconnecter** pour que la taille de l'équipe, la portée et les maisons s'appliquent à une île qu'il possède déjà.

Pour vendre des améliorations étape par étape (îles plus grandes, plus d'emplacements d'équipe, plus de maisons) avec de l'argent en jeu, voir l'addon [Upgrades](../addons/Upgrades/index.md).

## Autorisations du personnel { #staff-permissions }

| Rôle | Donner |
|---|---|
| Administrateur complet pour un mode de jeu | `bskyblock.admin.*` et `bskyblock.mod.*` |
| Modérateur qui peut regarder mais pas modifier les îles | `bskyblock.mod.info`, `bskyblock.admin.tp`, `bskyblock.mod.bypasslock`, `bskyblock.mod.bypassban` |
| Modérateur qui peut construire n'importe où | ajouter `bskyblock.mod.bypassprotect` et `bskyblock.mod.switch` (leur permet d'éteindre le contournement avec `/bsbadmin switch`) |
| Administrateur BentoBox (recharger, gérer, migrer) | `bentobox.admin` et ses sous-autorisations |

Toutes les autorisations de contournement de protection sont expliquées dans [Protection, Drapeaux et Rangs](Island-Protection,-Flags-&-Ranks.md#bypass-the-protection).

## Résolution des problèmes { #troubleshooting }

**Un avantage ne s'applique pas.**
Les avantages de l'île proviennent du propriétaire de l'île et sont mis à jour quand il se connecte. Faites se déconnecter et reconnecter le propriétaire. Pour la portée, vérifiez que `distance-between-islands` n'est pas inférieur au nombre.

**Un VIP a obtenu une équipe plus petite que les joueurs normaux.**
Un nombre inférieur dans un autre groupe a remplacé la valeur de configuration. Supprimez-le ; le nombre le plus élevé qu'un joueur a est utilisé.

**Les joueurs ne peuvent pas utiliser une commande.**
Exécutez `/bentobox perms` et vérifiez la valeur par défaut pour cette commande. Donnez l'autorisation à votre groupe par défaut si elle est `OP` ou `FALSE`.

**L'avantage fonctionne dans un mode de jeu mais pas dans un autre.**
Chaque mode de jeu a son propre préfixe. Donnez l'autorisation à nouveau pour `aoneblock.`, `acidisland.` et ainsi de suite.

## Voir aussi { #see-also }

- [Référence des autorisations](Permissions.md) : chaque autorisation BentoBox et mode de jeu
- [Référence des commandes](Commands.md)
- [Équipes et Rangs](About/Teams.md), [Îles](About/IslandManagement.md), [Protection, Drapeaux et Rangs](Island-Protection,-Flags-&-Ranks.md)
