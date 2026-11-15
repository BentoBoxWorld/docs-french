# Équipes et Rangs

Les équipes permettent à plusieurs joueurs de partager une île. Chaque île a un **propriétaire**, et le propriétaire peut inviter d'autres joueurs à rejoindre en tant que **membres**. Les joueurs qui ont seulement besoin d'aider pendant un moment peuvent être de **confiance** ou en **coopération** au lieu de rejoindre.

Cette page explique comment fonctionnent les équipes, ce que vous pouvez configurer en tant qu'administrateur et comment gérer les demandes courantes que vous recevrez des joueurs.

!!! info "Commandes sur cette page"
    Les commandes sont affichées pour BSkyBlock (`/island`, `/bsbadmin`). Les autres modes de jeu utilisent leurs propres noms de commandes, par exemple `/ob` dans AOneBlock ou `/acid` dans AcidIsland. Les autorisations commencent par le préfixe du mode de jeu, par exemple `bskyblock.` ou `aoneblock.`.

## Comment fonctionnent les équipes

- Un joueur crée une équipe en invitant quelqu'un avec `/island team invite <player>`. Le joueur invité accepte, abandonne sa propre île (par défaut) et est téléporté à l'île d'équipe.
- Tous les joueurs de l'île ont un **rang**. Le rang détermine ce qu'ils peuvent faire : casser des blocs, ouvrir des coffres, inviter des joueurs, expulser des joueurs, etc.
- Le propriétaire décide ce que chaque rang peut faire dans le menu des paramètres de l'île (`/island settings`). Voir [Protection, Drapeaux et Rangs](../Island-Protection,-Flags-&-Ranks.md).
- Il n'y a qu'un propriétaire. Le propriétaire peut donner l'île à un autre membre, mais doit le faire avant de partir.

### Les rangs

| Rang | Valeur | Qui l'a | Compte vers la taille de l'équipe ? |
|---|---|---|---|
| Propriétaire | 1000 | Le joueur qui possède l'île | Oui |
| Sous-propriétaire | 900 | Membres promus par le propriétaire | Oui |
| Membre | 500 | Joueurs qui ont accepté une invitation d'équipe | Oui |
| Confiance | 400 | Joueurs de confiance avec `/island team trust` | Non (limite séparée) |
| Coopération | 200 | Joueurs en coopération avec `/island team coop` | Non (limite séparée) |
| Visiteur | 0 | Tous les autres joueurs de l'île | Non |
| Banni | -1 | Joueurs bannis avec `/island ban` | Non |

Les rangs supérieurs peuvent faire tout ce que les rangs inférieurs peuvent faire. Vous pouvez ajouter vos propres rangs entre ceux-ci avec `/bentobox rank add` (voir [Rangs personnalisés](#custom-ranks)).

### Confiance et Coopération : aider sans rejoindre

Les joueurs de confiance et en coopération peuvent travailler sur une île sans devenir des membres d'équipe. Ils gardent leur propre île.

- **Les joueurs de confiance** gardent leur rang jusqu'à ce que quelqu'un le retire avec `/island team untrust <player>`.
- **Les joueurs en coopération** gardent leur rang uniquement tant que l'île a un membre d'équipe en ligne. Quand le dernier membre d'équipe se déconnecte, chaque joueur en coopération de cette île perd le rang. Un joueur en coopération qui se déconnecte perd également ses rangs de coopération.

La confiance et la coopération fonctionnent de la même manière que les invitations d'équipe : l'autre joueur reçoit une invitation et doit l'accepter.

## Ce que les joueurs peuvent faire

Les joueurs ouvrent le menu d'équipe avec `/island team`. À partir du menu, ils peuvent voir leur équipe, inviter des joueurs et changer les rangs sans taper de commandes. Toutes les mêmes actions sont également disponibles sous forme de commandes :

| Commande | Ce qu'elle fait |
|---|---|
| `/island team` | Ouvre le menu d'équipe |
| `/island team invite <player>` | Invite un joueur en ligne à rejoindre l'équipe |
| `/island team accept` | Accepte une invitation en attente (équipe, confiance ou coopération) |
| `/island team reject` | Rejette une invitation en attente |
| `/island team leave` | Quitte l'équipe. Le propriétaire ne peut pas partir ; il doit d'abord donner l'île |
| `/island team kick <player>` | Supprime un membre de l'équipe. Fonctionne quand le joueur est hors ligne |
| `/island team promote <player>` | Promeut un membre d'un rang (jamais à Propriétaire) |
| `/island team demote <player>` | Rétrograde un membre d'un rang (jamais en dessous de Membre) |
| `/island team setowner <player>` | Donne l'île à un autre membre. L'ancien propriétaire devient Sous-propriétaire |
| `/island team trust <player>` | Donne à un joueur le rang de Confiance |
| `/island team untrust <player>` | Retire le rang de Confiance |
| `/island team coop <player>` | Donne à un joueur en ligne le rang de Coopération |
| `/island team uncoop <player>` | Retire le rang de Coopération |

Un joueur ne peut avoir qu'**une** invitation en attente à la fois. Une nouvelle invitation remplace l'ancienne.

Sur Minecraft 26 et versions ultérieures, un joueur qui reçoit une invitation d'équipe voit un dialogue **Accepter / Refuser**, il n'a donc pas besoin de taper la commande. Les commandes sensibles comme `kick` et `leave` demandent également une confirmation dans un dialogue. Les deux peuvent être désactivés dans le `config.yml` de BentoBox (`island.dialogs.team-invites` et `island.dialogs.confirmations`).

### Laisser les membres gérer l'équipe { #letting-members-manage-the-team }

Par défaut, seul le propriétaire peut inviter, expulser, promouvoir, rétrograder, faire confiance et mettre en coopération. Le propriétaire peut permettre aux rangs inférieurs d'utiliser ces commandes à partir de la page **Rangs de Commande** du menu des paramètres. Par exemple, un propriétaire peut permettre aux Sous-propriétaires d'inviter et d'expulser.

La même page contrôle également les commandes de l'île telles que `ban`, `unban`, `expel`, `lock`, `setname` et `sethome`. Les commandes d'accueil (`sethome`, `renamehome`, `deletehome`) défaut à Membre ; les autres défaut à Propriétaire.

Les joueurs ne peuvent jamais expulser, promouvoir ou rétrograder quelqu'un du même rang ou plus élevé qu'eux-mêmes.

## Configuration des équipes (admins)

### Taille de l'équipe

La taille de l'équipe est définie dans le `config.yml` du mode de jeu. **La limite inclut le propriétaire**, donc `max-team-size: 4` signifie le propriétaire plus trois membres.

```yaml
island:
  # Propriétaire + membres
  max-team-size: 4
  # Limites séparées pour les joueurs en coopération et de confiance
  max-coop-size: 4
  max-trusted-size: 4
```

### Équipes plus grandes pour les VIP ou les rangs

Donnez au **propriétaire de l'île** une permission avec la taille à la fin :

| Permission | Effet |
|---|---|
| `bskyblock.team.maxsize.<number>` | Taille de l'équipe pour les îles que ce joueur possède |
| `bskyblock.coop.maxsize.<number>` | Limite de coopération |
| `bskyblock.trust.maxsize.<number>` | Limite de confiance |

Par exemple, avec LuckPerms :

```
/lp group vip permission set bskyblock.team.maxsize.8 true
```

L'autorisation est vérifiée quand le propriétaire est en ligne, et l'île se souvient du résultat. Seule l'autorisation du propriétaire compte ; les autorisations des membres sont ignorées.

Pour changer la limite d'une île sans autorisations, utilisez `/bsbadmin team maxsize <player> <size>`.

### Ce qui se passe avec les objets et l'argent quand les joueurs rejoignent ou partent { #what-happens-to-items-and-money-when-players-join-or-leave }

Quand un joueur accepte une invitation d'équipe, il **perd généralement sa propre île**. Avant d'accepter, il est averti et on lui demande de confirmer.

BentoBox peut également effacer l'inventaire du joueur, le coffre de l'Ender, l'argent, la santé, la faim et l'XP quand il rejoint ou quitte une équipe. Cela empêche les joueurs de transporter des objets d'une île à l'autre. Définissez-le dans le `config.yml` du mode de jeu :

```yaml
island:
  reset:
    # Partir ou être expulsé utilise l'une des réinitialisations de l'île du joueur
    leavers-lose-reset: false
    # Les joueurs expulsés gardent leur inventaire même si on-leave inventory est true
    kicked-keep-inventory: false
    on-join:      # quand un joueur rejoint une équipe ou crée une île
      inventory: false
      ender-chest: false
      money: false
      exp: false
      health: true
      hunger: true
    on-leave:     # quand un joueur quitte ou est expulsé
      inventory: false
      ender-chest: false
      money: false
      # ... mêmes options que on-join
```

!!! warning "Recommandé pour la plupart des serveurs"
    Les valeurs par défaut conservent les inventaires afin que vous ne perdiez pas d'objets lors des tests. Sur un serveur en direct, envisagez de définir les `inventory` et `ender-chest` de `on-join` et `on-leave` à `true`, et `leavers-lose-reset: true`. Sinon, un joueur peut remplir son inventaire, rejoindre l'île d'un ami, partir et recommencer.

Vous pouvez également exécuter des commandes quand les joueurs rejoignent ou quittent, par exemple pour réinitialiser leurs défis ou donner un kit :

```yaml
island:
  commands:
    on-join:
      - 'bsbadmin deaths set [name] 0'
    on-leave: []
```

Celles-ci s'exécutent depuis la console sauf si la commande commence par `[SUDO]`, qui l'exécute en tant que joueur.

### Refroidissements d'invitation et confirmations

Ceux-ci sont dans le `config.yml` **de BentoBox** (dans `plugins/BentoBox/`), et s'appliquent à tous les modes de jeu :

```yaml
island:
  cooldown:
    time:
      invite: 60   # minutes avant qu'un joueur expulsé ou parti puisse être réinvité à cette île
      coop: 5      # minutes avant qu'un joueur non-coopéré puisse être à nouveau mis en coopération
      trust: 5     # minutes avant qu'un joueur sans confiance puisse être à nouveau approuvé
  confirmation:
    time: 10       # secondes que les joueurs ont pour confirmer
    commands:
      kick: true
      leave: true
    invites: false # demander aussi aux invités de confiance/coopération de confirmer (les invitations d'équipe confirment toujours)
```

Le refroidissement d'invitation empêche les joueurs de rejoindre, terminer les défis, partir et de rejoindre à plusieurs reprises.

### Désactiver les équipes

Certains modes de jeu sont conçus pour le jeu en solo. Un mode de jeu peut désactiver les équipes pour son monde. Ensuite, les commandes invite, kick, leave, promote, demote et setowner refusent de s'exécuter, mais la confiance et la coopération fonctionnent toujours pour que les joueurs puissent s'aider mutuellement. Si vous activez cela pour un monde qui a déjà des équipes, exécutez `/bsbadmin team disbandall` une fois pour casser les équipes existantes.

### Joueurs avec plus d'une île

Si vous permettez plusieurs îles par joueur (`concurrent-islands` au-dessus de 1), `disallow-team-member-islands: true` empêche les membres d'équipe de créer aussi leurs propres îles. Voir [Îles Multiples](../ConcurrentIslands.md).

## Tâches courantes d'administration { #common-admin-tasks }

| Je veux… | Faire ceci |
|---|---|
| Voir qui est dans l'équipe d'un joueur | `/bsbadmin info <player>` |
| Ajouter un joueur à une équipe | `/bsbadmin team add <owner> <player>` |
| Retirer un joueur d'une équipe | `/bsbadmin team kick <player>` |
| Donner une île à un autre membre (le propriétaire a quitté le serveur) | `/bsbadmin team setowner <player>` |
| Casser une équipe | `/bsbadmin team disband <owner>` |
| Casser toute équipe dans ce monde | `/bsbadmin team disbandall` |
| Permettre à une île d'avoir une équipe plus grande | `/bsbadmin team maxsize <player> <size>` |
| Permettre à un rang de joueurs d'avoir des équipes plus grandes | Donnez-leur `bskyblock.team.maxsize.<number>` |
| Permettre aux membres d'inviter d'autres joueurs | Le propriétaire ouvre `/island settings` → Rangs de Commande |
| Changer ce que les membres peuvent faire sur l'île | Le propriétaire ouvre `/island settings` ; les administrateurs définissent les valeurs par défaut dans la configuration du mode de jeu. Voir [Protection, Drapeaux et Rangs](../Island-Protection,-Flags-&-Ranks.md) |

## Rangs personnalisés { #custom-ranks }

Vous pouvez ajouter des rangs entre les rangs intégrés avec la commande `/bentobox rank` :

```
/bentobox rank list
/bentobox rank add ranks.veteran 700
/bentobox rank remove ranks.veteran
```

La valeur décide où le rang s'assied. `700` est entre Membre (500) et Sous-propriétaire (900), donc promouvoir un Membre le rend Vétéran, et promouvoir à nouveau le rend Sous-propriétaire. Ajoutez le nom d'affichage du rang à vos fichiers de locale sous la référence que vous avez utilisée (ici `ranks.veteran`).

## Dépannage

**« L'île est pleine » mais l'équipe semble petite.**
La limite inclut le propriétaire. Vérifiez `max-team-size` et si le propriétaire a une permission `team.maxsize`. Le propriétaire doit se connecter une fois pour qu'une nouvelle autorisation s'applique.

**Un joueur ne peut pas être invité.**
Il peut déjà être dans une équipe (il doit d'abord partir), avoir déjà une invitation en attente, ou être dans le refroidissement d'invitation après avoir quitté ou été expulsé de cette île.

**Les joueurs en coopération perdent continuellement leur rang.**
C'est ainsi que fonctionne la coopération : elle se termine quand aucun membre d'équipe n'est en ligne. Utilisez la confiance à la place pour les joueurs qui doivent conserver l'accès.

**Le propriétaire veut partir.**
Les propriétaires ne peuvent pas partir. Ils doivent d'abord donner l'île à quelqu'un avec `/island team setowner <player>`, ou un administrateur peut le faire avec `/bsbadmin team setowner`.

**Les joueurs exploitent la participation/départ d'équipe pour dupliquer des objets ou des récompenses.**
Activez les réinitialisations `on-join` et `on-leave`, définissez `leavers-lose-reset: true`, et conservez le refroidissement d'invitation.

## Voir aussi

- [Protection, Drapeaux et Rangs](../Island-Protection,-Flags-&-Ranks.md) : ce que chaque rang peut faire sur une île
- [Îles](IslandManagement.md) : création, réinitialisation et suppression d'îles
- [Îles Multiples](../ConcurrentIslands.md)
- [Personnalisation des Menus](../../Tutorials/generic/Customizable-GUI.md) : le menu d'équipe est `plugins/BentoBox/panels/team_panel.yml`
