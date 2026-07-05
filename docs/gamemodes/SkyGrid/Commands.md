# Commandes SkyGrid

<h1><b>Commandes admin SkyGrid </b>(Alias: /sga)</h1>
<table width="100%" align="center">
<tr>
<td align='left'><b>Commande</b></td>
<td align='left'><b>Description</b></td>
<td align='left'><b>Permission</b></td>
</tr>
<tr>
<td align='left'><b>/sgadmin</b></td>
<td align='left'>affiche toutes les commandes SkyGrid admin</td>
<td align='left'>skygrid.admin</td>
</tr>
<tr>
<td align='left'><b>/sgadmin deaths</b></td>
<td align='left'>modifier les décès des joueurs</td>
<td align='left'>skygrid.admin.deaths</td>
</tr>
<tr>
<td align='left'><b>/sgadmin delete</b></td>
<td align='left'>supprime un joueur et régénère son aire</td>
<td align='left'>skygrid.admin.delete</td>
</tr>
<tr>
<td align='left'><b>/sgadmin getrank <player></b></td>
<td align='left'>obtenir le rang d'un joueur sur son aire</td>
<td align='left'>skygrid.admin.getrank</td>
</tr>
<tr>
<td align='left'><b>/sgadmin info <player></b></td>
<td align='left'>obtenir des informations sur votre emplacement ou l'aire du joueur</td>
<td align='left'>skygrid.mod.info</td>
</tr>
<tr>
<td align='left'><b>/sgadmin kick <player></b></td>
<td align='left'>expulser un joueur d'une équipe</td>
<td align='left'>skygrid.mod.team</td>
</tr>
<tr>
<td align='left'><b>/sgadmin range</b></td>
<td align='left'>Commande de portée d'aire admin</td>
<td align='left'>skygrid.admin.setrange</td>
</tr>
<tr>
<td align='left'><b>/sgadmin register <player></b></td>
<td align='left'>enregistrer un joueur sur une aire non possédée sur laquelle vous vous trouvez</td>
<td align='left'>skygrid.admin.register</td>
</tr>
<tr>
<td align='left'><b>/sgadmin reload</b></td>
<td align='left'>recharger le plugin</td>
<td align='left'>skygrid.admin.reload</td>
</tr>
<tr>
<td align='left'><b>/sgadmin resetflags</b></td>
<td align='left'>réinitialiser toutes les aires aux paramètres de drapeau par défaut dans config.yml</td>
<td align='left'>skygrid.admin.settingsreset</td>
</tr>
<tr>
<td align='left'><b>/sgadmin bp</b></td>
<td align='left'>manipuler les blueprints</td>
<td align='left'>skygrid.admin.blueprint</td>
</tr>
<tr>
<td align='left'><b>/sgadmin bp copy [air]</b></td>
<td align='left'>copier le presse-papiers défini par pos1 et pos2 et éventuellement les blocs air</td>
<td align='left'>skygrid.admin.blueprint</td>
</tr>
<tr>
<td align='left'><b>/sgadmin bp load <bp name></b></td>
<td align='left'>charger le blueprint dans le presse-papiers</td>
<td align='left'>skygrid.admin.blueprint</td>
</tr>
<tr>
<td align='left'><b>/sgadmin bp origin</b></td>
<td align='left'>définir l'origine du blueprint à votre position</td>
<td align='left'>skygrid.admin.blueprint</td>
</tr>
<tr>
<td align='left'><b>/sgadmin bp paste</b></td>
<td align='left'>coller le presse-papiers à votre emplacement</td>
<td align='left'>skygrid.admin.blueprint</td>
</tr>
<tr>
<td align='left'><b>/sgadmin bp pos1</b></td>
<td align='left'>définir le 1er angle du presse-papiers cubique</td>
<td align='left'>skygrid.admin.blueprint</td>
</tr>
<tr>
<td align='left'><b>/sgadmin bp pos2</b></td>
<td align='left'>définir le 2ème angle du presse-papiers cubique</td>
<td align='left'>skygrid.admin.blueprint</td>
</tr>
<tr>
<td align='left'><b>/sgadmin bp save <bp name></b></td>
<td align='left'>enregistrer le presse-papiers copié</td>
<td align='left'>skygrid.admin.blueprint</td>
</tr>
<tr>
<td align='left'><b>/sgadmin setowner <player> [area owner]</b></td>
<td align='left'>transférer la propriété de l'aire au joueur ; nommez le propriétaire actuel pour l'exécuter depuis la console</td>
<td align='left'>skygrid.mod.team</td>
</tr>
<tr>
<td align='left'><b>/sgadmin setrank <player> <rank></b></td>
<td align='left'>définir le rang d'un joueur sur son aire</td>
<td align='left'>skygrid.admin.setrank</td>
</tr>
<tr>
<td align='left'><b>/sgadmin setspawn</b></td>
<td align='left'>définir une aire comme spawn pour ce mode de jeu</td>
<td align='left'>skygrid.admin.setspawn</td>
</tr>
<tr>
<td align='left'><b>/sgadmin tp <player></b></td>
<td align='left'>se téléporter sur l'aire d'un joueur</td>
<td align='left'>skygrid.mod.tp</td>
</tr>
<tr>
<td align='left'><b>/sgadmin tpend <player></b></td>
<td align='left'>se téléporter sur l'aire de fin d'un joueur</td>
<td align='left'>skygrid.mod.tp</td>
</tr>
<tr>
<td align='left'><b>/sgadmin tpnether <player></b></td>
<td align='left'>se téléporter sur l'aire nether d'un joueur</td>
<td align='left'>skygrid.mod.tp</td>
</tr>
<tr>
<td align='left'><b>/sgadmin unregister <owner></b></td>
<td align='left'>désenregistrer le propriétaire de l'aire, mais garder les blocs de l'aire</td>
<td align='left'>skygrid.admin.unregister</td>
</tr>
<tr>
<td align='left'><b>/sgadmin version</b></td>
<td align='left'>afficher les versions de BentoBox et des addons</td>
<td align='left'>skygrid.admin.version</td>
</tr>
<tr>
<td align='left'><b>/sgadmin why <player></b></td>
<td align='left'>basculer le rapport de débogage de protection console</td>
<td align='left'>skygrid.admin.why</td>
</tr>
</table>

<h1><b>Commandes joueur SkyGrid </b>(Alias: /sg)</h1>
<table width="100%" align="center">
<tr>
<td align='left'><b>Commande</b></td>
<td align='left'><b>Description</b></td>
<td align='left'><b>Permission</b></td>
</tr>
<tr>
<td align='left'><b>/skygrid</b></td>
<td align='left'>La commande d'aire principale</td>
<td align='left'>skygrid.island</td>
</tr>
<tr>
<td align='left'><b>/skygrid ban <player></b></td>
<td align='left'>bannir un joueur de votre aire</td>
<td align='left'>skygrid.island.ban</td>
</tr>
<tr>
<td align='left'><b>/skygrid banlist</b></td>
<td align='left'>lister les joueurs bannis</td>
<td align='left'>skygrid.island.ban</td>
</tr>
<tr>
<td align='left'><b>/skygrid create</b></td>
<td align='left'>créer une nouvelle aire</td>
<td align='left'>skygrid.island.create</td>
</tr>
<tr>
<td align='left'><b>/skygrid expel <player></b></td>
<td align='left'>expulser un joueur de votre aire</td>
<td align='left'>skygrid.island.expel</td>
</tr>
<tr>
<td align='left'><b>/skygrid go</b></td>
<td align='left'>se téléporter à l'accueil de votre aire</td>
<td align='left'>skygrid.island.home</td>
</tr>
<tr>
<td align='left'><b>/skygrid info <player></b></td>
<td align='left'>afficher les informations sur votre aire ou l'aire d'un joueur</td>
<td align='left'>skygrid.island.info</td>
</tr>
<tr>
<td align='left'><b>/skygrid language</b></td>
<td align='left'>sélectionner la langue</td>
<td align='left'>skygrid.island.language</td>
</tr>
<tr>
<td align='left'><b>/skygrid reset</b></td>
<td align='left'>redémarrer votre aire et supprimer l'ancienne</td>
<td align='left'>skygrid.island.reset</td>
</tr>
<tr>
<td align='left'><b>/skygrid sethome</b></td>
<td align='left'>définir votre point de téléportation d'accueil</td>
<td align='left'>skygrid.island.sethome</td>
</tr>
<tr>
<td align='left'><b>/skygrid setname <name></b></td>
<td align='left'>définir un nom pour votre aire</td>
<td align='left'>skygrid.island.name</td>
</tr>
<tr>
<td align='left'><b>/skygrid settings</b></td>
<td align='left'>afficher les paramètres de l'aire</td>
<td align='left'>skygrid.island.settings</td>
</tr>
<tr>
<td align='left'><b>/skygrid spawn</b></td>
<td align='left'>se téléporter au spawn</td>
<td align='left'>skygrid.island.spawn</td>
</tr>
<tr>
<td align='left'><b>/skygrid resetname</b></td>
<td align='left'>réinitialiser le nom de votre aire</td>
<td align='left'>skygrid.mod.resetname</td>
</tr>
<tr>
<td align='left'><b>/skygrid unban <player></b></td>
<td align='left'>débannir un joueur de votre aire</td>
<td align='left'>skygrid.island.ban</td>
</tr>
<tr>
<td align='left'><b>/skygrid team</b></td>
<td align='left'>gérer votre équipe</td>
<td align='left'>skygrid.island.team</td>
</tr>
<tr>
<td align='left'><b>/skygrid team accept</b></td>
<td align='left'>accepter une invitation</td>
<td align='left'>skygrid.island.team</td>
</tr>
<tr>
<td align='left'><b>/skygrid team coop <player></b></td>
<td align='left'>rendre un joueur coop sur votre aire</td>
<td align='left'>skygrid.island.team.coop</td>
</tr>
<tr>
<td align='left'><b>/skygrid team demote <player></b></td>
<td align='left'>rétrograder un joueur d'un rang sur votre aire</td>
<td align='left'>skygrid.island.team</td>
</tr>
<tr>
<td align='left'><b>/skygrid team invite <player></b></td>
<td align='left'>inviter un joueur à rejoindre votre aire</td>
<td align='left'>skygrid.island.team</td>
</tr>
<tr>
<td align='left'><b>/skygrid team kick <player></b></td>
<td align='left'>expulser un membre de votre aire</td>
<td align='left'>skygrid.island.team</td>
</tr>
<tr>
<td align='left'><b>/skygrid team leave</b></td>
<td align='left'>quitter votre aire</td>
<td align='left'>skygrid.island.team</td>
</tr>
<tr>
<td align='left'><b>/skygrid team promote <player></b></td>
<td align='left'>promouvoir un joueur d'un rang sur votre aire</td>
<td align='left'>skygrid.island.team</td>
</tr>
<tr>
<td align='left'><b>/skygrid team reject</b></td>
<td align='left'>rejeter une invitation</td>
<td align='left'>skygrid.island.team</td>
</tr>
<tr>
<td align='left'><b>/skygrid team setowner <player></b></td>
<td align='left'>transférer la propriété de votre aire à un membre</td>
<td align='left'>skygrid.island.team</td>
</tr>
<tr>
<td align='left'><b>/skygrid team trust <player></b></td>
<td align='left'>donner un rang approuvé à un joueur sur votre aire</td>
<td align='left'>skygrid.island.team.trust</td>
</tr>
<tr>
<td align='left'><b>/skygrid team uncoop <player></b></td>
<td align='left'>retirer un rang coop à un joueur</td>
<td align='left'>skygrid.island.team.coop</td>
</tr>
<tr>
<td align='left'><b>/skygrid team untrust <player></b></td>
<td align='left'>retirer le rang approuvé du joueur</td>
<td align='left'>skygrid.island.team.trust</td>
</tr>
</table>
