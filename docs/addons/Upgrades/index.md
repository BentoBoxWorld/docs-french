# Upgrades

**Upgrades** offre aux joueurs une courbe de progression en leur permettant d'acheter des améliorations d'île — portée de protection étendue, limites de blocs/entités plus élevées, commandes personnalisées, boosts de spawner et boosts de croissance de cultures — en utilisant de l'argent, des objets, des permissions ou le niveau d'île.

Créé et maintenu par [tastybento](https://github.com/tastybento).

{{ addon_description("Upgrades", true) }}

!!! warning "La version 1.0.0 est une réécriture complète"
    Upgrades 1.0.0 a remplacé l'ancien système basé sur les fichiers de configuration par une architecture entièrement **pilotée par base de données**. Les définitions d'amélioration, les niveaux, les prix et les récompenses sont maintenant stockés dans la base de données de BentoBox et gérés entièrement en jeu. **L'ancien `config.yml` n'est plus utilisé** — supprimez-le avant d'installer 1.0.0 si vous mettez à jour depuis la version 0.x.

## Installation

1. Placez le jar de l'addon Upgrades dans le dossier addons du plugin BentoBox.
2. Redémarrez le serveur.
3. Au premier démarrage, 8 exemples d'améliorations sont créés automatiquement pour vous aider à démarrer.
4. Utilisez `/[admin_command] upgrades` pour personnaliser ou créer des améliorations en jeu.

## Fonctionnement

Les améliorations, leurs niveaux, prix et récompenses sont stockés dans la base de données de BentoBox (YAML, JSON, MySQL, MongoDB, etc.). Il n'y a pas de grand fichier de configuration à éditer. Toutes les données d'amélioration sont chargées, mises en cache et sauvegardées automatiquement par l'addon.

Au premier démarrage, 8 exemples d'améliorations sont créés. Une fois qu'une amélioration exemple est supprimée, elle ne sera plus recréée au prochain redémarrage. Pour déclencher à nouveau la création, supprimez le fichier marqueur `.seeded-gamemodes` du dossier de données de l'addon.

## Commandes

!!! tip
    `[player_command]` et `[admin_command]` sont des commandes qui diffèrent selon le mode de jeu que vous utilisez.

=== "Commandes joueur"
    - `/[player_command] upgrade`: ouvre le panneau d'achat des améliorations.

=== "Commandes admin"
    - `/[admin_command] upgrades`: ouvre l'interface admin pour créer, modifier et supprimer des améliorations et leurs niveaux.

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

| Type | Description |
|---|---|
| **Portée** | Augmente la portée de protection de l'île |
| **Limites de blocs** | Augmente la limite d'un type de bloc (nécessite l'addon Limits) |
| **Limites d'entités** | Augmente la limite d'un type d'entité (nécessite l'addon Limits) |
| **Limites de groupes d'entités** | Augmente la limite d'un groupe d'entités (nécessite l'addon Limits) |
| **Commandes** | Exécute des commandes console ou joueur lors de l'achat |
| **Boost de spawner** | Multiplie les taux d'apparition des spawners |
| **Boost de croissance de cultures** | Multiplie la vitesse de croissance des cultures |

## Variables de formule de niveau

Dans les formules de prix, les variables suivantes sont disponibles :

- `[level]` — le niveau actuel de l'amélioration en cours d'achat
- `[islandLevel]` — le niveau actuel de l'île (depuis l'addon Level ; peut être 0)
- `[numberPlayer]` — le nombre de joueurs dans l'équipe de l'île

## Permissions

Les permissions sont accordées automatiquement par l'addon selon la configuration des améliorations. Consultez le [addon.yml](https://github.com/BentoBoxWorld/Upgrades/blob/develop/src/main/resources/addon.yml) pour la liste complète des permissions.

## API

La classe `UpgradeAPI` est exposée pour que d'autres addons puissent interroger et modifier les données d'amélioration de manière programmatique. Consultez les JavaDocs liés depuis la description de l'addon ci-dessus.

## Journal des modifications

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

## Traductions

{{ translations("Upgrades") }}
