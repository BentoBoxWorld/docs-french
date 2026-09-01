# DeathChest

**DeathChest** met les articles d'un joueur dans un coffre quand il meurt au lieu de les laisser tomber au sol — et, contrairement à un plugin de coffre de mort à usage général, il sait où se trouvent les îles.

Créé et maintenu par [tastybento](https://github.com/tastybento).

{{ addon_description("DeathChest") }}

## Pourquoi un addon de coffre de mort spécifique à l'île

Un plugin de coffre de mort conventionnel suppose deux choses : que le joueur est mort quelque part où un coffre peut être placé, et qu'il peut y retourner par la suite. Sur un serveur d'île, aucune hypothèse ne tient.

- **Le vide.** Un joueur qui tombe de son île meurt dans un espace vide, souvent sous le sol du monde. Il n'y a pas de bloc pour construire une tombe, donc un plugin conventionnel laisse le coffre tomber dans le vide, abandonne, ou le place au niveau de la roche mère où personne ne peut l'atteindre.
- **Océans.** Sur AcidIsland l'espace autour d'une île est la mer. Le sol existe, mais il est à cent blocs de profondeur et sous l'eau — techniquement un endroit valide, pratiquement un coffre perdu.
- **Les îles d'autres joueurs.** Un visiteur qui meurt ne peut généralement pas construire là, ne peut généralement pas casser le coffre, et ne peut souvent pas l'ouvrir non plus.
- **Le sauvage.** L'espace entre les îles n'est ni protégé ni accessible sans voler.

C'est pourquoi le conseil habituel finit par être « activez juste `keepInventory` » — et avec cela, mourir n'a plus aucune importance.

DeathChest résout le problème du placement à la place, donc la mort peut toujours coûter quelque chose sans tout coûter.

## Comment l'emplacement du coffre est choisi

L'addon fonctionne en trois étapes et s'arrête à la première qui réussit.

1. **Où le joueur est mort** — mais uniquement s'il est mort à l'intérieur de la partie *protégée* d'une île dont il est membre, **et** il y a du sol accessible : un bloc libre avec quelque chose de solide dessous, dans `chest.search-depth` blocs sous eux, et non submergé. C'est le cas normal. Vous êtes mort sur votre île, vos affaires sont là où vous êtes mort.

2. **Sur sa propre île** — à côté du point d'accueil de son île. Les morts au vide, les morts en mer, les morts dans la lave, les morts en visitant quelqu'un d'autre et les morts dans le sauvage atterrissent tous ici, c'est aussi où le joueur réapparaît.

3. **Tenu par l'addon** — si le joueur n'a pas d'île du tout, les articles vont dans la base de données de l'addon et sont récupérés avec `/[commande joueur] deathchest claim 1`.

!!! info "Pourquoi le « sol accessible » est la partie importante"
    Exiger du sol solide à portée, plutôt que n'importe quel sol solide, c'est ce qui empêche un coffre de se retrouver quelque part d'inutile. Un joueur qui tombe dans le vide se trouve toujours dans la colonne de son île, donc une recherche vers le bas illimitée serait heureux de trouver la roche mère et de laisser le coffre là. Sur un mode de jeu océanique, il trouverait le fond marin. L'échec de cette vérification n'est pas une erreur — c'est le signal qui envoie le coffre à l'étape 2, où le joueur peut réellement s'y rendre à pied.

## Installation

1. Mettez le jar de l'addon dans le dossier `plugins/BentoBox/addons`
2. Redémarrez le serveur (pour activer l'addon et avoir le fichier `config.yml` généré)
3. Personnalisez les paramètres dans `config.yml` (optionnel)
4. Exécutez `/bentobox reload` ou redémarrez le serveur pour appliquer les nouveaux paramètres

!!! warning "DeathChest ne fait rien quand `keepInventory` est activé"
    Si la règle du jeu `keepInventory` conserve l'inventaire d'un joueur, il n'y a rien à stocker et l'addon s'écarte. Désactivez `keepInventory` dans vos mondes de mode de jeu si vous voulez que les coffres de mort sauvent les articles des joueurs.

## Commandes

!!! tip
    `[commande joueur]` et `[commande administrateur]` diffèrent en fonction du mode de jeu que vous exécutez.
    La configuration de `config.yml` du mode de jeu contient les paramètres qui vous permettent de les modifier.
    Par exemple, sur BSkyBlock la `[commande joueur]` par défaut est `island` et la `[commande administrateur]` par défaut est `bsbadmin`.

### deathchest
**Commande** : `/[commande joueur] deathchest`
**Alias** : `deaths`, `grave`
**Description** : Répertoriez vos coffres de mort, le plus récent en premier, avec où chacun est et combien de temps il lui reste.
**Permission** : `[gamemode].deathchest`. Défaut : `true`.

Les coffres tenus par l'addon plutôt que placés dans le monde sont affichés comme tenus au lieu de coordonnées.

### deathchest claim {number}
**Commande** : `/[commande joueur] deathchest claim {number}`
**Description** : Remet les articles que l'addon retient pour ce coffre, plus toute expérience stockée. Les articles qui ne tiennent pas dans l'inventaire du joueur sont laissés tomber à ses pieds.
**Permission** : `[gamemode].deathchest`. Défaut : `true`.
**Exemple** : `/[commande joueur] deathchest claim 1`

C'est ainsi qu'un joueur récupère un coffre qui ne pouvait pas être placé dans le monde. Il recueille également tout débordement — voir [Comment les articles sont stockés](#how-items-are-stored).

### deathchest tp {number}
**Commande** : `/[commande joueur] deathchest tp {number}`
**Description** : Téléportez le joueur à ce coffre de mort.
**Permission** : `[gamemode].deathchest.teleport`. Défaut : `true`.
**Exemple** : `/[commande joueur] deathchest tp 1`

Requiert que `commands.allow-teleport` soit `true` dans `config.yml`. Un coffre sans bloc dans le monde ne peut pas être visité — réclamez-le à la place.

### admin deathchest
**Commande** : `/[commande administrateur] deathchest`
**Description** : Rapportez combien de coffres de mort sont stockés sur le serveur.
**Permission** : `[gamemode].admin.deathchest`. Défaut : `op`.

### admin deathchest {player}
**Commande** : `/[commande administrateur] deathchest {player}`
**Alias** : `deathchests`
**Description** : Répertoriez les coffres de mort d'un joueur, montrant où le coffre est et où il est mort. Ces deux diffèrent quand le coffre a été relocalisé à l'île, ce qui rend facile de voir une mort au vide ou en mer en un coup d'œil.
**Permission** : `[gamemode].admin.deathchest`. Défaut : `op`.
**Exemple** : `/[commande administrateur] deathchest tastybento`

### admin deathchest purge
**Commande** : `/[commande administrateur] deathchest purge`
**Description** : Expliquez tous les coffres qui sont déjà en retard immédiatement, plutôt que d'attendre la prochaine vérification.
**Permission** : `[gamemode].admin.deathchest`. Défaut : `op`.

!!! tip
    `[gamemode]` est un préfixe qui diffère selon le mode de jeu que vous exécutez.
    Le préfixe est le nom du mode de jeu en minuscules, c'est-à-dire que si vous utilisez BSkyBlock, le préfixe est `bskyblock`.
    De la même manière, si vous utilisez AcidIsland, le préfixe est `acidisland`.

## Permissions

| Permission | Défaut | Description |
|---|---|---|
| `[gamemode].deathchest` | `true` | Utilisez `/[commande joueur] deathchest` pour répertorier les coffres et réclamer les articles retenus |
| `[gamemode].deathchest.teleport` | `true` | Utilisez `/[commande joueur] deathchest tp {number}` |
| `[gamemode].admin.deathchest` | `op` | Utilisez la commande d'administrateur |

## Comment les articles sont stockés

Le bloc du coffre retient les articles. L'inventaire d'un joueur est 41 emplacements incluant l'armure et la main d'appel, et un coffre est 27, donc le **débordement est normal plutôt que rare**.

Tout ce qui ne tient pas est retenu par l'addon et déplacé dans le coffre automatiquement chaque fois que le joueur le ferme. Donc un joueur vide le coffre, le ferme, et les articles suivants apparaissent — jusqu'à ce que rien ne reste. Une fois que le coffre et le magasin de l'addon sont tous deux vides, le bloc du coffre disparaît avec son record.

Si le bloc du coffre s'en va pour une raison que l'addon n'a pas causée — un world edit, un retour en arrière, un `/setblock` manuel — le record survit et se transforme en un coffre retenu qui peut être récupéré avec `deathchest claim`.

## Protection

Seul le propriétaire peut ouvrir ou casser son propre coffre de mort. Quiconque d'autre se voit refuser et se dit de qui c'est le coffre.

- `chest.team-access` prolonge cela aux membres de l'équipe de l'île, mais seulement quand le coffre se trouve sur une île que le propriétaire et l'autre joueur possèdent tous les deux.
- `chest.protect-from-explosions` garde les coffres de mort hors des listes de blocs d'explosion de creeper, TNT et lit.
- Les records sont supprimés quand une île est réinitialisée ou supprimée, parce que les blocs s'en vont être effacés avec.

!!! warning "Les entonnoirs ne sont pas bloqués"
    Un entonnoir sous un coffre de mort le viders. Le coffre se trouve sur la propre île du propriétaire, donc c'est auto-infligé plutôt que du griefing, mais c'est bon de savoir si vos joueurs construisent des systèmes de tri près du point d'accueil de leur île. Suivi comme [issue #5](https://github.com/BentoBoxWorld/DeathChest/issues/5).

## Configuration

Le fichier `config.yml` contient les paramètres ci-dessous. Les valeurs affichées sont les valeurs par défaut.

### Désactiver les modes de jeu
DeathChest opère dans tous les mondes de mode de jeu sur le serveur BentoBox par défaut.
Vous pouvez désactiver un mode de jeu en écrivant son nom sur une nouvelle ligne qui commence par `-`.

Exemple pour désactiver BSkyBlock :

```yml
disabled-gamemodes:
  - BSkyBlock
```

Valeur par défaut :

```yml
disabled-gamemodes: []
```

### Matériau du coffre
Le bloc utilisé pour le coffre de mort.

`CHEST` est l'apparence classique. `BARREL` est un bon choix pour les îles exiguës car il peut être ouvert même avec un bloc directement au-dessus.

Le matériau doit être un conteneur. S'il n'est pas — ou si le nom n'est pas un matériau réel — l'addon enregistre une erreur et revient à tenir les articles pour le joueur.

```yml
chest:
  material: CHEST
```

### Placer au lieu de mort
Placez le coffre où le joueur est mort, si c'est un endroit qu'il peut atteindre et construire.

Définissez à `false` pour toujours envoyer les coffres au point d'accueil de l'île à la place.

Les morts au vide, en dehors d'une zone d'autorisation de construction, ou dans un endroit inaccessible reviennent au point d'accueil de l'île indépendamment de ce paramètre.

```yml
chest:
  place-at-death-location: true
```

### Rayon de recherche
Jusqu'où regarder **latéralement**, en blocs, pour un endroit libre pour mettre le coffre. Plage 1 à 32.

```yml
chest:
  search-radius: 8
```

### Profondeur de recherche
Jusqu'où regarder **vers le bas**, en blocs, pour le sol pour que le coffre se tienne dessus. Plage 1 à 64.

C'est ce qui empêche un coffre de se retrouver loin en dessous du joueur — sur le fond marin d'un monde océanique, ou enterré dans le terrain. Si aucun sol n'est trouvé dans cette distance, le coffre va à l'île du joueur à la place, ce qui est généralement ce que vous voulez.

L'augmenter permet aux coffres de suivre une longue chute jusqu'au sol ; l'abaisser envoie plus de morts à l'île.

```yml
chest:
  search-depth: 16
```

### Minutes d'expiration
Combien de minutes un coffre de mort dure avant d'expirer. `0` signifie jamais.

```yml
chest:
  expiry-minutes: 60
```

### Action d'expiration
Ce qui se passe quand un coffre de mort expire.

- `DROP` — casser le coffre et laisser les articles tomber au sol. Ils vont disparaître comme n'importe quel article laissé tomber.
- `DELETE` — supprimer le coffre et son contenu.

```yml
chest:
  expiry-action: DROP
```

### Secondes de vérification d'expiration
À quelle fréquence, en secondes, vérifier les coffres expirés. Minimum 5.

```yml
chest:
  expiry-check-seconds: 60
```

### Max par joueur
Nombre maximum de coffres de mort qu'un joueur peut avoir à la fois. En cas de dépassement, le coffre le plus ancien du joueur expire tôt, suivant l'`expiry-action` ci-dessus. `0` signifie illimité.

Cela empêche un joueur qui continue de mourir de parsemer son île de coffres.

```yml
chest:
  max-per-player: 3
```

### Accès à l'équipe
Laissez les membres de l'équipe de l'île ouvrir les coffres de mort les uns des autres.

Définissez à `false` si seul le propriétaire devrait jamais ouvrir son propre coffre.

```yml
chest:
  team-access: true
```

### Protéger des explosions
Empêchez les coffres de mort d'être soufflés par des creepers, TNT et ainsi de suite.

```yml
chest:
  protect-from-explosions: true
```

### Stocker l'expérience
Stockez l'expérience abandonnée du joueur avec le coffre et remettez-la quand il est ouvert.

```yml
experience:
  store: true
```

### Pourcentage d'expérience
Pourcentage de l'expérience abandonnée du joueur à stocker, 0 à 100. Le reste est perdu, ce qui maintient un coût à la mort.

S'applique uniquement quand `experience.store` est `true`.

```yml
experience:
  percent: 100
```

### Notifier à la mort
Dites au joueur où son coffre de mort est quand il meurt, et combien de temps il durera.

Le message nomme le monde en utilisant le nom convivial du mode de jeu, ajoutant `Nether` ou `The End` quand la mort n'était pas dans le monde d'en haut.

```yml
notify:
  on-death: true
```

### Permettre le téléportation
Permettre à `/[commande joueur] deathchest tp {number}` de téléporter le joueur à son coffre.

Les joueurs ont encore besoin de la permission `[gamemode].deathchest.teleport`.

```yml
commands:
  allow-teleport: true
```

## Traductions

{{ translations("DeathChest") }}

## Source
Vous voulez contribuer ? Voir le code source de cette documentation à [GitHub](https://github.com/BentoBoxWorld/docs/blob/master/docs/addons/DeathChest/).
