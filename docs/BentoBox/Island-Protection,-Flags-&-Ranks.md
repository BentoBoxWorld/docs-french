# Protection de l'Île, Drapeaux et Rangs

[TOC]

## Introduction

Tout ce qu'un joueur (ou l'environnement : pistons, créatures, feu, explosions…) peut faire dans un monde BentoBox est contrôlé par des **Drapeaux**. Chaque drapeau couvre un type d'action, comme casser des blocs, ouvrir des coffres ou faire du mal à des animaux. La plupart des drapeaux viennent de BentoBox. Des addons comme [Greenhouses](https://github.com/BentoBoxWorld/Greenhouses) peuvent en ajouter d'autres.

Consultez la [liste des drapeaux](Flags.md) pour chaque drapeau, son icône et sa valeur par défaut.

Il existe trois types de drapeau :

| Type | Ce qu'il contrôle | Qui le modifie |
| --- | --- | --- |
| **Protection** | Quel [rang](#rangs) peut faire une action, par exemple *Casser des blocs*. Sur une île, c'est un rang. En dehors d'une île, c'est activé ou désactivé pour tout le monde. | Le propriétaire de l'île sur son île. Les administrateurs pour le monde et les nouvelles îles. |
| **Paramètre** | Un interrupteur activé/désactivé au niveau de l'île, par exemple *PVP* ou *Génération d'animaux*. | Le propriétaire de l'île. |
| **Paramètre mondial** | Un interrupteur pour tout le monde du jeu, par exemple *Dégâts des Creepers*. | Administrateurs uniquement. |

### Sur une île, en dehors d'une île, et les nouvelles îles

La confusion la plus courante est qu'un drapeau de protection peut avoir **trois valeurs différentes**, selon où se tient le joueur et quelle île est concernée :

| Question | Où c'est défini | Onglet du panneau |
| --- | --- | --- |
| Quel rang peut faire ceci sur **cette île** ? | Les paramètres de cette île | `/[player_command] settings` → **Protection** |
| Que peut faire n'importe qui **en dehors de toute île** dans ce monde ? | Les drapeaux de protection du monde (`world.flags` dans le `config.yml` du mode de jeu) | `/[admin_command] settings` → **Protections Mondiales** |
| Quel rang une **nouvelle île** commencera-t-elle ? | `world.default-island-flags` dans le `config.yml` du mode de jeu | `/[admin_command] settings` → **Défauts de l'Île** |

Modifier l'un ne modifie jamais les autres. En particulier, **Les Défauts de l'Île n'ont aucun effet en dehors des îles**, et **Les Protections Mondiales n'ont aucun effet sur les îles**.

### Où une île finit { #where-an-island-ends }

La protection d'une île ne couvre pas toute sa case de grille. Les îles sont placées à `distance-between-islands` l'une de l'autre, mais chacune n'est protégée que dans sa **plage de protection**, une case de `protection-range` blocs du centre de l'île dans chaque direction. La plage peut être augmentée par île avec `/[admin_command] range` ou la permission `[gamemode].island.range.<number>`.

N'importe où en dehors d'une plage de protection compte comme **en dehors de l'île**, même si c'est à l'intérieur de la case de grille d'une île. Cela inclut le vide entre les îles, la zone autour du spawn du monde s'il n'y a pas d'île, et la nature sauvage dans les modes de jeu comme Boxed. En dehors de l'île, les [Protections Mondiales](#world-protections) s'appliquent.

## Rangs

Chaque joueur a un rang sur chaque île : propriétaire, membre, visiteur, etc. Un drapeau de protection définit le **rang minimum autorisé** pour faire l'action. N'importe qui à ce rang ou plus élevé est autorisé. Les rangs sont des nombres, donc plus élevé signifie plus de confiance :

| Rang | Valeur | Qui l'a |
| --- | --- | --- |
| Banni | -1 | Les joueurs bannis de l'île. Ils ne peuvent pas y entrer. |
| Visiteur | 0 | N'importe qui qui ne fait pas partie de l'île. |
| Coopération | 200 | Les joueurs ajoutés avec `/[player_command] team coop`. Supprimés quand tous les membres de l'équipe se sont déconnectés. |
| Confiance | 400 | Les joueurs ajoutés avec `/[player_command] team trust`. Conservés à travers les connexions. |
| Membre | 500 | Les membres de l'équipe. |
| Sous-propriétaire | 900 | Les membres de l'équipe promus avec `/[player_command] team promote`. |
| Propriétaire | 1000 | Le propriétaire de l'île. |
| Modérateur | 5000 | Non donné aux joueurs. Réservé. |
| Administrateur | 10000 | Non donné aux joueurs. Réservé. |

Donc un drapeau défini sur *Membre* permet aux membres, sous-propriétaires et au propriétaire de faire l'action, mais pas aux joueurs en confiance, en coopération ou aux visiteurs. Un drapeau défini sur *Visiteur* permet à tout le monde de le faire.

Les addons peuvent enregistrer plus de rangs entre ceux-ci.

Les administrateurs peuvent voir ou modifier le rang d'un joueur avec `/[admin_command] getrank <player>` et `/[admin_command] setrank <player> <rank>`.

## Panneau des Paramètres de l'Île

Le **Panneau des Paramètres** est l'endroit où un propriétaire d'île configure son île. Ouvrez-le avec `/[player_command] settings` (permission `[gamemode].island.settings`). Tout le monde sur l'île peut le voir. Seul le propriétaire peut le modifier, ainsi que tout rang que le propriétaire autorise avec le drapeau **Modifier les paramètres** (la table de craft, haut).

![Vue par défaut du Panneau des Paramètres](https://user-images.githubusercontent.com/20014332/80591492-1689c100-8a1e-11ea-9a59-c55f35ab6ad9.png)

*Vue par défaut du Panneau des Paramètres.*

Le panneau affiche l'île dans la zone de laquelle le joueur se tient, ou sa propre île s'il est ailleurs. Les administrateurs peuvent ouvrir l'île de n'importe quel joueur avec `/[admin_command] settings <player_name>`.

### Onglet Protection

L'onglet **Protection** est affiché en premier et répertorie les **drapeaux de protection** de l'île.

**Clic gauche** sur un drapeau pour augmenter le rang dont il a besoin et **clic droit** pour le diminuer. Le lore répertorie les rangs et met en évidence le courant. Dépasser *Propriétaire* boucle à *Visiteur*, et vice-versa.

![Exemple d'un Drapeau de Protection](https://user-images.githubusercontent.com/20014332/62974085-b31c1c80-be17-11e9-8b27-2fd4bf54ae87.png)

*Exemple d'un Drapeau de Protection.*

Une nouvelle île commence avec les rangs définis sur l'onglet [Défauts de l'Île](#island-defaults). La plupart des drapeaux commencent à *Membre*, donc les visiteurs peuvent regarder mais pas toucher. Quelques-uns commencent plus bas pour que les visiteurs puissent les utiliser. Par exemple, *Verrou* commence à *Visiteur*, ce qui signifie que l'île est ouverte aux visiteurs.

![Exemple d'un Drapeau de Protection qui, par défaut, permet aux visiteurs de faire l'interaction.](https://user-images.githubusercontent.com/20014332/62974359-553c0480-be18-11e9-8679-0033fd8bf8bd.png)

*Exemple d'un Drapeau de Protection qui, par défaut, permet aux visiteurs de faire l'interaction.*

### Onglet Paramètres

L'onglet **Paramètres** répertorie les **drapeaux de paramètres** de l'île : des interrupteurs activés/désactivés pour l'île dans son ensemble, comme PVP, propagation du feu, décadence des feuilles et génération de créatures. Cliquez sur un paramètre pour le basculer.

Chaque paramètre a également besoin de la permission `[gamemode].settings.<FLAG_ID>` (ou `[gamemode].settings.*`). Cela permet à un serveur de retirer complètement un paramètre aux joueurs, par exemple pour les empêcher de désactiver le PVP. Certains paramètres, comme le PVP, ont un refroidissement entre les changements.

Cet onglet a également l'icône [Rangs de Commande](#command-ranks).

### Vue des Protections Mondiales

!!! new "Ajouté dans BentoBox 3.22.0"

Un joueur qui n'a pas d'île dans le monde et ne se tient pas dans la zone d'une autre île voit à la place un onglet **Protections Mondiales** en lecture seule. Il montre ce que n'importe qui peut faire en dehors de l'île, tel que défini par l'administrateur sur l'onglet [Protections Mondiales](#world-protections). C'est pour l'information uniquement et ne peut pas être modifié d'ici.

### Mode d'affichage

Selon le **mode d'affichage**, le Panneau des Paramètres affiche plus ou moins de drapeaux. Le mode est `BASIC`, `ADVANCED` ou `EXPERT`. Changez-le en cliquant sur le lingot dans le coin supérieur droit du panneau.

![Modification du mode d'affichage](https://user-images.githubusercontent.com/20014332/80592558-f0652080-8a1f-11ea-9b7a-eaf3d585b753.png)

`BASIC` est la valeur par défaut et affiche les drapeaux que la plupart des joueurs ont besoin.

![Drapeaux de Protection de Base](https://user-images.githubusercontent.com/20014332/80592424-b98f0a80-8a1f-11ea-94f5-3b2246b6ae61.png)

`ADVANCED` affiche plus de drapeaux pour un contrôle plus fin.

![Drapeaux de Protection Avancés](https://user-images.githubusercontent.com/20014332/80592698-24d8dc80-8a20-11ea-93d5-3b1b8dbcd18d.png)

`EXPERT` affiche chaque drapeau et nécessite des pages supplémentaires.

![Drapeaux de Protection Expert](https://user-images.githubusercontent.com/20014332/80592793-4df96d00-8a20-11ea-891e-8833578642e4.png)

!!! new "Modifié dans BentoBox 3.23.3"
    Le Panneau des Paramètres se souvient du mode d'affichage que chaque joueur a choisi en dernier et s'ouvre dedans la prochaine fois. Un mode est partagé par les onglets Protection et Paramètres. Si un onglet n'a aucun drapeau à afficher dans le mode choisi, il affiche le mode suivant sans modifier le choix du joueur. Le panneau des paramètres administrateur s'ouvre toujours en `EXPERT`.

### Masquer les Drapeaux

Les opérateurs peuvent masquer un drapeau aux joueurs : ouvrez le Panneau des Paramètres et ++shift+left-button++ l'icône du drapeau. L'icône reçoit une lueur "Malédiction de Disparition", et les joueurs ne voient plus le drapeau. Faites la même chose à nouveau pour le montrer. Les drapeaux masqués sont stockés dans `world.hidden-flags` dans le `config.yml` du mode de jeu.

Masquer un drapeau ne le supprime que du panneau. Le drapeau garde sa valeur actuelle et est toujours appliqué. Pour s'assurer que les joueurs ne peuvent pas modifier un drapeau, définissez d'abord sa valeur, puis masquez-le.

![Drapeaux par défaut](https://user-images.githubusercontent.com/20014332/80591609-45a03280-8a1e-11ea-9e37-4725d62cdb3c.png)

*Vue du joueur de tous les Drapeaux de Base autorisés à être affichés.*

![Malédiction de Disparition](https://user-images.githubusercontent.com/20014332/80591692-6799b500-8a1e-11ea-9ab8-e076f47d2220.png)

*La "Malédiction de Disparition" appliquée à l'un des Drapeaux.*

![Un tas de drapeaux masqués](https://user-images.githubusercontent.com/20014332/80591757-839d5680-8a1e-11ea-8864-83b09252a7b9.png)

*Vue du joueur des Drapeaux de Base, avec le Drapeau "trappe" masqué.*

### Personnaliser le Panneau des Paramètres

!!! new "Ajouté dans BentoBox 3.23.0"
    Le Panneau des Paramètres est disposé par un fichier modèle, comme les autres [GUIs personnalisables](/en/latest/Tutorials/generic/Customizable-GUI/).

La disposition du Panneau des Paramètres provient de `plugins/BentoBox/panels/settings_panel.yml`, que BentoBox écrit au premier démarrage. Un addon de mode de jeu peut en fournir sa propre copie dans son dossier `panels` (par exemple `plugins/BentoBox/addons/BSkyBlock/panels/settings_panel.yml`), et celle-ci est utilisée pour ce mode de jeu à la place. Le fichier par défaut reproduit le panneau exactement comme il était avant, donc rien ne change jusqu'à ce que vous le modifiiez. Si le fichier ne peut pas être lu, BentoBox enregistre une erreur et affiche le panneau intégré.

Chaque bouton est placé avec un `data.type` :

| Type | Ce qu'il affiche |
| --- | --- |
| `TAB` | Un bouton d'onglet. `data.tab` est `PROTECTION`, `SETTING`, ou `WORLD_PROTECTION` (la vue en lecture seule qu'un joueur obtient en ne se tenant pas sur une île). Un onglet qui ne s'applique pas n'est pas affiché et l'`fallback` du bouton est utilisé à la place. |
| `FLAG` | Un slot de la liste de drapeaux paginée. Mettez autant de ceux-ci que vous le souhaitez de drapeaux par page. Avec `data.flag: <FLAG_ID>`, le slot affiche toujours ce drapeau à la place, et le drapeau quitte la liste paginée ; c'est ainsi que les icônes de verrouillage et de modification des paramètres sont placées. |
| `MODE` | Le commutateur de mode d'affichage. Les icônes peuvent être définies par mode avec `basic-icon`, `advanced-icon` et `expert-icon` dans `data`. |
| `RESET` | Réinitialiser chaque drapeau à sa valeur par défaut. Seul le propriétaire de l'île le voit. |
| `NEXT`, `PREVIOUS` | Pagination. Affichée uniquement s'il y a une page à aller. |

**Le titre et les noms des onglets sont séparés.** Le titre du panneau est le `title` du modèle, par défaut l'entrée de locale `panels.settings.title`, qui est traduite avec `[tab]` (le nom de l'onglet affiché) et `[world_name]`. La valeur par défaut est juste `[tab]`. Chaque bouton d'onglet a son propre `title` et `description`, par défaut les entrées `protection.panel.PROTECTION.title` et similaires. Donc vous pouvez styliser le titre d'une manière et les boutons d'onglet d'une autre, soit dans le modèle, soit dans la locale.

**Disposition du lore.** Le lore d'un drapeau est construit à partir de `protection.panel.flag-item.description-layout` (drapeaux de protection), `setting-layout` (paramètres) ou `menu-layout` (drapeaux qui ouvrent un sous-panneau) dans la locale. À partir de 3.23.0, ces dispositions peuvent contenir `[ranks]`, où la liste des rangs d'un drapeau de protection est insérée, et `[tooltips]`, où les bulles d'aide des actions du bouton drapeau dans le modèle sont insérées. Sans `[ranks]`, la liste des rangs est ajoutée après la disposition, comme avant ; sans `[tooltips]`, les bulles d'aide sont ajoutées après une ligne vide. Pour déplacer les conseils de clic sous la liste des rangs, supprimez-les de la disposition, mettez `[ranks]` et `[tooltips]` où vous les voulez, et déclarez les conseils comme des bulles d'aide sur `flag_button` dans le modèle. Le propre `title` et `description` d'un bouton drapeau dans le modèle peuvent nommer une autre entrée de locale à utiliser comme nom et disposition du lore pour ce panneau uniquement.

### Rangs de Commande

L'icône **Rangs de Commande** sur l'onglet Paramètres ouvre un panneau où le propriétaire de l'île choisit le [rang](#rangs) minimum qui peut utiliser chaque commande d'équipe, par exemple qui peut inviter, expulser ou définir le nom de l'île. **Clic gauche** et **clic droit** sur une commande parcourt les rangs, comme pour un Drapeau de Protection. Les opérateurs peuvent masquer une commande aux joueurs avec ++shift+left-button++, de la même manière que [masquer un Drapeau](#hide-flags).

À partir de BentoBox 3.23.3, un joueur ne voit que les commandes qu'il a la permission d'utiliser. Si vous refusez la permission d'une commande sur votre serveur, par exemple `[gamemode].island.border`, elle n'apparaît plus dans ce panneau non plus. Auparavant, seule la commande de niveau supérieur était vérifiée, donc les sous-commandes que le joueur ne pouvait pas exécuter étaient toujours répertoriées.

#### Personnaliser le panneau Rangs de Commande

!!! new "Ajouté dans BentoBox 3.23.3"
    Le panneau Rangs de Commande est disposé par un fichier modèle, comme le [Panneau des Paramètres](#customizing-the-settings-panel).

La disposition provient de `plugins/BentoBox/panels/command_ranks_panel.yml`, que BentoBox écrit au premier démarrage. Un addon de mode de jeu peut en fournir sa propre copie dans son dossier `panels`, et celle-ci est utilisée pour ce mode de jeu à la place. Le fichier par défaut maintient le panneau tel qu'il était avant : une carte pour chaque commande, pas de remplissage, et seulement autant de lignes que les commandes en ont besoin. Si le fichier ne peut pas être lu, BentoBox affiche le panneau intégré.

Chaque bouton est placé avec un `data.type` :

| Type | Ce qu'il affiche |
| --- | --- |
| `COMMAND` | Un slot de la liste de commandes paginée. Mettez autant de ceux-ci que vous le souhaitez de commandes par page ; la valeur par défaut en a 45. |
| `NEXT`, `PREVIOUS` | Pagination. Affichée uniquement s'il y a une page à aller. |

Le panneau intégré s'arrêtait à 49 commandes, donc celles au-delà n'ont jamais été affichées. Le modèle pagine à la place.

La façon dont une commande est dessinée peut être modifiée sur `command_button` dans la section `reusable` du modèle :

- `icon` remplace le `MAP` par défaut.
- `title` est une entrée de locale (ou du texte) utilisée comme disposition du nom au lieu de `protection.panel.flag-item.name-layout`. `[name]` est la commande, par exemple `/island sethome`.
- `description` est une entrée de locale (ou du texte) utilisée comme disposition du lore au lieu de `protection.panel.flag-item.description-layout`. `[description]` est le texte de la commande à partir de `protection.panel.flag-item.command-instructions`. La liste des rangs est ajoutée après.
- `actions` ajoute uniquement des bulles d'aide, qui sont ajoutées après la liste des rangs. Les clics eux-mêmes fonctionnent toujours comme décrit ci-dessus. La disposition par défaut inclut déjà les conseils de clic.

Par exemple, pour afficher chaque commande comme du papier et remplir les emplacements vides :

```yaml
command_ranks_panel:
  title: protection.flags.COMMAND_RANKS.name
  type: INVENTORY
  background:
    icon: LIGHT_BLUE_STAINED_GLASS_PANE
    title: "&b&r"
  force-shown: 6
  content:
    # ... lignes de command_button, et les boutons de pagination, comme dans le fichier par défaut
  reusable:
    command_button:
      icon: PAPER
      data:
        type: COMMAND
```

## Panneau des Paramètres Administrateur

Exécutez `/[admin_command] settings` **sans arguments** tout en jouant dans le monde du jeu pour ouvrir le **Panneau des Paramètres Administrateur** (permission `[gamemode].admin.settings`). Il a trois onglets. Ils contrôlent le monde et les nouvelles îles, pas une île existante.

!!! tip
    Chaque mode de jeu a sa propre commande administrative et ses propres paramètres. Exécutez la commande du mode de jeu que vous voulez modifier, par exemple `/bsbadmin settings` pour BSkyBlock ou `/acid settings` pour AcidIsland.

!!! new "Ajouté dans BentoBox 3.23.0"
    Le Panneau des Paramètres Administrateur est disposé par `plugins/BentoBox/panels/admin_settings_panel.yml`, de la même manière que le [Panneau des Paramètres du joueur](#customizing-the-settings-panel). Ses types d'onglets sont `WORLD_SETTING`, `WORLD_DEFAULTS` et `ISLAND_DEFAULTS` ; les deux derniers ont besoin de la permission `[gamemode].admin.set-world-defaults` et sont masqués sans elle. Le même fichier dispose `/[admin_command] settings <player_name>` : chaque onglet de monde nomme un onglet d'île (`PROTECTION`, `SETTING`) comme son `fallback`, qui est ce qui est montré quand il y a une île.

Les modifications apportées dans ces onglets sont enregistrées dans le `config.yml` du mode de jeu immédiatement.

### Paramètres Mondiaux

Le premier onglet répertorie les drapeaux de **paramètre mondial** : des interrupteurs qui s'appliquent au monde entier du jeu, sur les îles et en dehors, comme *Dégâts des Creepers*, *Redstone hors ligne* ou *Les visiteurs gardent l'inventaire*. Cliquez sur un drapeau pour l'activer ou le désactiver. Chacun a besoin de la permission `[gamemode].admin.world.settings.<FLAG_ID>`, que les opérateurs ont.

Les paramètres mondiaux peuvent également être définis à partir de la console ou du chat :

```
/[admin_command] settings <FLAG_ID> <Active|Disabled>
```

!!! new "Ajouté dans BentoBox 3.23.6"
    L'élément **Types d'entité toujours autorisés** (lingot de fer) ouvre une liste de chaque type d'entité vivante. Les types verts apparaissent même lorsque la génération d'animaux ou de monstres est désactivée, sur n'importe quelle île ou dans le monde ; Golem de Fer est vert par défaut pour que les fermes de fer du village continuent à fonctionner. La liste de blocage **Génération de créatures mondiale** a toujours priorité. La liste est stockée par BentoBox, pas dans le `config.yml` du mode de jeu ; voir [Précédence de la génération de créatures](#mob-spawning-precedence). Nécessite `[gamemode].admin.settings.ALLOW_MOBS`.

#### Ce que chaque paramètre mondial fait

Ce sont les paramètres mondiaux que la plupart des serveurs voudront examiner. Les valeurs par défaut sont pour BSkyBlock ; les autres modes de jeu peuvent différer. Chaque drapeau est répertorié dans [Drapeaux](Flags.md).

| Paramètre | Ce qu'il fait | Défaut |
|---|---|---|
| **Types d'entité toujours autorisés** | Entités qui apparaissent indépendamment de ce que disent les drapeaux de génération d'animaux et de monstres, sur les îles et dans le monde. Utilisez-le pour laisser fonctionner les fermes de fer du village sur un serveur ou une île qui a la génération d'animaux désactivée. Golem de Fer est autorisé par défaut. La liste de blocage (*Génération de créatures mondiale*) gagne toujours. Voir [Précédence de la génération de créatures](#mob-spawning-precedence). | Golem de Fer |
| **Dégâts des explosions des coffres** | Protège les coffres d'être détruits par des explosions (Creepers, TNT, Withers, Ghasts). Prévient les dégâts mais signifie que les coffres peuvent être utilisés pour faire des pièces à l'épreuve des explosions. | Activé |
| **Nettoyage du terrain plat super** | Si le générateur de monde cesse de fonctionner, les nouveaux chunks se génèrent comme de l'herbe plate. Ce paramètre détecte et répare ces chunks. Laissez-le désactivé à moins que vous ayez ce problème — c'est gourmand en ressources. | Désactivé |
| **Labour de la terre grossière** | Empêche les joueurs de convertir la terre grossière en terre régulière à l'aide d'une houe. La terre est rare et précieuse dans la plupart des modes de jeu ; le labour de terre grossière peut être exploité pour la générer bon marché si le gravier est facile à obtenir. | Désactivé (prévention activée) |
| **Explosions des Creepers** | Empêcher les dégâts des explosions des Creepers aux blocs de l'île. Les Creepers sont la cause la plus courante de destruction d'île. Prévenir cela rend le jeu plus facile, mais réduit la charge de support administrateur. | Activé |
| **Allumage des Creepers par les visiteurs** | Empêcher les visiteurs d'utiliser du silex et de l'acier pour amorcer les Creepers sur l'île de quelqu'un d'autre — une méthode courante de griefing. | Activé |
| **Coffres de l'Ender** | Bloquer l'accès et l'artisanat des Coffres de l'Ender, qui peuvent contrebande des éléments entre les mondes du mode de jeu. Désactivez si vous utilisez un plugin Coffre de l'Ender par monde. | Activé (bloqué) |
| **Vol de blocs des Endermen** | Empêcher les Endermen de prendre des blocs des îles. Sans cela, les joueurs perdent des blocs qu'ils n'ont pas eux-mêmes supprimés. | Activé |
| **Limitation géographique des créatures** | Empêcher certaines créatures (par exemple le Wither, les créatures volantes) de quitter l'île sur laquelle elles ont été générées. S'ils traversent la limite, ils sont supprimés. | Activé |
| **Protection des visiteurs** | Protéger les visiteurs de la plupart des types de dégâts tout en étant sur l'île d'un autre joueur. Téléporte également les visiteurs en sécurité s'ils tombent dans le vide. | Activé |
| **Protection des cadres d'objets** | Empêcher les cadres d'objets d'être cassés ou d'avoir leurs objets frappés par des non-membres. | Activé |
| **Génération de créatures mondiale** | Définissez quels types de créatures peuvent apparaître n'importe où dans le monde, en remplaçant tous les autres paramètres de génération. Par exemple, désactiver les Fantômes au niveau du serveur. | Varie |
| **Flux de liquide en dehors des îles** | Arrêter la lave et l'eau de s'écouler au-delà des limites de protection de l'île, en prévenant la formation de pavé de cobblestone entre les îles ou les inondations. | Activé |
| **Génération de créatures en dehors des îles** | Empêcher les créatures de générer dans les zones entre les îles, en concentrant la génération dans les zones de l'île. Non recommandé pour AcidIsland car cela semble non naturel. | Désactivé |
| **Récupération d'obsidienne** | Permettre aux joueurs de clic droit sur un bloc d'obsidienne isolé unique avec un seau vide pour récupérer la lave. Aide les nouveaux joueurs qui créent accidentellement de l'obsidienne lors de la configuration du générateur de pavé de cobblestone. | Activé |
| **Croissance des plantes hors ligne** | Arrêter la croissance des cultures et des plantes sur une île quand aucun membre de l'équipe n'est en ligne, même si un visiteur charge les chunks. | Désactivé |
| **Redstone hors ligne** | Désactiver les circuits Redstone sur une île quand aucun membre de l'équipe n'est en ligne. | Désactivé |
| **Piston en dehors de la limite** | Arrêter les pistons de pousser des blocs au-delà de la limite de protection de l'île — un exploit courant pour griever les îles adjacentes. | Activé |
| **Supprimer les créatures au moment de la téléportation** | Supprimer les créatures hostiles de la zone quand un joueur se téléporte à son foyer d'île, en prévenant les décès par surprise à l'arrivée. | Activé |
| **Protection du type de générateur** | Empêcher les joueurs de changer le type de créature des blocs de générateur à l'aide d'œufs de génération. Utile quand les générateurs sont donnés comme récompenses. | Activé |
| **Limite de croissance des arbres** | Empêcher les arbres de croître au-delà de la limite de protection de l'île. Sans cela, les arbres peuvent empiéter sur d'autres îles ou créer des blocs inaccessibles. | Activé |
| **Dégâts du Wither** | Limiter la destruction que le Wither peut causer sur les îles et entre elles. | Activé |

#### Précédence de la génération de créatures { #mob-spawning-precedence }

La génération naturelle et celle des générateurs de créatures est décidée dans cet ordre. La première règle qui correspond gagne.

1. **Génération de créatures mondiale** liste de blocage (`protection.block-mobs` dans la config du mode de jeu). Un type bloqué ne génère jamais.
2. **Types d'entité toujours autorisés** liste d'autorisation. Un type autorisé génère indépendamment des drapeaux ci-dessous.
3. Les paramètres **Génération naturelle d'animaux**, **Génération naturelle de monstres**, **Génération de générateurs d'animaux** et **Génération de générateurs de monstres** de l'île, ou les valeurs par défaut du monde pour ces drapeaux quand il n'y a pas d'île.

Les générations causées directement par un joueur, comme l'élevage, les œufs de génération ou la construction d'un golem, ne sont jamais limitées par aucune de celles-ci.

!!! note "Où la liste d'autorisation est stockée"
    Contrairement aux autres paramètres mondiaux, la liste d'autorisation n'est pas dans le `config.yml` du mode de jeu. BentoBox la stocke elle-même, un enregistrement par mode de jeu, dans sa base de données : avec la base de données par fichier plat par défaut, c'est `plugins/BentoBox/database/CoreWorldSettings/<GameMode>.json`. Elle est ensemencée avec `IRON_GOLEM` la première fois que le mode de jeu est vu ; après cela, seules les modifications de l'administrateur dans le panneau s'appliquent. Supprimer l'enregistrement restaure l'ensemencement.

### Protections Mondiales

Le deuxième onglet, **Protections Mondiales**, décide ce que les joueurs peuvent faire **en dehors de la plage de protection de toute île**. Cela inclut le vide entre les îles, la zone de spawn si ce n'est pas une île, et la nature sauvage. Voir [Où une île finit](#where-an-island-ends).

En dehors d'une île, il n'y a pas d'équipe et pas de rangs, donc chaque drapeau de protection ici est juste **activé ou désactivé pour tout le monde**. Cliquez sur un drapeau pour le basculer :

- **Autorisé** : n'importe qui peut faire l'action en dehors de l'île.
- **Non autorisé** : personne ne peut, à part les opérateurs et les joueurs avec une [permission de contournement](#bypass-the-protection).

La plupart des drapeaux de protection sont **non autorisés** en dehors de l'île par défaut, donc les joueurs ne peuvent pas construire, casser des blocs ou utiliser des objets en dehors de leur île. Cet onglet a besoin de `[gamemode].admin.set-world-defaults`, et chaque drapeau a également besoin de `[gamemode].admin.world.settings.<FLAG_ID>`. Les opérateurs ont les deux. Les valeurs sont stockées sous `world.flags` dans le `config.yml` du mode de jeu.

!!! example "Permettre aux joueurs de construire des ponts entre les îles"
    Les joueurs ne peuvent construire que sur leur propre île, donc ils ne peuvent pas faire de pont vers un voisin. Pour leur permettre de construire en dehors de l'île :

    1. Tenez-vous dans le monde du jeu et exécutez `/[admin_command] settings` sans nom de joueur.
    2. Ouvrez l'onglet **Protections Mondiales**. Ce n'est ni le premier onglet ni **Défauts de l'Île**.
    3. Activez **Placer des blocs** et **Casser des blocs**, plus n'importe quoi d'autre dont les joueurs ont besoin là-bas, comme les seaux, les portes ou les plaques de pression.

    Les îles elles-mêmes restent protégées par leurs propres paramètres. Pour permettre aux visiteurs de prendre des choses d'autres îles aussi, définissez les [Défauts de l'Île](#island-defaults) pour les nouvelles îles, ou modifiez les îles existantes avec `/[admin_command] settings <player>`.

Les joueurs sans île peuvent voir ces valeurs (lecture seule) dans `/[player_command] settings`. Voir [Vue des Protections Mondiales](#world-protection-view).

### Défauts de l'Île { #island-defaults }

!!! new "Ajouté dans BentoBox 3.14.0"
    L'onglet **Défauts de l'Île** définit les drapeaux que les **îles nouvellement créées** commencent avec. Avant, cela ne pouvait être fait que dans le `config.yml` du mode de jeu.

Le troisième onglet définit la valeur de départ de chaque drapeau pour les **nouvelles îles** :

- Chaque **drapeau de protection** affiche son rang par défaut. Clic gauche ou clic droit pour parcourir les rangs.
- Chaque **drapeau de paramètre** affiche son état d'activation/désactivation par défaut. Cliquez pour le basculer.

Ces valeurs sont stockées dans `world.default-island-flags` et `world.default-island-settings` dans le `config.yml` du mode de jeu. Un drapeau qui n'est pas répertorié là utilise la valeur par défaut intégrée du drapeau.

Les modifications s'appliquent uniquement aux îles créées **après** le changement. Pour appliquer les valeurs par défaut aux **îles existantes**, exécutez `/[admin_command] resetflags` pour réinitialiser chaque drapeau sur chaque île, ou `/[admin_command] resetflags <FLAG_ID>` pour réinitialiser un seul drapeau. Cela remplace ce que les propriétaires d'île ont défini, donc on vous demande de confirmer.

Cet onglet **ne** contrôle pas ce que les joueurs peuvent faire en dehors des îles. Pour cela, utilisez [Protections Mondiales](#world-protections).

### Modifier l'île d'un joueur

`/[admin_command] settings <player_name>` ouvre les onglets Protection et Paramètres de l'île de ce joueur, comme le propriétaire les verrait, donc un administrateur peut modifier n'importe quel drapeau. `/[admin_command] settings spawn-island` fait la même chose pour l'île de spawn.

On peut aussi le faire à partir de la ligne de commande :

```
/[admin_command] settings <player_name> <FLAG_ID> <rank>              # drapeau de protection, par exemple Visiteur
/[admin_command] settings <player_name> <FLAG_ID> <Active|Disabled>   # drapeau de paramètre
```

## Contourner la protection

Les drapeaux de protection ne sont appliqués que dans les mondes de jeu BentoBox et seulement contre les joueurs qui n'ont pas de moyen légitime de passer. Il existe plusieurs façons de contourner la protection — certaines sont intentionnelles (rangs d'île), certaines sont pour le personnel (statut d'opérateur et permissions de modérateur), et certaines sont structurelles (le monde ou le type de drapeau).

!!! tip
    `[gamemode]` dans les permissions ci-dessous est le nom du mode de jeu en minuscules. Pour BSkyBlock, les nœuds commencent `bskyblock.mod…`, pour AcidIsland `acidisland.mod…`, etc.

### Rangs d'île — le moyen intentionnel { #island-ranks—the-intended-way }

Le moyen normal et conçu de « contourner » un drapeau de protection est d'avoir un **rang** assez élevé sur l'île. Chaque drapeau de protection a un rang requis, et tout membre dont le rang est supérieur ou égal est autorisé à faire l'action. C'est pourquoi un propriétaire peut construire alors qu'un visiteur ne peut pas — ce n'est pas vraiment un contournement, juste le drapeau fonctionnant comme configuré. Voir la liste [Rangs](#ranks) ci-dessus.

### Opérateurs

Un opérateur de serveur (`/op`) est le contournement le plus large. Les Ops passent **chaque drapeau de protection** dans chaque monde BentoBox, peuvent entrer dans les îles verrouillées et bannies, et sont immunisés contre le bannissement ou l'expulsion.

Deux mises en garde importantes :

- **Les Ops ne contournent pas les drapeaux de paramètres d'île.** Les drapeaux de type `SETTING` (bascules d'île comme *Permettre le PVP*, *Génération de créatures*, …) sont évalués avant la vérification d'opérateur, donc un op est sujet à eux exactement comme n'importe quel autre joueur. Le statut d'opérateur ne remplace que les drapeaux de *protection*.
- **L'interrupteur administrateur ne peut pas complètement « déop » un joueur sur sa propre île.** Même avec l'interrupteur activé (voir ci-dessous), un op est toujours autorisé sur une île car la vérification de rang traite le statut d'opérateur comme toujours autorisé. Pour tester la protection en tant que vrai non-op, supprimez le statut d'opérateur.

### Permissions de contournement de modérateur

Pour le personnel qui ne doit *pas* être des opérateurs complets, la protection peut être contournée avec des permissions à la place. Celles-ci sont limitées par l'interrupteur administrateur (voir ci-dessous), donc un modérateur peut basculer son propre contournement pour vivre le monde comme un joueur normal le ferait.

- `[gamemode].mod.bypassprotect` — contourner **tous** les drapeaux de protection, partout dans le monde.
- `[gamemode].mod.bypass.<FLAG_ID>.everywhere` — contourner **un** drapeau nommé (par exemple `BREAK_BLOCKS`) partout dans le monde.
- `[gamemode].mod.bypass.<FLAG_ID>.island` — contourner **un** drapeau nommé, mais seulement où le joueur serait autrement bloqué sur une île.

### L'interrupteur administrateur « » — tester en tant que joueur normal

La commande `/[admin_command] switch` (permission `[gamemode].mod.switch`) bascule les permissions de contournement d'un modérateur activées et désactivées. Par défaut, les permissions de contournement sont **actives** (le modérateur contourne la protection) ; exécuter la commande une fois bascule le contournement **off** pour qu'ils soient soumis à la protection comme un joueur ordinaire, et exécuter à nouveau le bascule sur. Cela affecte les permissions `mod.bypassprotect` et `mod.bypass.*` ci-dessus — cela **n'** éteint pas le statut d'opérateur brut.

### Verrous, bannissements et expulsions

Les verrous d'île, les bannissements et les expulsions ont leurs propres permissions de contournement, séparées du système de drapeaux :

- `[gamemode].mod.bypasslock` — entrer une île verrouillée.
- `[gamemode].mod.bypassban` — entrer une île dont vous êtes banni.
- `[gamemode].mod.bypassexpel` et `[gamemode].admin.noexpel` — ne peut pas être expulsé.
- `[gamemode].admin.noban` — ne peut pas être banni.

Toute entité portant les métadonnées Bukkit `NPC` (par exemple les PNJs Citizens) est également autorisée à travers le verrouillage, le bannissement, le PVP et les vérifications des visiteurs invulnérables, donc les PNJs de plugin ne sont pas piégés ou blessés par la protection de l'île.

### Refroidissements et délais

Les refroidissements de commande et les délais de préparation de téléportation peuvent être ignorés avec :

- `[gamemode].mod.bypasscooldowns` — ignorer les refroidissements de commande.
- `[gamemode].mod.bypassdelays` — ignorer le délai de préparation de mouvement sur les commandes de téléportation à délai.

### Ce qui n'est jamais protégé

- **Mondes non-BentoBox.** La protection n'existe que dans les mondes de mode de jeu (et leur Nether/End lié standard). Les mondes par défaut du serveur et les mondes d'autres plugins ne sont jamais vérifiés.
- **Les zones en dehors des îles suivent des règles différentes.** Quand un joueur est dans un monde de mode de jeu mais en dehors de la plage de protection de chaque île, les [Protections Mondiales](#world-protections) s'appliquent à la place des drapeaux d'une île.
- **Les îles supprimées sont l'exception :** sur une île en attente de suppression, rien n'est autorisé par défaut — à part les opérateurs et les titulaires d'une permission `mod.bypassprotect` / `mod.bypass.<FLAG_ID>.everywhere`, dont le contournement est vérifié en premier.

## Dépannage

**Les joueurs ne peuvent pas construire ou casser des blocs entre les îles.**
Cette zone est en dehors de l'île, donc l'onglet [Protections Mondiales](#world-protections) s'applique. Activez les drapeaux dont vous avez besoin là-bas. Modifier les Défauts de l'Île ne servira à rien.

**J'ai modifié les Défauts de l'Île mais les îles existantes n'ont pas changé.**
Les Défauts de l'Île ne s'appliquent qu'aux îles créées après. Utilisez `/[admin_command] resetflags` pour les appliquer aux îles existantes, ou modifiez une seule île avec `/[admin_command] settings <player>`.

**Un joueur ne peut pas modifier un paramètre bien qu'il possède l'île.**
Le paramètre a probablement besoin de la permission `[gamemode].settings.<FLAG_ID>`, ou le paramètre est en refroidissement.

**Je suis un opérateur et je ne peux pas tester si la protection fonctionne.**
Les opérateurs contournent chaque drapeau de protection. Testez avec un compte non-op. `/[admin_command] switch` désactive uniquement les permissions de contournement du modérateur, pas le statut d'opérateur.

**Je ne sais pas quel drapeau bloque une action.**
Exécutez `/[admin_command] why <player>` pour enregistrer chaque vérification de protection pour ce joueur dans la console, puis faites l'action. Le journal nomme le drapeau, l'emplacement et le résultat. Exécutez la commande à nouveau pour arrêter.

**`why` dit que l'action est autorisée, mais le joueur est toujours bloqué.**
Quelque chose d'autre que BentoBox le bloque : un autre plugin, ou le serveur lui-même (par exemple la protection de spawn dans `server.properties`).

**Dois-je utiliser WorldGuard dans les mondes BentoBox ?**
Vous n'en avez pas besoin : BentoBox protège les îles et l'espace entre elles. Si vous l'utilisez là-bas, ses régions et les drapeaux de BentoBox s'appliquent tous les deux, ce qui peut bloquer les choses de manière inattendue. Gardez les régions WorldGuard en dehors des mondes du mode de jeu, ou vérifiez-les d'abord quand quelque chose est bloqué.
