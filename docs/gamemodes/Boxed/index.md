# Boxed

Les joueurs survivent dans une boîte qui ne peut être agrandie qu'en accomplissant des avancements !

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

[Téléchargez le DataPack officiel Boxed](https://github.com/BentoBoxWorld/BoxedDataPack) pour les avancements personnalisés.
Ou vous pouvez le faire vous-même. Consultez la [vidéo de tutoriel pour plus d'informations](https://youtu.be/zNzQvIbweQs)

## Utilisation de Regionerator

*Remarque : Ce plugin est conçu pour supprimer les régions inutilisées de votre monde ! Assurez-vous de faire des sauvegardes si vous l'utilisez ! À utiliser à vos risques et périls !*

[Regionerator](https://github.com/Jikoo/Regionerator) est un plugin qui supprime progressivement les chunks inutilisés pour maintenir les tailles de mondes réduites. Il n'a pas été écrit par l'équipe BentoBox, mais il soutient BentoBox et respecte les limites de boîte. Il peut être utilisé pour supprimer les chunks de boîte afin qu'ils puissent être régénérés. Puisque Boxed utilise des mondes de graines pour copier à partir de, ceux-ci peuvent sembler inutilisés par Regionerator et supprimés, ce qui rend le démarrage très lent. Pour éviter cela, définissez les mondes de graines comme exempts de ses suppressions en les ayant dans la section monde du fichier de configuration de Regionerator :

```
# Mondes dans lesquels le plugin peut supprimer des régions
worlds:
  # "default" s'applique à tous les mondes non spécifiés.
  boxed_world/seed_base:
    days-till-flag-expires: -1
  boxed_world/seed:
    days-till-flag-expires: -1
  default:
    # Les drapeaux plus anciens que x jours peuvent être ignorés et la région supprimée.
    # Définissez à -1 pour désactiver Regionerator dans un monde.
    # Pour désactiver le signalisation, définissez à 0.
    # days-till-flag-expires doit être supérieur à 0 pour être utilisé avec delete-new-unvisited-chunks
    days-till-flag-expires: 0
```

Pour tirer le meilleur parti de Regionerator, changez le fichier config.yml de BentoBox pour *ne pas* supprimer les chunks lorsqu'une île est supprimée. Cela laissera la suppression à sa charge et elle devrait nettoyer les chunks si la zone inutilisée est assez grande. La configuration consiste à définir `keep-previous-island-on-reset: true` :

```
deletion:
    # Bascule si les îles, lorsque les joueurs les réinitialisent, doivent être conservées dans le monde ou supprimées.
    # * S'il est défini à 'true', chaque fois qu'un joueur réinitialise son île, son île précédente deviendra non possédée et ne sera pas supprimée du monde.
    #   Cependant, vous pouvez toujours supprimer ces îles non possédées en purgeant.
    #   Sur les serveurs plus grands, cela peut entraîner une taille de monde croissante.
    #   Pourtant, cela permet aux administrateurs de récupérer l'ancienne île d'un joueur en cas d'utilisation incorrecte de la commande de réinitialisation.
    #   Les administrateurs peuvent en effet rajouter le joueur à son ancienne île en l'enregistrant.
    # * S'il est défini à 'false', chaque fois qu'un joueur réinitialise son île, son île précédente sera supprimée du monde.
    #   C'est le comportement par défaut.
    # Ajouté depuis 1.13.0.
    keep-previous-island-on-reset: true
```


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

## Traductions

{{ translations("Boxed") }}
