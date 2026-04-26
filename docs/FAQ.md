# FAQ

Cette FAQ est ordonnée en fonction de la fréquence à laquelle chaque question revient sur le canal `#support-en` du [Discord BentoBox](https://discord.bentobox.world) — les questions les plus courantes sont en haut, et les problèmes rares ou hérités sont regroupés en bas.

!!! info "Pense-bête de diagnostic — exécutez ces commandes *avant* de demander de l'aide"
    - `/bentobox version` — affiche les versions de BentoBox + des compléments et le build du serveur
    - `/[admin_command] why <player>` — explique exactement quel flag BentoBox (le cas échéant) bloque l'action d'un joueur ; c'est de loin le moyen le plus rapide de déboguer les rapports « je ne peux pas casser/poser/interagir »
    - `/papi parse me <placeholder>` — vérifie si un placeholder PlaceholderAPI se résout effectivement sur votre serveur

## Sommaire

- [Installation et versions](#installation-et-versions)
- [Mondes et génération](#mondes-et-generation)
- [Mobs, apparition et entités](#mobs-apparition-et-entites)
- [Îles : taille, protection et réinitialisations](#iles-taille-protection-et-reinitialisations)
- [Équipes, coop et visiteurs](#equipes-coop-et-visiteurs)
- [Placeholders](#placeholders)
- [AOneBlock](#aoneblock)
- [Complément Level](#complement-level)
- [Complément Challenges](#complement-challenges)
- [Base de données et stockage](#base-de-donnees-et-stockage)
- [Personnalisation : locales, couleurs et blueprints](#personnalisation-locales-couleurs-et-blueprints)
- [Divers](#divers)
- [API et développement de compléments](#api-et-developpement-de-complements)
- [Problèmes moins courants / hérités](#problemes-moins-courants-herites)
- [Sources](#sources)

## Installation et versions

### Comment installer BentoBox, BSkyBlock et tous ces autres trucs d'addon ?

La façon la plus simple de commencer est de télécharger un « pack » de compléments et de BentoBox depuis [https://download.bentobox.world](https://download.bentobox.world).
Vous pouvez également consulter [ce tutoriel](BentoBox/Install-Bentobox.md) pour découvrir d'autres méthodes.
**Bienvenue dans notre communauté !**

### De quelle version de BentoBox ai-je besoin pour ma version de Minecraft ?

Les versions majeures de BentoBox suivent les versions de Minecraft :

- **BentoBox 3.x** — Minecraft **1.21.3 et plus récent**
- **BentoBox 2.7** — Minecraft **1.21.1**
- **BentoBox 2.6** — Minecraft **1.20.6**

Si vous mettez à niveau la version de Minecraft de votre serveur, vous devez également mettre à niveau BentoBox (et les compléments correspondants), et vice versa. Mélanger un BentoBox plus récent avec un Minecraft plus ancien empêchera le démarrage, et utiliser un ancien BentoBox sur un Minecraft plus récent provoque généralement des erreurs de particules manquantes, des « internal error occurred attempting to perform this command », ou des interfaces graphiques cassées. Les anciennes versions sont liées depuis la page *Releases* GitHub de chaque projet.

### De quelles versions de compléments ai-je besoin pour ma version de BentoBox ?

Choisissez des compléments dont les notes de version visent la même version majeure de BentoBox. Le moyen le plus simple est de télécharger un « pack » depuis [https://download.bentobox.world](https://download.bentobox.world), qui contient toujours un ensemble compatible. Mélanger BentoBox 3.x avec des compléments qui requièrent BentoBox 2.x (ou vice versa) est de loin la cause la plus fréquente d'échec de chargement des plugins.

### Pourquoi est-ce que ça affiche « internal error occurred attempting to perform this command » lorsque j'essaie de créer une île ?

Dans presque tous les cas, il s'agit d'une incompatibilité de version BentoBox/Minecraft (voir ci-dessus). Exécutez `/bentobox version` et vérifiez que la version majeure de BentoBox correspond à votre version de Minecraft. Si c'est le cas, partagez le journal complet du serveur (pas seulement l'erreur dans le chat) lorsque vous signalez le problème.

## Mondes et génération

### Comment faire d'un monde BentoBox le monde par défaut de mon serveur ?

Suivez [Définir un monde BentoBox comme monde par défaut du serveur](BentoBox/Set-a-BentoBox-world-as-the-server-default-world.md) étape par étape. Les deux choses que les gens manquent sont (1) définir le bon générateur pour le monde dans `bukkit.yml`, et (2) définir `level-name` dans `server.properties` au nom du monde BentoBox. Manquer l'un des deux provoque la génération de chunks superflat — voir [Des chunks superflat sont générés dans mes mondes](#des-chunks-superflat-sont-generes-dans-mes-mondes) au bas de cette page.

### Puis-je faire tourner deux modes de jeu (par ex. BSkyBlock et Boxed) sur le même serveur ?

Oui — vous ne pouvez pas faire tourner deux modes de jeu dans le **même monde**, mais chaque complément de mode de jeu BentoBox crée et gère ses propres mondes, donc installer plusieurs compléments de mode de jeu côte à côte vous donne simplement plusieurs ensembles de mondes. Les joueurs choisissent celui auquel ils veulent jouer avec la commande `/island` (ou `/box`, `/ob`, etc.) appropriée. Pour supprimer un mode de jeu, vous pouvez simplement supprimer le jar du complément ; supprimer les dossiers de mondes est optionnel.

### Comment réinitialiser complètement BentoBox / effacer toutes les îles ?

Arrêtez le serveur, supprimez les dossiers de mondes du mode de jeu (par ex. `bskyblock_world`, `bskyblock_world_nether`, `bskyblock_world_the_end`), et supprimez les fichiers correspondants dans `plugins/BentoBox/database/Island/` et `plugins/BentoBox/database/Players/` (ou les lignes correspondantes si vous utilisez SQL). Au prochain démarrage, BentoBox régénérera tout à neuf.

### Comment changer la distance entre les îles ?

Tous les modes de jeu ont une configuration pour la distance entre les îles des joueurs. Dans BSkyBlock, elle s'appelle `distance-between-islands` et se trouve dans le fichier config.yml ici :

```
# Rayon de l'île en blocs. (Donc la distance entre les îles est le double de cela)
  # C'est le même pour chaque dimension : Overworld, Nether et End.
  # Cette valeur ne peut pas être changée en cours de partie et le plugin ne démarrera pas si elle est différente.
  # /!\ BentoBox ne supporte actuellement pas le changement de cette valeur en cours de partie. Si vous devez la changer, faites une réinitialisation complète de vos bases de données et mondes.
  distance-between-islands: 400
```

Dans le cas de BSkyBlock, la valeur par défaut est 400, ce qui signifie que les joueurs commenceront à 800 blocs les uns des autres. Cela signifie également que la zone de protection d'un joueur peut atteindre une valeur de 400.

La plupart du temps, le paramètre par défaut devrait être suffisant pour votre serveur. Cependant, certains administrateurs aiment espacer davantage les joueurs, ou parfois les rapprocher. Quel que soit votre choix, une fois la partie en cours, **vous ne pouvez pas changer cette valeur**. Si vous essayez de la changer, BentoBox refusera de démarrer et donnera un avertissement dans la console comme ceci :

```
[14:08:20 ERROR]: [BentoBox] *****************CRITIAL ERROR!******************
[14:08:20 ERROR]: [BentoBox] Island distance mismatch!
World 'bskyblock_world' distance 800 != island range 400!
Island ID in database is BSkyBlock99ea1c15-f5f8-410a-9019-d6b843a5a254.
Island distance in config.yml cannot be changed mid-game! Fix config.yml or clean database.
[14:08:20 ERROR]: [BentoBox] Could not load islands! Disabling BentoBox...
[14:08:20 ERROR]: [BentoBox] *************************************************
```
C'est un mécanisme de protection, car si vous changez la valeur et étiez en mesure de continuer, les îles pourraient finir les unes sur les autres et cela conduirait à des joueurs très mécontents !

** Mais je commence juste mon serveur ! Comment changer cette valeur et nettoyer la base de données ? **

Je supposerai que vous utilisez la base de données JSON par défaut (fichier plat). Suivez ces étapes :

1. Arrêtez le serveur
2. Changez la valeur du config.yml pour la distance entre les îles à ce que vous voulez.
3. Si vous n'avez pas d'autres parties BentoBox en cours, ou voulez juste tout réinitialiser, alors supprimez les dossiers `plugins/BentoBox/database` et `plugins/BentoBox/database_backup`
4. Supprimez les mondes que les modes de jeu ont créés, pour BSkyBlock, ce sont par défaut ces dossiers dans le dossier de votre serveur : `bskyblock_world`, `bskyblock_world_nether`, et `bskyblock_world_the_end`
5. Redémarrez le serveur.

Si vous avez déjà d'autres modes de jeu BentoBox en cours sur votre serveur, alors les choses sont un peu plus complexes :
1. Arrêtez le serveur
2. Changez la valeur du config.yml pour la distance entre les îles à ce que vous voulez.
3. Ouvrez le dossier `plugins/BentoBox/database/Island` et supprimez tous les fichiers qui commencent par le nom de votre mode de jeu, par ex. `BSkyBlock99ea1c15-f5f8-410a-9019-d6b843a5a254.json`
4. Supprimez les mondes que les modes de jeu ont créés, pour BSkyBlock, ce sont par défaut ces dossiers dans le dossier de votre serveur : `bskyblock_world`, `bskyblock_world_nether`, et `bskyblock_world_the_end`
5. Redémarrez le serveur.

Si vous utilisez d'autres bases de données comme MySQL, alors les étapes sont les mêmes, mais vous devrez utiliser des commandes SQL pour supprimer la base de données, les tables ou les entrées.

### Comment activer la liaison entre les portails du Nether ?

Dans BentoBox 1.16, nous avons implémenté une option pour lier correctement les portails entre eux. Cependant, cette option ne fonctionne que si `allow-nether` est activé dans server.properties et `allow-end` dans bukkit.yml.

Pour activer la liaison des portails du Nether, vous devez trouver l'option dans la config du mode de jeu : `create-and-link-portals` et la définir sur `true`.

Pour activer la création d'une plateforme d'obsidienne d'End correcte (comme dans le End vanilla), vous devez trouver l'option `create-obsidian-platform` et la définir sur `true`.

Soyez conscient que l'activation de ces options ouvre les mêmes exploits avec une génération illimitée d'obsidienne que ceux du Minecraft original.

### Comment désactiver la génération de structures dans Boxed ?

Dans le `config.yml` de Boxed, il y a une liste `structures`. Supprimer des entrées de cette liste empêche ces structures d'être générées dans les nouvelles zones de boîte créées. Les boîtes existantes ne sont pas affectées.

### Puis-je utiliser Multiverse avec BentoBox ?

Multiverse fonctionne généralement avec la plupart des modes de jeu, **sauf Boxed et Poseidon**, qui nécessitent que leur propre générateur de monde soit défini dans `bukkit.yml`. Si vous utilisez Multiverse avec l'un d'eux, le monde ne se générera pas correctement. MyWorlds est une alternative populaire.

## Mobs, apparition et entités

### Pourquoi mes poissons, dauphins ou calmars n'apparaissent-ils que près de la bedrock à y -63 ?

C'est un [bug Mojang des mondes plats](https://github.com/BentoBoxWorld/BentoBox/issues/2593) qui affecte Minecraft 1.21.2+ : les mobs aquatiques n'apparaissent qu'au fond des mondes plats. Les nouveaux mondes BentoBox créés sur les versions récentes de BentoBox incluent le contournement. Les mondes existants nécessitent une édition NBT manuelle des données de niveau du monde — il n'y a pas de correction en jeu.

### Pourquoi les mobs n'apparaissent-ils pas du tout sur les îles ?

Exécutez `/op` et vérifiez la console du serveur en vous tenant sur l'île :

1. BentoBox affiche quel plugin (le cas échéant) a annulé l'apparition. Si rien n'est affiché, Minecraft n'a même pas tenté l'apparition — vérifiez les paramètres `spawn-limits` et `gamerule` dans `bukkit.yml`, votre plugin de monde (Multiverse, MyWorlds…) et les paramètres de `/[admin_command]`.
2. Vérifiez la section `world.spawn-limits` du `config.yml` du mode de jeu.
3. Pour les visiteurs qui ne peuvent pas être attaqués par des hostiles, regardez le flag *Protection des visiteurs*.

## Îles : taille, protection et réinitialisations

### Comment puis-je augmenter la taille de l'île d'un joueur ?

Chaque île a une zone protégée. Vous pouvez augmenter la zone protégée jusqu'à la distance entre îles. Il existe trois mécanismes et vous devez en choisir **un**, car ils sont mutuellement exclusifs dans certains modes de jeu (notamment Boxed) :

- **Permissions** — accordez `[gamemode].island.range.<number>` (par ex. `bskyblock.island.range.150`). Les permissions ne sont vérifiées que lorsqu'un joueur se connecte, donc le propriétaire doit se reconnecter pour qu'elles prennent effet. Si le propriétaire de l'île change, la portée de l'île s'ajustera à la permission du nouveau propriétaire, ou reviendra à la portée par défaut si le nouveau propriétaire n'en a pas.
- **Commande admin** — `/[admin_command] range set <player> <number>` — s'applique instantanément.
- **Avancements (Boxed uniquement, par défaut)** — la boîte grandit à mesure que le propriétaire débloque des avancements. Pour utiliser des commandes ou des permissions sur Boxed à la place, définissez `ignore-advancements: true` dans la config Boxed.

La portée de protection ne peut jamais dépasser la valeur `distance-between-islands` du mode de jeu. Souvenez-vous que la portée protégée s'applique à l'île dans son ensemble.

### Pourquoi ma zone Boxed rétrécit-elle à la valeur par défaut après chaque redémarrage ?

C'est le mode avancements en action : au démarrage, BentoBox recalcule la taille de la boîte à partir du nombre d'avancements que le propriétaire a débloqués. Soit donnez plus d'avancements au propriétaire, soit définissez `ignore-advancements: true` dans la config Boxed et utilisez plutôt des commandes/permissions.

### Comment empêcher les joueurs de voir les îles voisines ?

La valeur minimale de `distance-between-islands` qui cache les voisins est :

```
distance-between-islands ≥ portée_protection_max + (view-distance du serveur × 16) / 2
```

Par exemple, avec une portée de protection maximale de 50 (une île 100×100) et une distance de vue de 11 chunks :

```
distance-between-islands ≥ 50 + (11 × 16) / 2 = 138
```

`distance-between-islands` ne peut pas être changé en cours de partie sans une réinitialisation complète (voir [Comment changer la distance entre les îles ?](#comment-changer-la-distance-entre-les-iles)).

### Puis-je vendre des améliorations d'île / laisser les joueurs payer pour étendre leur île ?

BentoBox n'a pas de boutique intégrée. Les messages épinglés dans `#support-en` décrivent deux recettes communautaires : (1) utiliser le [complément Upgrades](addons/Upgrades/index.md) avec l'économie Vault, ou (2) utiliser n'importe quel plugin GUI/boutique externe pour accorder la permission `[gamemode].island.range.<number>` lors de l'achat.

### Pourquoi la bordure de l'île montre-t-elle la nouvelle taille mais le joueur ne peut toujours pas y construire ?

La bordure visuelle se trouve à la portée de protection. Si un joueur s'est vu accorder une permission de portée plus élevée mais ne s'est pas reconnecté, la bordure affiche toujours l'ancien rayon. Faites-le reconnecter (ou utilisez la commande admin range qui s'applique instantanément).

## Équipes, coop et visiteurs

### Quelle est la différence entre équipe, coop, trust et visite ?

- **Visiteur** — toute personne qui se téléporte ou marche sur l'île de quelqu'un d'autre. Par défaut, ils ne peuvent ni casser, ni poser, ni interagir avec la plupart des blocs.
- **Coop** — une amélioration temporaire accordée via `/island coop <player>`. Dure jusqu'à ce que le joueur se déconnecte (configurable). Les rangs coop peuvent être ajustés dans *Paramètres → Protection*.
- **Trust** — une amélioration persistante accordée via `/island trust <player>`. Survit à la déconnexion.
- **Membre d'équipe** — accordé via `/island team invite <player>`. L'invité doit accepter et **perd sa propre île dans le processus**. Il y a un seul propriétaire par île ; les membres de l'équipe ne sont pas propriétaires.
- **Promotion de propriétaire** — `/island team setowner <player>` transfère la propriété.

Pour tout ce qui précède, le rang exact requis pour chaque action de protection est configuré dans l'interface graphique `Settings` de l'île sous les onglets *Flags de protection* et *Rangs des commandes*.

### Comment laisser quelqu'un m'aider à construire sans lui donner mon île ?

Utilisez **trust**. Trust persiste à travers les déconnexions, et vous pouvez configurer exactement quelles actions les joueurs en confiance peuvent effectuer via le menu des paramètres de l'île.

## Placeholders

### Comment afficher un placeholder BentoBox dans le chat / tab / scoreboard ?

Vous avez besoin de [PlaceholderAPI](https://www.spigotmc.org/resources/placeholderapi.6245/) installé, et d'un plugin de chat/tab/scoreboard qui prend lui-même en charge PlaceholderAPI. Voir [Placeholders](BentoBox/Placeholders.md) pour la liste complète des placeholders disponibles. Pour vérifier qu'un placeholder fonctionne, exécutez :

```
/papi parse me %bentobox_island_name%
```

S'il retourne une valeur, le placeholder fonctionne et le problème vient de la configuration de votre plugin de chat/tab/scoreboard.

### Pourquoi `%Level_<gamemode>_island_level%` retourne-t-il vide ?

Trois vérifications, dans l'ordre :

1. Le complément Level est installé et activé pour ce mode de jeu.
2. Le joueur a effectivement exécuté `/[player_command] level` au moins une fois — par défaut, le niveau n'est calculé que lorsque le joueur exécute la commande. (Vous pouvez activer `calculate-level-on-login` dans la config du complément Level pour le calculer à la connexion à la place.)
3. `/papi parse me %Level_<gamemode>_island_level%` retourne un nombre lorsqu'il est exécuté par ce joueur. Si oui, le problème vient de votre plugin de chat/tab, pas de BentoBox.

## AOneBlock

### Comment ajouter des blocs personnalisés (ou des blocs ItemsAdder / Oraxen) à une phase ?

Modifiez le fichier de phase concerné dans `plugins/BentoBox/addons/AOneBlock/phases/`. Les fichiers de phase utilisent soit l'ancienne syntaxe courte, soit la syntaxe explicite `block-data` — voir l'exemple dans [Fichiers de configuration de phase AOneBlock](gamemodes/AOneBlock/index.md#phase-config-files). Pour les blocs ItemsAdder / Oraxen, vous aurez besoin de la forme bloc réelle (pas la forme objet) et votre entrée de phase doit utiliser `block-data` avec l'ID namespacé sous-jacent.

### Comment éditer le butin dans un coffre de phase ?

Placez un coffre, remplissez-le des objets que vous voulez, puis regardez-le et exécutez `/[admin_command] setchest`. Le contenu du coffre (et tout NBT de conteneur) est écrit dans le fichier de phase.

### Les joueurs apparaissent au spawn du monde au lieu d'obtenir une île à la première connexion — comment réparer ?

Dans le `config.yml` d'AOneBlock, activez l'option *create island on first login*. Sans elle, les joueurs qui rejoignent pour la première fois finissent au spawn du serveur et doivent exécuter `/island create` manuellement.

### Pourquoi le bloc magique casse-t-il les blocs voisins lorsqu'un grand mob apparaît ?

C'est intentionnel. AOneBlock efface les blocs à l'intérieur du cadre de délimitation de l'entité qui apparaît afin que les joueurs ne puissent pas piéger leur propre bloc magique en plaçant un cube au-dessus (ce qui tuerait immédiatement le mob qui apparaît). Le comportement peut être désactivé avec `mobs-clear-blocks: false` dans la config AOneBlock, au prix d'autoriser cet exploit.

## Complément Level

### Pourquoi mon Level n'est-il pas mis à jour en temps réel ?

Le niveau de l'île n'est calculé que lorsque le joueur exécute `/[player_command] level`, ou à la connexion si vous avez activé `calculate-level-on-login` dans la config du complément Level. Il n'y a pas de suivi continu — recalculer une île entière à chaque changement de bloc serait beaucoup trop coûteux.

### Pourquoi mes blocs personnalisés Oraxen / ItemsAdder / personnalisés ne sont-ils pas comptés ?

Le complément Level ne compte que les blocs listés dans son `blockconfig.yml`. Les blocs personnalisés des plugins item-adder doivent y être ajoutés explicitement avec la valeur que vous voulez qu'ils marquent. Si l'entrée est manquante, le bloc retombe sur la valeur de son bloc de base sous-jacent (ou zéro, si même celui-ci n'est pas listé).

### Devrais-je utiliser le complément Level avec Boxed ?

Généralement non — les mondes Boxed sont préremplis de terrain, donc le « niveau » d'une île est dominé par les chunks sous-jacents plutôt que par ce que le joueur a construit. Utilisez-le sur des modes de jeu de type vide (BSkyBlock, AOneBlock, AcidIsland) où il reflète réellement l'effort du joueur.

## Complément Challenges

### J'ai exécuté `/[admin_command] challenges` et le menu est vide — comment obtenir les défis par défaut ?

Ouvrez le menu, cliquez sur *Library*, choisissez un ensemble de défis par défaut (par ex. « default » pour BSkyBlock), et confirmez en tapant `confirm` dans le chat lorsque demandé. Les défis par défaut sont fournis avec le complément mais ne sont pas chargés automatiquement — vous devez les importer une fois par mode de jeu.

### Puis-je exécuter des défis depuis un monde différent / l'overworld ?

Non. Les défis sont liés au monde du mode de jeu dans lequel ils ont été créés. Si vous voulez du contenu de type quête dans votre overworld, vous aurez besoin d'un plugin de quêtes séparé.

## Base de données et stockage

### Quelle version de base de données est requise ?

Versions minimales requises :

* **MySQL** 5.7 ou ultérieur
* **MariaDB** 10.2.3 ou ultérieur
* **MongoDB** 3.6 ou ultérieur
* **SQLite** 3.28 ou ultérieur
* **PostgreSQL** la dernière est toujours recommandée

### Le dossier de mon monde BentoBox est énorme — comment le réduire ?

Les deux gros dévoreurs d'espace sont (1) les chunks générés par des joueurs qui ne sont jamais revenus, et (2) les anciennes régions d'île laissées après les réinitialisations. Pour récupérer de l'espace :

- **BentoBox 3.15.0+:** Utilisez `/[admin_command] purge <days>` — cette commande identifie désormais les îles obsolètes *et* supprime leurs fichiers de région en une seule étape. Pour les îles en suppression douce (marquées après une réinitialisation ou `/admin delete`), exécutez `/[admin_command] purge deleted` pour récupérer leurs fichiers de région. Redémarrez le serveur après le purge pour vider le cache de chunks de Paper.
- **BentoBox plus ancien :** Utilisez `/[admin_command] purge <days>` pour marquer les îles, puis `/[admin_command] purge regions` pour supprimer les fichiers de région.
- **Sauvegardez toujours le dossier du monde au préalable.**
- Pour les mondes vraiment anciens, un outil tiers comme Regionerator peut élaguer les chunks inutilisés.

### MariaDB vs MySQL — est-ce important ?

Oui. Dans le `config.yml` de BentoBox, vous devez définir le bon type de `database` : choisissez `MARIADB` si votre serveur est MariaDB, et `MYSQL` si votre serveur est MySQL. Le protocole filaire est similaire mais les pilotes JDBC et les listes de mots réservés diffèrent suffisamment pour que les confondre cause des erreurs de connexion ou de requête au démarrage.

### Comment migrer de JSON vers MySQL/MariaDB ?

Voir [Transition de base de données](BentoBox/Database-transition.md). En bref : arrêtez le serveur, changez le type de base de données dans `config.yml`, démarrez le serveur avec `database-transition` activé — BentoBox copie tous les enregistrements dans la nouvelle base de données au démarrage, puis désactivez `database-transition` et redémarrez.

## Personnalisation : locales, couleurs et blueprints

### Comment créer mes propres îles personnalisées ?

Vous parlez de notre **format de schematic interne** que nous appelons **_Blueprints_**.
La [page Blueprints](BentoBox/Blueprints.md) fournit toutes les informations pertinentes pour vous lancer avec les Blueprints, ainsi que quelques astuces et conseils que vous pouvez utiliser pour les personnaliser davantage.
Vous pouvez également jeter un œil à [cette vidéo](https://youtu.be/4gvaG89uxAs) qui, bien que dépassée, peut vous aider à créer votre premier Blueprint en quelques minutes.

### Comment changer une chaîne de langue / un message ?

Les fichiers de locale se trouvent sous `plugins/BentoBox/locales/` (cœur BentoBox) et `plugins/BentoBox/addons/<AddonName>/locales/` (chaque complément). Modifiez le fichier `<lang>.yml` concerné. Si vous ne voulez qu'une seule langue, définissez `default-language` dans le `config.yml` de BentoBox et retirez aux joueurs la permission de changer.

### Comment changer le préfixe de chat `[BentoBox]` ?

Regardez dans `plugins/BentoBox/locales/en-US.yml` (ou la locale que vous utilisez) pour une entrée sous `prefixes:`. Chaque complément peut également avoir son propre préfixe dans son fichier de locale.

### Comment utiliser des couleurs hex (RGB) dans les messages ?

Utilisez `&#RRGGBB`, par ex. `&#ff8800Bonjour` pour orange. Cela fonctionne partout où BentoBox accepte des codes de couleur. Notez que certains formateurs de chat externes peuvent avoir besoin de leur propre syntaxe hex — BentoBox ne peut pas contrôler cela.

### Où puis-je aider à traduire BentoBox dans ma langue ?

[https://download.bentobox.world/translate.html](https://download.bentobox.world/translate.html) — les traductions sont gérées via Crowdin et automatiquement intégrées dans les builds de release.

## Divers

### Pourquoi mon Magic Cobblestone Generator ne fait-il rien ?

Le joueur doit d'abord **activer** un générateur avec `/[player_command] generator` et en choisir un dans l'interface graphique. Placer simplement de la lave et de l'eau sans activer un générateur donnera de la pierre vanilla.

### Comment pré-générer des îles pour que les joueurs n'attendent pas ?

Il n'y a pas de pré-générateur intégré, mais vous pouvez scripter `/[admin_command] register <fakeplayer>` pour créer des îles à l'avance. Pour la pré-génération de chunks, utilisez un outil côté serveur comme Chunky.

## API et développement de compléments

### Comment commencer à écrire des compléments pour BentoBox ? Y a-t-il une API ?

Oui, il y a définitivement une API.
Écrire des compléments est très similaire à écrire des plugins sauf qu'il y a beaucoup plus d'API disponibles pour des choses comme les équipes, les protections, les commandes, les panneaux et le collage.

Suivez [ce tutoriel](Tutorials/api/Create-an-addon.md) pour créer votre premier complément !

## Problèmes moins courants / hérités

Les questions de cette section reviennent rarement maintenant, mais les réponses sont conservées ici pour les quelques serveurs qui les rencontrent encore.

### Des chunks superflat sont générés dans mes mondes

*Issues pertinentes :*
[BentoBox#1212](https://github.com/BentoBoxWorld/BentoBox/issues/1232),
[BSkyBlock#247](https://github.com/BentoBoxWorld/BSkyBlock/issues/247).

![Monde superflat](https://static.planetminecraft.com/files/resource_media/screenshot/1215/2012-04-15_205556_2000620.jpg)
*Un monde superflat. (Crédit : [1213videogamer sur PlanetMinecraft](https://www.planetminecraft.com/member/1213videogamer/)).*

Si vous commencez à voir des chunks superflat être générés dans votre monde, c'est parce que le générateur de monde ne fonctionne plus pour ce monde.
Il y a quelques raisons pour lesquelles cela peut se produire. Elles sont ordonnées selon leur probabilité.

**Nous vous recommandons fortement de revenir à des sauvegardes effectuées avant cette situation**.
Bien que nous fournissions des instructions pour aider à récupérer d'un tel événement au cas où vous n'auriez pas de sauvegardes disponibles, nous **ne garantissons pas leur efficacité**. De plus, ces solutions sont **conçues pour résoudre le problème autant que possible, mais en ignorant l'impact sur les performances ou les îles des joueurs**. Utilisez-les en connaissance de cause.

Comme solution rapide, il y a un paramètre dans la console des paramètres d'administration pour supprimer les chunks superflat. C'est l'outil principal pour réparer les dégâts, mais à moins que vous ne corrigiez la cause racine, cela causera juste un super lag et ne réparera jamais le problème correctement.

Dans tous les cas, **arrêtez votre serveur immédiatement pour empêcher d'autres dégâts d'être faits à vos mondes**.

#### Causes

##### BentoBox ou le complément du mode de jeu ne tourne plus

**Pourquoi ?**

BentoBox ou le complément du mode de jeu n'est pas activé sur le serveur.
Cela peut se produire si vous avez mis à jour BentoBox ou le complément du mode de jeu vers une version qui n'est pas compatible avec votre serveur ou qui est incompatible avec l'un de vos plugins.

**Solutions**

Enquêtez sur la raison pour laquelle BentoBox ou le complément du mode de jeu n'est plus activé.
Lisez les journaux pour trouver les erreurs au démarrage.
Essayez de démarrer votre serveur en ajoutant un seul plugin à la fois pour découvrir quel plugin est à l'origine du problème.

##### Aucun générateur n'est défini pour ce monde dans le fichier `bukkit.yml`

**Pourquoi ?**

C'est souvent la situation.
Lors de la définition du monde par défaut de votre serveur comme étant le monde du complément du mode de jeu, vous avez oublié de spécifier le bon générateur pour ledit monde dans le fichier `bukkit.yml`.

**Solutions**

Assurez-vous d'avoir suivi minutieusement chaque étape de [ce tutoriel](BentoBox/Set-a-BentoBox-world-as-the-server-default-world.md).

##### L'option `use-own-generator` de la config du mode de jeu est définie sur `true`

**Pourquoi ?**

C'est une erreur courante.

Les utilisateurs ont tendance à mal comprendre cette option comme leur permettant d'activer un générateur de pierre « magique » (mais [c'est un complément](addons/MagicCobblestoneGenerator/index.md) !).
Ce n'est en effet pas ce pour quoi cette option est conçue, et c'est clairement expliqué dans les commentaires entourant cette option dans le fichier de config :

```yaml
# Utilisez votre propre générateur de monde pour ce monde.
# Dans ce cas, le plugin ne générera rien.
# Si utilisé, vous devez spécifier le nom du monde et le générateur dans le fichier bukkit.yml.
# Voir https://bukkit.gamepedia.com/Bukkit.yml
use-own-generator: false
```

En fin de compte, cela peut aussi se produire si vous avez oublié de spécifier le nom du monde et le générateur dans le fichier `bukkit.yml`.

**Solutions**

Si vous ne prévoyez pas d'utiliser un plugin externe pour générer le monde, alors vous devriez remettre cette option à `false`.

Au contraire, vous devriez vous assurer d'avoir spécifié le nom du monde et le nom du plugin correspondant comme son générateur dans le fichier `bukkit.yml`.

##### Un autre plugin essaie de contrôler le générateur de ce monde

**Pourquoi ?**

Bien que très rare, cela peut quand même se produire.

Certains plugins, en particulier les plugins de gestion de monde (par ex. Multiverse), ont tendance à fournir des paramètres qui pourraient remplacer le générateur de nos mondes.

**Solutions**

Examinez tous vos plugins pour découvrir lequel est le plus susceptible de causer le problème.
Les plugins de gestion de monde ou ceux codés sur mesure qui interagissent avec les mondes doivent être enquêtés en premier.
Soit signalez le problème à leurs développeurs, soit corrigez les fichiers de configuration concernés.

##### Il y a un bug dans BentoBox ou dans le complément du mode de jeu

**Pourquoi ?**

*Oups !*

De nos jours, c'est extrêmement rare.
Mais cela peut encore se produire pour certaines raisons.

**Solutions**

Assurez-vous qu'il s'agit bien d'un bug lié à BentoBox : retirez tous les plugins de votre serveur un par un jusqu'à ce qu'il ne reste que BentoBox.

Si le problème ne se produit plus, cela signifie qu'un autre plugin en est la cause.
Dans ce cas, veuillez vous référer à [cette section](https://bentobox-world.readthedocs.io/en/latest/FAQ/#another-plugin-is-trying-to-control-the-generator-of-this-world).

Si le problème persiste, cela signifie qu'il s'agit d'un bug BentoBox.
Veuillez [le signaler sur notre traqueur de bugs](https://github.com/BentoBoxWorld/BentoBox/issues).

#### Comment nettoyer les chunks superflat par la suite ?

Si vous avez des sauvegardes, utilisez-les pour rétablir les mondes de votre serveur et les bases de données BentoBox à leurs états précédents.

Si vous n'avez pas de sauvegardes, connectez-vous à votre serveur et ouvrez le Panneau des Paramètres d'Administration en utilisant la commande `/[admin-command] settings`.
Trouvez le flag « *Clean Super Flat* » et activez-le.
Selon vos paramètres, vos locales et la version de BentoBox que vous utilisez, le nom, l'icône ou la description peuvent être différents.
Mais nous sommes sûrs que vous pourrez trouver ce flag par vous-même !

![image](https://user-images.githubusercontent.com/20014332/77770414-8256c380-7045-11ea-8ab6-8efe31d6fb87.png)
*Le flag Clean Super Flat dans le Panneau des Paramètres d'Administration de BSkyBlock*.

Ce flag **régénérera lentement tout chunk superflat de votre monde au fil du temps**.
Cela se produit lorsque les chunks sont chargés, donc vous voudrez peut-être soit vous téléporter vers lesdits chunks pour forcer la régénération, soit laisser le flag activé pendant quelques jours.
**N'oubliez pas de désactiver le flag à un moment donné !**
C'est assez gourmand en ressources...

### Mon serveur lague quand un joueur crée son île !

Le collage de l'île ou la génération des chunks sont les principales causes de ce problème.

Tout d'abord, la vitesse de collage peut être trop élevée pour votre serveur.
Essayez de la baisser.
Regardez dans le `config.yml` de BentoBox pour ce paramètre :

```yaml
# Nombre de blocs à coller par tick lors du collage de blueprints.
# Des valeurs plus petites aideront à réduire le lag perceptible mais rendront le collage légèrement plus long.
# Au contraire, des valeurs plus grandes rendront le collage plus rapide, mais ce bénéfice est rapidement sévèrement impacté par
# le nombre de chunks qui doivent être chargés pour accomplir le processus, ce qui fait souvent figer le serveur.
paste-speed: 64
```

Si vous exécutez les timings, la tâche `BlueprintPaster` devrait idéalement prendre longtemps, tout en prenant un faible pourcentage du temps d'un tick.

Si le serveur peine encore lors du collage des îles, cela implique qu'il peine à générer les chunks.
C'est quelque chose sur lequel nous avons peu de contrôle en tant que plugin, mais voici quelques choses que vous pourriez faire pour atténuer cela :

* Essayez de réduire le paramètre « distance entre îles » dans le fichier de config du mode de jeu.
Des valeurs plus basses signifient moins de chunks à générer.
Cela vous obligera à réinitialiser entièrement les mondes et les bases de données.
* Utilisez Paper comme logiciel de serveur.
Paper gère la génération asynchrone des chunks.
* Pré-générez le monde.
Surtout pour les modes de jeu dont les générateurs sont gourmands en ressources, comme CaveBlock ou SkyGrid.

### Je ne peux pas placer de pousses sur mon île !

*Issue pertinente :*
[BentoBox#277](https://github.com/BentoBoxWorld/BentoBox/issues/277).

Si aucun message n'apparaît au joueur lui disant qu'il ne peut pas placer la pousse, alors cela signifie que BentoBox **n'est pas** la cause de ce problème.

Si vous utilisez **GriefPrevention** sur votre serveur, il y a une [option de config](https://github.com/TechFortress/GriefPrevention/wiki/Setup-and-Configuration#preventing-tree-grief) dans ce plugin qui empêche les joueurs de placer ce qu'on appelle des « Sky Trees ».

## Sources

Les entrées issues de Discord ci-dessus ont été tirées du canal `#support-en` entre janvier 2025 et avril 2026. Exemples de discussions (une par sujet, pour le contexte) :

- Versions et compatibilité — [discussion discord](https://discord.com/channels/272499714048524288/310623455462686720/1490517535152410745)
- Mondes et génération — [discussion discord](https://discord.com/channels/272499714048524288/310623455462686720/1488648048589672488)
- Apparition de mobs — [discussion discord](https://discord.com/channels/272499714048524288/310623455462686720/1475550306799583316)
- Permissions et rangs — [discussion discord](https://discord.com/channels/272499714048524288/310623455462686720/1480457734842220566)
- Création et réinitialisation d'île — [discussion discord](https://discord.com/channels/272499714048524288/310623455462686720/1468577190126948455)
- Taille et protection des îles — [discussion discord](https://discord.com/channels/272499714048524288/310623455462686720/1471174102957031506)
- Équipes et coop — [discussion discord](https://discord.com/channels/272499714048524288/310623455462686720/1467986323137757357)
- Placeholders — [discussion discord](https://discord.com/channels/272499714048524288/310623455462686720/1465642012341698713)
- Complément Level — [discussion discord](https://discord.com/channels/272499714048524288/310623455462686720/1459181292175360162)
- AOneBlock — [discussion discord](https://discord.com/channels/272499714048524288/310623455462686720/1466486743287988346)
- Challenges — [discussion discord](https://discord.com/channels/272499714048524288/310623455462686720/1426655803473133795)
- Base de données et stockage — [discussion discord](https://discord.com/channels/272499714048524288/310623455462686720/1461304120668323910)
- Localisation — [discussion discord](https://discord.com/channels/272499714048524288/310623455462686720/1482135823947272203)
- Complément Border — [discussion discord](https://discord.com/channels/272499714048524288/310623455462686720/1462044129448951872)
- Complément Bank — [discussion discord](https://discord.com/channels/272499714048524288/310623455462686720/1440031441995169833)
- BSkyBlock — [discussion discord](https://discord.com/channels/272499714048524288/310623455462686720/1486436566032318474)
- Boxed — [discussion discord](https://discord.com/channels/272499714048524288/310623455462686720/1415368394374647948)
- Erreurs et plantages — [discussion discord](https://discord.com/channels/272499714048524288/310623455462686720/1441184039175327757)
