# InvSwitcher

**InvSwitcher** sépare les inventaires des joueurs et d'autres aspects entre les différents mondes.

Créé et maintenu par [tastybento](https://github.com/tastybento).

{{ addon_description("InvSwitcher") }}

Ce qui suit est commuté par monde :

* Inventaire et armure
* Avancées
* Niveau de nourriture
* Expérience
* Santé
* Mode de jeu (créatif, survie, etc.)
* Argent (économie par monde, ajouté dans 1.18.0 — **désactivé par défaut depuis 1.19.3**, activer avec `options.money: true`)

## Comment l'utiliser

1. Placez le fichier jar de l'addon dans le dossier des addons du plugin BentoBox
2. Redémarrez le serveur
3. Fait!

## Config.yml

InvSwitcher possède un `config.yml` avec deux sections principales.

### Mondes

Liste les mondes de mode de jeu dans lesquels InvSwitcher opère. Les mondes Nether et End sont inclus automatiquement.

```yml
worlds:
- acidisland_world
- oneblock_world
- boxed_world
- bskyblock_world
- skyblock-world
- caveblock-world
- poseidon_world
- stranger_world
- skygrid-world     # ajouté à la config par défaut dans 1.19.2
- raft_world        # ajouté dans 1.19.2
- brix_world        # ajouté dans 1.19.2
- parkour_world     # ajouté dans 1.19.2
- tradewinds_world
```

!!! warning "Les configs existantes ne sont pas réécrites"
    Les nouveaux mondes par défaut n'apparaissent qu'à la première installation. Si votre `config.yml` précède 1.19.2 et que vous utilisez SkyGrid, Raft, Brix, Parkour ou TradeWinds, ajoutez ces entrées à la liste `worlds:` à la main et redémarrez. Un monde qui n'est pas listé n'est pas géré en silence — InvSwitcher enregistre les mondes sur lesquels il se branche au démarrage, donc vérifiez cette liste pour confirmer.

### Options

Contrôle quels aspects du joueur sont commutés par monde et, optionnellement, par île.

```yml
options:
  inventory: true
  health: true
  food: true
  advancements: true
  gamemode: true       # mode de jeu (Survie/Créatif/etc.)
  experience: true
  ender-chest: true
  statistics: true
  money: false         # Argent par monde (ajouté dans 1.18.0). Désactivé par défaut depuis 1.19.3. Nécessite Vault.
  # Commutation d'inventaire par île (ajoutée dans 1.17.0)
  # L'option au niveau du monde doit aussi être true pour que l'option île prenne effet.
  islands:
    active: true       # Activer la commutation par île globalement
    inventory: true    # Donner aux joueurs un inventaire différent sur chaque île qu'ils possèdent
    health: false
    food: false
    advancements: false
    gamemode: false
    experience: false
    ender-chest: true
    statistics: false
    money: false       # Portefeuilles par île (ajouté dans 1.18.0). False = argent par monde uniquement.
```

Définissez `islands.active: true` pour permettre aux joueurs qui possèdent plus d'une île d'avoir des inventaires séparés (et autres aspects) par île, pas seulement par monde de mode de jeu.

### Économie

Ajouté dans 1.18.0. **Désactivé par défaut depuis 1.19.3** — InvSwitcher ne s'enregistre plus en tant qu'économie Vault sauf si vous optez pour `options.money: true`. Une fois activé, InvSwitcher s'enregistre comme fournisseur d'économie Vault et garde un **solde distinct pour chaque monde commuté**. Les transactions (ventes en boutique, `/pay`, jobs, etc.) sont dirigées vers le solde du monde auquel elles appartiennent — même quand le joueur ciblé est hors ligne ou dans un autre monde. Les mondes qu'InvSwitcher ne gère pas sont transmis à votre plugin d'économie existant (par ex. EssentialsX) ; si aucune autre économie n'est présente, InvSwitcher gère tous les mondes lui-même.

!!! warning "Nécessite Vault"
    L'argent par monde nécessite le plugin [Vault](https://www.spigotmc.org/resources/vault.34315/). Un plugin d'économie séparé est optionnel — InvSwitcher peut être la seule économie. Si vous utilisez l'addon **Bank**, les portefeuilles d'île deviennent eux aussi par monde.

Le bloc `economy:` n'est utilisé que lorsque `options.money` vaut `true` :

```yml
economy:
  starting-balance: 0.0              # Solde donné à la première entrée dans un monde géré (sauf si importé)
  currency-name-singular: Dollar
  currency-name-plural: Dollars
  fractional-digits: 2               # Chiffres après la virgule
  import-existing-balances: true     # Importer une fois le solde existant de chaque joueur, à la première entrée
  delegate-unmanaged-worlds: true    # Transmettre les mondes non gérés au plugin d'économie précédent
  debug: false                       # Journaliser chaque transaction dans la console (verbeux)
```

## Commandes

Ajouté dans 1.18.0. Chaque mode de jeu géré obtient ses propres commandes d'économie, limitées au monde de ce mode de jeu, donc `/bsb balance` affiche votre solde BSkyBlock et `/ai balance` votre solde AcidIsland, où que vous vous trouviez.

!!! tip
    `[player_command]` et `[admin_command]` sont les commandes qui diffèrent selon le mode de jeu que vous utilisez.

=== "Commandes joueur"

    | Commande | Description |
    |---|---|
    | `/[player_command] balance` | Afficher votre solde d'argent pour ce monde |
    | `/[player_command] pay <joueur> <montant>` | Payer un autre joueur |

=== "Commandes admin"

    | Commande | Description |
    |---|---|
    | `/[admin_command] eco give <joueur> <montant>` | Donner de l'argent à un joueur |
    | `/[admin_command] eco take <joueur> <montant>` | Retirer de l'argent à un joueur |
    | `/[admin_command] eco set <joueur> <montant>` | Définir le solde d'un joueur |
    | `/[admin_command] eco balance <joueur>` | Afficher le solde d'un joueur |

## Permissions

!!! tip
    `[gamemode]` est un préfixe qui diffère selon le mode de jeu que vous exécutez — par exemple `bskyblock.invswitcher.balance`.

Les commandes d'économie ne sont enregistrées que lorsque `options.money` est activé et que Vault est installé, donc ces permissions n'ont d'importance que sur les serveurs exécutant l'économie par monde. *(Déclarées dans `addon.yml` depuis 1.19.2 — avant cela, les nœuds n'étaient pas enregistrés, donc les commandes étaient refusées à tous sauf aux ops.)*

=== "Permissions joueur"
    - `[gamemode].invswitcher.balance` - (par défaut : `true`) - Le joueur peut utiliser la commande `balance`.
    - `[gamemode].invswitcher.pay` - (par défaut : `true`) - Le joueur peut utiliser la commande `pay`.

=== "Permissions admin"
    - `[gamemode].invswitcher.admin.eco` - (par défaut : `op`) - Le joueur peut utiliser la commande admin `eco`.
    - `[gamemode].invswitcher.admin.eco.balance` - (par défaut : `op`) - Le joueur peut utiliser la commande admin `eco balance`.
    - `[gamemode].invswitcher.admin.eco.give` - (par défaut : `op`) - Le joueur peut utiliser la commande admin `eco give`.
    - `[gamemode].invswitcher.admin.eco.take` - (par défaut : `op`) - Le joueur peut utiliser la commande admin `eco take`.
    - `[gamemode].invswitcher.admin.eco.set` - (par défaut : `op`) - Le joueur peut utiliser la commande admin `eco set`.

!!! note
    Les nœuds joueur sont par défaut à `true`, donc la plupart des serveurs n'ont rien à faire. Si votre plugin de permissions refuse les nœuds non listés, accordez-les à votre groupe par défaut.

## Ce qu'il fait
Cet addon donnera aux joueurs un inventaire, une santé, un niveau de nourriture, des avancées et une expérience séparés pour chaque mode de jeu installé et leurs mondes correspondants. Il permet aux joueurs de jouer à chaque mode de jeu indépendamment l'un de l'autre.

## Un exemple
L'inventaire, la santé, le niveau de nourriture, les avancées et l'expérience de **BSkyBlock** sont partagés uniquement entre ses mondes correspondants :
- BSkyBlock_world
- BSkyBlock_world_nether
- BSkyBlock_world_the_end

**Veuillez noter :**
- Ce n'est pas limité aux mondes BentoBox. Cela s'applique à tous les mondes du serveur (pour l'instant).

## Journal des modifications

??? note "Nouveautés dans v1.19.3"
    **Publié :** 4 août 2026

    - ⚙️ **L'argent par monde est maintenant désactivé par défaut.** InvSwitcher ne s'enregistre plus en tant qu'économie Vault sauf si vous optez pour `options.money: true` dans `config.yml`. Rien d'autre à propos de la fonctionnalité n'a changé.

    ⚙️ **Les configs existantes ne sont pas réécrites** — le nouveau défaut s'applique uniquement aux nouvelles installations. Si votre `config.yml` contient déjà `options.money: true` et que vous ne voulez pas qu'InvSwitcher gère l'argent, réglez-le à `false` et redémarrez.

    [Release v1.19.3](https://github.com/BentoBoxWorld/InvSwitcher/releases/tag/1.19.3)

??? warning "Nouveautés dans v1.19.2 — correction de retour en arrière, nouvelles permissions et mondes par défaut"
    **Publié :** 4 août 2026

    Compatibilité : BentoBox 3.17.0 · Paper Minecraft 1.21.5 – 26.1.2 · Java 21.

    - 🐛 **Les inventaires ne font plus un retour en arrière pour les joueurs en ligne à l'arrêt.** BentoBox ferme sa base de données immédiatement après la désactivation des addons, donc la sauvegarde d'arrêt asynchrone a perdu la course et a été silencieusement abandonnée — tout ce qu'un joueur a fait depuis son dernier changement de monde a été perdu, et l'instantané périmé a ensuite été réécrit sur son inventaire réel à la connexion. Les sauvegardes d'arrêt sont maintenant synchrones ; les sauvegardes en jeu normales restent asynchrones. Les joueurs qui se sont déconnectés avant l'arrêt n'étaient jamais affectés, et les données déjà perdues ne peuvent pas être récupérées.
    - 🔺 **Les commandes d'économie fonctionnent pour les joueurs normaux.** `/[player_command] balance` et `pay` ont échoué avec une erreur de permission pour tous les non-op car `addon.yml` n'a déclaré aucune permission. Les nœuds sont maintenant enregistrés — `[gamemode].invswitcher.balance` et `.pay` sont par défaut à `true`, les nœuds admin `eco` à `op`. Voir la section Permissions ci-dessus. Si votre plugin de permissions refuse les nœuds non listés, accordez les nœuds joueur à votre groupe par défaut.
    - ⚙️ **Les mondes de mode de jeu manquants ajoutés à la config par défaut.** `skygrid-world`, `raft_world`, `brix_world` et `parkour_world` étaient absents de la liste `worlds:` expédiée, donc une installation fraîche ne les gérait pas en silence. **Les configs existantes ne sont pas réécrites** — ajoutez les entrées à la main si vous utilisez ces modes de jeu.
    - 📄 Nouvelle section sur la non-exécution d'un deuxième gestionnaire d'inventaire (Multiverse-Inventories, PerWorldInventory, MultiInv) — voir [Compatibilité avec d'autres plugins d'inventaire](#compatibility-with-other-inventory-plugins).

    [Release v1.19.2](https://github.com/BentoBoxWorld/InvSwitcher/releases/tag/1.19.2)

??? note "Nouveautés dans v1.19.1"
    **Publié :** 2 juillet 2026

    Version de correction de bugs — remplaçable sans modification de configuration ou de locale.

    - 🐛 **Boucle infinie de mort/résurrection avec santé par île corrigée.** Avec la santé par île activée, un joueur propriétaire de plus d'une île pouvait rester bloqué dans une boucle de respawn/écran de mort sans fin après la mort. Quand son état était capturé en pleine mort, il enregistrait une santé de `0` ; recharger cette valeur sur l'île de mort appliquait `setHealth(0)`, le tuant à nouveau dès le chargement du monde. InvSwitcher n'applique maintenant jamais une santé stockée fatale à un joueur vivant — une valeur stockée de `0` (seulement jamais produite en pleine mort) restaure la santé complète à la place, correspondant au comportement de respawn vanilla.

    [Release v1.19.1](https://github.com/BentoBoxWorld/InvSwitcher/releases/tag/1.19.1)

??? note "Nouveautés dans v1.19.0"
    **Publié :** 21 juin 2026

    Suite à la version 1.18.0 d'économie par monde. Remplaçable sans modification de configuration ou de locale.

    - 🐛 **L'économie autonome fonctionne maintenant toute seule.** InvSwitcher enregistre sa propre économie Vault par monde, mais BentoBox accroche Vault avant l'activation des addons, donc quand InvSwitcher était la seule économie du serveur, cet accrochage précoce ne trouvait rien et était abandonné — et les addons dépendant de l'économie comme **Bank** se désactivaient avec *"Vault est nécessaire"*. InvSwitcher enregistre maintenant un accrochage Vault frais avec BentoBox une fois que son fournisseur est en direct, donc il fonctionne comme l'économie unique du serveur (aucun plugin d'économie séparé comme EssentialsX n'est nécessaire).
    - 🐛 **Solde correct rapporté pour les transactions d'économie hors ligne.** L'admin `eco give/set/take` sur un joueur hors ligne rapportait un solde obsolète (par ex. « Nouveau solde : 0.00 » juste après avoir donné 2 000). L'argent était toujours stocké correctement ; le message de confirmation relisait le solde avant que la sauvegarde asynchrone n'ait vidé. Les commandes rapportent désormais le solde autoritaire retourné par la transaction elle-même, et le chemin de lecture après écriture hors ligne a été renforcé pour que deux transactions séquentielles rapides ne puissent plus perdre une mise à jour.

    [Release v1.19.0](https://github.com/BentoBoxWorld/InvSwitcher/releases/tag/1.19.0)

??? note "Nouveautés dans v1.17.0"
    **Publié :** 31 mars 2026

    - **Commutation d'inventaire par île.** Les joueurs qui possèdent plus d'une île peuvent maintenant avoir des inventaires séparés (et optionnellement santé, nourriture, expérience, coffre de l'end, statistiques) par île dans le même mode de jeu. Activez avec `options.islands.active: true` et configurez chaque sous-option. L'option au niveau du monde doit aussi être `true` pour que son équivalent île prenne effet.
    - ⚙️ Nouvelle section `options.islands` dans `config.yml`.
    - Correction : l'inventaire était perdu lors du retour à l'île d'origine.

    [Release v1.17.0](https://github.com/BentoBoxWorld/InvSwitcher/releases/tag/1.17.0)

??? note "Nouveautés dans v1.17.1"
    **Publié le :** 2026-05-09

    - 🐛 **Correction de l'inventaire vidé lors d'un téléport d'un monde BentoBox vers un monde non-BentoBox.** Auparavant, quand un joueur quittait un monde de jeu BentoBox (par ex. BSkyBlock) pour un monde non-BentoBox (par ex. l'overworld par défaut ou un monde d'un plugin tiers), son inventaire « extérieur » pouvait être perdu parce que chaque monde non-BentoBox stockait ses données sous sa propre clé. Tous les mondes non-BentoBox partagent désormais une seule clé de stockage, donc l'inventaire du joueur est toujours restauré correctement. Inclut une migration automatique des données enregistrées sous les anciennes clés par monde.

    [Release v1.17.1](https://github.com/BentoBoxWorld/InvSwitcher/releases/tag/1.17.1)

??? warning "Nouveautés dans v1.18.0 — nécessite BentoBox 3.17.0"
    **Publié le :** 2026-05-31

    - 🔺⚙️🔡 **Argent par monde.** InvSwitcher peut désormais donner à chaque monde de jeu sa propre économie séparée, en plus des inventaires, de la santé, de l'XP et des statistiques qu'il commute déjà. Avec `options.money` activé, il s'enregistre comme fournisseur d'économie Vault et dirige chaque transaction vers le solde du bon monde — même quand le joueur est hors ligne ou dans un autre monde.
    - ⚙️ **Nouvelle config :** `options.money`, `options.islands.money`, et un bloc `economy:` (solde de départ, noms de devise, chiffres décimaux, bascule d'import, bascule de délégation, débogage). Les configs existantes continuent de fonctionner ; les nouvelles clés sont ajoutées avec des valeurs par défaut sûres.
    - 🔡 **Nouvelles commandes et placeholders :** `balance` et `pay` par mode de jeu pour les joueurs, `eco give/take/set/balance` pour les admins, ainsi que les placeholders `<gamemode>_invswitcher_balance` et `<gamemode>_invswitcher_balance_formatted`, traduits dans toutes les langues fournies par BentoBox.
    - 🐛 Les avancées ne gonflent plus l'expérience lors d'un changement de monde.
    - 🐛 Les réinitialisations d'île de BentoBox ne vident plus l'inventaire du mauvais monde — InvSwitcher efface désormais les données *stockées* du bon monde à la place.

    🔺 **Nécessite BentoBox 3.17.0 :** InvSwitcher écoute désormais les événements de réinitialisation de joueur de BentoBox (dont le nouvel événement de réinitialisation d'argent), introduits dans la 3.17.0. Il ne se chargera pas sur les versions antérieures de BentoBox.

    🔺 **Changement de comportement de l'économie :** quand `options.money` est activé, InvSwitcher devient le fournisseur d'économie Vault du serveur. Les mondes qu'il ne gère pas sont transmis à votre économie existante (par ex. EssentialsX) ; les mondes gérés obtiennent leur propre solde par monde. Nécessite le plugin Vault.

    [Release v1.18.0](https://github.com/BentoBoxWorld/InvSwitcher/releases/tag/1.18.0)

## Placeholders

{{ placeholders_source("InvSwitcher") }}

## Traductions

{{ translations("InvSwitcher") }}
