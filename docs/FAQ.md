# FAQ

## Installation

### Comment installer BentoBox, BSkyBlock et tous ces autres trucs d'addon ?

Le moyen le plus facile de commencer est de télécharger un « pack » d'addons et de BentoBox depuis [https://download.bentobox.world](https://download.bentobox.world).
Vous pouvez également consulter [ce tutoriel](BentoBox/Install-Bentobox.md) pour en savoir plus sur d'autres méthodes.
**Bienvenue dans notre communauté !**

## Configuration

### Comment créer mes propres îles personnalisées ?

Vous faites référence à notre **format de schéma maison** que nous appelons **_Plans directeurs_**.
La [page Plans directeurs](BentoBox/Blueprints.md) fournit toutes les informations pertinentes pour bien démarrer avec les Plans directeurs, ainsi que quelques conseils et astuces que vous pouvez utiliser pour les personnaliser davantage.
Vous pouvez également regarder [cette vidéo](https://youtu.be/4gvaG89uxAs) qui, bien qu'obsolète, pourrait vous aider à créer votre premier Plan directeur en quelques minutes.

### Quelle version de base de données est requise ?

Versions minimales requises :

* **MySQL** 5.7 ou ultérieur
* **MariaDB** 10.2.3 ou ultérieur
* **MongoDB** 3.6 ou ultérieur
* **SQLite** 3.28 ou ultérieur
* **PostgreSQL** la dernière version est toujours recommandée

### Comment augmenter la taille de l'île d'un joueur ?

Chaque île a une zone protégée. Vous pouvez augmenter la zone protégée jusqu'à la distance inter-îles. Les portées des îles peuvent être augmentées via des commandes ou en donnant une permission au propriétaire de l'île. Les permissions ne sont vérifiées que lorsqu'un joueur se connecte, donc si vous utilisez une permission uniquement, le joueur doit se reconnecter pour que cela fonctionne. Les commandes fonctionnent instantanément. Rappelez-vous que la plage protégée s'applique à l'île dans son ensemble.

**Permissions**

Accordez aux propriétaires la permission `[gamemode].island.range.<number>`.

* Le propriétaire de l'île devra se reconnecter sur le serveur pour appliquer les modifications
* Si le propriétaire de l'île change, la portée de l'île s'ajustera à la permission de portée du nouveau propriétaire, ou reviendra à la portée par défaut si le propriétaire n'a pas de permission.

**Commandes**

Utilisez les commandes `/[admin_command] range`.

## Problèmes

### Des chunks superflattes se génèrent dans mes mondes

*Problèmes pertinents :*
[BentoBox#1212](https://github.com/BentoBoxWorld/BentoBox/issues/1232),
[BSkyBlock#247](https://github.com/BentoBoxWorld/BSkyBlock/issues/247).

![Monde superflat](https://static.planetminecraft.com/files/resource_media/screenshot/1215/2012-04-15_205556_2000620.jpg)
*Un monde superflat. (Crédit : [1213videogamer sur PlanetMinecraft](https://www.planetminecraft.com/member/1213videogamer/)).*

Si vous commencez à voir des chunks superflattes se générer dans votre monde, c'est parce que le générateur de monde ne fonctionne plus pour le monde.
Il y a quelques raisons pour lesquelles cela pourrait se produire. Elles sont ordonnées selon leur probabilité.

**Nous vous recommandons fortement de revenir aux sauvegardes effectuées avant cette situation**.
Bien que nous fournissions des instructions pour vous aider à vous rétablir d'un tel événement au cas où vous n'auriez pas de sauvegardes disponibles, nous **ne garantissons pas leur efficacité**. De plus, ces solutions sont **conçues pour résoudre le problème autant que possible, cependant, en ignorant l'impact sur les performances ou les îles des joueurs**. Utilisez-les en toute connaissance de cause.

En tant que solution rapide, il existe un paramètre dans la console des paramètres d'administration pour supprimer les chunks superflattes. C'est l'outil principal pour réparer les dégâts, mais à moins de corriger la cause première, cela ne fera que causer un super lag et ne résoudra jamais le problème correctement.

En tout cas, **arrêtez immédiatement votre serveur pour éviter que d'autres dégâts soient causés à vos mondes**.

#### Causes

##### BentoBox ou le module de mode de jeu n'est plus en cours d'exécution

**Pourquoi ?**

BentoBox ou le module de mode de jeu n'est pas activé sur le serveur.
Cela peut se produire si vous avez mis à jour BentoBox ou le module de mode de jeu vers une version qui n'est pas compatible avec votre serveur ou qui est incompatible avec l'un de vos plugins.

**Solutions**

Enquêtez sur les raisons pour lesquelles BentoBox ou le module de mode de jeu n'est plus activé.
Lisez les logs pour trouver les erreurs au démarrage.
Essayez de démarrer votre serveur en ajoutant un seul plugin à la fois pour savoir quel plugin cause le problème.

##### Aucun générateur n'est défini pour ce monde dans le fichier `bukkit.yml`

**Pourquoi ?**

C'est souvent le cas.
Lors de la définition du monde par défaut de votre serveur comme monde du module de mode de jeu, vous avez oublié de spécifier le bon générateur pour ce monde dans le fichier `bukkit.yml`.

**Solutions**

Assurez-vous d'avoir suivi chaque étape de [ce tutoriel](BentoBox/Set-a-BentoBox-world-as-the-server-default-world.md) attentivement.

##### L'option `use-own-generator` de la configuration du mode de jeu est définie sur `true`

**Pourquoi ?**

C'est une erreur courante.

Les utilisateurs ont tendance à mal comprendre cette option en la considérant comme permettant d'activer un générateur de pierre à moudre « magique » (mais [c'est un addon](addons/MagicCobblestoneGenerator/index.md) !).
Ce n'est en fait pas à cela que sert cette option, et c'est clairement expliqué dans les commentaires entourant cette option dans le fichier de configuration :

```yaml
# Utilisez votre propre générateur de monde pour ce monde.
# Dans ce cas, le plugin ne générera rien.
# Si utilisé, vous devez spécifier le nom du monde et le générateur dans le fichier bukkit.yml.
# Voir https://bukkit.gamepedia.com/Bukkit.yml
use-own-generator: false
```

En fin de compte, cela peut aussi se produire si vous avez oublié de spécifier le nom du monde et le générateur dans le fichier `bukkit.yml`.

**Solutions**

Si vous n'envisagez pas d'utiliser un plugin externe pour générer le monde, vous devez redéfinir cette option sur `false`.

Au contraire, vous devez vous assurer que vous avez spécifié le nom du monde et le nom du plugin correspondant comme générateur dans le fichier `bukkit.yml`.

##### Un autre plugin essaie de contrôler le générateur de ce monde

**Pourquoi ?**

Bien que très rare, cela peut toujours se produire.

Certains plugins, en particulier ceux de gestion de mondes (par exemple Multiverse), ont tendance à fournir des paramètres qui pourraient remplacer le générateur de nos mondes.

**Solutions**

Examinez tous vos plugins pour savoir lequel est le plus susceptible de causer le problème.
Les plugins de gestion de mondes ou les plugins personnalisés qui interagissent avec les mondes doivent être étudiés en premier.
Signalez le problème à leurs développeurs ou corrigez les fichiers de configuration impliqués.

##### Il y a un bug dans BentoBox ou le module de mode de jeu

**Pourquoi ?**

*Oups !*

Aujourd'hui, c'est extrêmement rare.
Mais cela pourrait toujours se produire pour certaines raisons.

**Solutions**

Assurez-vous que c'est vraiment un bug lié à BentoBox : supprimez tous les plugins de votre serveur un par un jusqu'à ce que seul BentoBox soit resté.

Si le problème ne se produit plus, cela signifie qu'un autre plugin le cause.
Dans ce cas, veuillez vous référer à [cette section](https://bentobox-world.readthedocs.io/en/latest/FAQ/#another-plugin-is-trying-to-control-the-generator-of-this-world).

Si le problème persiste toujours, cela signifie que c'est un bug de BentoBox.
Veuillez le [signaler sur notre suivi des bugs](https://github.com/BentoBoxWorld/BentoBox/issues).

#### Comment nettoyer les chunks superflattes après ?

Si vous avez des sauvegardes, utilisez-les pour restaurer les mondes de votre serveur et les bases de données de BentoBox à leurs états précédents.

Si vous n'avez pas de sauvegardes, connectez-vous à votre serveur et ouvrez le panneau des paramètres d'administration en utilisant la commande `/[admin-command] settings`.
Trouvez le drapeau « *Clean Super Flat* » et activez-le.
Selon vos paramètres, vos locales et la version de BentoBox que vous exécutez, le nom, l'icône ou la description peuvent être différents.
Mais nous sommes sûrs que vous pourrez trouver ce drapeau par vous-même !

![image](https://user-images.githubusercontent.com/20014332/77770414-8256c380-7045-11ea-8ab6-8efe31d6fb87.png)
*Le drapeau Clean Super Flat dans le panneau des paramètres d'administration de BSkyBlock*.

Ce drapeau **régénérera lentement tous les chunks superflattes de votre monde au fil du temps**.
Cela se produit lorsque les chunks sont chargés, donc vous pourriez vouloir soit vous téléporter vers ces chunks pour forcer la régénération, soit laisser le drapeau activé pendant quelques jours.
**N'oubliez pas de désactiver le drapeau à un moment donné !**
C'est assez gourmand en ressources...

### Mon serveur lag quand un joueur crée son île !

Coller l'île ou générer les chunks sont les principales causes de ce problème.

Premièrement, la vitesse de collage peut être trop importante pour votre serveur.
Essayez de la réduire.
Cherchez ce paramètre dans le `config.yml` de BentoBox :

```yaml
# Nombre de blocs à coller par tick lors du collage des plans directeurs.
# Les valeurs plus petites aideront à réduire le lag notable mais rendront le collage un peu plus long.
# Au contraire, les valeurs plus grandes rendront le collage plus rapide, mais cet avantage est rapidement sévèrement impacté par la
# quantité résultante de chunks qui doivent être chargés pour accomplir le processus, ce qui souvent fait que le serveur perd patience.
paste-speed: 64
```

Si vous exécutez des timings, la tâche `BlueprintPaster` devrait idéalement prendre beaucoup de temps, tout en prenant un faible pourcentage du temps de tick.

Si le serveur continue à avoir du mal lors du collage d'îles, cela implique qu'il a du mal à générer les chunks.
C'est quelque chose sur lequel nous avons peu de contrôle en tant que plugin, mais voici quelques choses que vous pourriez faire pour atténuer cela :

* Essayez de réduire le paramètre « distance entre îles » dans le fichier de configuration du mode de jeu.
Les valeurs plus basses signifient moins de chunks à générer.
Cela nécessitera une réinitialisation complète des mondes et des bases de données.
* Utilisez Paper comme logiciel de serveur.
Paper gère la génération de chunks asynchrone.
* Pré-générez le monde.
Surtout pour les modes de jeu dont les générateurs sont gourmands en ressources, comme CaveBlock ou SkyGrid.

### Je ne peux pas placer de semis sur mon île !

*Problème pertinent :*
[BentoBox#277](https://github.com/BentoBoxWorld/BentoBox/issues/277).

Si aucun message n'apparaît au joueur lui disant qu'il ne peut pas placer le semis, cela signifie que BentoBox **ne cause pas** ce problème.

Si vous utilisez **GriefPrevention** sur votre serveur, il y a une [option de configuration](https://github.com/TechFortress/GriefPrevention/wiki/Setup-and-Configuration#preventing-tree-grief) dans ce plugin qui empêche les joueurs de placer les soi-disant « Sky Trees ».

### Comment changer la distance entre îles ?

Tous les modes de jeu ont une configuration pour la distance entre les îles des joueurs. Dans BSkyBlock, c'est appelé `distance-between-islands` et il se trouve dans le fichier config.yml ici :

```
# Rayon de l'île en blocs. (Donc la distance entre les îles est deux fois cela)
  # C'est pareil pour chaque dimension : Overworld, Nether et End.
  # Cette valeur ne peut pas être changée en milieu de jeu et le plugin ne démarrera pas si elle est différente.
  # /!\ BentoBox ne supporte actuellement pas le changement de cette valeur en milieu de jeu. Si vous avez besoin de la changer, faites une réinitialisation complète de vos bases de données et mondes.
  distance-between-islands: 400
```

Dans le cas de BSkyBlock, la valeur par défaut est 400, ce qui signifie que les joueurs seront espacés de 800 blocs. Cela signifie aussi qu'une zone de protection d'un joueur peut croître jusqu'à une valeur de 400.

La plupart du temps, le paramètre par défaut devrait être suffisant pour votre serveur. Cependant, certains administrateurs aiment espacer les joueurs encore plus, ou parfois les avoir plus près. Quoi que vous choisissiez, une fois le jeu en cours d'exécution, **vous ne pouvez pas changer cette valeur**. Si vous essayez de la changer, BentoBox refusera de démarrer et donnera un avertissement dans la console comme celui-ci :

```
[14:08:20 ERROR]: [BentoBox] *****************CRITIAL ERROR!******************
[14:08:20 ERROR]: [BentoBox] Island distance mismatch!
World 'bskyblock_world' distance 800 != island range 400!
Island ID in database is BSkyBlock99ea1c15-f5f8-410a-9019-d6b843a5a254.
Island distance in config.yml cannot be changed mid-game! Fix config.yml or clean database.
[14:08:20 ERROR]: [BentoBox] Could not load islands! Disabling BentoBox...
[14:08:20 ERROR]: [BentoBox] *************************************************
```
C'est un mécanisme de protection, car si vous changez la valeur et pouviez continuer, les îles pourraient finir les unes sur les autres et cela rendrait les joueurs très mécontents !

** Mais je viens de démarrer mon serveur ! Comment changer cette valeur et nettoyer la base de données ? **

Je vais supposer que vous utilisez la base de données JSON par défaut (fichier plat). Suivez ces étapes :

1. Arrêtez le serveur
2. Changez la valeur config.yml pour la distance entre îles à ce que vous voulez.
3. Si vous n'avez pas d'autres jeux BentoBox en cours d'exécution, ou si vous voulez juste tout réinitialiser, supprimez les dossiers `plugins/BentoBox/database` et `plugins/BentoBox/database_backup`
4. Supprimez les mondes que les modes de jeu ont créés, pour BSkyBlock, ce sont par défaut ces dossiers dans votre dossier serveur : `bskyblock_world`, `bskyblock_world_nether`, et `bskyblock_world_the_end`
5. Redémarrez le serveur.

Si vous avez déjà d'autres modes de jeu BentoBox en cours d'exécution sur votre serveur, les choses sont un peu plus complexes :
1. Arrêtez le serveur
2. Changez la valeur config.yml pour la distance entre îles à ce que vous voulez.
3. Ouvrez le dossier `plugins/BentoBox/database/Island` et supprimez tous les fichiers qui commencent par le nom de votre mode de jeu, par exemple, `BSkyBlock99ea1c15-f5f8-410a-9019-d6b843a5a254.json`
4. Supprimez les mondes que les modes de jeu ont créés, pour BSkyBlock, ce sont par défaut ces dossiers dans votre dossier serveur : `bskyblock_world`, `bskyblock_world_nether`, et `bskyblock_world_the_end`
5. Redémarrez le serveur.

Si vous utilisez d'autres bases de données comme MySQL, les étapes sont les mêmes, mais vous devrez utiliser des commandes SQL pour supprimer la base de données, les tables ou les entrées.


### Comment puis-je activer les portails du Nether pour se lier ensemble ?

Dans BentoBox 1.16, nous avons implémenté une option pour lier correctement les portails ensemble. Cependant, cette option ne fonctionne que si `allow-nether` est activé dans server.properties et `allow-end` dans bukkit.yml.

Pour activer la liaison des portails du Nether, vous devez trouver l'option dans la configuration du mode de jeu : `create-and-link-portals` et la définir sur `true`.

Pour activer la création d'une plateforme d'obsidienne correcte à la fin (comme dans la fin vanilla), vous devez trouver l'option `create-obsidian-platform` et la définir sur `true`.

Soyez conscient que l'activation de ces options ouvre les mêmes exploits avec la génération d'obsidienne illimitée que celui original de Minecraft.


## API

### Comment commencer à écrire des addons pour BentoBox ? Y a-t-il une API ?

Oui, il y a définitivement une API.
L'écriture d'addons est très similaire à l'écriture de plugins, sauf qu'il y a beaucoup plus d'API disponible pour des choses comme les équipes, les protections, les commandes, les panneaux et le collage.

Suivez [ce tutoriel](Tutorials/api/Create-an-addon.md) pour créer votre premier addon !
