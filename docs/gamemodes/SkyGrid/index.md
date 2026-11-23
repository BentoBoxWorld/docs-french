# SkyGrid

Chaque quatrième bloc dans chaque direction est un vrai bloc. Tout le reste est de l'air.

Cela signifie du gravier flottant au-dessus du vide. Des flaques de lave suspendues dans le néant. Un creeper sur un bloc de sable à douze mètres au-dessus de vous. Aller n'importe où nécessite de la planification, de la précision et un respect sain de ce qui se passe si vous manquez un saut.

**SkyGrid** a été créé par SethBling en 2012 et est devenu l'une des meilleures cartes de défi Minecraft jamais faites. Ceci est la version BentoBox — même grille chaotique, s'exécutant désormais en tant qu'expérience d'île multijoueur complète avec toute la progression, les défis et les tableaux de classement que les joueurs attendent.

Créé et maintenu par [tastybento](https://github.com/tastybento).

{{ addon_description("SkyGrid") }}

## Installation

0. Installez BentoBox et exécutez-le sur le serveur au moins une fois pour créer ses dossiers de données.
1. Placez ce jar dans le dossier addons du plugin BentoBox.
2. Redémarrez le serveur.
3. L'addon créera des mondes et un dossier de données contenant un fichier config.yml.
4. Arrêtez le serveur.
5. Modifiez le fichier config.yml selon vos préférences.
6. Supprimez tous les mondes créés par défaut si vous avez apporté des modifications qui les affecteraient.
7. Redémarrez le serveur.

## Configuration

Le `config.yml` de SkyGrid liste les blocs qui composent la grille dans chaque monde, avec un poids pour chacun. La version la plus récente du fichier se trouve [ici](https://github.com/BentoBoxWorld/SkyGrid/blob/master/src/main/resources/config.yml).

### Mobs des générateurs { #spawner-mobs }

Depuis SkyGrid 2.3.0, vous choisissez les mobs qui sortent des générateurs de la grille. Chaque monde a sa propre liste, au format `EntityType: weight` :

| Monde | Liste |
|---|---|
| Overworld | `world.spawners` |
| Nether | `world.nether.spawners` |
| End | `world.end.spawners` |

```yaml
world:
  end:
    spawners:
      ENDERMAN: 45
      ENDERMITE: 54
      SHULKER: 1
```

- Un mob est choisi proportionnellement à son poids. Dans l'exemple, 1 générateur de l'End sur 100 est un générateur de shulkers.
- Pour empêcher la création de générateurs d'un type donné, supprimez le mob ou mettez son poids à `0`. Par exemple, supprimez `VILLAGER` et `IRON_GOLEM` de `world.spawners`.
- Pour n'avoir aucun générateur du tout, supprimez `SPAWNER` de la liste des blocs de ce monde.
- Si une liste est vide, SkyGrid utilise sa liste intégrée et l'écrit dans le fichier.
- Les mobs qui ne peuvent pas être dans un générateur, comme `ARROW`, sont ignorés avec un avertissement dans la console.

Les modifications n'affectent que les chunks générés par la suite.

### Hauteur et alignement de la grille { #grid-height-and-alignment }

Les blocs de grille sont placés tous les 4 blocs. Depuis la 2.3.0, `world.skygrid-height` est arrondi au multiple de 4 le plus proche (maximum 252), de sorte que le centre de la zone de chaque joueur se trouve sur une couche de la grille.

`world.start-x`, `world.start-z` et `world.space-around-players` devraient également être des multiples de 4. SkyGrid consigne un avertissement dans le journal s'ils ne le sont pas, mais ne les modifie pas, car cela déplacerait toutes les zones d'un monde existant.

## Permissions

Les permissions peuvent être trouvées [ici](Permissions).

## Commandes

Les commandes peuvent être trouvées [ici](Commands).

## Placeholders

Les placeholders peuvent être trouvés [ici](Placeholders).

## Journal des modifications

??? warning "Nouveautés dans v2.2.4 — correctif de la génération du monde"
    **Publié :** 5 novembre 2026

    Compatibilité : BentoBox API 3.3.1 · Minecraft 1.21.x (testé sur Paper 26.3) · Java 21.

    - 🔺 **La grille n'est plus remplie de pierre et d'herbe.** Le terrain vanilla était généré sous la grille et la génération de surface vanilla remplaçait des blocs par de l'herbe. Les emplacements de la grille ne reçoivent désormais que les blocs de votre configuration. [PR #88](https://github.com/BentoBoxWorld/SkyGrid/pull/88)
    - 🔺 **Les chunks ne se répètent plus.** Chaque chunk partait de la même séquence aléatoire, si bien que le même motif se répétait tous les 16 blocs. Chaque chunk a désormais la sienne. [PR #88](https://github.com/BentoBoxWorld/SkyGrid/pull/88)
    - **La canne à sucre a maintenant de l'eau.** Elle se trouve dans un petit bassin de grès pour que l'eau reste en place. L'eau du bassin peut geler dans les biomes froids. [PR #89](https://github.com/BentoBoxWorld/SkyGrid/pull/89)
    - **Les cactus et les buissons morts ne flottent plus.** Ils reposent désormais sur du sable, posé sur du grès. [PR #89](https://github.com/BentoBoxWorld/SkyGrid/pull/89)

    🔺 **Mondes existants :** les chunks déjà générés ne changent pas, il y aura donc une démarcation visible là où les anciens et les nouveaux chunks se rejoignent. Pour une grille homogène, supprimez vos mondes SkyGrid et laissez-les se régénérer — **cela supprime toutes les îles de ces mondes**, alors planifiez-le avec vos joueurs et faites d'abord une sauvegarde.

    [Release v2.2.4](https://github.com/BentoBoxWorld/SkyGrid/releases/tag/2.2.4)

!!! warning "Nouveautés dans v2.3.0 — mobs des générateurs, et commandes d'équipe et de maison pour les joueurs"
    **Publié :** 22 novembre 2026

    Compatibilité : BentoBox API 3.3.1 · Minecraft 1.21.x et 26.x · Java 21.

    - ⚙️ **Mobs des générateurs configurables.** De nouvelles listes, `world.spawners`, `world.nether.spawners` et `world.end.spawners`, définissent les mobs que les générateurs peuvent contenir et la fréquence de chacun. Elles sont ajoutées aux configs existantes avec les mêmes probabilités qu'avant. Voir [Mobs des générateurs](#spawner-mobs). [PR #94](https://github.com/BentoBoxWorld/SkyGrid/pull/94)
    - ⚙️ **La hauteur de la grille s'aligne sur la grille.** `skygrid-height` est arrondi au multiple de 4 le plus proche (maximum 252). La grille ne change pas, mais les points d'apparition des joueurs peuvent se déplacer de 2 blocs au maximum. SkyGrid avertit si `start-x`, `start-z` ou `space-around-players` ne sont pas des multiples de 4. Voir [Hauteur et alignement de la grille](#grid-height-and-alignment). [PR #94](https://github.com/BentoBoxWorld/SkyGrid/pull/94)
    - 🔺 **Les joueurs peuvent utiliser les commandes d'équipe et de maison.** 12 permissions de joueur n'étaient pas déclarées, si bien que seuls les opérateurs les avaient : équipe `invite`, `accept`, `reject`, `kick`, `leave`, `promote` et `setowner`, `info`, `near`, et `homes`, `renamehome` et `deletehome`. Elles sont désormais accordées par défaut à tout le monde. Voir [Permissions](Permissions.md). [PR #92](https://github.com/BentoBoxWorld/SkyGrid/pull/92)
    - ⚙️ **Nouveaux paramètres par défaut pour les nouvelles installations.** Huit paramètres liés aux dangers sont masqués aux joueurs (`TNT_DAMAGE`, `BLOCK_EXPLODE_DAMAGE`, `FIRE_BURNING`, `FIRE_IGNITE`, `FIRE_SPREAD`, `LEAF_DECAY`, `ENDERMAN_TELEPORT`, `SHULKER_TELEPORT`), et `PISTON_PUSH` est listé et désactivé. Les serveurs existants conservent leur `config.yml` ; copiez les entrées dans `world.hidden-flags` et `world.flags` si vous les voulez. [PR #93](https://github.com/BentoBoxWorld/SkyGrid/pull/93)

    🔺 **Si vous aviez volontairement réservé les commandes d'équipe ou de maison aux opérateurs ou à certains rangs,** refusez explicitement, dans votre plugin de permissions, les permissions que vous voulez garder restreintes, par exemple `skygrid.island.team.invite`.

    [Release v2.3.0](https://github.com/BentoBoxWorld/SkyGrid/releases/tag/2.3.0)

## Traductions

{{ translations("SkyGrid") }}
