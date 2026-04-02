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

## Panneau des Paramètres d'Administration

### Paramètres Mondiaux

### Protection Par Défaut du Monde
