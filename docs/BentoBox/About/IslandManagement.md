# Îles { #islands }

Chaque mode de jeu BentoBox est construit sur les **îles** : une zone protégée du monde qui appartient à un joueur ou à une équipe. (Dans des modes de jeu comme CaveBlock ou Boxed, l'« île » est une grotte ou une boîte, mais cela fonctionne de la même manière.) Cette page couvre comment les îles sont créées, dimensionnées, réinitialisées et supprimées, comment les foyers fonctionnent, et comment nettoyer les anciennes îles.

!!! info "Commandes sur cette page"
    Les commandes sont affichées pour BSkyBlock (`/island`, `/bsbadmin`). Les autres modes de jeu utilisent leurs propres noms de commandes, par exemple `/ob` dans AOneBlock. Les autorisations commencent par le préfixe du mode de jeu, par exemple `bskyblock.` ou `aoneblock.`. Pour ce que voient les joueurs, envoyez-les au [Guide du Joueur](../Player-Guide.md).

## Avant d'ouvrir : planifiez le monde { #before-you-open-plan-the-world }

Deux paramètres du `config.yml` du mode de jeu **ne peuvent pas être modifiés après que les îles existent**. Les modifier ultérieurement signifie effacer le monde et la base de données, donc décidez avant que les joueurs ne rejoignent :

```yaml
world:
  # Rayon de l'espace de chaque île, en blocs.
  # Les centres des îles sont deux fois cela écartés, donc 400 met les centres 800 blocs écartés.
  distance-between-islands: 400
  # Combien de cet espace le propriétaire protège au départ (un rayon).
  # Peut être augmenté plus tard par île, jusqu'à distance-between-islands.
  protection-range: 50
```

- `distance-between-islands` est le **maximum** qu'une île puisse jamais grandir. Définissez-le sur la plus grande taille que vous pourriez donner aux VIP ou vendre comme améliorations.
- `protection-range` est où les îles **commencent**. C'est la zone que les joueurs peuvent construire et protéger.

D'autres paramètres que vous voudrez peut-être regarder : `island-height` (niveau Y de l'île de démarrage), `max-islands` (limite le nombre d'îles du monde, `0` = pas de limite) et `start-x`/`start-z` (qui aussi ne peuvent pas changer plus tard).

## Créer des îles { #creating-islands }

Les nouveaux joueurs tapent `/island`. BentoBox :

1. Affiche le menu **Créer une Île** s'il y a plus d'une île de démarrage à choisir (sinon il saute cela).
2. Trouve le prochain endroit libre, colle l'île de démarrage et téléporte le joueur là-bas.

Vous pouvez changer ce qui se passe :

| Paramètre (game mode `config.yml`) | Défaut | Ce qu'il fait |
|---|---|---|
| `new-player-action` | `create` | Ce que `/island` fait pour les joueurs sans île |
| `default-action` | `go` | Ce que `/island` fait pour les joueurs avec une île |
| `create-island-on-first-login.enable` | `false` | Créer une île automatiquement quand un nouveau joueur rejoint |
| `teleport-player-to-island-when-created` | `true` | Téléporter le joueur quand son île est prête |

**Choix d'îles de démarrage.** Chaque choix du menu Créer une Île est un bundle de blueprint. Pour le rendre disponible uniquement pour certains joueurs (par exemple une île VIP), définissez-le pour exiger une autorisation dans `/bsbadmin blueprint`, puis donnez `bskyblock.island.create.<bundle-name>`. Voir [Îles de Démarrage (Blueprints)](../Blueprints.md).

## Taille de l'île (étendue de protection) { #island-size-protection-range }

L'étendue de la protection est le rayon autour du centre de l'île que le propriétaire contrôle. Les joueurs le voient avec `/island info` ; les administrateurs peuvent l'afficher en jeu avec `/bsbadmin range display`.

Pour donner à certains joueurs des îles plus grandes :

| Comment | Commande ou autorisation |
|---|---|
| Par rang ou VIP, automatiquement | Donnez au propriétaire `bskyblock.island.range.<number>`. Vérifié quand l'île est créée et quand le propriétaire se connecte |
| Une île, à la main | `/bsbadmin range set <player> <range>`, ou `range add` / `range remove` pour le changer d'un montant |
| Revenir à la valeur par défaut | `/bsbadmin range reset <player>` |

La portée ne peut pas dépasser `distance-between-islands`. Les add-ons comme [Upgrades](../../addons/Upgrades/index.md) peuvent aussi ajouter une portée comme bonus ; supprimer les bonus des add-ons avec `/bsbadmin range removebonus <player>`.

## Foyers { #homes }

Les joueurs se téléportent à leur île avec `/island` ou `/island go`, et déplacent leur foyer avec `/island sethome`.

Par défaut chaque île a un foyer. Pour autoriser plus de foyers nommés :

```yaml
island:
  max-homes: 1    # game mode config.yml
```

ou donnez au propriétaire `bskyblock.island.maxhomes.<number>`. Les joueurs utilisent ensuite `/island sethome <name>`, `/island go <name>` et `/island homes`. Les administrateurs peuvent changer une île avec `/bsbadmin maxhomes <player> <number>`.

`/island go <name>` trouve le foyer même si le joueur se trompe avec les majuscules ou ne tape que le début du nom. Sur Minecraft 26 et versions ultérieures, un joueur avec plusieurs foyers qui tape `/island go` obtient une fenêtre contextuelle pour en choisir un (`island.dialogs.go-picker` dans le `config.yml` de BentoBox).

**Foyers dans le Nether et l'End** (quand le mode de jeu a des mondes Nether et End d'îles) sont contrôlés par `island.sethome.nether.allow` et `island.sethome.the-end.allow`.

| Tâche d'administration | Commande |
|---|---|
| Remettre le foyer d'un joueur à l'endroit par défaut | `/bsbadmin resethome <player>` |
| Supprimer tous les foyers nommés d'un joueur | `/bsbadmin deletehomes <player>` |
| Aller à l'île d'un joueur | `/bsbadmin tp <player>` |

## Noms d'îles { #island-names }

Les joueurs nomment leur île avec `/island setname <name>` et la supprime avec `/island resetname`. Les noms s'affichent dans les classements, les warps et les placeholders.

Définissez les règles dans le `config.yml` **de BentoBox** :

```yaml
island:
  name:
    min-length: 4
    max-length: 20
    uniqueness: false   # true = aucune deux îles dans un mode de jeu ne peuvent partager un nom
```

Les joueurs ont besoin de `bskyblock.island.name.format` pour utiliser des couleurs dans les noms. Les administrateurs peuvent effacer un nom offensant en se tenant sur l'île et en exécutant `/bsbadmin resetname`.

## Réinitialiser les îles { #resetting-islands }

`/island reset` donne au joueur une île fraîche. **L'ancienne île est supprimée.** Seul le propriétaire peut réinitialiser ; tous les membres d'équipe sont supprimés de l'île.

Contrôlez-le dans le `config.yml` du mode de jeu :

```yaml
island:
  reset:
    reset-limit: -1   # -1 = illimité, 0 = pas de réinitialisations, 2 = deux réinitialisations (trois îles au total)
```

et dans le `config.yml` de BentoBox :

```yaml
island:
  cooldown:
    time:
      reset: 300        # secondes qu'un joueur doit attendre entre les réinitialisations
  confirmation:
    commands:
      reset: true       # les joueurs doivent confirmer avant de réinitialiser
```

Ce qui est effacé du joueur (inventaire, coffre de l'Ender, argent, XP) sur une nouvelle île est défini par les options `on-join` décrites dans [Équipes et Rangs](Teams.md#what-happens-to-items-and-money-when-players-join-or-leave).

Pour donner à un joueur plus de réinitialisations, changez son nombre de réinitialisations :

| Commande | Effet |
|---|---|
| `/bsbadmin resets reset <player>` | Revenir à 0 réinitialisations utilisées |
| `/bsbadmin resets set <player> <number>` | Définir combien de réinitialisations ils ont utilisées |
| `/bsbadmin resets add <player> <number>` | Compter plus de réinitialisations comme utilisées |
| `/bsbadmin resets remove <player> <number>` | Redonnez des réinitialisations |

Il n'y a pas de permission pour des réinitialisations supplémentaires ; utilisez ces commandes, par exemple à partir d'un plugin de classement ou de magasin.

## Supprimer des îles { #deleting-islands }

| Je veux… | Commande |
|---|---|
| Supprimer l'île d'un joueur | `/bsbadmin delete <player>` |
| Supprimer l'île sur laquelle je me tiens | `/bsbadmin delete` (refusé tant qu'elle a une équipe) |
| Annuler une suppression avant le nettoyage | Tenez-vous dessus et exécutez `/bsbadmin undelete` |
| Donner une île supprimée ou sans propriétaire à un joueur | Tenez-vous dessus et exécutez `/bsbadmin register <player>` |
| Supprimer un propriétaire mais garder les blocs | `/bsbadmin unregister <owner>` |

Supprimer une île supprime le propriétaire immédiatement, ainsi le joueur peut en créer une nouvelle. Les **blocs** sont supprimés plus tard, quand les fichiers de région sont nettoyés (voir ci-dessous). Jusque-là, `undelete` ou `register` peuvent ramener l'île.

## Nettoyage des anciennes îles { #cleaning-up-old-islands }

Les îles supprimées et réinitialisées, et les îles des joueurs qui n'ont jamais revenir, occupent de l'espace disque. BentoBox les supprime en supprimant les **fichiers de région** du monde (chacun couvre une zone de 512×512 blocs) une fois qu'aucune île active n'y est.

**Le nettoyage automatique** est défini dans le `config.yml` de BentoBox :

```yaml
island:
  deletion:
    housekeeping:
      deleted-sweep:
        enabled: true         # nettoyer les îles supprimées et réinitialisées
        interval-hours: 24
      age-sweep:
        enabled: false        # aussi nettoyer les îles que personne n'a visitées
        interval-days: 30
        min-age-days: 60
  purge-level: 10             # jamais purger les îles au-dessus de ce niveau (nécessite Level)
```

Le balayage des îles supprimées est sûr et activé par défaut. Le balayage de l'âge est désactivé par défaut car il supprime les îles abandonnées qui n'ont jamais été supprimées.

**Nettoyage manuel :**

| Commande | Ce qu'elle fait |
|---|---|
| `/bsbadmin purge <days>` | Supprime les îles dans les fichiers de région que personne n'a touchées depuis ce nombre de jours |
| `/bsbadmin purge deleted` | Nettoie les îles supprimées maintenant au lieu d'attendre le balayage |
| `/bsbadmin purge unowned` | Marque les îles sans propriétaire comme supprimables |
| `/bsbadmin purge protect` | Tenez-vous sur une île et exécutez ceci pour la protéger contre tous les purgages |

Les purgages ignorent les îles avec des joueurs en ligne, les îles de spawn, les îles protégées et les îles au-dessus de `purge-level`.

!!! warning "Faites une sauvegarde en premier"
    La purge supprime les fichiers de région du disque et ne peut pas être annulée. Sauvegardez le dossier du monde avant votre premier purge. Les îles qui partagent un fichier de région avec une île active restent jusqu'à ce que la région soit claire.

## Îles multiples par joueur { #multiple-islands-per-player }

Les joueurs peuvent posséder plus d'une île dans un mode de jeu si vous le permettez :

```yaml
island:
  concurrent-islands: 1          # BentoBox config.yml : défaut pour tous les modes de jeu

world:
  concurrent-islands: 1          # game mode config.yml : 0 = utiliser la valeur de BentoBox
  disallow-team-member-islands: true
```

Ou donnez aux joueurs `bskyblock.island.number.<number>`. Voir [Îles Multiples](../ConcurrentIslands.md) pour comment les joueurs créent et passent entre les îles.

## Découvrir une île { #finding-out-about-an-island }

| Commande | Affiche |
|---|---|
| `/island info` | Propriétaire, équipe, taille et emplacement de l'île sur laquelle vous vous tenez |
| `/bsbadmin info [player]` | Détails complets : propriétaire, membres, portée, foyers, réinitialisations, morts et plus. Sans nom, l'île sur laquelle vous vous tenez |
| `/bsbadmin why <player>` | Enregistre pourquoi un joueur peut ou ne peut pas faire quelque chose. Voir [Outils d'Administration](AdminTools.md) |

## Dépannage { #troubleshooting }

**Le serveur ne démarre pas après que j'ai modifié `distance-between-islands`.**
Il ne peut pas changer une fois que les îles existent. Remettez l'ancienne valeur.

**L'autorisation d'un VIP pour une plus grande île ou plus de foyers ne s'est pas appliquée.**
Les autorisations sont vérifiées pour le **propriétaire** de l'île, quand il se connecte (et à la création de l'île pour la portée). Faites que le propriétaire se déconnecte et se reconnecte.

**Un joueur n'a pas de réinitialisations restantes.**
`/bsbadmin resets reset <player>`.

**Une île supprimée est encore là.**
Ses blocs s'en vont quand le fichier de région est nettoyé, au prochain balayage d'île supprimée (24 heures par défaut), ou exécutez `/bsbadmin purge deleted`. Si une autre île active partage le fichier de région, les blocs restent.

**L'utilisation du disque continue de croître.**
Assurez-vous que `deleted-sweep` est activé, et envisagez `/bsbadmin purge <days>` ou le balayage de l'âge pour les îles abandonnées.

## Voir aussi { #see-also }

- [Guide du Joueur](../Player-Guide.md) : les commandes que vos joueurs utilisent
- [Équipes et Rangs](Teams.md)
- [Protection, Drapeaux et Rangs](../Island-Protection,-Flags-&-Ranks.md)
- [Îles de Démarrage (Blueprints)](../Blueprints.md)
- [Îles Multiples](../ConcurrentIslands.md)
- [Outils d'Administration](AdminTools.md)
