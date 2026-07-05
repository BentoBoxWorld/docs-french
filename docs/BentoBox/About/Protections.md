# Protection
BentoBox fournit un système complet de protection du monde et des îles pour les GameModes insulaires. La configuration se fait en jeu via les paramètres administrateur ou joueur, et en dehors du jeu via les permissions et les fichiers de configuration.

## Qu'est-ce que la Protection ?
Minecraft multijoueur ne fournit aucune protection intégrée pour la carte sauf pour la zone immédiatement autour du spawn. En conséquence, n'importe quel joueur aléatoire peut endommager ou « griffer » la zone d'un autre sur laquelle il a investi du temps. Avec BentoBox, les joueurs ont leurs propres îles et le système de protection empêche ou limite ce que les autres joueurs peuvent faire dans cet espace.

La protection s'étend également à la limitation des commandes qui peuvent être exécutées. Par exemple, un administrateur peut empêcher les commandes de téléportation d'être exécutées quand un joueur tombe pour les empêcher de tricher sur les dégâts de chute.

### Qu'en est-il de WorldGuard ?
WorldGuard est un plugin de protection qui fournit également des fonctions de protection. BentoBox n'utilise pas WorldGuard et il est recommandé qu'il soit désactivé dans les mondes BentoBox pour éviter les chocs. Les administrateurs peuvent utiliser WorldGuard s'ils le souhaitent dans les mondes BentoBox, mais ils doivent considérer qu'il peut y avoir des chocs entre les deux systèmes.

## Comment la Protection est-elle Gérée dans BentoBox ?
BentoBox utilise le concept de « drapeaux » pour gérer les paramètres de protection. Il y a trois types de drapeaux :

 1. **Drapeaux de protection** - ceux-ci sont explicitement conçus pour permettre ou interdire certains aspects de la protection mondiale ou insulaire.
 2. **Drapeaux de paramètres** - ce sont généralement des paramètres vrai/faux ou on/off qui peuvent être appliqués. Ils peuvent fournir une protection.
 3. **Drapeaux de paramètres mondiaux** - ce sont des drapeaux de paramètres qui déterminent le fonctionnement des choses dans le monde du jeu en général.

### Zones Protégées
BentoBox a deux zones de protection :

 1. L'île du joueur
 2. Partout ailleurs, le reste du monde

Ces zones sont généralement traitées indépendamment, mais certains paramètres mondiaux peuvent s'appliquer à l'île du joueur. Les propriétaires d'îles ont généralement la possibilité de définir les paramètres de leur propre île et les administrateurs configurent les paramètres partout ailleurs. Les administrateurs peuvent également déterminer les paramètres par défaut d'une île en ajustant le `config.yml` du mode de jeu.

La zone de protection de l'île du joueur est définie par défaut dans le `config.yml` du mode de jeu et peut être agrandie ou réduite en jeu via les commandes administrateur ou parce que le joueur a une permission. La taille de protection maximale est gouvernée par la distance entre les îles, qui est également définie dans le `config.yml` du mode de jeu.

### Modification des Paramètres
BentoBox fournit une interface graphique de paramètres d'île aux propriétaires d'îles qui leur permet de voir les paramètres de l'île. Les administrateurs peuvent réduire les paramètres d'île visibles via l'interface graphique des paramètres administrateur. Les administrateurs peuvent permettre aux joueurs de modifier les paramètres via les permissions. La valeur par défaut est que les joueurs peuvent modifier tous les paramètres qu'ils peuvent voir.

## Protection Fournie
Il y a beaucoup de drapeaux de protection et de nouveaux sont ajoutés régulièrement. Les protections peuvent être restreintes par rang, vous pouvez donc permettre aux joueurs de confiance de faire des choses que les visiteurs ne peuvent pas :

 - Visiteur
 - Coop
 - Confiance
 - Membre
 - Sous-propriétaire

Les propriétaires peuvent toujours tout faire.

Chaque fois qu'un joueur essaie de faire quelque chose dans une zone protégée, BentoBox vérifie s'il en a le droit. S'il ne l'a pas, il est bloqué et reçoit une explication.

### Trouver la raison pour laquelle quelque chose peut ou ne peut pas être fait
BentoBox fournit un outil de diagnostic administrateur : la commande `why <player>`, par ex. `/bsb why tastybento`. Quand actif, la console du serveur enregistre la raison de chaque action que ce joueur prend — autorisée ou bloquée, et quel drapeau l'a causée. Cela facilite le diagnostic des paramètres mal configurés.

Si la commande `why` dit qu'un joueur *peut* faire quelque chose mais en jeu, il ne peut pas, cela indique qu'un autre plugin ou le serveur lui-même bloque l'action, pas BentoBox.

### Qu'est-ce qui est Protégé

- Casser et placer des blocs
- Interaction de bloc : conteneurs, fours, tables de travail, tables d'enchantement, enclumes, supports de brassage, chaudrons, barils, ruches, composteurs, jukeboxs, blocs de note, leviers, boutons, portes, trappes, lits, balises, œufs de dragon, cadres d'objets, barrières, gâteau, buissons de baies
- Blocs liés à la redstone
- Élevage d'animaux
- Utilisation de seau
- Utilisation de teinture, d'œuf et d'élytres
- Véhicules : bateaux, chariots de mine, animaux montables
- Commerce avec les villageois
- Utilisation d'étiquettes de noms
- Récupération d'objets/d'expérience et lâchage d'objets
- Feu : allumage, propagation, incendie, foudre
- Endommagement ou mise à mort de mobs et d'animaux
- Utilisation de laisse et de pupitre
- Utilisation du portail
- Tonte
- Téléportation (fruit de chorus, perles de l'Ender)
- Lancer des objets y compris les potions
- TNT et autres dégâts d'explosion

## Paramètres que les Propriétaires d'Île Peuvent Modifier

Les propriétaires d'îles ouvrent l'interface graphique des paramètres avec `/island settings`. Les administrateurs peuvent masquer les paramètres individuels des joueurs s'ils préfèrent les contrôler de manière centralisée.

| Paramètre | Qu'est-ce qu'il fait |
|---|---|
| **PVP (Joueur contre Joueur)** | Si les joueurs peuvent s'attaquer mutuellement sur cette île. Désactivé par défaut. |
| **Décomposition des feuilles** | Si les blocs de feuilles se décomposent naturellement quand les bûches sont supprimées. |
| **Génération de mobs** | Si les monstres ou les animaux peuvent apparaître sur l'île, y compris à partir des blocs générateurs. |

## Paramètres Mondiaux Controlés par les Administrateurs

Ces paramètres s'appliquent à tout le monde du mode de jeu. Seuls les administrateurs peuvent les modifier, via `/[admin_command] settings`. Les joueurs peuvent voir (mais ne pas modifier) ceux-ci en mode lecture seule pour qu'ils comprennent les règles du serveur.

| Paramètre | Qu'est-ce qu'il fait | Défaut |
|---|---|---|
| **Dégâts d'explosion du coffre** | Protège les coffres d'être détruits par les explosions (Creepers, TNT, Withers, Ghasts). Prévient le griefing mais signifie que les coffres peuvent être utilisés pour faire des salles à l'épreuve des explosions. | On |
| **Clean Super Flat** | Si le générateur de monde cesse de fonctionner, les nouveaux chunks se génèrent en tant qu'herbe plate. Ce paramètre détecte et répare ces chunks. Laissez-le désactivé sauf si vous avez ce problème — c'est intensif en ressources. | Off |
| **Tilling de Terre Grossière** | Empêche les joueurs de convertir la terre grossière en terre normale en utilisant une houe. La terre est rare et précieuse dans la plupart des modes de jeu ; le labourage de terre grossière peut être exploité pour le générer à bas prix si le gravier est facile à obtenir. | Off (prévention on) |
| **Explosions Creeper** | Empêche les dégâts d'explosion Creeper aux blocs d'île. Les Creepers sont la cause la plus courante de destruction d'île. Empêcher cela facilite le jeu, mais réduit la charge de support administrateur. | On |
| **Ignition Visiteur Creeper** | Empêcher les visiteurs d'utiliser l'acier à silex pour amorcer les Creepers sur l'île de quelqu'un d'autre — une méthode de griefing courante. | On |
| **Ender Chests** | Bloquer l'accès à et la fabrication des Ender Chests, qui peuvent contrebander des objets entre les mondes du mode de jeu. Désactivez si vous utilisez un plugin Ender Chest par monde. | On (bloqué) |
| **Vol de Bloc Enderman** | Empêcher les Endermen de ramasser les blocs des îles. Sans cela, les joueurs perdent les blocs qu'ils n'ont pas supprimés eux-mêmes. | On |
| **Limitation Géographique des Mobs** | Empêcher certains mobs (par ex. le Wither, les mobs volants) de quitter l'île sur laquelle ils ont été engendrés. S'ils traversent la limite, ils sont supprimés. | On |
| **Protection Visiteur** | Protéger les visiteurs de la plupart des types de dégâts sur l'île d'un autre joueur. Téléporte également les visiteurs en sécurité s'ils tombent dans le vide. | On |
| **Protection du Cadre d'Objet** | Empêcher les cadres d'objets d'être cassés ou leurs objets frappés par les non-membres. | On |
| **Génération de Mobs Global** | Définir quels types de mobs peuvent apparaître n'importe où dans le monde, remplaçant tous les autres paramètres de génération. Par exemple, désactiver les Phantoms à l'échelle du serveur. | Varie |
| **Flux Liquide en Dehors des Îles** | Arrêter la lave et l'eau de s'écouler au-delà des limites de protection de l'île, prévenant la formation de pierre de taille entre les îles ou les inondations. | On |
| **Génération de Mobs en Dehors des Îles** | Empêcher les mobs d'apparaître dans les zones entre les îles, en concentrant l'apparition à l'intérieur des zones insulaires. Non recommandé pour AcidIsland car cela ressemble à un non-naturel. | Off |
| **Scooping d'Obsidienne** | Permettre aux joueurs de clic droit sur un seul bloc d'obsidienne isolé avec un seau vide pour récupérer la lave. Aide les nouveaux joueurs qui font accidentellement de l'obsidienne lors de la configuration du générateur de pierre de taille. | On |
| **Croissance des Plantes Hors Ligne** | Arrêter les cultures et les plantes de grandir sur une île quand aucun membre de l'équipe n'est en ligne, même si un visiteur charge les chunks. | Off |
| **Redstone Hors Ligne** | Désactiver les circuits Redstone sur une île quand aucun membre de l'équipe n'est en ligne. | Off |
| **Piston en Dehors de la Limite** | Arrêter les pistons de pousser les blocs au-delà de la limite de protection de l'île — une exploitation courante pour griffer les îles adjacentes. | On |
| **Supprimer les Mobs au Téléportation** | Effacer les mobs hostiles de la zone quand un joueur se téléporte à l'accueil de son île, prévenant les morts surprises à l'arrivée. | On |
| **Protection du Type de Générateur** | Empêcher les joueurs de modifier le type de mob des blocs générateurs en utilisant des œufs de spawn. Utile quand les générateurs sont donnés en récompenses. | On |
| **Limite de Croissance des Arbres** | Empêcher les arbres de grandir au-delà de la limite de protection de l'île. Sans cela, les arbres peuvent empiéter sur d'autres îles ou créer des blocs inaccessibles. | On |
| **Dégâts Wither** | Limiter la destruction que le Wither peut causer sur et entre les îles. | On |
