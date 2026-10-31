# IslandStats

**IslandStats** conserve les statistiques pour chaque île plutôt que pour chaque joueur. Il commence par les décès de monstres : combien de chaque monstre est mort sur une île et combien d'entre eux un joueur a tués. Il fonctionne avec tous les modes de jeu.

Créé et maintenu par [tastybento](https://github.com/tastybento).

{{ addon_description("IslandStats") }}

## Installation

1. Placez le fichier jar de l'addon IslandStats dans le dossier addons du plugin BentoBox.
2. Redémarrez le serveur.
3. L'addon créera un dossier de données et dans ce dossier se trouvera un config.yml.
4. Modifiez le config.yml comme vous le souhaitez.
5. Redémarrez le serveur si vous apportez une modification.

IslandStats nécessite BentoBox 3.23.0 ou version ultérieure, Minecraft 26.2 ou version ultérieure et Java 25.

!!! warning "Le comptage commence quand l'addon est installé"
    IslandStats ne lit pas les anciennes statistiques des joueurs, donc chaque île commence à zéro.

## Statistiques

L'addon conserve deux comptages pour chaque type de monstre :

| Statistique | Comptages |
|---|---|
| `KILL_ENTITY` | Monstres tués par un joueur sur l'île. Même signification que la statistique de joueur vanilla `KILL_ENTITY`. |
| `ENTITY_DEATH` | Monstres qui sont morts sur l'île pour n'importe quelle cause : joueurs, fermes de monstres, chute, lave. |

Une mort est comptée pour l'île dans la zone protégée de laquelle elle s'est produite. Les joueurs et les porte-armures ne sont pas comptés. Les monstres tués par des visiteurs comptent dans `KILL_ENTITY` sauf si `count-visitor-kills` est désactivé. Chaque mort sur l'île compte toujours dans `ENTITY_DEATH`.

L'addon n'utilise pas les statistiques de joueur vanilla, car elles n'enregistrent que les mises à mort attribuées à un joueur et n'enregistrent pas l'endroit où se trouvait le monstre. Les fermes à monstres seraient ignorées et la mise à mort serait attribuée à l'île du tueur plutôt qu'à l'île où le monstre est mort.

### Boîte de dialogue des statistiques

`/[player_command] stats` ouvre une boîte de dialogue :

- La page de synthèse affiche un total pour chaque statistique, avec un bouton pour l'ouvrir.
- Chaque page de statistique répertorie les monstres du plus au moins nombreux, avec les boutons Précédent, Suivant, Retour et Fermer.
- Les noms des monstres sont envoyés sous forme de texte traduisible, de sorte que chaque joueur les voit dans sa propre langue client.

### Stockage

Les statistiques sont stockées via l'API de base de données BentoBox, elles sont donc enregistrées dans la base de données que BentoBox est configuré pour utiliser, quelle qu'elle soit. Il y a un enregistrement par île. Avec la base de données JSON, ceux-ci se trouvent dans `plugins/BentoBox/database/IslandStatsData/`. Le comptage se fait en mémoire, et les îles modifiées sont sauvegardées à intervalle régulier (`save-interval`) et quand le serveur s'arrête. Quand une île est supprimée ou réinitialisée, ses statistiques le sont aussi.

## Configuration

Le dernier `config.yml` se trouve [ici](https://github.com/BentoBoxWorld/IslandStats/blob/develop/src/main/resources/config.yml).

??? note "disabled-gamemodes"
    Les modes de jeu répertoriés ici sont ignorés par IslandStats.

    Défaut : `[]`

    ```yaml
    disabled-gamemodes:
      - BSkyBlock
    ```

??? note "count-visitor-kills"
    Compte les monstres tués sur une île par des joueurs qui ne sont pas des membres, comme les visiteurs ou les coops. Ceci n'affecte que la statistique « tués par les joueurs ». Chaque mort de monstre sur l'île est toujours comptée dans la statistique « tous les décès de monstres ».

    Défaut : `true`

??? note "ignored-entities"
    Les types d'entités qui ne sont jamais comptés. Utilisez les noms de type d'entité Bukkit. Les porte-armures sont des entités vivantes pour le serveur, ils sont donc ignorés par défaut.

    Défaut : `ARMOR_STAND`

??? note "save-interval"
    La fréquence, en minutes, à laquelle les statistiques modifiées sont écrites dans la base de données. Les statistiques sont comptées en mémoire et toujours sauvegardées quand le serveur s'arrête. Minimum 1.

    Défaut : `5`

??? note "dialog.page-size"
    Combien de lignes de monstre afficher sur chaque page de la boîte de dialogue des statistiques. Plage 1 à 50.

    Défaut : `15`

## Commandes

!!! tip
    `[player_command]` et `[admin_command]` sont des commandes qui diffèrent selon le mode de jeu que vous exécutez.
    Le fichier `config.yml` des modes de jeu contient des options qui vous permettent de modifier ces valeurs.
    Par exemple, sur BSkyBlock, le `[player_command]` par défaut est `island`, et le `[admin_command]` par défaut est `bsbadmin`.

=== "Commandes joueur"
    - `/[player_command] stats` : ouvre la boîte de dialogue des statistiques de votre île.

=== "Commandes Admin"
    - `/[admin_command] stats <player>` : affiche les statistiques de l'île de ce joueur. Un joueur voit la boîte de dialogue, et la console reçoit les statistiques sous forme de lignes de chat.
    - `/[admin_command] stats <player> reset` : efface les statistiques de l'île après confirmation.

!!! warning "Utilisez la commande du monde dans lequel vous êtes"
    `/[player_command] stats` ne fonctionne que dans le monde de ce mode de jeu. Par exemple, dans le monde OneBlock, utilisez la commande OneBlock, pas `/is`, afin que les joueurs qui ont des îles dans plusieurs modes de jeu voient la bonne.

## Permissions

!!! tip
    `[gamemode]` est un préfixe qui diffère selon le mode de jeu que vous exécutez.

| Permission | Défaut | Ce qu'elle autorise |
|---|---|---|
| `[gamemode].island.stats` | true | `/[player_command] stats`, qui ouvre les statistiques de votre île |
| `[gamemode].admin.stats` | op | `/[admin_command] stats <player> [reset]` |

## Placeholders

{{ placeholders_source("IslandStats") }}

`<entity>` est le type de monstre en minuscules, comme `zombie` ou `iron_golem`. Avec PlaceholderAPI, les placeholders ressemblent à `%IslandStats_bskyblock_island_kill_entity_zombie%`.

## Pour les développeurs d'addon

D'autres addons peuvent lire les comptages via le gestionnaire :

```java
IslandStats stats = (IslandStats) BentoBox.getInstance().getAddonsManager().getAddonByName("IslandStats").orElseThrow();
long zombies = stats.getManager().getCount(island, IslandStat.KILL_ENTITY, EntityType.ZOMBIE);
long allDeaths = stats.getManager().getTotal(island, IslandStat.ENTITY_DEATH);
```

??? note "Nouveautés dans v1.0.0 — première version"
    **Publié :** 4 octobre 2026

    Première version. Compatibilité : BentoBox API 3.23.0 · Minecraft 26.2 et versions ultérieures · Java 25. [Release 1.0.0](https://github.com/BentoBoxWorld/IslandStats/releases/tag/1.0.0)

    - Comptages des monstres tués et morts de monstres par île (`KILL_ENTITY` et `ENTITY_DEATH`).
    - Boîte de dialogue des statistiques avec `/[player_command] stats`, et une vue et réinitialisation admin avec `/[admin_command] stats <player> [reset]`.
    - Placeholders pour les totaux de l'île, les comptages par monstre et l'île sur laquelle se tient le joueur.
    - 🔡 Seule la locale `en-US` est incluse dans cette version. Les traductions sont bienvenues.

## Traductions

{{ translations("IslandStats") }}
