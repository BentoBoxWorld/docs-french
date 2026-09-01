# Permissions ChunkBlock

Chaque permission ChunkBlock est préfixée par `chunkblock.`. Les valeurs par défaut sont choisies pour qu'une installation vanilla joue le jeu prévu sans aucun plugin de permissions du tout : tout ce qu'un joueur a besoin est `true`, les outils administrateur sont OP, et les deux nœuds qui changeraient le jeu lui-même — le GUI des phases et le contournement du verrouillage des chunks — sont désactivés jusqu'à ce que vous les accordiez.

!!! warning "`chunkblock.mod.bypasschunks` n'est délibérément pas une valeur par défaut OP"
    Il exempte le titulaire du verrouillage des chunks entièrement et active `/chadmin bypass`. Sa valeur par défaut est `false`, **pas** `op`, donc le personnel joue selon les mêmes règles que tout le monde jusqu'à ce que vous l'accordiez explicitement dans votre plugin de permissions.

    C'est un nœud séparé de `chunkblock.mod.bypasslock`, qui est le contournement du *verrouillage* de l'île BentoBox et ne fait rien pour les verrous des chunks.

!!! note "Deux nœuds sont désactivés par défaut"
    - `chunkblock.phases` — le GUI `/ch phases`. Accordez-le si vous voulez que les joueurs parcourent et rejouent les phases.
    - `chunkblock.island.setcount` — rejouer une phase. OP uniquement par défaut, et le GUI des phases le vérifie avant d'offrir *« Cliquez pour modifier »*.

## Permissions spécifiques à ChunkBlock

| Permission | Description | Par défaut |
|------------|-------------|---------|
| `chunkblock.admin.chunks` | Autoriser l'utilisation de la commande '/chadmin chunks' - inspecter, définir ou recalculer les chunks déverrouillés d'un joueur | OP |
| `chunkblock.admin.phases` | Autoriser l'utilisation de la commande '/chadmin phases' - ouvrir l'éditeur d'ordre de phase | OP |
| `chunkblock.admin.sanity` | Autoriser l'utilisation de la commande '/chadmin sanity' - afficher une vérification de santé des probabilités de phase dans la console | OP |
| `chunkblock.admin.setchest` | Autoriser l'utilisation de la commande '/chadmin setchest' - mettre le coffre regardé dans une phase avec la rareté spécifiée | OP |
| `chunkblock.admin.setcount` | Autoriser l'utilisation de la commande '/chadmin setcount' - définir le compteur de blocs du joueur | OP |
| `chunkblock.count` | Autoriser l'utilisation de la commande '/ch count' - afficher le compteur de blocs et la phase | `true` |
| `chunkblock.island.actionbar` | Autoriser l'utilisation de la commande '/ch actionbar' - basculer la barre d'action | `true` |
| `chunkblock.island.bossbar` | Autoriser l'utilisation de la commande '/ch bossbar' - basculer la barre de boss | `true` |
| `chunkblock.island.chunks` | Autoriser l'utilisation de la commande '/ch chunks' - afficher vos chunks déverrouillés et la carte de territoire | `true` |
| `chunkblock.island.setcount` | Autoriser l'utilisation de la commande '/ch setCount' - définir le compteur de blocs à une valeur déjà complétée | OP |
| `chunkblock.mod.bypasschunks` | Exempte le titulaire du verrouillage des chunks entièrement ; autorise également '/chadmin bypass' pour la basculer. Non donné à ops par défaut - il doit être accordé explicitement pour que le personnel joue selon les mêmes règles jusqu'à ce qu'il s'y inscrive. | `false` |
| `chunkblock.phases` | Autoriser l'utilisation de la commande '/ch phases' - afficher une liste de toutes les phases | `false` |
| `chunkblock.respawn-block` | Autoriser l'utilisation de la commande '/ch respawnBlock' - réapparaître le bloc magique dans les situations où il disparaît | `true` |

## Liste complète

| Permission | Description | Par défaut |
|------------|-------------|---------|
| `chunkblock.admin` | Autoriser l'utilisation de la commande '/chadmin' - commande administrateur | OP |
| `chunkblock.admin.blueprint` | Autoriser l'utilisation de la commande '/chadmin blueprint' - manipuler les blueprints | OP |
| `chunkblock.admin.blueprint.copy` | Autoriser l'utilisation de la commande '/chadmin blueprint copy' - copier l'ensemble du presse-papiers défini par pos1 et pos2 et éventuellement les blocs d'air | OP |
| `chunkblock.admin.blueprint.delete` | Autoriser l'utilisation de la commande '/chadmin blueprint delete' - supprimer le blueprint | OP |
| `chunkblock.admin.blueprint.list` | Autoriser l'utilisation de la commande '/chadmin blueprint list' - lister les blueprints disponibles | OP |
| `chunkblock.admin.blueprint.load` | Autoriser l'utilisation de la commande '/chadmin blueprint load' - charger le blueprint dans le presse-papiers | OP |
| `chunkblock.admin.blueprint.origin` | Autoriser l'utilisation de la commande '/chadmin blueprint origin' - définir l'origine du blueprint à votre position | OP |
| `chunkblock.admin.blueprint.paste` | Autoriser l'utilisation de la commande '/chadmin blueprint paste' - coller le presse-papiers à votre emplacement | OP |
| `chunkblock.admin.blueprint.pos1` | Autoriser l'utilisation de la commande '/chadmin blueprint pos1' - définir le 1er coin du presse-papiers cubique | OP |
| `chunkblock.admin.blueprint.pos2` | Autoriser l'utilisation de la commande '/chadmin blueprint pos2' - définir le 2e coin du presse-papiers cubique | OP |
| `chunkblock.admin.blueprint.rename` | Autoriser l'utilisation de la commande '/chadmin blueprint rename' - renommer un blueprint | OP |
| `chunkblock.admin.blueprint.save` | Autoriser l'utilisation de la commande '/chadmin blueprint save' - enregistrer le presse-papiers copié | OP |
| `chunkblock.admin.chunks` | Autoriser l'utilisation de la commande '/chadmin chunks' - inspecter, définir ou recalculer les chunks déverrouillés d'un joueur | OP |
| `chunkblock.admin.deaths` | Autoriser l'utilisation de la commande '/chadmin deaths' - modifier les morts des joueurs | OP |
| `chunkblock.admin.deaths.add` | Autoriser l'utilisation de la commande '/chadmin deaths add' - ajouter des morts au joueur | OP |
| `chunkblock.admin.deaths.remove` | Autoriser l'utilisation de la commande '/chadmin deaths remove' - supprimer des morts au joueur | OP |
| `chunkblock.admin.deaths.reset` | Autoriser l'utilisation de la commande '/chadmin deaths reset' - réinitialiser les morts du joueur | OP |
| `chunkblock.admin.deaths.set` | Autoriser l'utilisation de la commande '/chadmin deaths set' - définir les morts du joueur | OP |
| `chunkblock.admin.delete` | Autoriser l'utilisation de la commande '/chadmin delete' - supprimer l'île d'un joueur | OP |
| `chunkblock.admin.getrank` | Autoriser l'utilisation de la commande '/chadmin getrank' - obtenir le rang d'un joueur sur son île ou l'île du propriétaire | OP |
| `chunkblock.admin.noban` | Le joueur ne peut pas être banni d'une île | OP |
| `chunkblock.admin.noexpel` | Le joueur ne peut pas être expulsé d'une île | OP |
| `chunkblock.admin.phases` | Autoriser l'utilisation de la commande '/chadmin phases' - ouvrir l'éditeur d'ordre de phase | OP |
| `chunkblock.admin.purge` | Autoriser l'utilisation de la commande '/chadmin purge' - purger les îles abandonnées depuis plus de [jours] | OP |
| `chunkblock.admin.purge.protect` | Autoriser l'utilisation de la commande '/chadmin purge protect' - basculer la protection de purge de l'île | OP |
| `chunkblock.admin.purge.status` | Autoriser l'utilisation de la commande '/chadmin purge status' - afficher l'état de la purge | OP |
| `chunkblock.admin.purge.stop` | Autoriser l'utilisation de la commande '/chadmin purge stop' - arrêter une purge en cours | OP |
| `chunkblock.admin.purge.unowned` | Autoriser l'utilisation de la commande '/chadmin purge unowned' - purger les îles non possédées | OP |
| `chunkblock.admin.range` | Autoriser l'utilisation de la commande '/chadmin range' - commande de plage d'île administrateur | OP |
| `chunkblock.admin.range.add` | Autoriser l'utilisation de la commande '/chadmin range add' - augmenter la plage protégée de l'île | OP |
| `chunkblock.admin.range.display` | Autoriser l'utilisation de la commande '/chadmin range display' - afficher/masquer les indicateurs de plage d'île | OP |
| `chunkblock.admin.range.remove` | Autoriser l'utilisation de la commande '/chadmin range remove' - diminuer la plage protégée de l'île | OP |
| `chunkblock.admin.range.reset` | Autoriser l'utilisation de la commande '/chadmin range reset' - réinitialiser la plage protégée de l'île à la valeur par défaut du monde | OP |
| `chunkblock.admin.range.set` | Autoriser l'utilisation de la commande '/chadmin range set' - définir la plage protégée de l'île | OP |
| `chunkblock.admin.register` | Autoriser l'utilisation de la commande '/chadmin register' - enregistrer le joueur sur l'île non possédée sur laquelle vous êtes | OP |
| `chunkblock.admin.reload` | Autoriser l'utilisation de la commande '/chadmin reload' - recharger | OP |
| `chunkblock.admin.resetflags` | Autoriser l'utilisation de la commande '/chadmin resetflags' - Réinitialiser tous les paramètres d'île à la valeur par défaut dans config.yml | OP |
| `chunkblock.admin.resets` | Autoriser l'utilisation de la commande '/chadmin resets' - modifier les valeurs de réinitialisation des joueurs | OP |
| `chunkblock.admin.resets.add` | Autoriser l'utilisation de la commande '/chadmin resets add' - ajoute le nombre de réinitialisations de l'île du joueur | OP |
| `chunkblock.admin.resets.remove` | Autoriser l'utilisation de la commande '/chadmin resets remove' - réduit le nombre de réinitialisations de l'île du joueur | OP |
| `chunkblock.admin.resets.set` | Autoriser l'utilisation de la commande '/chadmin resets set' - définir le nombre de fois que le joueur a réinitialisé son île | OP |
| `chunkblock.admin.sanity` | Autoriser l'utilisation de la commande '/chadmin sanity' - afficher une vérification de santé des probabilités de phase dans la console | OP |
| `chunkblock.admin.setchest` | Autoriser l'utilisation de la commande '/chadmin setchest' - mettre le coffre regardé dans une phase avec la rareté spécifiée | OP |
| `chunkblock.admin.setcount` | Autoriser l'utilisation de la commande '/chadmin setcount' - définir le compteur de blocs du joueur | OP |
| `chunkblock.admin.setprotectionlocation` | Autoriser l'utilisation de la commande '/chadmin setprotectionlocation' - définir l'emplacement actuel ou [x y z] comme centre de la zone de protection de l'île | OP |
| `chunkblock.admin.setrank` | Autoriser l'utilisation de la commande '/chadmin setrank' - définir le rang d'un joueur sur son île ou l'île du propriétaire | OP |
| `chunkblock.admin.setspawn` | Autoriser l'utilisation de la commande '/chadmin setspawn' - définir une île comme spawn pour ce mode de jeu | OP |
| `chunkblock.admin.setspawnpoint` | Autoriser l'utilisation de la commande '/chadmin setspawnpoint' - définir l'emplacement actuel comme point de spawn pour cette île | OP |
| `chunkblock.admin.settings` | Autoriser l'utilisation de la commande '/chadmin settings' - ouvrir le GUI des paramètres ou définir les paramètres | OP |
| `chunkblock.admin.tp` | Autoriser l'utilisation de la commande '/chadmin tp/tpnether/tpend' - téléporter sur l'île d'un joueur | OP |
| `chunkblock.admin.unregister` | Autoriser l'utilisation de la commande '/chadmin unregister' - annuler l'enregistrement du propriétaire de l'île, mais garder les blocs d'île | OP |
| `chunkblock.admin.version` | Autoriser l'utilisation de la commande '/chadmin version' - afficher les versions BentoBox et des addons | OP |
| `chunkblock.admin.why` | Autoriser l'utilisation de la commande '/chadmin why' - basculer le rapport de débogage de protection console | OP |
| `chunkblock.count` | Autoriser l'utilisation de la commande '/ch count' - afficher le compteur de blocs et la phase | `true` |
| `chunkblock.island` | Autoriser l'utilisation de la commande '/ch' - la commande d'île principale | `true` |
| `chunkblock.island.actionbar` | Autoriser l'utilisation de la commande '/ch actionbar' - basculer la barre d'action | `true` |
| `chunkblock.island.ban` | Autoriser l'utilisation de la commande '/ch ban' ou '/ch unban' ou '/ch banlist' - joueurs bannis | `true` |
| `chunkblock.island.bossbar` | Autoriser l'utilisation de la commande '/ch bossbar' - basculer la barre de boss | `true` |
| `chunkblock.island.chunks` | Autoriser l'utilisation de la commande '/ch chunks' - afficher vos chunks déverrouillés et la carte de territoire | `true` |
| `chunkblock.island.create` | Autoriser l'utilisation de la commande '/ch create' - créer une île, en utilisant un blueprint optionnel (nécessite la permission) | `true` |
| `chunkblock.island.deletehome` | Autoriser l'utilisation de la commande '/ch deletehome' - supprimer un emplacement de maison | OP |
| `chunkblock.island.expel` | Autoriser l'utilisation de la commande '/ch expel' - expulser un joueur de votre île | `true` |
| `chunkblock.island.home` | Autoriser l'utilisation de la commande '/ch go' - vous téléporter à votre île | `true` |
| `chunkblock.island.homes` | Autoriser l'utilisation de la commande '/ch homes' - lister vos maisons | OP |
| `chunkblock.island.info` | Autoriser l'utilisation de la commande '/ch info' - afficher des informations sur votre île ou l'île du joueur | `true` |
| `chunkblock.island.language` | Autoriser l'utilisation de la commande '/ch language' - sélectionner la langue | `true` |
| `chunkblock.island.lock` | Permet le verrouillage de l'île dans les paramètres | `true` |
| `chunkblock.island.name` | Autoriser l'utilisation de la commande '/ch setname' ou '/ch resetname' - votre nom d'île | `true` |
| `chunkblock.island.near` | Autoriser l'utilisation de la commande '/ch near' - afficher le nom des îles voisines autour de vous | `true` |
| `chunkblock.island.renamehome` | Autoriser l'utilisation de la commande '/ch renamehome' - renommer un emplacement de maison | OP |
| `chunkblock.island.reset` | Autoriser l'utilisation de la commande '/ch reset' - redémarrer votre île et supprimer l'ancienne | `true` |
| `chunkblock.island.setcount` | Autoriser l'utilisation de la commande '/ch setCount' - définir le compteur de blocs à une valeur déjà complétée | OP |
| `chunkblock.island.sethome` | Autoriser l'utilisation de la commande '/ch sethome' - définir votre point de téléportation à la maison | `true` |
| `chunkblock.island.settings` | Autoriser l'utilisation de la commande '/ch settings' - afficher les paramètres d'île | `true` |
| `chunkblock.island.spawn` | Autoriser l'utilisation de la commande '/ch spawn' - vous téléporter au spawn | `true` |
| `chunkblock.island.team` | Autoriser l'utilisation de la commande '/ch team' - gérer votre équipe | `true` |
| `chunkblock.island.team.accept` | Autoriser l'utilisation de la commande '/ch team accept' - accepter une invitation | `true` |
| `chunkblock.island.team.coop` | Autoriser l'utilisation de la commande '/ch team coop, uncoop' | `true` |
| `chunkblock.island.team.invite` | Autoriser l'utilisation de la commande '/ch team invite' - inviter un joueur à rejoindre votre île | `true` |
| `chunkblock.island.team.kick` | Autoriser l'utilisation de la commande '/ch team kick' - supprimer un membre de votre île | `true` |
| `chunkblock.island.team.leave` | Autoriser l'utilisation de la commande '/ch team leave' - quitter votre île | `true` |
| `chunkblock.island.team.promote` | Autoriser l'utilisation de la commande '/ch team promote, demote' | `true` |
| `chunkblock.island.team.reject` | Autoriser l'utilisation de la commande '/ch team reject' - rejeter une invitation | `true` |
| `chunkblock.island.team.setowner` | Autoriser l'utilisation de la commande '/ch team setowner' - transférer la propriété de votre île à un membre | `true` |
| `chunkblock.island.team.trust` | Autoriser l'utilisation de la commande '/ch team trust, untrust' | `true` |
| `chunkblock.mod.bypassban` | Contourner le ban de l'île | OP |
| `chunkblock.mod.bypasschunks` | Exempte le titulaire du verrouillage des chunks entièrement ; autorise également '/chadmin bypass' pour la basculer. Non donné à ops par défaut - il doit être accordé explicitement pour que le personnel joue selon les mêmes règles jusqu'à ce qu'il s'y inscrive. | `false` |
| `chunkblock.mod.bypasscooldowns` | Autoriser le modérateur à contourner les cooldowns | OP |
| `chunkblock.mod.bypassdelays` | Autoriser le modérateur à contourner les retards | OP |
| `chunkblock.mod.bypassexpel` | Autoriser le modérateur à contourner l'expulsion de l'île | OP |
| `chunkblock.mod.bypasslock` | Contourner un verrouillage d'île | OP |
| `chunkblock.mod.bypassprotect` | Autoriser le modérateur à contourner la protection de l'île | OP |
| `chunkblock.mod.clearreset` | Autoriser l'effacement de la limite de réinitialisation de l'île | `false` |
| `chunkblock.mod.deletehomes` | Autoriser l'utilisation de la commande '/chadmin deletehomes' - supprimer tous les noms de maisons d'une île | OP |
| `chunkblock.mod.info` | Autoriser l'utilisation de la commande '/chadmin info' - obtenir des informations sur où vous êtes ou l'île du joueur | OP |
| `chunkblock.mod.lock` | Autoriser le verrouillage ou le déverrouillage d'une île | OP |
| `chunkblock.mod.resetname` | Autoriser l'utilisation de la commande '/chadmin resetname' - réinitialiser le nom d'île du joueur | OP |
| `chunkblock.mod.switch` | Autoriser l'utilisation de la commande '/chadmin switch' - basculer le contournement de protection | OP |
| `chunkblock.mod.team` | Autoriser l'utilisation de la commande '/chadmin team' - gérer les équipes | `false` |
| `chunkblock.mod.team.add` | Autoriser l'utilisation de la commande '/chadmin team add' ou '/chadmin add' - ajouter un joueur à l'équipe du propriétaire | OP |
| `chunkblock.mod.team.disband` | Autoriser l'utilisation de la commande '/chadmin team disband' ou '/chadmin disband' - dissoudre l'équipe du propriétaire | OP |
| `chunkblock.mod.team.fix` | Autoriser l'utilisation de la commande '/chadmin team fix' ou '/chadmin fix' - analyser et corriger l'appartenance à l'île croisée dans la base de données | OP |
| `chunkblock.mod.team.kick` | Autoriser l'utilisation de la commande '/chadmin team kick' ou '/chadmin kick' - expulser un joueur d'une équipe | OP |
| `chunkblock.mod.team.setowner` | Autoriser l'utilisation de la commande '/chadmin team setowner' - transférer la propriété de l'île au joueur | OP |
| `chunkblock.phases` | Autoriser l'utilisation de la commande '/ch phases' - afficher une liste de toutes les phases | `false` |
| `chunkblock.respawn-block` | Autoriser l'utilisation de la commande '/ch respawnBlock' - réapparaître le bloc magique dans les situations où il disparaît | `true` |
| `chunkblock.settings.*` | Autoriser l'utilisation des paramètres sur l'île | `true` |
