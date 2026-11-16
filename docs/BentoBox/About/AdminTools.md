# Outils d'Administration { #admin-tools }

BentoBox dispose d'outils en jeu pour rechercher les îles, découvrir pourquoi quelque chose est bloqué et gérer le serveur, afin que vous ayez rarement besoin d'éditer les fichiers de données à la main. Cette page couvre les outils que vous utiliserez le plus ; chaque commande est dans la [référence des commandes](../Commands.md).

!!! info "Commandes sur cette page"
    Les commandes d'administration des modes de jeu sont affichées comme `/bsbadmin` (BSkyBlock). Utilisez la commande d'administration de votre mode de jeu à la place, par exemple `/oba` (AOneBlock), `/acid` (AcidIsland) ou `/cbadmin` (CaveBlock). Elles sont réservées aux opérateurs par défaut ; voir [Autorisations et Avantages VIP](../Permissions-Guide.md#staff-permissions) pour les donner au personnel.

## Rechercher une île { #look-up-an-island }

| Je veux… | Commande |
|---|---|
| Voir tout ce qui concerne l'île d'un joueur : propriétaire, équipe, portée, foyers, réinitialisations, morts, bannissements | `/bsbadmin info <player>` |
| Voir l'île sur laquelle je me tiens | `/bsbadmin info` |
| Voir l'une des plusieurs îles qu'un joueur possède | `/bsbadmin info <player> <island name>` |
| Aller à l'île d'un joueur (ou ses îles Nether/End) | `/bsbadmin tp <player>`, `tpnether`, `tpend` |
| Envoyer un joueur à l'île de quelqu'un d'autre | `/bsbadmin tpuser <player> <island owner>` |
| Voir le rang d'un joueur sur une île | `/bsbadmin getrank <player>` |
| Afficher la zone protégée de l'île en jeu | `/bsbadmin range display` |

## Découvrir pourquoi quelque chose est bloqué { #find-out-why-something-is-blocked }

Quand un joueur dit qu'il ne peut pas faire quelque chose (ou qu'il peut faire quelque chose qu'il ne devrait pas), activez l'outil **why** :

```
/bsbadmin why <player>
```

Ensuite, demandez au joueur de réessayer. La console enregistre chaque vérification de protection pour ce joueur : ce qu'il a essayé, où, si c'était autorisé et quel drapeau ou rang l'a décidé. Exécutez la même commande à nouveau pour le désactiver. Le joueur doit être en ligne.

La plupart des problèmes s'avèrent être un drapeau défini pour un rang différent de celui attendu, ou le joueur étant sur l'île de quelqu'un d'autre. Voir [Protection, Drapeaux et Rangs](../Island-Protection,-Flags-&-Ranks.md).

## Agir comme un joueur normal { #act-as-a-normal-player }

Les opérateurs et modérateurs disposant des permissions de contournement ignorent la protection des îles, ce qui rend les tests confus. **`/bsbadmin switch`** désactive votre contournement afin que vous soyez protégé comme un joueur normal ; exécutez-le à nouveau pour le réactiver. Le statut d'opérateur lui-même n'est pas affecté. Voir [Contourner la protection](../Island-Protection,-Flags-&-Ranks.md#bypass-the-protection).

## Réparer une île { #fix-an-island }

| Je veux… | Commande | Plus |
|---|---|---|
| Changer le rang d'un joueur sur une île | `/bsbadmin setrank <player> <rank>` | [Équipes et Rangs](Teams.md) |
| Ajouter ou retirer des membres d'équipe, changer le propriétaire | `/bsbadmin team add`, `team kick`, `team setowner` | [Équipes et Rangs](Teams.md#common-admin-tasks) |
| Changer les paramètres d'une île | `/bsbadmin settings <player>` | [Protection, Drapeaux et Rangs](../Island-Protection,-Flags-&-Ranks.md) |
| Agrandir ou réduire une île | `/bsbadmin range set <player> <range>` | [Îles](IslandManagement.md#island-size-protection-range) |
| Réinitialiser le foyer d'un joueur, ou supprimer ses foyers | `/bsbadmin resethome <player>`, `deletehomes <player>` | [Îles](IslandManagement.md#homes) |
| Effacer le nom d'une île | tenez-vous dessus, `/bsbadmin resetname` | [Îles](IslandManagement.md#island-names) |
| Redonnez des réinitialisations à un joueur | `/bsbadmin resets reset <player>` | [Îles](IslandManagement.md#resetting-islands) |
| Supprimer, restaurer ou réaffecter une île | `/bsbadmin delete`, `undelete`, `register` | [Îles](IslandManagement.md#deleting-islands) |
| Déplacer le centre de la zone protégée d'une île | tenez-vous à cet endroit, `/bsbadmin setprotectionlocation` | |
| Réinitialiser les paramètres de chaque île aux valeurs par défaut de la configuration | `/bsbadmin resetflags` | |
| Faire d'une île le spawn du mode de jeu | tenez-vous dessus, `/bsbadmin setspawn` | |

## Paramètres mondiaux { #world-settings }

**`/bsbadmin settings`** ouvre le menu des paramètres administrateur du mode de jeu du monde : paramètres mondiaux (tels que les dégâts de creeper ou le maintien de l'inventaire des visiteurs), les règles de protection en dehors des îles, les valeurs par défaut pour les nouvelles îles, et les paramètres de l'île que les joueurs peuvent voir. Voir [Panneau des Paramètres Administrateur](../Island-Protection,-Flags-&-Ranks.md#admin-settings-panel).

## Gestion de BentoBox { #managing-bentobox }

| Commande | Ce qu'elle fait |
|---|---|
| `/bentobox version` | Versions de BentoBox, du mode de jeu et des add-ons, version du serveur et base de données. **Incluez ceci quand vous demandez de l'aide ou signalez un bug.** |
| `/bentobox manage` | Le Panneau de Gestion : onglets pour vos modes de jeu, add-ons et crochets (autres plugins avec lesquels BentoBox fonctionne), plus le catalogue des add-ons |
| `/bentobox catalog` | Parcourir les modes de jeu et les add-ons que vous pouvez télécharger |
| `/bentobox reload` | Recharge les paramètres de BentoBox et des add-ons, les fichiers de langue et les modèles de menu |
| `/bsbadmin reload` | Recharge les paramètres d'un mode de jeu |
| `/bentobox perms` | Affiche chaque permission de commande et sa valeur par défaut (console) |
| `/bentobox locale` | Vérifier les fichiers de langue pour les traductions manquantes |
| `/bentobox placeholders` | Parcourir les placeholders et les activer ou les désactiver. Voir [Placeholders](../Placeholders.md) |

Certains paramètres, comme la génération du monde et `distance-between-islands`, ne prennent effet qu'après un redémarrage complet.

## Base de données { #database }

BentoBox stocke les îles et les joueurs dans une base de données définie dans le `config.yml` de BentoBox. La valeur par défaut est des fichiers **JSON** dans le dossier BentoBox, qui ne nécessite aucune configuration. Pour les serveurs plus importants, ou plusieurs serveurs partageant des données, vous pouvez utiliser **MySQL** (5.7+), **MariaDB** (10.2.3+), **PostgreSQL** (9.4+), **SQLite** (3.28+) ou **MongoDB** (3.6+).

Pour changer le type de base de données sans perdre les données, voir [Modification de la Base de Données](../Database-transition.md). Faites toujours une sauvegarde en premier.

## Voir aussi { #see-also }

- [Référence des commandes](../Commands.md)
- [Autorisations et Avantages VIP](../Permissions-Guide.md)
- [Notes de Version BentoBox](../Release-Notes.md)
