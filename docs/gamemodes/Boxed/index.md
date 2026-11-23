# Boxed

Vous commencez à l'intérieur d'une boîte. Une petite boîte. Tout ce qui se trouve en dehors — les mobs, les blocs, les ressources — est interdit. Pour obtenir plus d'espace, vous devez le gagner : accomplissez des avancements et votre boîte grandit. Chaque avancement compte. Chaque nouveau bloc de territoire est une récompense pour laquelle vous avez travaillé.

**Boxed** est un mode de jeu d'îles avec une particularité : votre monde ne s'étend pas en minant ou en construisant, il s'étend en *faisant des choses*. Créez quelque chose de nouveau. Explorez une structure. Tuez un mob. Cultivez une récolte. Tout l'arbre d'avancement vanilla alimente votre progression, et le datapack personnalisé optionnel ajoute encore plus à chercher.

Créé et maintenu par [tastybento](https://github.com/tastybento).

{{ addon_description("Boxed") }}

## Exigences BentoBox

* Toujours utiliser la dernière version de BentoBox (Les snapshots peuvent être téléchargés ici : [https://ci.bentobox.world](https://ci.bentobox.world))
* InvSwitcher — garde les avancements, l'inventaire, etc. séparés entre les mondes sur un serveur.
* Border — affiche la boîte

## Comment installer

### Démarrage rapide

1. Placez l'addon Boxed dans le dossier addons de BentoBox avec InvSwitcher et Border (utilisez les dernières versions !).
2. Redémarrez le serveur — de nouveaux mondes seront créés. *Cela prendra longtemps la première fois*
3. Connectez-vous
4. Tapez `/boxed` pour commencer.
5. (Optionnel) Désactivez les annonces d'avancements `/gamerule announceAdvancements false` sinon il y aura beaucoup de spam du serveur quand les joueurs obtiennent des avancements.

* Vous commencerez près d'un arbre. Il y a un coffre avec des articles pratiques dedans. (C'est le blueprint de l'île)
* La seule zone sur laquelle vous pouvez opérer est votre boîte qui apparaît sous forme de bordure.
* Pour agrandir votre boîte, complétez les avancements.
* Vérifiez votre progression avec l'écran Avancements, (touche L).
* Les monstres ne se reproduisent pas par défaut en dehors de votre boîte, mais votre boîte s'agrandit, et il ne faut qu'un bloc pour générer un mob !
* Le propriétaire de la boîte peut déplacer la boîte en utilisant des enderpearls lancées de l'intérieur. Attention ! C'est un aller simple. (Paramètre optionnel dans config.yml)
* Les paramètres de la boîte ont une option pour permettre le déplacement de la boîte par d'autres rangs (recherchez l'icône du composter)

## Avancements personnalisés

Le **BoxedDataPack** officiel ajoute un ensemble d'avancements personnalisés spécialement conçus pour Boxed, donnant aux joueurs plus à faire et à votre serveur une expérience plus complète hors de la boîte.

[Téléchargez la dernière version de BoxedDataPack](https://github.com/BentoBoxWorld/BoxedDataPack/releases) et déposez le `.zip` dans le dossier `world/datapacks/` de votre serveur (ou le monde dans lequel Boxed s'exécute), puis exécutez `/reload` ou redémarrez.

Préférez construire le vôtre ? Consultez la [vidéo de tutoriel](https://youtu.be/zNzQvIbweQs) pour savoir comment créer des avancements personnalisés qui s'intègrent au système d'expansion de Boxed.

## Réduire la taille du monde

!!! warning "Regionerator n'est plus nécessaire"
    Les anciennes versions de ce guide recommandaient le plugin tiers [Regionerator](https://github.com/Jikoo/Regionerator) pour élaguer les chunks inutilisés. **Depuis BentoBox 3.15.0, cette fonctionnalité est intégrée** — BentoBox supprime désormais directement les fichiers de région (`.mca`), donc Regionerator n'est plus requis et n'est plus recommandé pour Boxed. Si vous l'utilisez encore, vous pouvez le retirer : il est redondant et, à moins que ses exemptions de mondes de graines ne soient correctement configurées, il peut supprimer les mondes de graines de Boxed et rendre le démarrage du serveur très lent.

Les mondes Boxed grandissent à mesure que les joueurs agrandissent et réinitialisent leurs boîtes, et cet espace disque est maintenant récupéré par BentoBox lui-même de deux façons.

**Entretien automatique (activé par défaut).** Lorsqu'une boîte est réinitialisée, elle est *supprimée en douceur* (marquée pour suppression plutôt qu'effacée bloc par bloc), et un balayage planifié récupère ses fichiers de région en arrière-plan. Le balayage « deleted » s'exécute toutes les 24 heures par défaut. La section concernée du `config.yml` de BentoBox est :

```yaml
island:
  deletion:
    housekeeping:
      # Récupère les fichiers de région des boîtes déjà marquées pour suppression (ex. après une réinitialisation).
      # Activé par défaut.
      deleted-sweep:
        enabled: true
        interval-hours: 24
      # Récupère les fichiers de région qui n'ont tout simplement pas été touchés depuis longtemps,
      # que la boîte ait été réinitialisée ou non. Désactivé par défaut — activez ceci
      # pour le contrôle de taille le plus agressif.
      age-sweep:
        enabled: false
        interval-days: 30
        min-age-days: 60
```

**Purge manuelle.** Vous pouvez aussi récupérer de l'espace à la demande depuis la console du serveur ou en jeu (voir [Commandes](Commands)) :

* `/boxadmin purge deleted` — récupère immédiatement les fichiers de région de chaque boîte déjà marquée pour suppression.
* `/boxadmin purge <days>` — récupère les fichiers de région des boîtes dont les propriétaires ne se sont pas connectés depuis `<days>` jours et dont les fichiers de région sont au moins aussi anciens.
* `/boxadmin purge unowned` — marque chaque boîte sans propriétaire comme supprimable afin que le prochain balayage la retire.

!!! note "Redémarrez après une grosse purge"
    Les fichiers de région sont supprimés du disque immédiatement, mais Paper conserve les chunks récemment chargés dans un cache en mémoire. **Redémarrez le serveur après une grosse purge** afin que ce cache soit vidé et que l'espace libéré soit pleinement restitué. Les boîtes protégées de la purge, les îles de spawn et (si l'addon Level est installé) les boîtes au-dessus du niveau de purge configuré sont toujours ignorées. Comme toujours, **sauvegardez votre dossier de monde avant de purger.**

L'ancien paramètre `keep-previous-island-on-reset` n'existe plus — les boîtes sont toujours supprimées en douceur lors d'une réinitialisation puis nettoyées par l'entretien automatique, il n'y a donc rien à configurer pour que Regionerator « prenne le relais ».


## Configuration avancée

### config.yml
La configuration est très similaire à BSkyBlock, AcidIsland, etc.

Chaque joueur aura sa propre terre à explorer jusqu'à la limite de la valeur de distance de l'île. La valeur par défaut est 400, donc la terre sera 800 x 800 blocs. La terre est semi-aléatoire, mais chaque joueur obtiendra à peu près la même disposition (voir la configuration des biomes). Les structures telles que les villages, les portes du nether cassées, les épaves, etc. sont aléatoires et donc certains joueurs peuvent les obtenir, d'autres non. Dans une version future, l'arrêt des structures sera une option de configuration. Les forteresses sont désactivées et n'existent pas. La terre de chaque joueur est entourée de mers de différentes températures. Si la bordure n'est pas solide, les joueurs peuvent théoriquement explorer d'autres terres.

*Graine du monde*
La graine du monde est ce qui est utilisé pour générer les terres. Je recommande de conserver cette valeur. Si vous la changez, la terre peut être très différente.

Options ajoutées dans Boxed 3.5.0 :

??? note "boxed.structure-time-budget"
    Millisecondes par tick que le placement des structures vanilla (villages, épaves, etc.) dans les boîtes peut utiliser. Les structures sont placées une par une jusqu'à épuisement de ce temps, si bien qu'une nouvelle boîte reçoit ses structures en quelques secondes quand le serveur a du temps disponible. Un tick dure 50 ms. Baissez cette valeur si le placement des structures cause du lag. `0` place une structure par tick.

    Une structure n'est placée qu'une fois que tous les chunks qu'elle pourrait toucher sont chargés : une structure proche du bord d'une boîte apparaît donc quand un joueur s'en approche pour la première fois, et non juste après la création de la boîte.

    Par défaut : `10`

??? note "world.structure-settings"
    Désactive ou active individuellement des structures vanilla dans les mondes Boxed. Cela couvre la génération du monde et les recherches de structures : `/locate`, les yeux de l'Ender, les cartes d'exploration et au trésor, les dauphins et les échanges des cartographes. La clé est l'identifiant vanilla de la structure et la valeur est `false` pour désactiver la structure, ou `true` pour la forcer même si la liste globale `world.disabled-structures` de BentoBox la désactive. Les structures non listées suivent la liste globale de BentoBox.

    ```yaml
    structure-settings:
      monument: false
      trial_chambers: false
    ```

    Par défaut : `{}`

??? note "area.teams-disabled"
    Désactive le système d'équipe dans les mondes Boxed. Avec `true`, les joueurs ne peuvent pas inviter, accepter d'invitations d'équipe, expulser, quitter l'équipe, promouvoir, rétrograder ni changer le propriétaire. La confiance et la coopération fonctionnent toujours. Après l'avoir activé, exécutez une fois `/boxadmin team disbandall` pour dissoudre les équipes existantes. Voir [Désactiver les équipes](../../BentoBox/About/Teams.md#turning-teams-off).

    Par défaut : `false`

!!! tip "Si la création d'une boîte cause du lag"
    Essayez la prégénération de chunks de BentoBox : `island.pregeneration.enabled: true` dans le `config.yml` de BentoBox (BentoBox 3.14.0 et versions ultérieures). Elle génère en arrière-plan les chunks des prochaines boîtes, avant que quiconque en ait besoin.

### Blueprint

Il y a un blueprint "island" qui est utilisé pour générer l'arbre, le coffre et les blocs en dessous jusqu'à y = 5. La hauteur de la surface par défaut est d'environ y = 65, donc le blueprint doit faire environ 60 blocs de haut. Si vous créez de bons blueprints, veuillez les partager !

### advancements.yml
Ce fichier contient tous les avancements et de combien votre boîte doit grandir si vous en obtenez un. Le fichier peut contenir des avancements personnalisés si vous les avez.

Il y a deux paramètres en haut — le premier `default-root-increase` vous n'avez probablement pas besoin de le changer. Cela définit le score de tout avancement racine à 0. En d'autres termes, les joueurs n'obtiendront pas l'expansion de boîte juste en voyant le nouvel onglet d'avancement.

Le deuxième paramètre `unknown-advancement-increase` donne à tous les avancements inconnus, c'est-à-dire ceux non listés dans ce fichier, une valeur par défaut. C'est la valeur par défaut utilisée si vous ajoutez des avancements personnalisés via un data pack et elle vous libère de devoir énumérer chaque nouvel avancement dans ce fichier.

Exemple :

```
# Liste le nombre de blocs par lequel la boîte augmentera lorsqu'un avancement est obtenu
settings:
  default-root-increase: 0
  unknown-advancement-increase: 1
advancements:
  'minecraft:adventure/adventuring_time': 1
  'minecraft:adventure/arbalistic': 1
  'minecraft:adventure/bullseye': 1
...
```

### biomes.yml
La terre du joueur a des biomes et ils sont définis ici. Il n'est pas possible de définir où se trouvent les biomes en ce moment, seulement l'effet qu'ils ont sur le terrain.

* height: la hauteur par défaut est 8. Des nombres plus bas produiront une terre plus basse, des nombres plus élevés une terre plus élevée.
* scale: c'est le degré de lissage du terrain. Des nombres plus petits sont plus déchiquetés, des nombres plus grands sont plus plats.

Définir les biomes océaniques à des nombres de hauteur plus élevés entraînera le lit océanique au-dessus du niveau de la mer et créera de la terre.

Beaucoup de ces nombres sont des estimations approximatives en ce moment et si vous trouvez de meilleures valeurs, veuillez les partager !


## Permissions

Les permissions peuvent être trouvées [ici](Permissions).

## Commandes

Les commandes peuvent être trouvées [ici](Commands).

## Placeholders

Les placeholders peuvent être trouvés [ici](Placeholders).

## Journal des modifications

!!! warning "Nouveautés dans v3.5.0 — nécessite Java 25 et BentoBox 3.23.0"
    **Publié :** 21 novembre 2026

    Compatibilité : BentoBox 3.23.0 ou version ultérieure · Paper 1.21.5 – 26.3 · Java 25.

    - 🔺 **Java 25 requis.** Boxed est désormais compilé pour Java 25 et BentoBox 3.23. Il ne se chargera pas sur une version plus ancienne de Java, même sur les serveurs Minecraft 1.21.x.
    - ⚙️ **Placement des structures plus fluide dans les nouvelles boîtes.** Les villages, épaves, ruines et autres structures d'une nouvelle boîte étaient auparavant placés au rythme d'un toutes les 3 secondes, soit environ 3½ minutes par boîte. Ils sont désormais placés dans un budget de temps par tick, `boxed.structure-time-budget` (`10` ms par défaut), et apparaissent en quelques secondes. Ils ne forcent plus le serveur à générer des chunks pendant un tick : une structure attend que tous les chunks qu'elle pourrait toucher soient chargés, si bien qu'une structure proche du bord d'une boîte apparaît quand un joueur s'en approche pour la première fois.
    - 🔺 **Les structures ne sont plus placées deux fois.** Après un redémarrage, des structures pouvaient être placées de nouveau par-dessus la boîte d'un joueur, écrasant des constructions et faisant apparaître des mobs supplémentaires. C'est corrigé, et les listes enregistrées par les anciennes versions sont nettoyées automatiquement.
    - ⚙️ **Désactivez les équipes** avec la nouvelle option `area.teams-disabled` (`false` par défaut). La confiance et la coopération fonctionnent toujours.
    - ⚙️ **Contrôlez les structures vanilla** avec la nouvelle option `world.structure-settings`, qui désactive des structures individuelles, ou les force, dans les mondes Boxed.
    - 🔺 **Les joueurs peuvent lister, renommer et supprimer leurs maisons.** `boxed.island.homes`, `boxed.island.renamehome` et `boxed.island.deletehome` n'étaient pas déclarées, si bien que seuls les opérateurs les avaient. Elles sont désormais accordées par défaut à tout le monde. Refusez-les explicitement dans votre plugin de permissions si vous ne le souhaitez pas.
    - 🔺 **`/boxadmin place` utilise `boxed.admin.place`** (opérateurs par défaut). Elle vérifiait auparavant le nœud non déclaré `boxed.boxed.commands.boxadmin.place`. Si vous l'aviez accordé à des membres du staff qui ne sont pas opérateurs, accordez-leur `boxed.admin.place` à la place.
    - 🐛 Une structure qui n'a pas pu être chargée ne bloque plus toutes les structures suivantes jusqu'à un redémarrage, et un nom de structure manquant dans `structures.yml` ne fait plus ignorer toutes les structures listées après lui.

    Les nouvelles options sont ajoutées au `config.yml` avec leurs valeurs par défaut ; voir [config.yml](#configyml).

    [Release v3.5.0](https://github.com/BentoBoxWorld/Boxed/releases/tag/3.5.0)

??? note "Nouveautés dans v3.4.1"
    **Publié :** 25 septembre 2026

    Une version de maintenance. Nécessite BentoBox **3.17.0** ou une version plus récente. Compatibilité : Paper 1.21.x – 26.x · Java 21.

    - 🐛 **Plus de plantage `contloc out of spec` à l'activation.** Au premier démarrage, une carte d'explorateur obtenue d'une caisse de butin pouvait rechercher très loin en dehors de la zone de graine, où la continentalité tombe en dessous de -1,2, et BentoBox a ignoré Boxed. Les valeurs hors plage tombent maintenant dans les bandes les plus externes.
    - 🐛 **`/boxadmin place ... NO_MOBS` fonctionne.** Le 7e argument était rejeté avant de pouvoir être lu ; il est maintenant accepté et ne se reporte plus aux placements ultérieurs.
    - 🐛 Une parenthèse manquante choisissait le mauvais biome dans certaines zones de graine de niveau d'érosion 5. Seuls les mondes de graine générés après la mise à niveau sont affectés.
    - ⚙️ Les commentaires `area.deaths` plus clairs dans `config.yml`, expliquant quels paramètres de mort affectent les niveaux d'île sous [Level](../../addons/Level/index.md) 2.29.0 et lesquels n'affectent que le compteur de morts de BentoBox et `%boxed_deaths%`. Seuls les commentaires ont changé.
    - Les versions sont maintenant également publiées sur CurseForge et Hangar.

    [Release v3.4.1](https://github.com/BentoBoxWorld/Boxed/releases/tag/3.4.1)

??? note "Nouveautés dans v3.4.0"
    **Publié le :** 2026-05-30

    - **Prise en charge des Chambres d'épreuves (Trial Chambers).** Boxed capture et restaure désormais l'état des Trial Spawners — y compris les configurations normale *et* sinistre (ominous) — quand des structures sont tirées du monde-graine dans la boîte d'un joueur, et reconnaît `trial_chambers` comme structure suivie pour la croissance de boîte liée aux avancées.
    - 🐛 **Plus de perte de progression entre modes de jeu.** Boxed n'efface plus les avancées et statistiques d'un joueur lorsqu'une île est réinitialisée dans un *autre* mode de jeu non-Boxed.
    - 🐛 Les collages de structure en attente sont désormais annulés lorsqu'une île est supprimée, évitant de placer des structures dans une boîte qui n'existe plus.
    - 🐛 Les trial spawners sinistres restaurent maintenant la bonne configuration au lieu de toujours appliquer la normale.
    - Modernisation de la chaîne de build et de test : Paper 1.21.11, API BentoBox 3.13.0, JUnit 5 + Mockito + MockBukkit.

    !!! note
        Les Chambres d'épreuves sont capturées depuis le monde-graine lors de la génération d'une boîte ; les boîtes créées *avant* la 3.4.0 ne les obtiendront donc pas rétroactivement. Les nouvelles boîtes (et les régions nouvellement étendues) les incluront.

    [Release v3.4.0](https://github.com/BentoBoxWorld/Boxed/releases/tag/3.4.0)

## Traductions

{{ translations("Boxed") }}
