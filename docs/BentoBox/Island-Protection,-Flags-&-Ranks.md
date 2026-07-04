# Protection de l'Île, Drapeaux & Rangs

[TOC]

## Introduction
Les interactions des joueurs (et même de l'Environnement, comme les entités, les pistons...) avec les îles sont régies par un ensemble de **Drapeaux** qui **déterminent *qui* ou *quoi* peut faire quoi sur une île**. Ces Drapeaux sont surtout gérés et fournis par BentoBox, mais les compléments (par ex. [Greenhouses](https://github.com/BentoBoxWorld/Greenhouses)) peuvent ajouter les leurs.

Voir une liste de drapeaux [ici](/en/latest/BentoBox/Flags).

## Panneau des Paramètres

Le **Panneau des Paramètres** est l'interface graphique dans laquelle le propriétaire de l'île est capable d'éditer comment les Drapeaux sont configurés pour son île. D'autres joueurs, y compris les membres de l'île, ne peuvent que les voir.

Cette interface graphique peut être ouverte en utilisant la commande suivante : `/[player_command] settings` (qui exige la permission suivante : `[gamemode].island.settings`).

![Vue par défaut du Panneau des Paramètres](https://user-images.githubusercontent.com/20014332/80591492-1689c100-8a1e-11ea-9a59-c55f35ab6ad9.png)

*Vue par défaut du Panneau des Paramètres.*

Les administrateurs peuvent modifier les paramètres de l'île d'un joueur en utilisant la commande d'administration des paramètres : `/[admin_command] settings <player_name>`

### Onglet de Protection

L'**Onglet de Protection** est l'onglet affiché lors de l'ouverture du Panneau des Paramètres. Il inclut les **Drapeaux de Protection**.

Les **Drapeaux de Protection** sont des Drapeaux qui peuvent être définis par [rang](#rangs). Par **clic gauche** ou **clic droit** sur l'icône d'un Drapeau, le propriétaire de l'île parcourra les différents rangs afin que l'interaction que le Drapeau règle soit autorisée ou interdite en fonction du rang d'un joueur.

![Exemple d'un Drapeau de Protection](https://user-images.githubusercontent.com/20014332/62974085-b31c1c80-be17-11e9-8b27-2fd4bf54ae87.png)

*Exemple d'un Drapeau de Protection.*

Par défaut, la plupart des Drapeaux de Protection sont définis pour ne permettre que les membres de l'île (ou un rang supérieur) de faire l'interaction. Cependant, certains sont initialement autorisés pour les visiteurs aussi. Voir [le config.yml du mode de jeu].

![Exemple d'un Drapeau de Protection qui, par défaut, permet aux visiteurs de faire l'interaction.](https://user-images.githubusercontent.com/20014332/62974359-553c0480-be18-11e9-8679-0033fd8bf8bd.png)

*Exemple d'un Drapeau de Protection qui, par défaut, permet aux visiteurs de faire l'interaction.*

Les administrateurs peuvent définir le fonctionnement des protections en dehors des limites de l'île en utilisant la commande d'administration des paramètres : `/[admin_command] settings`

### Onglet des Paramètres

### Mode d'Affichage

À partir de [BentoBox 1.6.0](https://github.com/BentoBoxWorld/BentoBox/releases/tag/1.6.0), diverses quantités de Drapeaux peuvent être affichées dans le Panneau des Paramètres, selon le **mode d'affichage**.
C'est soit `BASIC`, `ADVANCED` soit `EXPERT`.
Le mode d'affichage peut être changé en cliquant sur le lingot dans le coin supérieur droit du Panneau des Paramètres.

![Modification du mode d'affichage](https://user-images.githubusercontent.com/20014332/80592558-f0652080-8a1f-11ea-9b7a-eaf3d585b753.png).

`BASIC` est le mode d'affichage par défaut et présente les Drapeaux que nous jugeons essentiels pour gérer l'île.

![Drapeaux de Protection de Base](https://user-images.githubusercontent.com/20014332/80592424-b98f0a80-8a1f-11ea-94f5-3b2246b6ae61.png)

`ADVANCED` présente plus de Drapeaux pour permettre une personnalisation supplémentaire de l'île.

![Drapeaux de Protection Avancée](https://user-images.githubusercontent.com/20014332/80592698-24d8dc80-8a20-11ea-93d5-3b1b8dbcd18d.png)

`EXPERT` présente tous les Drapeaux disponibles. Il y en a tellement qu'il nécessite des pages supplémentaires.

![Drapeaux de Protection Expert](https://user-images.githubusercontent.com/20014332/80592793-4df96d00-8a20-11ea-891e-8833578642e4.png)

### Masquer les Drapeaux

À partir de [BentoBox 1.4.0](https://github.com/BentoBoxWorld/BentoBox/releases/tag/1.4.0), les administrateurs peuvent masquer les Drapeaux dans l'interface graphique en ouvrant le Panneau des Paramètres et ++shift+left-button++ sur l'icône du Drapeau qu'ils veulent masquer.
Cela appliquera une enchantement « Malédiction de Disparition » à l'icône et entraînera le Drapeau correspondant à être caché aux joueurs.
Les administrateurs peuvent plus tard afficher le Drapeau en réitérant la même procédure.

![Drapeaux par défaut](https://user-images.githubusercontent.com/20014332/80591609-45a03280-8a1e-11ea-9e37-4725d62cdb3c.png)

*Vue du joueur de tous les Drapeaux de Base autorisés à être affichés.*

![Malédiction de Disparition](https://user-images.githubusercontent.com/20014332/80591692-6799b500-8a1e-11ea-9ab8-e076f47d2220.png)

*La « Malédiction de Disparition » appliquée à l'un des Drapeaux.*

![Un tas de drapeaux masqués](https://user-images.githubusercontent.com/20014332/80591757-839d5680-8a1e-11ea-8864-83b09252a7b9.png)

*Vue du joueur des Drapeaux de Base, avec le Drapeau « trapdoor » masqué.*

## Rangs

À FAIRE.

* BANNI : -1 (partiellement inutilisé)
* VISITEUR : 0
* COOP : 200
* CONFIANCE : 400
* MEMBRE : 500
* SOUS-PROPRIÉTAIRE : 900
* PROPRIÉTAIRE : 1000
* MOD : 5000 (inutilisé)
* ADMINISTRATEUR : 10000 (inutilisé)

## Contourner la Protection

Les drapeaux de protection ne s'appliquent que dans les mondes de jeu BentoBox, et uniquement contre les joueurs qui n'ont aucun moyen légitime de les contourner. Il existe plusieurs façons de contourner la protection — certaines sont intentionnelles (rangs de l'île), certaines sont pour le personnel (statut d'opérateur et permissions de modérateur), et certaines sont structurelles (le monde ou le type de drapeau).

!!! tip
    `[gamemode]` dans les permissions ci-dessous est le nom du mode de jeu en minuscules. Pour BSkyBlock, les nœuds commencent par `bskyblock.mod…`, pour AcidIsland `acidisland.mod…`, et ainsi de suite.

### Rangs de l'île — la méthode intentionnelle

La façon normale et conçue de « contourner » un drapeau de protection est d'avoir un rang suffisamment élevé sur l'île. Chaque drapeau de protection a un rang requis, et tout membre dont le rang est supérieur ou égal à celui-ci est autorisé à effectuer l'action. C'est pourquoi un propriétaire peut construire alors qu'un visiteur ne le peut pas — ce n'est pas vraiment un contournement, juste le drapeau fonctionnant comme configuré. Voir la liste des [Rangs](#rangs) ci-dessus.

### Opérateurs

Un opérateur serveur (`/op`) est le contournement le plus large. Les ops passent **chaque drapeau de protection** dans chaque monde BentoBox, peuvent accéder aux îles verrouillées et bannies, et sont immunisés contre l'interdiction ou l'expulsion.

Deux avertissements importants :

- **Les ops ne contournent pas les drapeaux de paramètres d'île.** Les drapeaux de type `SETTING` (bascules d'île telles que *Autoriser PVP*, *Spawn de créatures*, …) sont évalués avant la vérification de l'opérateur, donc un op est soumis à ceux-ci exactement comme n'importe quel autre joueur. Le statut d'opérateur remplace uniquement les drapeaux de *protection*.
- **Le commutateur administrateur ne peut pas entièrement « désopérer » un joueur sur sa propre île.** Même si le commutateur est activé (voir ci-dessous), un op est toujours autorisé sur une île car la vérification de rang traite le statut d'opérateur comme toujours autorisé. Pour tester la protection en tant que véritable non-op, supprimez le statut d'opérateur.

### Permissions de contournement du modérateur

Pour le personnel qui ne devrait *pas* être des opérateurs complets, la protection peut être contournée avec des permissions à la place. Celles-ci sont contrôlées par le commutateur administrateur (voir ci-dessous), donc un modérateur peut désactiver son propre contournement pour expérimenter le monde comme le ferait un joueur normal.

- `[gamemode].mod.bypassprotect` — contourner **tous** les drapeaux de protection, partout dans le monde.
- `[gamemode].mod.bypass.<FLAG_ID>.everywhere` — contourner **un** drapeau nommé (par exemple `BREAK_BLOCKS`) partout dans le monde.
- `[gamemode].mod.bypass.<FLAG_ID>.island` — contourner **un** drapeau nommé, mais uniquement où le joueur serait autrement bloqué sur une île.

### Le « commutateur » administrateur — tester en tant que joueur normal

La commande `/[admin_command] switch` (permission `[gamemode].mod.switch`) bascule les permissions de contournement d'un modérateur on et off. Par défaut, les permissions de contournement sont **actives** (le modérateur contourne la protection) ; exécuter la commande une fois bascule le contournement **off** afin qu'il soit soumis à la protection comme un joueur ordinaire, et l'exécuter à nouveau le réactive. Cela affecte les permissions `mod.bypassprotect` et `mod.bypass.*` ci-dessus — cela ne désactive **pas** le statut d'opérateur brut.

### Verrous, interdictions et expulsions

Les verrous d'île, les interdictions et les expulsions ont leurs propres permissions de contournement, séparées du système de drapeaux :

- `[gamemode].mod.bypasslock` — accéder à une île verrouillée.
- `[gamemode].mod.bypassban` — accéder à une île dont vous êtes interdit.
- `[gamemode].mod.bypassexpel` et `[gamemode].admin.noexpel` — ne peuvent pas être expulsés.
- `[gamemode].admin.noban` — ne peuvent pas être bannis.

Toute entité portant les métadonnées Bukkit `NPC` (par exemple Citizens NPCs) est également autorisée à passer par le verrouillage, l'interdiction, les vérifications PVP et visiteur invincible, donc les PNJ de plugin ne sont pas piégés ou endommagés par la protection d'île.

### Refroidissements et délais

Les refroidissements de commande et les délais de préchauffage de téléportation peuvent être ignorés avec :

- `[gamemode].mod.bypasscooldowns` — ignorer les refroidissements de commande.
- `[gamemode].mod.bypassdelays` — ignorer le délai de préchauffage du mouvement sur les commandes de téléportation retardée.

### Ce qui n'est jamais protégé

- **Les mondes non-BentoBox.** La protection n'existe que dans les mondes de mode de jeu (et leurs Nether/End standard liés). Les mondes par défaut du serveur et les mondes des autres plugins ne sont jamais vérifiés.
- **Le « terrain sauvage ».** Lorsqu'un joueur se trouve dans un monde de mode de jeu mais ne se tient sur aucune île, les paramètres de drapeau par défaut du monde s'appliquent plutôt que ceux d'une île — ceux-ci sont configurés dans le **Panneau des Paramètres d'Administration** ci-dessous (ou le `config.yml` du mode de jeu).
- **Les îles supprimées sont l'exception :** sur une île en attente de suppression, rien n'est autorisé par défaut — à part les opérateurs et les détenteurs d'une permission `mod.bypassprotect` / `mod.bypass.<FLAG_ID>.everywhere`, dont le contournement est vérifié en premier.

## Panneau des Paramètres d'Administration

Le **Panneau des Paramètres d'Administration** est accessible via `/[admin_command] settings` (sans argument). Il contient trois onglets :

### Paramètres Mondiaux

Bascule les flags de paramètres au niveau du monde qui s'appliquent à l'ensemble du monde de jeu.

### Protection Par Défaut du Monde

Contrôle quels flags de protection sont actifs en dehors des limites de toute île (c'est-à-dire pour les visiteurs dans la nature).

### Paramètres Par Défaut des Îles

!!! new "Ajouté dans BentoBox 3.14.0"
    L'onglet **Paramètres Par Défaut des Îles** est un nouvel onglet du Panneau des Paramètres d'Administration qui permet aux administrateurs de définir les valeurs par défaut des flags appliquées aux **îles nouvellement créées**.

Auparavant, ces valeurs par défaut ne pouvaient être modifiées que dans le `config.yml` du mode de jeu. Elles peuvent désormais être modifiées directement en jeu en ouvrant `/[admin_command] settings` et en naviguant vers l'onglet **Paramètres Par Défaut des Îles** (onglet 3).

Chaque flag de protection est listé avec son rang par défaut actuel — cliquer le fait défiler dans l'échelle des rangs. Chaque flag de paramètre d'île affiche son état `true`/`false` par défaut actuel — cliquer le bascule. Les changements sont sauvegardés immédiatement dans les paramètres du monde et prennent effet pour toutes les **nouvelles** îles créées après le changement. Les îles existantes ne sont pas affectées.
