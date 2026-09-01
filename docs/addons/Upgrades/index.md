# Upgrades

**Upgrades** offre aux joueurs une courbe de progression en leur permettant d'acheter des améliorations d'île — portée de protection étendue, limites de blocs/entités plus élevées, commandes personnalisées, boosts de spawner et boosts de croissance de cultures — en utilisant de l'argent, des objets, des permissions ou le niveau d'île.

Créé et maintenu par [tastybento](https://github.com/tastybento).

{{ addon_description("Upgrades", true) }}

!!! warning "La version 1.0.0 est une réécriture complète"
    Upgrades 1.0.0 a remplacé l'ancien système basé sur les fichiers de configuration par une architecture entièrement **pilotée par base de données**. Les définitions d'amélioration, les niveaux, les prix et les récompenses sont maintenant stockés dans la base de données de BentoBox et gérés entièrement en jeu. **L'ancien `config.yml` ne définit plus les améliorations** — supprimez-le avant d'installer 1.0.0 si vous mettez à jour depuis la version 0.x. Le fichier 1.0.x généré ne contient que quelques paramètres ; voir [Ce que `config.yml` fait toujours](#ce-que-configyml-fait-toujours).

## Installation

1. Placez le jar de l'addon Upgrades dans le dossier addons du plugin BentoBox.
2. Redémarrez le serveur.
3. Au premier démarrage, 8 exemples d'améliorations sont créés automatiquement pour vous aider à démarrer.
4. Utilisez `/[admin_command] upgrade` pour personnaliser ou créer des améliorations en jeu.

## Fonctionnement

Les améliorations, leurs niveaux, prix et récompenses sont stockés dans la base de données de BentoBox (YAML, JSON, MySQL, MongoDB, etc.). Il n'y a pas de grand fichier de configuration à éditer. Toutes les données d'amélioration sont chargées, mises en cache et sauvegardées automatiquement par l'addon.

Au premier démarrage, 8 exemples d'améliorations sont créés. Une fois qu'une amélioration exemple est supprimée, elle ne sera plus recréée au prochain redémarrage. Pour déclencher à nouveau la création, supprimez le fichier marqueur `.seeded-gamemodes` du dossier de données de l'addon.

### Ce que `config.yml` fait toujours

!!! info "Depuis 1.0.4"
    Le `config.yml` indique maintenant clairement que les améliorations **ne** sont pas définies là, et les sections inertes `range-upgrade`, `command-upgrade`, `entity-icon`, `entity-group-icon` et `command-icon` de l'ancien système axé sur la configuration ont été supprimées. Le dernier fichier est [ici](https://github.com/BentoBoxWorld/Upgrades/blob/develop/src/main/resources/config.yml).

    Trois sections sont toujours lues — `block-limits-upgrade`, `entity-limits-upgrade` et `entity-group-limits-upgrade` — mais elles **ne** créent pas d'améliorations. Elles indiquent à Upgrades quelles limites il possède, afin que les limites basées sur les permissions du propre addon [Limits](../Limits/index.md) soient supprimées pour elles et que les deux ne se battent pas sur la même limite. **Seuls les noms de clés importent** (`HOPPER`, `CHICKEN`, `group1`…) ; les valeurs de palier au-dessous d'elles sont ignorées et conservées uniquement pour que les fichiers plus anciens se chargent toujours. Un bloc `gamemodes:` peut remplacer l'ensemble par mode de jeu.

    `disabled-gamemodes` (modes de jeu où Upgrades est inactif) et `chat-input-escape` (la chaîne qui annule une invite de chat dans les panneaux admin, défaut `END`) s'appliquent aussi toujours. Tout le reste dans un fichier plus ancien est inerte et peut être supprimé ; les fichiers existants ne sont pas réécrits lors de la mise à jour.

    🔺 Avant 1.0.4, une entrée `entity-limits-upgrade` n'avait d'effet que si la même entité apparaissait aussi dans la section `entity-icon` maintenant supprimée. Les entrées d'entité ont maintenant effet d'elles-mêmes — si vous aviez une entité listée sans icône correspondante, ses permissions Limits sont maintenant supprimées là où auparavant elles ne l'étaient pas.

## Niveaux et paliers

Chaque amélioration est composée d'un ou plusieurs **paliers**. Un palier couvre une plage de niveaux — par exemple, un palier peut couvrir les niveaux 0 à 4, ce qui signifie que tout joueur dont le niveau d'amélioration se situe dans cette plage bénéficie des récompenses de ce palier.

- Chaque fois qu'un joueur achète une amélioration, son niveau augmente de 1.
- Le panneau d'achat affiche la progression de chaque amélioration dans l'étiquette de l'objet, par ex. `Niveau : 2 / 5` — le niveau actuel de l'île et le niveau le plus élevé que ses paliers permettent. La ligne est stylisée par la clé de locale `upgrades.ui.upgradepanel.currentlevel` ; videz la clé pour la masquer. *(Depuis 1.0.5.)*
- Les récompenses appliquées sont toujours celles du palier dont la plage contient le niveau actuel du joueur. Entrer dans la plage d'un nouveau palier bascule immédiatement vers les récompenses de ce palier.
- Un palier peut exiger **plusieurs prix** (tous doivent être payés) et accorder **plusieurs récompenses** (toutes sont appliquées).
- Les formules de prix et de récompenses peuvent utiliser des variables (voir [Variables de formule](#variables-de-formule)) pour s'adapter automatiquement au niveau, au niveau d'île ou à la taille de l'équipe.

## Commandes

!!! tip
    `[player_command]` et `[admin_command]` sont des commandes qui diffèrent selon le mode de jeu que vous utilisez.

=== "Commandes joueur"
    - `/[player_command] upgrade`: ouvre le panneau d'achat des améliorations.

=== "Commandes admin"
    - `/[admin_command] upgrade`: ouvre l'interface admin pour créer, modifier et supprimer des améliorations et leurs niveaux.

## Types de prix

Chaque niveau d'amélioration peut exiger n'importe quelle combinaison des prix suivants (tous doivent être satisfaits pour acheter) :

| Type | Description |
|---|---|
| **Argent** | Coût en économie Vault |
| **Objets** | Des objets spécifiques doivent être dans l'inventaire du joueur |
| **Permissions** | Le joueur doit posséder un nœud de permission spécifique |
| **Niveau d'île** | Niveau d'île minimum requis (nécessite l'addon Level) |

## Types de récompenses

Chaque niveau d'amélioration peut accorder n'importe quelle combinaison des récompenses suivantes :

| Type | Description | Application |
|---|---|---|
| **Portée** | Augmente la portée de protection de l'île | À l'achat |
| **Limites de blocs** | Augmente la limite d'un type de bloc par île (nécessite l'addon Limits) | À l'achat |
| **Limites d'entités** | Augmente la limite d'un type d'entité (nécessite l'addon Limits) | À l'achat |
| **Limites de groupes d'entités** | Augmente la limite d'un groupe d'entités (nécessite l'addon Limits) | À l'achat |
| **Commandes** | Exécute des commandes console ou joueur lors de l'achat | À l'achat |
| **Boost de spawner** | Ajoute des apparitions supplémentaires à chaque événement de spawner sur l'île | Passif — toujours actif |
| **Boost de croissance de cultures** | Ajoute des ticks de croissance supplémentaires à chaque événement de croissance naturelle sur l'île | Passif — toujours actif |

### Limites de blocs, d'entités et de groupes d'entités

Les trois récompenses Limites utilisent toutes le **même éditeur de récompense** et vous permettent d'augmenter une limite par île lorsqu'une amélioration est achetée. Elles nécessitent l'addon [Limits](../Limits/index.md) — sans lui, la récompense ne fait rien.

!!! info "Upgrades *ajoute à* la limite de base — il ne la définit pas"
    La **limite de base (de départ)** pour un bloc, une entité ou un groupe est configurée dans l'**addon Limits**, pas ici. Une récompense Limites ne fait qu'ajouter un **décalage** par-dessus cette base. Chaque niveau acheté ajoute à nouveau le montant de la récompense, de sorte que la limite effective du joueur est `base de l'addon Limits + (somme des décalages d'amélioration)`.

    Exemple : si l'addon Limits plafonne les entonnoirs à `8` et qu'un joueur achète 3 niveaux d'une amélioration qui ajoute `1` entonnoir par niveau, son île peut placer `8 + 3 = 11` entonnoirs.

#### Configurer une récompense de limite

1. Exécutez `/[admin_command] upgrade` pour ouvrir l'interface admin et créer ou sélectionner une amélioration.
2. Ouvrez l'amélioration, ajoutez un **palier** (une amélioration nécessite au moins un palier), puis ouvrez ce palier et cliquez sur **Récompenses**.
3. Créez une nouvelle récompense **Limits** (l'icône de barrière). L'éditeur de récompense comporte trois paramètres :

| Paramètre | Description |
|---|---|
| **Type** | Cliquez pour faire défiler entre `BLOCK`, `ENTITY` et `ENTITY_GROUP`. Choisissez `BLOCK` pour limiter un bloc tel qu'un entonnoir. |
| **Cible** | L'élément limité. Tapez-le dans le chat. Pour `BLOCK`, utilisez un nom de [Material](https://hub.spigotmc.org/javadocs/bukkit/org/bukkit/Material.html) Bukkit (par ex. `HOPPER`, `CHEST`) ; pour `ENTITY`, un nom d'[EntityType](https://hub.spigotmc.org/javadocs/bukkit/org/bukkit/entity/EntityType.html) (par ex. `CHICKEN`) ; pour `ENTITY_GROUP`, un nom de groupe qui **correspond à un groupe défini dans l'addon Limits**. |
| **Montant** | De combien la limite est augmentée **par niveau**. Accepte un nombre simple ou une formule utilisant les [Variables de formule](#variables-de-formule) (par ex. `1`, ou `[level] * 2`). |

4. Listez la même Cible dans la section correspondante de `config.yml` (`block-limits-upgrade`, `entity-limits-upgrade` ou `entity-group-limits-upgrade`) afin que la limite basée sur les permissions du addon Limits pour elle soit supprimée — voir [Ce que `config.yml` fait toujours](#ce-que-configyml-fait-toujours).

Un panneau vert dans l'éditeur de récompense signifie que la configuration est valide ; un panneau rouge signifie qu'un champ requis (généralement la Cible) est toujours manquant.

!!! tip "Différents blocs nécessitent différentes améliorations ou paliers"
    Chaque récompense Limites cible un seul bloc/entité/groupe. Pour augmenter la limite de plusieurs types de blocs, ajoutez une récompense Limites distincte pour chacun — soit en tant que récompenses multiples sur le même palier, soit en tant qu'améliorations distinctes — et donnez à chacune sa propre Cible.

### Commandes

La récompense Commandes exécute une ou plusieurs commandes lorsqu'un joueur achète une amélioration.

- **Mode console** : les commandes s'exécutent en tant que console du serveur (à utiliser pour `/give`, les commandes de rang ou tout ce qui nécessite des permissions élevées).
- **Mode joueur** : les commandes s'exécutent en tant que joueur achetant l'amélioration (limitées à ses permissions).

Les espaces réservés suivants sont disponibles dans les chaînes de commandes :

- `[player]` — le nom du joueur qui a acheté l'amélioration
- `[owner]` — le nom du propriétaire de l'île

### Boost de spawner

Le Boost de spawner est un effet **passif, toujours actif**. Il ne fait rien au moment de l'achat ; il prend effet immédiatement et reste actif tant que l'île conserve ce niveau d'amélioration.

Chaque fois qu'un spawner sur l'île se déclenche, l'addon additionne la valeur totale de Boost de spawner de l'île pour tous les paliers d'amélioration actifs et fait apparaître autant de créatures supplémentaires du même type au même endroit.

La valeur de formule est un **multiplicateur de bonus** :

| Valeur de formule | Effet par événement de spawner |
|---|---|
| `0.5` | 50 % de chance d'une créature supplémentaire |
| `1.0` | Toujours 1 créature supplémentaire |
| `1.5` | Toujours 1 créature supplémentaire + 50 % de chance d'une deuxième |
| `2.0` | Toujours 2 créatures supplémentaires |

Les bonus provenant de plusieurs améliorations incluant une récompense de Boost de spawner sont **additionnés**. Le boost fonctionne pour tous les types de spawners.

### Boost de croissance de cultures

Le Boost de croissance de cultures est également un effet **passif, toujours actif**. Lorsqu'une culture pousse naturellement, l'addon applique des ticks de croissance supplémentaires (comme de l'os moulu) égaux à la valeur du bonus — plus le niveau d'amélioration d'un joueur est élevé, plus ses cultures poussent vite.

La valeur de formule fonctionne de la même manière que pour le Boost de spawner :

| Valeur de formule | Effet par événement de croissance naturelle |
|---|---|
| `0.5` | 50 % de chance d'un tick de croissance supplémentaire |
| `1.0` | Toujours 1 tick supplémentaire |
| `2.0` | Toujours 2 ticks supplémentaires |

Les bonus de plusieurs améliorations se cumulent. Cultures prises en charge : **Blé, Carottes, Pommes de terre, Betteraves, Verrue du Nether, Buisson de baies sucrées, Torchflower, Pitcher Plant**.

## Variables de formule

Les champs de formule dans les prix comme dans les récompenses prennent en charge les variables suivantes :

- `[level]` — le niveau actuel de l'amélioration en cours d'achat (ou actif)
- `[islandLevel]` — le niveau actuel de l'île (depuis l'addon Level ; peut être 0 si Level n'est pas installé)
- `[numberPlayer]` — le nombre de joueurs dans l'équipe de l'île

Ces variables permettent d'écrire des formules qui s'adaptent automatiquement, par exemple un coût en argent de `500 * [level]` ou un bonus de spawner de `0.1 * [level]`.

## Permissions

Les permissions sont accordées automatiquement par l'addon selon la configuration des améliorations. Consultez le [addon.yml](https://github.com/BentoBoxWorld/Upgrades/blob/develop/src/main/resources/addon.yml) pour la liste complète des permissions.

## API

La classe `UpgradeAPI` est exposée pour que d'autres addons puissent interroger et modifier les données d'amélioration de manière programmatique. Consultez les JavaDocs liés depuis la description de l'addon ci-dessus.

## Journal des modifications

??? note "Nouveautés dans v1.0.5"
    **Publié :** 3 août 2026

    - 🔡 **Niveau actuel / max dans l'étiquette de l'amélioration.** Chaque élément d'amélioration dans le panneau d'achat conduit maintenant son étiquette avec une ligne `Niveau : courant / max`, y compris sur les améliorations au maximum, afin que les joueurs puissent voir leur progression en un coup d'œil. Piloté par la nouvelle clé de locale `upgrades.ui.upgradepanel.currentlevel` (traduite dans les cinq locales fournies) — restylisez ou videz-la pour personnaliser ou masquer la ligne.
    - **API :** `UpgradeAPI` gagne un crochet `getMaxLevel(Island)` remplaçable (défaut `-1` = inconnu, qui omet la ligne) afin que les améliorations personnalisées puissent adhérer.

    [Release v1.0.5](https://github.com/BentoBoxWorld/Upgrades/releases/tag/1.0.5)

??? note "Nouveautés dans v1.0.4"
    **Publié :** 2 août 2026

    - 🔺 **Les améliorations de limites fonctionnent à nouveau.** L'achat d'améliorations de bloc/entité/groupe d'entité a échoué avec une `NoSuchMethodError` contre les versions actuelles de l'addon Limits. Upgrades utilise maintenant l'API Limits par environnement — **mettez à jour Limits à 1.28.2 ou plus récent**.
    - ⚙️ **`config.yml` nettoyé.** Le fichier documente maintenant que les améliorations sont pilotées par base de données ; les sections inertes de l'ancien système axé sur la configuration ont été supprimées. Les noms de clés `block/entity/entity-group-limits-upgrade` sont toujours lus pour supprimer les propres limites basées sur les permissions du addon Limits.
    - Neuf bugs latents corrigés (NPEs potentielles dans les chemins de formule) et nettoyage interne des classes inutilisées.

    [Release v1.0.4](https://github.com/BentoBoxWorld/Upgrades/releases/tag/1.0.4)

??? note "Nouveautés dans v1.0.3"
    **Publié le :** 16 juin 2026

    - 🐛 **Crash au démarrage corrigé.** Résout une `ConcurrentModificationException` qui pouvait crasher l'addon au démarrage lorsqu'un tier d'amélioration référençait une entrée de données d'amélioration manquante (par ex. après un seeding partiel ou des édits manuels de données). Les tiers orphelins sont maintenant ignorés en toute sécurité avec un avertissement au lieu d'avorter le chargement de tout l'addon.

    [Release v1.0.3](https://github.com/BentoBoxWorld/Upgrades/releases/tag/1.0.3)

??? warning "Nouveautés dans v1.0.0 — réécriture complète, action requise"
    **Publié :** 12 avril 2026

    - **Système d'amélioration piloté par base de données.** Toutes les améliorations, niveaux, prix et récompenses sont maintenant stockés dans la base de données de BentoBox — aucune modification de fichier de configuration requise.
    - **Nouvelle interface admin.** `/[admin_command] upgrades` ouvre une interface admin complète en jeu pour créer et modifier des améliorations via GUI et saisie par chat.
    - **Nouveaux types de récompenses :** Boost de spawner (multiplie les taux de spawner) et Boost de croissance de cultures (multiplie la vitesse de croissance).
    - **Panneau joueur basé sur template.** Le panneau d'amélioration joueur est maintenant un `TemplatedPanel` BentoBox — entièrement personnalisable via `panels/upgrades_panel.yml`.
    - **`UpgradeAPI` complet** pour l'accès programmatique depuis d'autres addons.
    - 8 exemples d'améliorations créés automatiquement au premier démarrage.
    - Corrections de compatibilité pour l'addon Limits 1.28.

    🔺 **Non compatible avec la version 0.x.** Supprimez votre ancien `config.yml` et toutes les données d'amélioration existantes avant d'installer. Il n'y a pas de migration automatique.

    [Release v1.0.0](https://github.com/BentoBoxWorld/Upgrades/releases/tag/1.0.0)

??? note "Nouveautés dans v1.0.1"
    **Publié :** 12 avril 2026

    - **Correction du créateur d'exemples.** Les exemples d'améliorations ne se régénèrent plus à chaque redémarrage après avoir été supprimés. Le créateur suit maintenant quels modes de jeu ont été initialisés dans un fichier marqueur `.seeded-gamemodes` persistant.

    [Release v1.0.1](https://github.com/BentoBoxWorld/Upgrades/releases/tag/1.0.1)

??? note "Nouveautés dans v1.0.2"
    **Publié :** 13 avril 2026

    - **Correction de la persistance.** Les définitions d'amélioration administrateur (nom, icône, prix, récompenses, paramètres de palier) et les niveaux d'achat des joueurs n'étaient stockés qu'en mémoire et perdus au redémarrage du serveur. Tous les gestionnaires de mutation sauvegardent maintenant immédiatement dans la base de données après chaque modification.

    [Release v1.0.2](https://github.com/BentoBoxWorld/Upgrades/releases/tag/1.0.2)

## Traductions

{{ translations("Upgrades") }}
