Les placeholders vous permettent d'afficher les données de n'importe quel complément BentoBox ou modes de jeu dans d'autres plugins. Et l'opposé est également vrai !

## Comment utiliser les placeholders ?

### Téléchargez l'API placeholder dont vous avez besoin.

BentoBox utilise [**PlaceholderAPI**](https://www.spigotmc.org/resources/placeholderapi.6245/) pour les placeholders.

### Lancez le serveur et vous êtes prêt !

Peu importe l'API placeholder que vous utilisez, il vous suffit de démarrer le serveur. Il n'y a **pas d'expansions à télécharger** : BentoBox gère tout !

## Comment afficher un placeholder dans le chat ?

Si vous utilisez **EssentialsChat** et **PlaceholderAPI**, vous **devez** installer [**ChatInjector**](https://www.spigotmc.org/resources/chatinjector-1-13.81201/) pour que les placeholders apparaissent dans le chat. Cependant, veuillez noter qu'il a été signalé que ChatInjector pourrait causer des problèmes.

Nous vous recommandons d'utiliser un plugin de chat alternatif qui supporte PlaceholderAPI, comme [**ChatControl**](https://www.spigotmc.org/resources/chatcontrol%E2%84%A2-the-ultimate-chat-plugin-500-000-downloads-1-2-5-1-14-4.271/).

## Comment afficher un placeholder dans un scoreboard ?

Si vous utilisez un plugin scoreboard qui ne supporte pas nativement **PlaceholderAPI**, mais supporte **MVdWPlaceholderAPI** (comme **Featherboard**), vous pouvez toujours utiliser les placeholders BentoBox, cependant, vous devez ajouter **{placeholderapi_[text]}**, et remplacez *[text]* par un placeholder sans caractères *%*, comme *{placeholderapi_bskyblock_island_name}*.

## Comment suggérer un nouveau placeholder ?

Si vous pensez qu'un placeholder pour BentoBox ou un autre placeholder par défaut pour les modes de jeu devrait être ajouté, veuillez soumettre une [demande de placeholder](https://github.com/BentoBoxWorld/BentoBox/issues/new?assignees=&labels=Status%3A+Pending%2C+Type%3A+Enhancement&template=placeholder_request.md&title=Placeholder%3A+).

## Placeholders par défaut pour les compléments de mode de jeu

Tous les compléments de mode de jeu obtiennent automatiquement certains placeholders par défaut.

**Placeholders par défaut disponibles**

| Placeholder | Description | Version |
|-------------------------------------------------------|--------------------------------------------------------------------------------|-----------|
| %[gamemode]_world_friendly_name% | Nom du monde du mode de jeu | 1.4.0 |
| %[gamemode]_world_islands% | Nombre d'îles dans le monde du mode de jeu | 1.5.0 |
| %[gamemode]_island_distance% | La moitié de la distance entre les centres des îles du monde du mode de jeu | 1.4.0 |
| %[gamemode]_island_distance_diameter% | Distance entre les îles du monde du mode de jeu | 1.5.0 |
| %[gamemode]_island_protection_range% | Rayon de la plage de protection de l'île | 1.4.0 |
| %[gamemode]_island_protection_range_diameter% | Diamètre de la plage de protection de l'île | 1.5.0 |
| %[gamemode]_island_owner% | Nom du propriétaire de l'île | 1.4.0 |
| %[gamemode]_island_creation_date% | Date de création de l'île | 1.4.0 |
| %[gamemode]_island_name% | Nom de l'île | 1.4.0 |
| %[gamemode]_island_center% | Coordonnées du centre de l'île | 1.5.0 |
| %[gamemode]_island_center_x% | Coordonnée X du centre de l'île | 1.5.0 |
| %[gamemode]_island_center_y% | Coordonnée Y du centre de l'île | 1.5.0 |
| %[gamemode]_island_center_z% | Coordonnée Z du centre de l'île | 1.5.0 |
| %[gamemode]_island_members_max% | Nombre maximum de membres que l'île peut avoir | 1.5.0 |
| %[gamemode]_island_members_count% | Nombre de membres, sous-propriétaires et propriétaire que l'île a | 1.5.0 |
| %[gamemode]_island_members_list% | Liste séparée par des virgules des noms de joueurs qui sont au moins MEMBRE de l'île | 1.13.0 |
| %[gamemode]_island_coop_list% | Liste séparée par des virgules des noms de joueurs qui sont COOP sur l'île | 2.4.2 |
| %[gamemode]_island_trusted_list% | Liste séparée par des virgules des noms de joueurs qui sont CONFIANCE sur l'île | 2.4.2 |
| %[gamemode]_island_trustees_count% | Nombre de joueurs confiés à l'île | 1.5.0 |
| %[gamemode]_island_coops_count% | Nombre de joueurs coop à l'île | 1.5.0 |
| %[gamemode]_island_visitors_count% | Nombre de joueurs actuellement visitant l'île | 1.5.0 |
| %[gamemode]_island_bans_count% | Nombre de joueurs bannis de l'île | 1.5.0 |
| %[gamemode]_island_uuid% | L'ID unique de l'île tel qu'utilisé dans la base de données | 1.15.4 |
| %[gamemode]_visited_island_protection_range% | Rayon de la plage de protection de l'île sur laquelle le joueur se tient | 1.5.2 |
| %[gamemode]_visited_island_protection_range_diameter% | Diamètre de la plage de protection de l'île sur laquelle le joueur se tient | 1.5.2 |
| %[gamemode]_visited_island_owner% | Nom du propriétaire de l'île sur laquelle le joueur se tient | 1.5.2 |
| %[gamemode]_visited_island_creation_date% | Date de création de l'île sur laquelle le joueur se tient | 1.5.2 |
| %[gamemode]_visited_island_name% | Nom de l'île sur laquelle le joueur se tient | 1.5.2 |
| %[gamemode]_visited_island_center% | Coordonnées du centre de l'île sur laquelle le joueur se tient | 1.5.2 |
| %[gamemode]_visited_island_center_x% | Coordonnée X du centre de l'île sur laquelle le joueur se tient | 1.5.2 |
| %[gamemode]_visited_island_center_y% | Coordonnée Y du centre de l'île sur laquelle le joueur se tient | 1.5.2 |
| %[gamemode]_visited_island_center_z% | Coordonnée Z du centre de l'île sur laquelle le joueur se tient | 1.5.2 |
| %[gamemode]_visited_island_members_max% | Nombre maximum de membres que l'île sur laquelle le joueur se tient peut avoir | 1.5.2 |
| %[gamemode]_visited_island_members_count% | Nombre de membres, sous-propriétaires et propriétaire que l'île a | 1.5.2 |
| %[gamemode]_visited_island_coop_list% | Liste séparée par des virgules des noms de joueurs qui sont COOP sur l'île sur laquelle le joueur se tient | 2.4.2 |
| %[gamemode]_visited_island_trusted_list% | Liste séparée par des virgules des noms de joueurs qui sont CONFIANCE sur l'île sur laquelle le joueur se tient | 2.4.2 |
| %[gamemode]_visited_island_members_list% | Liste séparée par des virgules des noms de joueurs qui sont au moins MEMBRE de l'île sur laquelle le joueur se tient | 1.13.0 |
| %[gamemode]_visited_island_trustees_count% | Nombre de joueurs confiés à l'île sur laquelle le joueur se tient | 1.5.2 |
| %[gamemode]_visited_island_coops_count% | Nombre de joueurs coop à l'île sur laquelle le joueur se tient | 1.5.2 |
| %[gamemode]_visited_island_visitors_count% | Nombre de joueurs actuellement visitant l'île sur laquelle le joueur se tient | 1.5.2 |
| %[gamemode]_visited_island_bans_count% | Nombre de joueurs bannis de l'île sur laquelle le joueur se tient | 1.5.2 |
| %[gamemode]_visited_island_uuid% | L'ID unique de l'île sur laquelle le joueur se tient | 1.15.4 |
| %[gamemode]_has_island% | Si le joueur a une île ou non | 1.5.0 |
| %[gamemode]_rank% | Rang que le joueur a sur son île | 1.5.0 |
| %[gamemode]_resets% | Nombre de fois que le joueur a réinitialisé son île | 1.5.0 |
| %[gamemode]_resets_left% | Nombre de fois que le joueur peut réinitialiser son île | 1.5.0 |
| %[gamemode]_deaths% | Nombre de fois que le joueur est mort | 1.12.0 |
| %[gamemode]_on_island% | Si le joueur est sur une île dont il fait partie ou non | 1.13.0 |

## Voir aussi
Les Gamemodes et les Compléments peuvent également apporter leurs propres placeholders. Nous vous recommandons vivement de consulter les pages suivantes, qui sont probablement plus adaptées à vos besoins.

- Gamemodes
    - [AcidIsland](../../gamemodes/AcidIsland/Placeholders)
    - [AOneBlock](../../gamemodes/AOneBlock/Placeholders)
    - [Boxed](../../gamemodes/Boxed/Placeholders)
    - [BSkyBlock](../../gamemodes/BSkyBlock/Placeholders)
    - [CaveBlock](../../gamemodes/CaveBlock/Placeholders)
    - [SkyGrid](../../gamemodes/SkyGrid/Placeholders)
- Compléments
    - [Bank](../../addons/Bank/#placeholders)
    - [Challenges](../../addons/Challenges/#placeholders)
    - [Level](../../addons/Level/#placeholders)
    - [Likes](../../addons/Likes/#placeholders)
    - [Limits](../../addons/Limits/#placeholders)
    - [MagicCobblestoneGenerator](../../addons/MagicCobblestoneGenerator/#placeholders)
