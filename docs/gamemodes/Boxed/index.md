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
