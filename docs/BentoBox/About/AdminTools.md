# Outils d'Administration

BentoBox donne aux administrateurs de serveur une gamme d'outils pour gérer le jeu, enquêter sur les problèmes et garder les choses fonctionnant correctement — tout sans avoir besoin d'éditer les fichiers manuellement.

## Le Panneau de Gestion

Le hub administrateur principal est le **Panneau de Gestion**, ouvert avec :
```
/bentobox manage
```
(ou son alias `/bbox manage`)

De là, vous pouvez voir tous les modes de jeu exécutés, les îles actives et la santé du serveur de base en un coup d'œil.

## La Commande `/bentobox`

Toute l'administration BentoBox de haut niveau passe par `/bentobox` (alias `/bbox`) :

| Commande | Qu'est-ce qu'elle fait |
|---|---|
| `/bentobox version` | Affiche la version de BentoBox et tous les compléments chargés. **Incluez toujours ceci lors de la déclaration de bugs.** |
| `/bentobox manage` | Ouvre le Panneau de Gestion Interface Graphique |
| `/bentobox reload` | Recharge les fichiers de configuration BentoBox et les locales sans redémarrage du serveur complet |
| `/bentobox catalog` | Ouvre le catalogue de compléments |
| `/bentobox perms` | Affiche les permissions effectives pour BentoBox et tous les compléments |
| `/bentobox rank` | Liste, ajoute ou supprime les rangs personnalisés |

## Commandes d'Administration par Mode de Jeu

Chaque mode de jeu a sa propre commande d'administration. Pour BSkyBlock c'est `/bsb`, pour AcidIsland c'est `/acid admin`, et ainsi de suite. Celles-ci vous donnent les contrôles spécifiques à ce mode de jeu :

| Commande | Qu'est-ce qu'elle fait |
|---|---|
| `/[admin] info <player>` | Affiche les détails complets de l'île d'un joueur |
| `/[admin] delete <player>` | Supprime l'île d'un joueur |
| `/[admin] delete` | *(3.19.0)* Sans argument joueur, supprime en douceur l'île sur laquelle vous **êtes debout** après confirmation (refusé si elle a encore une équipe) |
| `/[admin] undelete` | *(3.19.0)* Efface l'état de suppression en attente de l'île sur laquelle vous **êtes debout**, la laissant sans propriétaire, avant que ses fichiers de région ne soient purgés |
| `/[admin] register <player>` | Enregistre une île sans propriétaire à un joueur. Sur une île en attente de suppression, cela affiche désormais une invite de confirmation et annule la suppression au lieu de refuser |
| `/[admin] setrange <player> <range>` | Change la plage de protection de l'île d'un joueur |
| `/[admin] range removebonus <player> [id]` | Supprime tous les bonus de plages de protection d'une seule île, ou seulement ceux d'un id donné |
| `/[admin] range purgebonus <id>` | Supprime un id de plage de bonus de **toutes** les îles du monde — idéal après désinstallation d'un addon qui accordait des bonus de plages. L'analyse s'exécute de façon asynchrone pour ne pas geler les gros serveurs |
| `/[admin] settings` | Ouvre le panneau des paramètres mondiaux pour les administrateurs |
| `/[admin] settings <player>` | Ouvre le panneau des paramètres de l'île pour un joueur spécifique |
| `/[admin] why <player>` | Commence à suivre pourquoi un joueur peut ou ne peut pas faire quelque chose (voir ci-dessous) |
| `/[admin] reload` | Recharge la configuration du mode de jeu |
| `/[admin] blueprint` | Ouvre l'Interface Graphique du Gestionnaire de Blueprint |

Le préfixe de commande administrateur exact dépend de la configuration du mode de jeu. Vérifiez la documentation du mode de jeu pour sa commande spécifique.

## L'Outil de Diagnostic « Why »

L'un des outils administrateur les plus utiles est la commande `why`. Si un joueur signale qu'il ne peut pas faire quelque chose sur son île (ou qu'il *peut* faire quelque chose qu'il ne devrait pas), exécutez :

```
/[admin_command] why <player>
```

Après cela, la console du serveur enregistrera la raison de chaque action que ce joueur prend — si elle a été autorisée ou bloquée, et quel drapeau de protection l'a causée. Cela facilite le diagnostic des permissions mal configurées sans deviner.

Pour arrêter le suivi, exécutez à nouveau la commande.

## Panneau des Paramètres Administrateur

Le panneau des paramètres administrateur (ouvert avec `/[admin] settings`) contrôle les défauts à l'échelle mondiale — les paramètres qui s'appliquent partout dans le monde du mode de jeu, pas seulement sur une île. Cela inclut :

- Drapeaux de protection par défaut pour les nouvelles îles
- Restrictions à l'échelle mondiale (par ex. dégâts d'explosion creeper, comportement du piston)
- Paramètres de visibilité du panneau de paramètres du joueur (masquez les drapeaux que vous ne voulez pas que les joueurs changent)

Voir [Protection](Protections.md) pour une explication complète du système de drapeaux.

## Contrôle Basé sur les Permissions

BentoBox est fortement basé sur les permissions. Presque tout — du nombre de foyers qu'un joueur peut avoir, à s'il peut voler, à la taille de son île — peut être contrôlé en accordant ou en refusant les permissions via votre plugin de permissions (par ex. LuckPerms).

!!! tip
    Exécutez `/bentobox perms` dans la console pour voir une liste de toutes les permissions enregistrées par BentoBox et ses compléments au format YAML. C'est utile pour configurer votre plugin de permissions.

## Gestion de la Base de Données

BentoBox supporte plusieurs bases de données pour stocker les données des îles et des joueurs :

- **JSON (fichier plat)** — la valeur par défaut ; facile à configurer, aucun logiciel supplémentaire nécessaire
- **MySQL** (5.7+)
- **MariaDB** (10.2.3+)
- **MongoDB** (3.6+)
- **SQLite** (3.28+)
- **PostgreSQL**

Le type de base de données est défini dans le `config.yml` BentoBox. Pour migrer d'un type de base de données à un autre sans perdre de données, utilisez :
```
/bentobox migrate
```

!!! warning
    Faites toujours une sauvegarde complète avant de migrer les bases de données.

## Rechargement sans Redémarrage

Après avoir modifié un fichier de configuration, vous pouvez l'appliquer sans redémarrer entièrement le serveur :
```
/bentobox reload
```
Cela recharge BentoBox et tous les compléments, y compris les locales. Notez que certains changements (comme les paramètres de génération de monde) nécessitent toujours un redémarrage complet pour prendre effet.

## Journal des modifications

!!! note "Nouveautés dans v3.22.3 — désactivation de bStats et Paper 26.2"
    **Publié :** 22 août 2026

    Principalement une version de correction de bugs et d'API. Compatibilité : Paper Minecraft 1.21.5 – 26.2, Java 25+.

    - ⚙️ **Désactivation des métriques bStats.** Une nouvelle option `general.metrics` dans `config.yml` (par défaut **`true`**) vous permet de désactiver les statistiques d'utilisation anonymes et agrégées de BentoBox sans toucher au commutateur global dans `plugins/bStats/config.yml`, qui désactive bStats pour tous les plugins du serveur. Réglez-la à `false` et **redémarrez** — le collecteur est enregistré au démarrage, donc `/bbox reload` ne suffit pas. Aucune donnée personnelle n'est jamais envoyée ; consultez [Confidentialité et collecte de données](../Privacy.md).
    - 🔺 **Construit contre Paper 26.2 et Adventure 5.** Auteurs d'addons : Adventure 5 scelle `Component` (Mockito ne peut plus le simuler) et remplace `ClickEvent.value()` par `payload()`. Les addons déjà déployés sur un serveur 26.2 peuvent être affectés à l'exécution ; recompiler contre BentoBox 3.22.3 met à surface les problèmes à la compilation — consultez [PR #3067](https://github.com/BentoBoxWorld/BentoBox/pull/3067) pour la liste complète des suppressions. Les administrateurs du serveur n'ont rien à faire.
    - 🔲 **Disposition de grille de dialogue pour les développeurs d'addons.** `DialogBuilder#columns(int)` dispose les boutons d'un dialogue multi-action dans une grille au lieu de la liste par défaut de deux colonnes, et `DialogButton` gagne une largeur (1–1024) plus `withWidth(int)`. Les appelants existants ne sont pas affectés.
    - 🐛 **Les erreurs HTTP 429 des têtes de joueur arrêtées.** L'ouverture d'un panneau avec des têtes de joueur (une liste top-dix, par exemple) pouvait inonder la console d'erreurs HTTP 429 de `sessionserver.mojang.com`, car les têtes livrées sans données de texture étaient re-résolues à chaque ouverture. Les têtes sans texture se dégradent maintenant en une tête simple, et une récupération échouée n'évince plus une tête en cache qui fonctionne déjà.
    - 🐛 **Les nombres YAML se chargent dans le type de champ déclaré.** Une valeur de configuration telle que `20`, écrite sans point décimal, se charge maintenant correctement dans les champs `double`, `float` et `long` au lieu de lever `ClassCastException`.
    - 🐛 **Les noms de couleur littéraux dans les panneaux.** Le panneau de gestion affichait les noms d'addons comme `whiteChallenges` après une refonte des couleurs ; corrigé.
    - 📄 Schémas JSON publiés (brouillon 2020-12) pour les formats de fichier `.blueprint` et bundle de modèles.

    [Release v3.22.3](https://github.com/BentoBoxWorld/BentoBox/releases/tag/3.22.3)

??? note "Nouveautés dans v3.22.2"
    **Publié :** 10 août 2026

    Un correctif de bug au-dessus de la 3.22.0 — pas de nouvelles fonctionnalités, clés de configuration ou modifications de locale ; un remplacement sans problème. Il n'y a pas de version 3.22.1. Compatibilité : Paper Minecraft 1.21.5 – 26.2, Java 25+.

    - 🔺 🐛 **Les recherches de noms de joueurs se résolvent au bon compte.** `/[player_command] team trust <name>` et `/[player_command] info <name>` pouvaient répondre silencieusement pour un UUID qui n'avait pas porté ce nom depuis des mois : les enregistrements de noms remplacés n'étaient jamais supprimés de la base de données, et la recherche prenait la première correspondance. Les noms sont maintenant appairés sans tenir compte de la casse, les enregistrements périmés sont supprimés, et les joueurs en ligne sont vérifiés en premier. **Faites une sauvegarde avant la mise à jour** — les bases de données existantes se réparent au fil de la connexion des joueurs (la purge s'exécute une fois par renommage, pas par connexion) et aucune migration manuelle n'est nécessaire.
    - 🐛 **Les joueurs Bedrock peuvent à nouveau utiliser les panneaux.** Geyser développe un appui en plusieurs paquets de clic Java dans le même tick, et la vérification `panel.click-cooldown-ms` introduite dans 3.22.0 avalait celle qui importait — chaque appui recevait `slow-down` et rien ne se produisait. Les clics du même tick sont maintenant traités comme un geste ; la protection contre les abus reste inchangée à un clic porteur d'action par tick.
    - 🐛 **Un addon désactivé ne laisse plus les commandes cassées derrière lui.** Un mode de jeu abandonné pour une dépendance manquante (ChunkBlock sans Level, par exemple) conservait ses commandes enregistrées, et chaque sous-commande levait une NPE. Les commandes, les drapeaux et les écouteurs sont maintenant tous retirés quand un addon échoue à s'activer.
    - 🐛 **Revenir d'un nether standard vous débarque sur votre propre île.** Avec un nether partagé et `create-and-link-portals: false` (le défaut d'AOneBlock), les joueurs revenant par un portail étaient débarqués sur l'île qui s'assied la plus proche de 0,0. La destination tombe maintenant sur l'emplacement personnel de l'île.

    [Release v3.22.2](https://github.com/BentoBoxWorld/BentoBox/releases/tag/3.22.2)

??? note "Nouveautés dans v3.22.0 — commandes Brigadier"
    **Publié :** 1er août 2026

    Une version consacrée aux commandes et à leur visibilité. Compatibilité : Paper Minecraft 1.21.5 – 26.2, Java 25+.

    - ⚙️ 🔺 **Les commandes sont désormais enregistrées via l'API Brigadier de Paper.** Les joueurs voient les sous-commandes et les complétions de BentoBox *pendant* qu'ils tapent — `/island t…` propose `team` directement dans la barre de chat — au lieu que le client ne sache rien avant la touche entrée ou TAB. L'arbre des sous-commandes est annoncé jusqu'à une profondeur de 4 ; les sous-commandes plus profondes fonctionnent toujours, elles ne sont simplement pas annoncées à l'avance. Les alias et la forme `plugin:label` sont envoyés comme des redirections plutôt que comme des arbres dupliqués. Une nouvelle option `general.brigadier-commands` dans `config.yml` est activée **par défaut** ; passez-la à `false` puis lancez `/bbox reload` pour revenir à l'ancienne command map si un autre plugin entre en conflit. BentoBox bascule également automatiquement s'il ne parvient pas à s'accrocher au registrar.
    - 🔺 **Les recherches de structures sont supprimées automatiquement dans les mondes qui n'en génèrent pas.** Un cartographe tirant un échange de carte d'explorateur — ou un Œil de l'Ender, un dauphin, une carte au trésor — lançait une recherche de structure synchrone qui ne pouvait jamais aboutir dans un monde vide : elle balayait jusqu'à la limite du rayon et dépassait le chien de garde de 60 secondes. BentoBox demande maintenant au générateur du monde s'il place des structures et saute la recherche dans le cas contraire, **sans aucune configuration**. AOneBlock et BSkyBlock en bénéficient automatiquement ; SkyGrid, Boxed, CaveBlock et AcidIsland ne sont pas concernés puisqu'ils génèrent bien des structures. Une entrée `structures` à `true` par monde force toujours l'activation d'une structure, ce qui sert de porte de sortie pour les mondes convertis contenant des structures préexistantes. Cela complète la liste `world.disabled-structures`, optionnelle, ajoutée en 3.20.0.
    - **`/island settings` s'ouvre désormais en plein monde.** Les joueurs qui ne se trouvaient sur aucune île et n'en possédaient pas obtenaient auparavant « Vous n'avez pas d'île ! ». Le panneau s'ouvre maintenant avec un onglet **Protections du monde** en lecture seule, indiquant quels drapeaux de protection sont actifs pour le monde — c'est-à-dire exactement ce qui régit le joueur là où il se tient. Voir [Protection](Protections.md#consulter-les-regles-du-monde-hors-ile).
    - 🐛 **Les données mises en file d'attente par les addons pendant l'arrêt ne sont plus jetées.** Tout ce qu'un addon enregistrait depuis `onDisable()` était mis en file dans un pipeline de base de données qui avait déjà cessé de se vider, ce qui provoquait une perte de données silencieuse et intermittente à chaque redémarrage. Neuf addons fournis enregistrent leur état à la désactivation : Boxed, AOneBlock, Raft, Challenges, Limits, DragonFights, CheckMeOut, ControlPanel et InvSwitcher. Avec InvSwitcher, l'inventaire stocké périmé était ensuite réappliqué à la connexion, ce qui en faisait un retour en arrière et non une simple écriture perdue. Les écritures d'arrêt sont maintenant vidées avant la fermeture de la base de données.
    - 🐛 **Les commandes BentoBox fonctionnent de nouveau depuis les PNJ, les panneaux et les plugins d'interface.** L'enregistrement Brigadier avait sorti les commandes BentoBox de la command map Bukkit par laquelle les autres plugins passent, si bien qu'un PNJ exécutant `/oneblock go` renvoyait le message de permission refusée du serveur sans rien exécuter. Les commandes sont désormais également enregistrées dans la command map. Cela n'a affecté que les builds de développement de la 3.22.0.
    - 🐛 **`Island.setFlag` ne jette plus les écritures.** Définir un rang de protection sur une île qui n'avait pas encore d'entrée pour ce drapeau — c'est-à-dire toute île fraîchement créée — ne faisait silencieusement rien. Les drapeaux `SETTING` et `WORLD_SETTING` n'étaient pas concernés.
    - 🐛 **Les avertissements répétés restent limités.** Un joueur alternant entre deux messages de limite différents contournait entièrement le délai de 4 secondes entre notifications. Chaque message distinct est maintenant limité indépendamment.
    - 🐛 **Les jeux de marqueurs BlueMap restent dans leur propre monde.** Le jeu de marqueurs d'un addon n'apparaît plus dans la barre latérale de toutes les autres cartes du serveur, et `createMarkerSet()` / `removeMarkerSet()` ne lèvent plus d'exception pendant un `/bluemap reload`.
    - 🐛 **Ménage côté Multiverse.** Les mondes BentoBox reçoivent désormais `auto-load: false` même lorsque Multiverse les connaissait déjà, et l'enregistrement obsolète du monde de graine (`<world>/bentobox`) a été supprimé. Les entrées résiduelles existantes nécessitent toujours `/mv remove`.
    - 🐛 **Les drapeaux des addons écartés faute de dépendance sont nettoyés.** Un addon dont la dépendance obligatoire était absente avait déjà enregistré ses drapeaux et ses écouteurs avant d'être écarté, laissant des écouteurs se déclencher pour un monde qui n'a jamais existé.
    - **Six nouveaux graphiques bStats** indiquent les versions des addons et des modes de jeu, les niveaux d'API des addons, les paramètres modifiés par rapport à leurs valeurs par défaut, ainsi que comment et où les commandes échouent. Seuls le type d'échec et une clé de commande stable dérivée de la permission sont transmis — jamais les arguments ni les noms de joueurs.
    - 🔡 **Ajout de la traduction en chinois traditionnel (`zh-TW`)**, contribuée par @qwe664. Aucune clé de traduction existante n'a changé, les fichiers de langue personnalisés ne demandent donc aucun travail.

    [Release v3.22.0](https://github.com/BentoBoxWorld/BentoBox/releases/tag/3.22.0)

??? note "Nouveautés dans v3.21.0 — boîtes de dialogue modales"
    **Publié :** 22 juillet 2026

    Une version axée sur l'expérience joueur. Compatibilité : Paper Minecraft 1.21.5 – 26.2, Java 25+.

    - ⚙️ 🔡 **Boîtes de dialogue modales pour les actions à friction élevée.** Les confirmations de commandes sensibles, le sélecteur de destination de `/island go`, les invitations d'équipe et le choix du mode de jeu à la première connexion peuvent désormais apparaître sous forme de véritables boîtes de dialogue modales, que le joueur ne peut ni mal lire ni faire défiler sans les voir. Une nouvelle section `island.dialogs` dans `config.yml` contient un commutateur par flux — `confirmations`, `go-picker` et `team-invites` sont **activés** par défaut, `game-mode-selection` est **désactivé** par défaut car il est intrusif par conception. Les boîtes de dialogue nécessitent un serveur Minecraft 26+ ; sur toute version antérieure, chaque commutateur est ignoré et le comportement classique en chat/commande est utilisé, donc aucune action n'est nécessaire.
    - **Correspondance tolérante pour `/island go`.** `/island go myisland`, `hom`, ou un nom saisi avec la mauvaise casse ou une double espace parasite téléporte désormais le joueur là où il le souhaitait, au lieu d'échouer sur une correspondance exacte et d'afficher la liste complète. Voir [Emplacements du Foyer](IslandManagement.md#emplacements-du-foyer).
    - 🔡 **Note sur les locales :** de nouvelles clés de dialogue (`general.dialogs.*`, ainsi que des clés de dialogue et de sélecteur sous les commandes de confirmation, `island go` et d'invitation d'équipe) ont été ajoutées aux 22 locales fournies. Régénérez ou mettez à jour tout fichier de locale personnalisé.
    - 🔧 **Les développeurs de compléments** disposent de la même API `world.bentobox.bentobox.api.dialogs` que celle utilisée par le cœur — voir [Boîtes de dialogue modales](../Developer-Documentation.md#boites-de-dialogue-modales).

    [Release v3.21.0](https://github.com/BentoBoxWorld/BentoBox/releases/tag/3.21.0)

??? note "Nouveautés dans v3.20.0 — suggestions de commandes & suppression des structures dans le cœur"
    **Publié :** 11 juillet 2026

    Une version de confort. Compatibilité : Paper Minecraft 1.21.5 – 26.2, Java 25+. Rien ne change à la mise à niveau, sauf si vous activez explicitement une option.

    - 🔡 ⚙️ **Suggestions de commandes « vouliez-vous dire ».** Une commande mal tapée comme `/teams` ou `/island invit Floris` propose désormais la commande BentoBox la plus proche — cliquable, ou acceptée en tapant `yes`/`y` dans les 30 secondes — au lieu d'afficher le texte d'aide. Les suggestions correspondent aux libellés et aux alias de toutes les arborescences de commandes, sont filtrées par permission, et utilisent le monde du mode de jeu où se trouve le joueur pour lever l'ambiguïté. Deux nouveaux commutateurs sous `general.did-you-mean` dans `config.yml` — `unknown-commands` et `subcommands` — tous deux **activés** par défaut ; mettez l'un ou l'autre à `false` puis `/bbox reload` pour désactiver.
    - ⚙️ 🔺 **Suppression des structures vanilla au niveau du cœur pour chaque mode de jeu.** Désactiver une structure vanilla est désormais un unique paramètre du cœur au lieu d'une tâche par complément. Une nouvelle liste `world.disabled-structures` dans `config.yml` (appliquée à chaque Overworld/Nether/End BentoBox) empêche les structures listées de se générer **et** les ignore dans les recherches de structures — `/locate`, Yeux de l'Ender, cartes d'explorateur/au trésor, dauphins et échanges de cartographe villageois — corrigeant le gel du thread principal de `/locate` de longue date et les fuites de structures près du spawn. Les clés sont insensibles à la casse et aux séparateurs (`trial_chambers`, `ancient-city`). Un mode de jeu peut surcharger la liste structure par structure. **La liste est vide par défaut, donc le comportement est inchangé jusqu'à ce que vous l'activiez.**
    - 🔌 **Hook Nexo.** BentoBox peut désormais placer et détecter les blocs et objets personnalisés [Nexo](https://nexomc.com/), aux côtés des autres intégrations d'objets personnalisés.
    - 🔌 **Placement de blocs Oraxen.** `OraxenHook.placeBlock` expose le placement de blocs personnalisés Oraxen aux compléments, à l'image des autres hooks de blocs personnalisés.
    - 🔡 **Note sur les locales :** trois nouvelles clés `general.did-you-mean` ont été ajoutées aux 22 locales fournies, et la clé manquante préexistante `commands.admin.team.setowner.specify-island` a été remplie dans chaque fichier non anglais. Régénérez ou mettez à jour tout fichier de locale personnalisé.

    [Release v3.20.0](https://github.com/BentoBoxWorld/BentoBox/releases/tag/3.20.0)

??? warning "Nouveautés dans v3.19.0 — Lits/ancres de respawn maintenant honorées"
    **Publié :** 8 juillet 2026

    Compatibilité : Paper Minecraft 1.21.5 – 26.2, Java 25+.

    - 🔡 **Nouveau drapeau de protection `FISHING`.** Empêche les joueurs de pêcher dans les zones protégées depuis l'extérieur de l'île (le drapeau vérifie la position du crochet). Par défaut au rang visiteur, donc rien ne change jusqu'à ce que vous l'augmentiez.
    - 🔺 **Les respawns au lit et à l'ancre de respawn sont maintenant honorés.** Mourir sur une île vous rend désormais à votre lit ou à votre ancre de respawn chargée si elle se trouve sur une île dont vous êtes membre. Contrôlé par le nouveau paramètre mondial `BED_ANCHOR_RESPAWN` (**activé par défaut**) ; les serveurs sensibles à l'économie qui veulent l'ancien comportement « toujours respawn à l'accueil de l'île » devraient le désactiver.
    - 🐛 **Le portail de sortie de l'End ne vous jette plus au spawn du monde.** Sauter par le portail de sortie de l'End vous achemine maintenant vers votre accueil d'île sûr sur les serveurs multi-modes de jeu.
    - 🐛 **Les cadres et peintures survivent aux plans.** Les cadres conservent leur orientation et leur contenu, et les peintures restaurent leur œuvre d'art, au lieu de disparaître ou de faire face à la mauvaise direction.
    - 🔡 **Récupérer les îles en attente de suppression.** Le nouveau `/[admin] undelete`, un `/[admin] delete` debout (sans argument joueur), et une invite de confirmation sur `/[admin] register` peuvent maintenant sauver les îles supprimées en douceur avant que leurs fichiers de région soient purgés (voir le tableau Commandes d'Administration par Mode de Jeu ci-dessus).
    - ⚙️ **La couche d'île BlueMap survit aux recharges.** Les épingles de propriétaire et les boîtes de zone ne disparaissent plus après `/bluemap reload`. Une nouvelle section `bluemap` dans `config.yml` ajoute les commutateurs `island-markers` et `island-areas` (tous deux par défaut `true`), reflétant les commutateurs Dynmap, plus la personnalisation des marqueurs.
    - ⚙️ **Icônes de bouton de panneau d'équipe configurables + texte membre/prospect.** Les boutons STATUS, RANK-filter et INVITE du panneau d'équipe honorent désormais le `icon:` défini dans `team_panel.yml`, et le nom et la description du bouton membre/prospect sont maintenant commandés par les clés de locale. Les valeurs par défaut reproduisent exactement l'apparence précédente.
    - ⚡ **Le spam de clic GUI Paramètres n'augmente plus le MSPT.** Le spam de clic `/is settings` est passé de ~30-40 MSPT à négligeable via l'actualisation du panneau en place et un cache de traduction.

    [Release v3.19.0](https://github.com/BentoBoxWorld/BentoBox/releases/tag/3.19.0)

??? warning "Nouveautés dans v3.18.0 — Support Minecraft 26.2 nécessite Java 25 (serveur)"
    **Publié :** 27 juin 2026

    - 🔺 **Support Minecraft 26.2 + Java 25.** BentoBox fonctionne désormais sur la ligne Minecraft 26.x (26.2 supporté à l'exécution) et la compilation a migré vers la chaîne d'outils Java 25. **Votre serveur doit fonctionner sur une build Paper capable de Java 25 pour la ligne 26.x.** Les jars d'addon déjà compilés continuent à fonctionner sans modification — seuls les *développeurs* d'addon recompilant contre cette version doivent passer leur propre compilation à Java 25. Compatibilité : Paper Minecraft 1.21.5 – 26.2, Java 25+.
    - ⚙️ **Bascules de marqueur/zone Dynmap pour île.** Une nouvelle section `dynmap` dans `config.yml` ajoute les interrupteurs `island-markers` (l'icône maison au centre de chaque île) et `island-areas` (la boîte de bordure de zone protégée). Les deux sont par défaut `true`, préservant le comportement existant ; réglez l'un d'eux à `false` et exécutez `/bbox reload` pour masquer ces superpositions sur les serveurs où les îles denses inondent la carte.
    - **Gestion des bonus de plage d'administration.** Nouvelles commandes `/[admin] range removebonus` et `/[admin] range purgebonus` qui effacent les bonus de plages de protection d'une île ou de toutes les îles — idéal après désinstallation d'un addon qui les accordait (voir le tableau des Commandes d'Administration par Mode de Jeu ci-dessus).
    - 🐛 `/is team setowner` n'est plus bloqué par la limite d'île lors du transfert à un membre d'équipe existant.
    - 🐛 Le crochet Vault réessaye maintenant après l'activation des addons, corrigeant l'intégration d'économie qui dépendait de l'ordre de chargement.

    [Release v3.18.0](https://github.com/BentoBoxWorld/BentoBox/releases/tag/3.18.0)

??? note "Nouveautés dans v3.18.1"
    **Publié :** 1er juillet 2026

    Maintenance release.

    - 🐛 **Les titres et noms multilignes conservent leur couleur.** Le texte après la première ligne d'une infobulle GUI ne retombe plus sur le violet par défaut — le sérialiseur réémet désormais la couleur active (et les décorations) après chaque nouvelle ligne, corrigeant les infobulles sur tous les addons.

    [Release v3.18.1](https://github.com/BentoBoxWorld/BentoBox/releases/tag/3.18.1)
