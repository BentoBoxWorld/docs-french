# Commandes { #commands }

Toutes les commandes de BentoBox et ses modes de jeu, générées depuis la source de BentoBox. Pour savoir comment les utiliser, consultez les [Guides Administrateur](About/Teams.md) et le [Guide du Joueur](Player-Guide.md).

## Comment les commandes des modes de jeu sont nommées { #how-game-mode-commands-are-named }

Chaque mode de jeu a sa propre commande joueur et administrateur. Les tableaux ci-dessous les écrivent comme `/[player_command]` et `/[admin_command]`. Les permissions commencent par le préfixe du mode de jeu, écrit `[gamemode].` :

| Mode de jeu | `[player_command]` | `[admin_command]` | `[gamemode]` |
|---|---|---|---|
| BSkyBlock | `/island`, `/is` | `/bsbadmin`, `/bsb` | `bskyblock` |
| AOneBlock | `/ob`, `/oneblock` | `/oba`, `/obadmin` | `aoneblock` |
| AcidIsland | `/ai` | `/acid` | `acidisland` |
| CaveBlock | `/cave`, `/cb` | `/cbadmin`, `/cba` | `caveblock` |

D'autres modes de jeu énumèrent les leurs sur leur propre page. Tous les noms peuvent être changés dans le `config.yml` du mode de jeu.

Taper une commande sans sous-commande exécute une commande par défaut : pour les joueurs, `/[player_command]` crée une île ou téléporte à la maison (voir [Îles](About/IslandManagement.md#creating-islands)) ; `/[admin_command]` et `help` énumèrent les commandes que le joueur peut utiliser.

Les addons ajoutent leurs propres sous-commandes à celles-ci, par exemple `/island level` ou `/island challenges`. Voir la page de chaque [addon](../addons/Bank/index.md).

## Commandes BentoBox { #bentobox-commands }

La commande `/bentobox` (alias `/bbox`) gère BentoBox lui-même.

| Commande | Description | Permission |
|---|---|---|
| `/bentobox about` | Informations sur le copyright et la licence | `bentobox.about` |
| `/bentobox version` | Versions BentoBox, addon et serveur. Incluez ceci quand vous demandez de l'aide | `bentobox.version` |
| `/bentobox reload` | Rechargez BentoBox et tous les addons, les paramètres, les locales et les modèles de menu | `bentobox.admin.reload` |
| `/bentobox reload locales` | Rechargez seulement les fichiers de locale | `bentobox.admin.reload` |
| `/bentobox manage` | Ouvrir le Panneau de Gestion | `bentobox.admin.manage` |
| `/bentobox catalog` | Ouvrir le catalogue des modes de jeu et des addons | `bentobox.admin.catalog` |
| `/bentobox locale` | Vérifier les fichiers de locale pour les traductions manquantes | `bentobox.admin.locale` |
| `/bentobox migrate` | Déplacer les données d'un type de base de données à un autre. Voir [Changer de Base de Données](Database-transition.md) | `bentobox.admin.migrate` |
| `/bentobox perms` | Affiche chaque permission de commande et sa valeur par défaut (console uniquement) | `bentobox.admin.perms` |
| `/bentobox rank [list \| add \| remove] [rank reference] [rank value]` | Énumérez, ajoutez ou supprimez les rangs de l'île. Voir [Équipes et Rangs](About/Teams.md#custom-ranks) | `bentobox.admin.rank` |
| `/bentobox placeholders` | Ouvrir le navigateur de placeholders | `bentobox.admin.placeholders` |
| `/bentobox dump-placeholders` | Écrire chaque placeholder enregistré dans un fichier markdown | `bentobox.admin.dump-placeholders` |

## Commandes du Joueur { #player-commands }

| Commande | Description | Permission |
|---|---|---|
| `/[player_command] ban <player>` | Bannir un joueur de votre île | `[gamemode].island.ban` |
| `/[player_command] banlist` | Énumérer les joueurs bannis | `[gamemode].island.ban` |
| `/[player_command] create <blueprint>` | Créer une île, en utilisant un modèle optionnel (nécessite la permission) | `[gamemode].island.create` |
| `/[player_command] deletehome [home name]` | Supprimer un emplacement de maison | `[gamemode].island.deletehome` |
| `/[player_command] expel <player>` | Expulser un joueur de votre île | `[gamemode].island.expel` |
| `/[player_command] go [home name]` | Vous téléporter à votre île | `[gamemode].island.home` |
| `/[player_command] homes` | Énumérer vos maisons | `[gamemode].island.homes` |
| `/[player_command] info <player>` | Afficher les informations sur votre île ou l'île du joueur | `[gamemode].island.info` |
| `/[player_command] language [language]` | Sélectionner la langue | `[gamemode].island.language` |
| `/[player_command] lock` | Verrouiller ou déverrouiller votre île | `[gamemode].island.lock` |
| `/[player_command] near` | Afficher le nom des îles voisines autour de vous | `[gamemode].island.near` |
| `/[player_command] renamehome [home name]` | Renommer un emplacement de maison | `[gamemode].island.renamehome` |
| `/[player_command] reset <blueprint>` | Redémarrer votre île et supprimer l'ancienne | `[gamemode].island.reset` |
| `/[player_command] resetname` | Réinitialiser le nom de votre île | `[gamemode].island.name` |
| `/[player_command] sethome` | Définir votre point de téléportation à la maison | `[gamemode].island.sethome` |
| `/[player_command] setname <name>` | Définir un nom pour votre île | `[gamemode].island.name` |
| `/[player_command] settings` | Afficher les paramètres de l'île | `[gamemode].island.settings` |
| `/[player_command] spawn` | Vous téléporter au spawn | `[gamemode].island.spawn` |
| `/[player_command] team` | Gérer votre équipe | `[gamemode].island.team` |
| `/[player_command] team accept` | Accepter une invitation | `[gamemode].island.team.accept` |
| `/[player_command] team coop <player>` | Faire d'un joueur un rang coop sur votre île | `[gamemode].island.team.coop` |
| `/[player_command] team demote <player>` | Rétrograder un joueur d'un rang (jamais en dessous de Membre) | `[gamemode].island.team.promote` |
| `/[player_command] team invite <player>` | Inviter un joueur à rejoindre votre île | `[gamemode].island.team.invite` |
| `/[player_command] team kick <player>` | Supprimer un membre de votre île | `[gamemode].island.team.kick` |
| `/[player_command] team leave` | Quitter votre île | `[gamemode].island.team.leave` |
| `/[player_command] team promote <player>` | Promouvoir un joueur d'un rang sur votre île | `[gamemode].island.team.promote` |
| `/[player_command] team reject` | Rejeter une invitation | `[gamemode].island.team.reject` |
| `/[player_command] team setowner <player>` | Transférer la propriété de votre île à un membre | `[gamemode].island.team.setowner` |
| `/[player_command] team trust <player>` | Donner un rang de confiance à un joueur sur votre île | `[gamemode].island.team.trust` |
| `/[player_command] team uncoop <player>` | Supprimer un rang coop d'un joueur | `[gamemode].island.team.coop` |
| `/[player_command] team uninvite <player>` | Retirer une invitation d'équipe, de confiance ou de coopération en attente (BentoBox 3.24.0+) | `[gamemode].island.team.invite` |
| `/[player_command] team untrust <player>` | Supprimer le rang de confiance d'un joueur | `[gamemode].island.team.trust` |
| `/[player_command] unban <player>` | Débannir un joueur de votre île | `[gamemode].island.ban` |

## Commandes d'Administration { #admin-commands }

Les commandes d'administration sont des opérateurs par défaut. Les commandes avec une permission `mod.` sont destinées aux modérateurs qui ne sont pas des administrateurs complets ; voir [Permissions et Avantages VIP](Permissions-Guide.md#staff-permissions).

| Commande | Description | Permission |
|---|---|---|
| `/[admin_command] blueprint <load/copy/paste/pos1/pos2/save>` | Manipuler les modèles | `[gamemode].admin.blueprint` |
| `/[admin_command] blueprint copy [air] [biome] [nowater]` | Copier le presse-papiers défini par pos1 et pos2 et optionnellement l'air, le biome et les blocs d'eau | `[gamemode].admin.blueprint.copy` |
| `/[admin_command] blueprint delete <name>` | Supprimer le modèle | `[gamemode].admin.blueprint.delete` |
| `/[admin_command] blueprint list` | Énumérer les modèles disponibles | `[gamemode].admin.blueprint.list` |
| `/[admin_command] blueprint load <name>` | Charger le modèle dans le presse-papiers | `[gamemode].admin.blueprint.load` |
| `/[admin_command] blueprint origin` | Définir l'origine du modèle à votre position | `[gamemode].admin.blueprint.origin` |
| `/[admin_command] blueprint paste` | Coller le presse-papiers à votre emplacement | `[gamemode].admin.blueprint.paste` |
| `/[admin_command] blueprint pos1` | Définir le 1er coin du presse-papiers cubique | `[gamemode].admin.blueprint.pos1` |
| `/[admin_command] blueprint pos2` | Définir le 2e coin du presse-papiers cubique | `[gamemode].admin.blueprint.pos2` |
| `/[admin_command] blueprint rename <blueprint name> <new name>` | Renommer un modèle | `[gamemode].admin.blueprint.rename` |
| `/[admin_command] blueprint save <blueprint name>` | Enregistrer le presse-papiers copié | `[gamemode].admin.blueprint.save` |
| `/[admin_command] blueprint sink` | Définir ce modèle pour s'enfoncer au fond de l'océan lors du collage | `[gamemode].admin.blueprint.sink` |
| `/[admin_command] deaths` | Modifier les décès des joueurs | `[gamemode].admin.deaths` |
| `/[admin_command] deaths add <player> <deaths>` | Ajouter des décès au joueur | `[gamemode].admin.deaths.add` |
| `/[admin_command] deaths remove <player> <deaths>` | Supprimer des décès du joueur | `[gamemode].admin.deaths.remove` |
| `/[admin_command] deaths reset <player>` | Réinitialiser les décès du joueur | `[gamemode].admin.deaths.reset` |
| `/[admin_command] deaths set <player> <deaths>` | Définir les décès du joueur | `[gamemode].admin.deaths.set` |
| `/[admin_command] delete [player]` | Supprimer l'île d'un joueur, ou l'île sur laquelle vous vous tenez si aucun joueur n'est donné | `[gamemode].admin.delete` |
| `/[admin_command] deletehomes <player>` | Supprimer toutes les maisons nommées d'une île | `[gamemode].mod.deletehomes` |
| `/[admin_command] getrank <player> [island owner]` | Obtenir le rang d'un joueur sur son île ou l'île du propriétaire | `[gamemode].admin.getrank` |
| `/[admin_command] info <player> [island name]` | Obtenir des informations sur l'endroit où vous êtes ou l'île d'un joueur | `[gamemode].mod.info` |
| `/[admin_command] maxhomes <number / player> <number> [island name]` | Changer le nombre de maisons autorisées sur cette île ou l'île d'un joueur | `[gamemode].mod.maxhomes` |
| `/[admin_command] purge [days]` | Supprimer les fichiers de région pour les îles intactes pendant plus de [days] jours (libère de l'espace disque) | `[gamemode].admin.purge` |
| `/[admin_command] purge age-regions [days]` | Débogage/test : réécrire les timestamps des fichiers de région pour les rendre purgables | `[gamemode].admin.purge.age-regions` |
| `/[admin_command] purge deleted` | Purger les fichiers de région pour toute île déjà marquée comme supprimée | `[gamemode].admin.purge.deleted` |
| `/[admin_command] purge protect` | Basculer la protection de purge de l'île | `[gamemode].admin.purge.protect` |
| `/[admin_command] purge unowned` | Marquer les îles non possédées comme supprimables pour qu'elles puissent être récoltées | `[gamemode].admin.purge.unowned` |
| `/[admin_command] range` | Commande de plage d'île administrateur | `[gamemode].admin.range` |
| `/[admin_command] range add <player> <range> [island location]` | Augmenter la plage de protection de l'île | `[gamemode].admin.range.add` |
| `/[admin_command] range display` | Afficher/masquer les indicateurs de plage de l'île | `[gamemode].admin.range.display` |
| `/[admin_command] range purgebonus <id>` | Supprimer un id de plage bonus de chaque île (par exemple après suppression de l'addon qui l'a ajouté) | `[gamemode].admin.range.purgebonus` |
| `/[admin_command] range remove <player> <range> [island location]` | Diminuer la plage de protection de l'île | `[gamemode].admin.range.remove` |
| `/[admin_command] range removebonus <player> [id]` | Supprimer les plages bonus de l'île (toutes, ou une par id) | `[gamemode].admin.range.removebonus` |
| `/[admin_command] range reset <player>` | Réinitialiser la plage de protection de l'île à la valeur par défaut du monde | `[gamemode].admin.range.reset` |
| `/[admin_command] range set <player> <range> [island location]` | Définir la plage de protection de l'île | `[gamemode].admin.range.set` |
| `/[admin_command] register <player>` | Enregistrer le joueur à l'île non possédée sur laquelle vous êtes | `[gamemode].admin.register` |
| `/[admin_command] reload` | Recharger | `[gamemode].admin.reload` |
| `/[admin_command] resetflags [flag]` | Réinitialiser toutes les îles aux paramètres de drapeau par défaut dans config.yml | `[gamemode].admin.resetflags` |
| `/[admin_command] resethome <player> [island name]` | Réinitialiser la maison du joueur à la valeur par défaut | `[gamemode].mod.resethome` |
| `/[admin_command] resetname` | Réinitialiser le nom de l'île du joueur | `[gamemode].mod.resetname` |
| `/[admin_command] resets` | Modifier les valeurs de réinitialisation du joueur | `[gamemode].admin.resets` |
| `/[admin_command] resets add <player> <resets>` | Augmenter le nombre de réinitialisations de l'île du joueur | `[gamemode].admin.resets.add` |
| `/[admin_command] resets remove <player> <resets>` | Réduire le nombre de réinitialisations de l'île du joueur | `[gamemode].admin.resets.remove` |
| `/[admin_command] resets reset <player>` | Définir le nombre de réinitialisations de l'île du joueur à 0 | `[gamemode].admin.resets.remove` |
| `/[admin_command] resets set <player> <resets>` | Définir le nombre de fois où ce joueur a réinitialisé son île | `[gamemode].admin.resets.set` |
| `/[admin_command] setprotectionlocation [x y z coords]` | Définir l'emplacement actuel ou [x y z] comme centre de la zone de protection de l'île | `[gamemode].admin.setprotectionlocation` |
| `/[admin_command] setrank <player> <rank> [island owner \| x,y,z]` | Promouvoir ou rétrograder un joueur à un rang sur son île d'équipe, ou sur l'île nommée par son propriétaire ou centre x,y,z | `[gamemode].admin.setrank` |
| `/[admin_command] setspawn` | Définir une île comme spawn pour ce mode de jeu | `[gamemode].admin.setspawn` |
| `/[admin_command] setspawnpoint` | Définir l'emplacement actuel comme point de spawn de cette île | `[gamemode].admin.setspawnpoint` |
| `/[admin_command] settings [player]/[world flag]/spawn-island [flag/active/disable] [rank/active/disable]` | Ouvrir l'interface graphique des paramètres ou définir les paramètres | `[gamemode].admin.settings` |
| `/[admin_command] switch` | Basculer la contournement de protection on/off | `[gamemode].mod.switch` |
| `/[admin_command] team` | Gérer les équipes | `[gamemode].mod.team` |
| `/[admin_command] team add <owner> <player>` | Ajouter un joueur à l'équipe du propriétaire | `[gamemode].mod.team.add` |
| `/[admin_command] team disband <owner>` | Dissoudre l'équipe du propriétaire | `[gamemode].mod.team.disband` |
| `/[admin_command] team disbandall` | Supprimer chaque membre et sous-propriétaire de chaque île dans ce monde | `[gamemode].mod.team.disbandall` |
| `/[admin_command] team kick <team player> [x,y,z]` | Expulser un joueur d'une équipe | `[gamemode].mod.team.kick` |
| `/[admin_command] team maxsize <player> <size>` | Définir la taille maximale de l'équipe pour l'île d'un joueur (utilisez 0 pour réinitialiser à la valeur par défaut du monde) | `[gamemode].mod.team.maxsize` |
| `/[admin_command] team setowner <player> [island owner]` | Transférer la propriété de l'île au joueur. Nommez le propriétaire de l'île actuel pour l'exécuter depuis la console | `[gamemode].mod.team.setowner` |
| `/[admin_command] tp <player> [player's island]` | Téléporter à l'île d'un joueur | `[gamemode].admin.tp` |
| `/[admin_command] tpend <player> [player's island]` | Téléporter à l'île d'un joueur dans l'End | `[gamemode].admin.tp` |
| `/[admin_command] tpnether <player> [player's island]` | Téléporter à l'île d'un joueur dans le Nether | `[gamemode].admin.tp` |
| `/[admin_command] tpuser <teleporting player> <island's player> [player's island]` | Téléporter un joueur à l'île d'un autre joueur | `[gamemode].admin.tpuser` |
| `/[admin_command] tpuserend <teleporting player> <island's player> [player's island]` | Téléporter un joueur à l'île d'un autre joueur dans l'End | `[gamemode].admin.tpuser` |
| `/[admin_command] tpusernether <teleporting player> <island's player> [player's island]` | Téléporter un joueur à l'île d'un autre joueur dans le Nether | `[gamemode].admin.tpuser` |
| `/[admin_command] undelete` | Supprimer le statut de suppression en attente de l'île non possédée sur laquelle vous êtes | `[gamemode].admin.undelete` |
| `/[admin_command] unregister <owner> [x,y,z]` | Annuler l'enregistrement du propriétaire de l'île, mais garder les blocs de l'île | `[gamemode].admin.unregister` |
| `/[admin_command] version` | Afficher les versions BentoBox et les addons | `[gamemode].admin.version` |
| `/[admin_command] why <player>` | Basculer le rapport de débogage de protection de la console | `[gamemode].admin.why` |

`/[admin_command] add`, `disband`, `kick` et `setowner` fonctionnent également sans `team` (par exemple `/bsbadmin kick <player>`), pour la compatibilité avec les versions antérieures.
