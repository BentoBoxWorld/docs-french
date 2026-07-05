# Glossaire

Nouveau sur BentoBox ? Cette page explique les termes clés utilisés dans la documentation.

---

## Addon
Un fichier (`.jar`) qui étend BentoBox avec de nouvelles fonctionnalités. Les addons vont dans `plugins/BentoBox/addons/` — **pas** dans le dossier `plugins/` de votre serveur. Il y a deux types : [addons de mode de jeu](#mode-de-jeu) et [addons de fonctionnalité](#addon-de-fonctionnalite). Voir [Addons](BentoBox/About/Addons.md).

## Commande d'administration
Chaque mode de jeu a une commande réservée aux administrateurs pour gérer les îles, les paramètres et les joueurs. Pour BSkyBlock c'est `/bsb`, pour AcidIsland c'est `/acid admin`, etc. La commande exacte est listée dans la documentation de chaque mode de jeu.

## Plan directeur
Un modèle sauvegardé d'une île construite utilisé lorsqu'un joueur crée une nouvelle île. BentoBox est livré avec des plans directeurs par défaut, mais les administrateurs peuvent créer les leurs dans le jeu. Les plans directeurs sont stockés dans `plugins/BentoBox/blueprints/`. Voir [Plans directeurs](BentoBox/About/BlueprintsSummary.md).

## Paquet de plans directeurs
Un ensemble nommé de plans directeurs (un chacun pour l'Overworld, le Nether et l'End) groupés ensemble. Lorsqu'un joueur crée une nouvelle île, il peut se voir proposer un choix de paquets. Chaque paquet peut avoir sa propre icône, description et exigence de permission.

## Coop
Un rang d'île temporaire accordé aux joueurs qui ne sont pas des membres d'équipe à part entière. L'accès d'un joueur coop expire quand le membre d'équipe qui l'a accordé se déconnecte. Voir [Équipes](BentoBox/About/Teams.md).

## Addon de fonctionnalité
Un addon qui ajoute des fonctionnalités supplémentaires (défis, vol, portails, etc.) en plus d'un mode de jeu. Les addons de fonctionnalité sont optionnels. Voir [Addons](BentoBox/About/Addons.md).

## Drapeau
Un seul bouton de protection ou de paramètres qui contrôle ce qui est ou n'est pas autorisé sur une île ou dans le monde du jeu. Les drapeaux sont gérés via l'interface graphique des paramètres en jeu. Exemples : si les visiteurs peuvent casser des blocs, si les creepers peuvent exploser, si les blocs de feuilles pourrissent. Voir [Protection](BentoBox/About/Protections.md).

## Mode de jeu
Un addon qui définit le type de monde de jeu dans lequel jouent les joueurs — le type de monde, la façon dont les îles sont générées et le défi global. Exemples : BSkyBlock, AcidIsland, AOneBlock. Vous devez installer au moins un mode de jeu pour que BentoBox fasse quelque chose. Voir [Modes de jeu](BentoBox/About/GameModes.md).

## Île
La zone protégée du monde du jeu qui appartient à un joueur ou à une équipe. Chaque joueur obtient une île par mode de jeu. Les îles sont créées automatiquement lorsqu'un joueur utilise la commande principale pour la première fois. Voir [Gestion des îles](BentoBox/About/IslandManagement.md).

## Distance entre îles
L'écart entre les centres des îles adjacentes dans la grille du monde. Défini une fois dans le `config.yml` du mode de jeu et **ne peut pas être changé** une fois que les îles existent. La plage de protection ne peut jamais dépasser la moitié de cette valeur. Voir la [FAQ](FAQ.md#how-do-i-change-the-island-distance).

## Locale
Un fichier de langue qui contient tout le texte en jeu pour BentoBox ou un addon dans une langue spécifique. Les fichiers locale vivent dans `plugins/BentoBox/locales/`. Voir [Support multilingue](BentoBox/About/Multilingual.md).

## Propriétaire
Le joueur qui a créé une île ou à qui la propriété a été transférée. Il y a toujours exactement un propriétaire par île. Les propriétaires ont un contrôle total sur les paramètres de leur île et leur équipe.

## Espace réservé
Un code court comme `%bskyblock_island_name%` que d'autres plugins peuvent utiliser pour afficher les données de BentoBox — par exemple dans le chat, les tableaux de bord ou les hologrammes. BentoBox utilise PlaceholderAPI. Voir [Espaces réservés](BentoBox/Placeholders.md).

## Commande du joueur
La commande principale que les joueurs utilisent pour interagir avec un mode de jeu. Pour BSkyBlock c'est `/island` (ou `/is`), pour AOneBlock c'est `/oneblock` (ou `/ob`), etc. La commande exacte est listée dans la documentation de chaque mode de jeu.

## Plage de protection
Le rayon de la zone autour du centre d'une île qui est protégée. Aucun autre joueur ne peut construire, casser ou interagir dans cette zone sans permission. Toujours plus petit ou égal à la moitié de la [distance entre îles](#distance-entre-iles). Peut être étendu par commande d'administration ou permission du joueur.

## Rang
Un niveau de confiance assigné aux joueurs par rapport à une île spécifique. Du plus bas au plus haut : **Banni**, **Visiteur**, **Coop**, **Réputé**, **Membre**, **Propriétaire secondaire**, **Propriétaire**. Les rangs contrôlent quelles actions un joueur peut effectuer sur une île. Voir [Équipes](BentoBox/About/Teams.md).

## Réinitialisation
Quand un joueur supprime sa propre île et recommence avec une nouvelle. Le nombre de fois qu'un joueur peut réinitialiser est configurable. Voir [Gestion des îles](BentoBox/About/IslandManagement.md#resetting-an-island).

## Propriétaire secondaire
Un rang d'île en dessous du Propriétaire mais au-dessus du Membre. Les propriétaires secondaires ont presque les mêmes permissions que le propriétaire. Plusieurs propriétaires secondaires peuvent exister sur une île.

## Réputé
Un rang de visiteur permanent pour les joueurs qui ne sont pas des membres d'équipe à part entière. Contrairement à [coop](#coop), le statut de réputé n'expire pas quand le joueur qui l'accorde se déconnecte. Voir [Équipes](BentoBox/About/Teams.md).

## Visiteur
Le rang par défaut pour tout joueur qui est sur une île qu'il ne possède pas ou auxquelle il n'appartient pas. Ce que les visiteurs peuvent faire est contrôlé par le propriétaire de l'île via l'interface graphique des paramètres.

## Paramètres du monde
Les paramètres de protection et de comportement qui s'appliquent à tout le monde du mode de jeu, pas seulement aux îles individuelles. Seuls les administrateurs peuvent les modifier. Accessibles via `/[admin_command] settings`. Voir [Protection](BentoBox/About/Protections.md).
