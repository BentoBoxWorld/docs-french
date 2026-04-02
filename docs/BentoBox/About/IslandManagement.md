# Gestion des Îles

Au cœur de chaque mode de jeu BentoBox se trouve l'**île** — une zone protégée du monde qui appartient à un joueur ou à une équipe. BentoBox gère le cycle de vie complet des îles, donc vous n'avez pas à le gérer manuellement.

## Création d'une Île

Quand un joueur rejoint un mode de jeu pour la première fois et exécute la commande principale (par ex. `/island` pour BSkyBlock, `/oneblock` pour AOneBlock), BentoBox fait automatiquement :

1. Trouve un emplacement libre dans le monde pour eux.
2. Colle leur **île de démarrage** à partir d'un Blueprint (un modèle d'île sauvegardé).
3. Les téléporte au point d'apparition de leur nouvelle île.
4. Enregistre l'île comme leur dans la base de données.

Les joueurs reçoivent exactement une île par mode de jeu. Si votre serveur exécute plusieurs modes de jeu (par ex. BSkyBlock et AcidIsland), chaque joueur obtient une île distincte dans chaque monde.

## Noms des Îles

Les joueurs peuvent donner à leur île un nom personnalisé avec `/island setname <name>`. Les noms apparaissent à différents endroits — classements, complément Warps, et placeholders affichés par d'autres plugins. Les administrateurs peuvent restreindre les noms autorisés via le `config.yml` du mode de jeu.

## Emplacements du Foyer

Les joueurs peuvent définir plusieurs emplacements du foyer sur leur île avec `/island sethome`. Quand ils utilisent `/island go` ou `/island home`, ils se téléportent à leur point d'accueil. Plusieurs foyers nommés peuvent être déverrouillés via des permissions :

```
[gamemode].island.home.maxhomes.<number>
```

## Réinitialisation d'une Île

Les joueurs peuvent recommencer à zéro en réinitialisant leur île avec `/island reset`. Cela **supprime l'île actuelle** et crée une toute nouvelle. Les administrateurs peuvent :

- Limiter le nombre de fois qu'un joueur peut réinitialiser (défini dans `config.yml`).
- Accorder des réinitialisations supplémentaires via la permission `[gamemode].island.reset.maxresets.<number>`.
- Définir les réinitialisations comme illimitées avec la valeur `-1`.

!!! warning
    Les réinitialisations d'îles sont permanentes. L'ancienne île et tout ce qui a été construit dessus est supprimé. Conseillez aux joueurs de sauvegarder tout ce qui est important avant de réinitialiser.

## Suppression d'Île (Admin)

Les administrateurs peuvent supprimer l'île d'un joueur avec :
```
/[admin_command] delete <player>
```

Cela supprime l'île de la base de données et met la zone en attente de nettoyage. Le joueur pourra créer une nouvelle île après.

## Nettoyage des Îles Inactives

Si les joueurs abandonnent le serveur, leurs îles restent dans le monde. BentoBox ne supprime pas automatiquement les îles inactives, mais le **drapeau de suppression** et les outils externes peuvent être utilisés pour cela. De nombreux administrateurs de serveur gèrent cela en définissant une limite de réinitialisation et en examinant périodiquement les joueurs inactifs.

## Ce qui se Passe Quand un Joueur Quitte une Équipe

Si un joueur est un membre (pas propriétaire) et quitte une équipe ou est expulsé, il perd l'accès à cette île. Il peut ensuite créer sa propre île, sous réserve des limites de réinitialisation. Si le joueur *était* le propriétaire, il doit transférer la propriété avant de partir — il ne peut pas simplement abandonner une île qu'il possède.

## Plusieurs Îles (Îles Concurrentes)

Par défaut, chaque joueur a une île par mode de jeu. BentoBox supporte optionnellement les **îles concurrentes** — permettant à un seul joueur de posséder plus d'une île à la fois. C'est une fonctionnalité avancée configurée dans le `config.yml` du mode de jeu et contrôlée par les permissions.

### Exemples de Configuration

Il y a deux endroits où les îles concurrentes peuvent être configurées :

**1. `config.yml` BentoBox** — définit le défaut global pour tous les modes de jeu :

```yaml
island:
  # Le nombre par défaut d'îles concurrentes qu'un joueur peut avoir.
  # Cela peut être remplacé par les paramètres de configuration des modes de jeu individuels.
  concurrent-islands: 1
```

**2. `config.yml` du mode de jeu** (par ex. BSkyBlock) — remplace le défaut global pour ce mode de jeu :

```yaml
world:
  # Le nombre d'îles concurrentes qu'un joueur peut avoir dans le monde.
  # Une valeur de 0 utilisera le défaut du config.yml BentoBox.
  concurrent-islands: 1
  # Empêcher les joueurs d'avoir d'autres îles s'ils sont dans une équipe.
  disallow-team-member-islands: true
```

Par exemple, pour permettre à chaque joueur de posséder jusqu'à **3** îles dans BSkyBlock, définissez `concurrent-islands: 3` dans le `config.yml` BSkyBlock. Si vous voulez également que les membres d'une équipe puissent créer leurs propres îles, définissez `disallow-team-member-islands: false`.

### Permission

Le maximum par joueur peut être remplacé par un nœud de permission :

```
[gamemode].island.number.<number>
```

Remplacez `[gamemode]` par le préfixe du mode de jeu et `<number>` par le nombre maximum d'îles autorisées. Par exemple :

| Permission | Effet |
|---|---|
| `bskyblock.island.number.5` | Permet au joueur jusqu'à 5 îles dans BSkyBlock |
| `acidisland.island.number.3` | Permet au joueur jusqu'à 3 îles dans AcidIsland |
| `caveblock.island.number.2` | Permet au joueur jusqu'à 2 îles dans CaveBlock |

La valeur de permission remplace la valeur de configuration `concurrent-islands` pour ce joueur. Si un joueur n'a pas la permission, la valeur de configuration est utilisée comme défaut.

!!! tip
    Pour un guide complet — y compris comment les joueurs créent, naviguent et gèrent plusieurs îles — voir la page [Îles Concurrentes](../../BentoBox/ConcurrentIslands.md).

## Plage d'Île et Espacement

Les îles sont placées dans une grille. L'espacement entre les centres des îles est défini une fois dans `config.yml` (`distance-between-islands`) et **ne peut pas être changé une fois le monde créé**. Choisissez cette valeur avant que les joueurs commencent à rejoindre. Une plus grande valeur offre plus d'espace de construction entre les îles ; une plus petite valeur rend le monde plus compact.

La **plage de protection** du joueur — la zone qu'il possède réellement et peut protéger — est toujours inférieure ou égale à la moitié de la distance d'île. Elle peut être agrandie par les administrateurs ou par les permissions des joueurs jusqu'à ce maximum.

## Voir les Informations de l'Île

Les joueurs peuvent vérifier les informations de leur propre île avec `/island info`. Les administrateurs peuvent vérifier n'importe quelle île avec :
```
/[admin_command] info <player>
```
Cela affiche l'emplacement de l'île, le propriétaire, les membres de l'équipe et la plage de protection actuelle.
