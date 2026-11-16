# Placeholders { #placeholders }

Les placeholders permettent à d'autres plugins d'afficher les informations de BentoBox : le nom de l'île d'un joueur ou son niveau sur un tableau de bord, son rang dans le chat, le nombre d'îles dans un hologramme, etc.

## Configuration { #setting-up }

1. Installez [PlaceholderAPI](https://www.spigotmc.org/resources/placeholderapi.6245/).
2. Redémarrez le serveur.

C'est tout. BentoBox enregistre ses placeholders auprès de PlaceholderAPI lui-même ; il n'y a pas d'expansion à télécharger avec `/papi ecloud`.

Utilisez ensuite les placeholders dans n'importe quel plugin qui supporte PlaceholderAPI (tableaux de bord, listes de tab, chat, hologrammes…).

## Comment les placeholders sont nommés { #how-placeholders-are-named }

Chaque mode de jeu enregistre sa propre copie de chaque placeholder, commençant par le nom du mode de jeu en minuscules :

```
%bskyblock_island_name%
%aoneblock_island_members_count%
%acidisland_rank%
```

Les tableaux ci-dessous écrivent ce préfixe comme `[gamemode]`. Les placeholders des addons commencent par le nom de l'addon, puis le mode de jeu, par exemple `%Level_bskyblock_island_level%` ; ils sont répertoriés sur la page de chaque [addon](../addons/Level/index.md#placeholders).

Il y a deux sortes :

- `[gamemode]_island_...` concerne **l'île propre du joueur** dans ce mode de jeu.
- `[gamemode]_visited_island_...` concerne **l'île sur laquelle le joueur se tient**, qui pourrait être celle de quelqu'un d'autre.

## Trouver un placeholder en jeu { #finding-a-placeholder-in-game }

| Commande | Ce qu'elle fait |
|---|---|
| `/bentobox placeholders` | Ouvre un menu pour parcourir chaque placeholder de BentoBox et les addons, et activez ou désactivez les placeholders individuels |
| `/bentobox dump-placeholders` | Écrit chaque placeholder enregistré dans `plugins/BentoBox/placeholder-dump.md` |
| `/papi parse me %bskyblock_island_name%` | Montre ce qu'un placeholder retourne pour vous (une commande de PlaceholderAPI) |

## Placeholders BentoBox { #bentobox-placeholders }

Ceux-ci sont enregistrés pour chaque mode de jeu.

{{ placeholders_source("BentoBox") }}

### Placeholders numérotés { #numbered-placeholders }

Les placeholders se terminant par `_<n>` sont enregistrés une fois pour chaque nombre :

- `island_member_name_<n>`, `island_member_rank_<n>` et `island_banned_name_<n>` (et leurs versions `visited_island_`) vont de 1 à 50, pour lister une équipe ou une liste de bannissement une ligne à la fois, par exemple `%bskyblock_island_member_name_1%`.
- `island_name_<n>` et `island_memberlist_<n>` vont de 1 au nombre d'îles qu'un joueur peut posséder (`concurrent-islands`). Voir [Îles Multiples](ConcurrentIslands.md).

### Placeholders de drapeaux { #flag-placeholders }

Chaque drapeau de protection, paramètre d'île et paramètre mondial a un placeholder : `flag_` suivi de l'ID du drapeau en minuscules.

| Type de drapeau | Retourne |
|---|---|
| Drapeau de protection | Le rang minimum autorisé sur l'île du joueur, par exemple `Membre` |
| Paramètre d'île | `true` ou `false` pour l'île du joueur |
| Paramètre mondial | `true` ou `false` pour le monde du mode de jeu |

```
%bskyblock_flag_break_blocks%    → Membre
%bskyblock_flag_pvp_overworld%   → false
```

Les ID des drapeaux sont répertoriés dans [Drapeaux](Flags.md). Les drapeaux ajoutés par les addons obtiennent des placeholders automatiquement.

## Pages des modes de jeu { #game-mode-pages }

La page de chaque mode de jeu répertorie ces placeholders avec son propre préfixe rempli, avec les propres placeholders du mode de jeu :

[AcidIsland](../gamemodes/AcidIsland/Placeholders.md) · [AOneBlock](../gamemodes/AOneBlock/Placeholders.md) · [Boxed](../gamemodes/Boxed/Placeholders.md) · [BSkyBlock](../gamemodes/BSkyBlock/Placeholders.md) · [CaveBlock](../gamemodes/CaveBlock/Placeholders.md) · [ChunkBlock](../gamemodes/ChunkBlock/Placeholders.md) · [Poseidon](../gamemodes/Poseidon/Placeholders.md) · [SkyGrid](../gamemodes/SkyGrid/Placeholders.md) · [TradeWinds](../gamemodes/TradeWinds/Placeholders.md)

## Dépannage { #troubleshooting }

**Un placeholder s'affiche comme du texte (`%bskyblock_island_name%`) au lieu d'une valeur.**
Vérifiez que PlaceholderAPI est installé, que le plugin qui l'affiche supporte PlaceholderAPI, et que le placeholder n'est pas désactivé dans `/bentobox placeholders`. Certains plugins de chat ont besoin d'un paramètre supplémentaire ou d'un plugin pour analyser les placeholders dans les messages de chat. Testez avec `/papi parse me <placeholder>`.

**Un placeholder est vide.**
Le joueur n'a pas d'île dans ce mode de jeu, ou pour les placeholders `visited_island_`, ne se tient pas sur une île.

**Un placeholder d'un addon n'existe pas.**
Vérifiez que l'addon est installé et activé pour ce mode de jeu. Les placeholders des addons commencent par le nom de l'addon, puis le mode de jeu : `%Level_bskyblock_island_level%`. Vérifiez aussi qu'il n'a pas été désactivé dans `/bentobox placeholders`.

**J'ai besoin d'un placeholder qui n'existe pas.**
[Demandez-en un](https://github.com/BentoBoxWorld/BentoBox/issues/new?labels=Status%3A+Pending%2C+Type%3A+Enhancement&template=placeholder_request.md&title=Placeholder%3A+) sur GitHub.
