# Équipes

BentoBox gère les équipes pour les modes de jeu. Les équipes permettent aux joueurs de se grouper sur une île. Les équipes ont un propriétaire ou un leader et au moins un membre de l'équipe.

## Interface Graphique de l'Équipe

Quand les joueurs émettent la commande `team`, cela fait apparaître une interface graphique qui leur permet de voir leur équipe, d'inviter d'autres joueurs, de rechercher des joueurs et de gérer l'équipe. Les commandes peuvent également être utilisées, mais les joueurs aiment souvent l'interface graphique.

## Commandes d'équipe
Ceci est une liste des commandes d'équipe disponibles pour les joueurs. La commande est utilisée après la commande du joueur principal, par exemple `/island team` pour BSkyBlock.
<table width="100%" align="center">
<tr>
<td align='left'><b>Commande</b></td>
<td align='left'><b>Description</b></td>
<td align='left'><b>Permission</b></td>
</tr>
<tr>
<td align='left'><b> team</b></td>
<td align='left'>gérez votre équipe</td>
<td align='left'>[gamemode].island.team</td>
</tr>
<tr>
<td align='left'><b> team accept</b></td>
<td align='left'>acceptez une invitation</td>
<td align='left'>[gamemode].island.team</td>
</tr>
<tr>
<td align='left'><b> team coop <player></b></td>
<td align='left'>faire un joueur coop rang sur votre île</td>
<td align='left'>[gamemode].island.team.coop</td>
</tr>
<tr>
<td align='left'><b> team demote <player></b></td>
<td align='left'>rétrograder un joueur sur votre île d'un rang</td>
<td align='left'>[gamemode].island.team</td>
</tr>
<tr>
<td align='left'><b> team leave</b></td>
<td align='left'>quittez votre île</td>
<td align='left'>[gamemode].island.team</td>
</tr>
<tr>
<td align='left'><b> team invite</b></td>
<td align='left'>invitez un joueur à rejoindre votre île</td>
<td align='left'>[gamemode].island.team</td>
</tr>
<tr>
<td align='left'><b> team kick <player></b></td>
<td align='left'>supprimer un membre de votre île</td>
<td align='left'>[gamemode].island.expel</td>
</tr>
<tr>
<td align='left'><b> team promote <player></b></td>
<td align='left'>promouvoir un joueur sur votre île d'un rang</td>
<td align='left'>[gamemode].island.team</td>
</tr>
<tr>
<td align='left'><b> team reject</b></td>
<td align='left'>rejetez une invitation</td>
<td align='left'>[gamemode].island.team</td>
</tr>
<tr>
<td align='left'><b> team setowner <player></b></td>
<td align='left'>transférez la propriété de votre île à un membre</td>
<td align='left'>[gamemode].island.team</td>
</tr>
<tr>
<td align='left'><b> team trust <player></b></td>
<td align='left'>donnez à un joueur le rang de confiance sur votre île</td>
<td align='left'>[gamemode].island.team.trust</td>
</tr>
</table>

## La Commande Principale d'Équipe
La commande d'équipe principale est `team`. Pour émettre cette commande, vous devez avoir une île. S'il est exécuté seul, il fournira les informations suivantes au joueur :

 - Si le joueur est le propriétaire, il lui dira combien de joueurs il peut inviter sur son équipe.
 - Il affichera tous les membres de l'équipe. Cela inclut des informations sur le rang du joueur, le statut en ligne/hors ligne et la dernière fois qu'il a été vu en ligne.

## Tailles des Équipes
Les équipes peuvent être de n'importe quelle taille et la taille maximale peut être définie globalement sur une base par mode de jeu ou déterminée par une permission numérotée donnée au propriétaire de l'équipe. La taille d'équipe maximale par défaut est 4. Le nombre maximum de membres coop et de confiance est également défini à 4.

### Permissions de Taille d'Équipe

* Taille de l'équipe : La permission pour la taille de l'équipe est `[gamemode].team.maxsize.X` où X est un nombre.
* Taille Coop : `[gamemode].team.coopsize.X` où X est un nombre
* Taille de Confiance : `[gamemode].team.trustsize.X` où X est un nombre

## Rangs des Membres de l'Équipe
BentoBox a les rangs d'équipe suivants intégrés :

* Propriétaire - c'est le propriétaire de l'île. Il ne peut y avoir qu'un seul propriétaire.
* Sous-propriétaire - c'est un rang de membre qui a presque les mêmes permissions que le propriétaire. Il peut y avoir plusieurs sous-propriétaires.
* Membre - c'est le rang de membre par défaut.

### Rangs des Non-Membres de l'Équipe
Les îles ont d'autres rangs qui sont liés aux équipes mais ne sont pas des membres de l'équipe :

* Confiance - c'est un non-membre d'équipe qui a des permissions permanentes sur l'île, c'est-à-dire qu'il les a jusqu'à ce qu'il ne soit pas approuvé par un membre de l'équipe.
* Coop - c'est un non-membre d'équipe qui a des permissions temporaires sur l'île et ces permissions cesseront si le membre de l'équipe qui les a accordées se déconnecte, ou s'il n'est pas décoopoéré.
* Visiteur - c'est le rang par défaut pour tous les joueurs qui visitent l'île
* Banni - ces joueurs ont été bannis par un membre de l'équipe et ne peuvent pas entrer sur l'île

### Commandes de Rang Configurable
Le propriétaire de l'île est capable d'accorder l'accès aux commandes de gestion d'équipe à des rangs inférieurs via le menu Rangs de Commande dans le menu des paramètres en jeu. Cela permet au propriétaire de permettre à d'autres membres d'inviter d'autres membres, par exemple.

### Promotion et Rétrogradation
Les membres de l'équipe peuvent être promus ou rétrogradés par le propriétaire de l'île ou un membre de l'île qui a le rang requis pour utiliser ces commandes.

Un joueur ne peut pas se rétrograder ou se promouvoir lui-même.

Actuellement, la seule promotion ou rétrogradation possible est entre les rangs de Membre et Sous-propriétaire. À l'avenir, des rangs supplémentaires ou des rangs personnalisés peuvent être possibles.

## Rejoindre les Équipes
### Invitation
Les joueurs peuvent être invités à rejoindre une équipe en utilisant la commande `team invite`. Pour inviter des joueurs à rejoindre une équipe, l'inviteur doit être un propriétaire d'île ou avoir un rang suffisant pour utiliser la commande (voir [Commandes de Rang Configurable](#commandes-de-rang-configurable)). Les joueurs sont invités par nom et doivent être en ligne. Les invitations ne peuvent être faites qu'à des joueurs qui ne sont pas déjà dans une équipe. Si un joueur veut changer d'équipe, il doit d'abord quitter son équipe actuelle avant de pouvoir être invité.
Les joueurs invités ne peuvent pas être invités à nouveau jusqu'à ce qu'ils rejettent l'invitation.
Les joueurs invités ne peuvent avoir qu'**une** invitation active à la fois. Cela inclut les invitations d'équipe, coop et de confiance. Si un joueur reçoit une nouvelle invitation valide alors qu'une autre est en attente, l'ancienne est remplacée par la nouvelle invitation.
Si la taille de l'équipe de l'île est déjà au maximum, la commande d'invitation dira à l'utilisateur que l'île est complète.

#### Refroidissement
Les invitations peuvent être abusées par les joueurs, donc BentoBox empêche le même joueur d'être invité à une île pendant la période de refroidissement. Le refroidissement est appliqué à l'île dans son ensemble, donc il n'est pas possible pour les différents membres de l'île de spammer un autre joueur avec des invitations. Les temps de refroidissement par défaut pour les différentes invitations sont :

* Membre de l'équipe - 60 minutes
* Invitation Coop - 5 minutes
* Invitation de Confiance - 5 minutes
Voir le `config.yml` du mode de jeu pour modifier.

### Vérification des invitations
Un joueur peut vérifier qui l'a invité en utilisant la commande `invite` sans arguments. Cela affichera toute invitation d'équipe, coop ou de confiance actuelle.

### Accepter une invitation
Un joueur accepte une invitation en émettant la commande `team invite accept`.

#### Confirmation
L'administrateur peut décider si la confirmation est requise ou non pour cette commande. Le défaut est de le nécessiter pour l'adhésion à une équipe mais pas pour le statut de coop ou de confiance. C'est parce que les membres de l'équipe perdent leur île s'ils en rejoignent une autre. Si la confirmation est requise, le joueur recevra un avertissement que s'il a une île, il la perdra. Une fois que le joueur accepte à nouveau l'invitation, il devient un membre de l'équipe et se téléporte à l'île d'équipe.

Il y a une petite chance que l'inviteur perde le rang requis pour inviter les joueurs avant que le joueur n'accepte l'invitation. Dans ce cas, l'acceptation ne sera pas traitée et l'utilisateur sera informé que l'invitation n'est plus valide.

!!! tip "Temps de Confirmation"
    Le temps par défaut que les joueurs ont pour confirmer une commande est 10 secondes. Si vos joueurs ont besoin de plus de temps, augmentez cette valeur dans le `config.yml` BentoBox. Les joueurs peuvent également appuyer sur la flèche vers le haut pour rappeler la commande précédente plutôt que de la retaper.

#### Ce qui se passe quand un joueur accepte

Quand un joueur accepte une invitation d'équipe, BentoBox le fait automatiquement :

- Les retire en tant que propriétaire de leur île précédente (s'ils en avaient une) et commence à la supprimer
- Efface le joueur en fonction des paramètres de configuration du mode de jeu (ender chest, inventaire, argent, santé, faim, expérience)
- Les ajoute en tant que membre de la nouvelle île et les téléporte à son point d'accueil

!!! warning "Nettoyage de l'Inventaire"
    Par défaut, BentoBox **ne** efface pas l'inventaire d'un joueur quand il rejoint une équipe, pour éviter les accidents lors de la configuration initiale. Cependant, **les administrateurs doivent activer cela dans le `config.yml` du mode de jeu** pour empêcher les joueurs de porter des objets de leur ancienne île vers la nouvelle. Vérifiez la configuration pour les paramètres de nettoyage `on-join`.

### Rejeter une invitation
Un joueur rejette une invitation en émettant la commande `team invite reject`.

Un joueur doit avoir une invitation valide pour la rejeter sinon il reçoit juste une erreur. Une fois rejetée, l'inviteur est notifié.

## Modification de la Propriété de l'Équipe

Les propriétaires peuvent faire d'un autre membre de l'équipe un propriétaire en utilisant la commande `team setowner` avec le nom du nouveau propriétaire comme paramètre. Une fois la propriété transférée, le propriétaire précédent devient un Sous-propriétaire.

Les propriétaires doivent sélectionner un nouveau propriétaire avant de pouvoir quitter une équipe.

## Expulsion d'un Joueur
Parfois, un membre de l'équipe doit être forcé de quitter une équipe. Ceci est fait en utilisant la commande `team kick`. Le propriétaire peut toujours expulser les joueurs et le propriétaire peut permettre aux membres de rang inférieur d'expulser également via le menu Rangs de Commande dans les paramètres de l'île. Le membre de l'équipe n'a pas besoin d'être en ligne pour être expulsé.

La commande exige par défaut une confirmation. Cela peut être configuré dans le `config.yml` BentoBox.

Quand un joueur est expulsé, BentoBox le retire de l'île, exécute toutes les commandes configurées on-leave, nettoie son inventaire/ender chest/argent en fonction de la configuration du mode de jeu, et notifie les deux parties. Un refroidissement d'invitation est appliqué pour éviter l'exploitation de l'expulsion répétée et de la réinvitation de joueurs.

## Quitter une Équipe
Un joueur peut volontairement quitter une équipe en utilisant la commande `team leave`. La commande exige une confirmation par défaut, mais cela peut être désactivé dans le config BentoBox. Quand un joueur quitte volontairement une équipe, il peut utiliser une de ses réinitialisations d'île autorisées. Ceci est défini dans la configuration du GameMode et le défaut est de ne pas perdre une réinitialisation. Si le joueur perdra une réinitialisation, il sera avertit à ce sujet si la commande leave a des exigences de confirmation. **Remarque :** il est possible qu'un joueur utilise toutes ses réinitialisations en quittant une équipe et donc ne soit pas capable de faire sa propre île. C'est quelque chose que les administrateurs devront considérer.

Quand un joueur quitte l'île, la séquence et le processus sont les mêmes que quand un joueur est expulsé, sauf que le joueur peut perdre une réinitialisation.


## Faire Confiance et Coooping à D'autres Joueurs
Parfois, les joueurs veulent aider sur d'autres îles sans avoir à rejoindre l'équipe en tant que membre à part entière. Cela peut être fait en faisant confiance à un joueur ou en coopant un joueur en ligne :

 - `team trust <player>` : le joueur devient un membre permanent de l'île à un rang inférieur à Membre
 - `team coop <player>` : le joueur devient un membre temporaire de l'île à un rang inférieur à Confiance

Les propriétaires d'îles peuvent faire confiance ou coop à des joueurs et permettent également aux joueurs de rang inférieur d'utiliser ces commandes via la page Rangs de Commande dans les paramètres de l'île.

Ces commandes envoient en fait une invitation au joueur qu'il peut accepter ou rejeter, tout comme la commande de jointure d'équipe. Si l'invitation est rejetée, il ne sera pas possible d'envoyer une autre invitation pendant une période de refroidissement, qui est définie à 5 minutes par défaut. Cela protège les joueurs du spam d'invitations.

Si un joueur a déjà une invitation en attente de quelqu'un d'autre ou pour un rang différent, cette invitation sera remplacée par celle-ci.

Une fois accepté, le joueur recevra le rang donné pour la nouvelle île. L'inviteur est notifié de l'acceptation.

Les joueurs Coop conservent leur rang jusqu'à ce que le joueur qui les a invités se déconnecte, ou jusqu'à l'arrêt du serveur, selon ce qui se produit en premier.

### Suppression de Confiance ou Décoooping des Joueurs
Les propriétaires d'îles, ou les joueurs avec un rang suffisamment élevé, peuvent émettre les commandes `team untrust` ou `team uncoop` pour supprimer les joueurs de l'île avec ces rangs. Le joueur supprimé revient au statut Visiteur.

## Désactivation des Équipes par Monde

Depuis BentoBox 3.16.0, un mode de jeu peut se retirer du sous-système d'équipes monde par monde via l'API `WorldSettings#isTeamsDisabled()` (par défaut `false`). Lorsque cela est activé, les commandes d'action qui ajoutent, suppriment ou réorganisent les membres de l'équipe refusent de s'exécuter en affichant le message de la locale `commands.island.team.errors.teams-disabled`.

**Bloquées lorsque les équipes sont désactivées :**

- `/island team invite` et `team invite accept` (uniquement les invitations d'ÉQUIPE — les invitations COOP et TRUST restent acceptées)
- `/island team kick`, `team leave`, `team promote`, `team demote`, `team setowner`
- `/[admin] team add`

**Toujours disponibles :**

- Commandes joueur en lecture seule : le panneau `/island team`, `team info`, `team invites`, `team invite reject`
- Relations de confiance et coop : `trust`, `coop`, `untrust`, `uncoop` — ce sont les alternatives prises en charge quand les équipes sont désactivées
- Commandes admin qui opèrent sur des équipes existantes : `kick`, `disband`, `disbandall`, `setowner`, `fix`, `maxsize`

Après avoir activé `isTeamsDisabled` pour un monde qui contient déjà des équipes, exécutez `/[admin] team disbandall` une fois pour nettoyer les équipes préexistantes. Cette commande admin retire tous les membres et sous-propriétaires de chaque île du monde courant en une seule passe avec confirmation. Les joueurs trust et coop sont intentionnellement laissés intacts.

??? note "Nouveautés de la v3.16.0"
    **Publié :** 2026-05-10

    Voir les notes complètes : [Release 3.16.0](https://github.com/BentoBoxWorld/BentoBox/releases/tag/3.16.0)

    **Gestion des équipes**

    - Nouvelle API `WorldSettings#isTeamsDisabled()` (par défaut `false`) permettant à un mode de jeu de se retirer du sous-système d'équipes monde par monde.
    - Nouvelle commande admin `/[admin] team disbandall` qui retire tous les membres et sous-propriétaires de chaque île du monde courant en une seule passe avec confirmation.
    - `/[admin] team kick` exige désormais des coordonnées `x,y,z` explicites quand la cible est sur plusieurs îles d'équipe, et refuse de kicker les propriétaires d'île (en redirigeant l'admin vers `setowner` ou `disband`).
    - Le plafond de setowner est désormais appliqué sur `/island team setowner` ET `/[admin] team setowner` — les transferts sont refusés si le destinataire est à son plafond d'îles concurrentes.

    **Corrections de bugs**

    - `ISLAND_RESPAWN` ne dépose plus les joueurs au point d'apparition du monde (0,0) quand leur bloc de maison manque — il suit désormais une chaîne de repli se terminant par `SafeSpotTeleport`.
    - `OFFLINE_GROWTH` bloque désormais toutes les plantes qui se propagent (lianes, lianes pleureuses/tordues, etc.) et les arbres/champignons poussant depuis des pousses — pas seulement le varech et le bambou.
    - Les marqueurs de zone/polygone Dynmap utilisent désormais la hauteur min/max complète du monde au lieu de toujours afficher à y=64.

    **Ajouts d'API**

    - `CraftEngineHook.getItemStack(String id)` et `CraftEngineHook.getItemId(ItemStack item)` permettent aux addons d'afficher et de reconnaître les objets personnalisés CraftEngine sans dépendre directement de CraftEngine.

    **Locale**

    - Nouvelles clés : `commands.admin.team.disbandall.{description,confirmation,success}`, `commands.island.team.errors.teams-disabled`, `commands.admin.team.setowner.errors.at-max`.
    - Mise à jour du message `commands.admin.team.kick.cannot-kick-owner` qui redirige les admins vers `setowner`/`disband`.
    - Suppression de la clé morte `commands.admin.team.kick.success-all`.
    - Les 22 traductions intégrées sont toutes synchronisées.

    **Compatibilité :** Paper Minecraft 1.21.5 – 26.1.2, Java 21+.
