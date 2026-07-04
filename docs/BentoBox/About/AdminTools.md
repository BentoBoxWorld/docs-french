# Outils d'Administration

BentoBox donne aux administrateurs de serveur une gamme d'outils pour gérer le jeu, enquêter sur les problèmes et garder les choses fonctionnant correctement — tout sans avoir besoin d'éditer les fichiers manuellement.

## Le Panneau de Gestion

Le hub administrateur principal est le **Panneau de Gestion**, ouvert avec :
```
/bentobox manage
```
(ou son alias `/bbox manage`)

De là, vous pouvez voir tous les modes de jeu exécutés, les îles actives et la santé du serveur de base en un coup d'œil.

## La Commande `/bentobox`

Toute l'administration BentoBox de haut niveau passe par `/bentobox` (alias `/bbox`) :

| Commande | Qu'est-ce qu'elle fait |
|---|---|
| `/bentobox version` | Affiche la version de BentoBox et tous les compléments chargés. **Incluez toujours ceci lors de la déclaration de bugs.** |
| `/bentobox manage` | Ouvre le Panneau de Gestion Interface Graphique |
| `/bentobox reload` | Recharge les fichiers de configuration BentoBox et les locales sans redémarrage du serveur complet |
| `/bentobox catalog` | Ouvre le catalogue de compléments |
| `/bentobox perms` | Affiche les permissions effectives pour BentoBox et tous les compléments |
| `/bentobox rank` | Liste, ajoute ou supprime les rangs personnalisés |

## Commandes d'Administration par Mode de Jeu

Chaque mode de jeu a sa propre commande d'administration. Pour BSkyBlock c'est `/bsb`, pour AcidIsland c'est `/acid admin`, et ainsi de suite. Celles-ci vous donnent les contrôles spécifiques à ce mode de jeu :

| Commande | Qu'est-ce qu'elle fait |
|---|---|
| `/[admin] info <player>` | Affiche les détails complets de l'île d'un joueur |
| `/[admin] delete <player>` | Supprime l'île d'un joueur |
| `/[admin] setrange <player> <range>` | Change la plage de protection de l'île d'un joueur |
| `/[admin] range removebonus <player> [id]` | Supprime tous les bonus de plages de protection d'une seule île, ou seulement ceux d'un id donné |
| `/[admin] range purgebonus <id>` | Supprime un id de plage de bonus de **toutes** les îles du monde — idéal après désinstallation d'un addon qui accordait des bonus de plages. L'analyse s'exécute de façon asynchrone pour ne pas geler les gros serveurs |
| `/[admin] settings` | Ouvre le panneau des paramètres mondiaux pour les administrateurs |
| `/[admin] settings <player>` | Ouvre le panneau des paramètres de l'île pour un joueur spécifique |
| `/[admin] why <player>` | Commence à suivre pourquoi un joueur peut ou ne peut pas faire quelque chose (voir ci-dessous) |
| `/[admin] reload` | Recharge la configuration du mode de jeu |
| `/[admin] blueprint` | Ouvre l'Interface Graphique du Gestionnaire de Blueprint |

Le préfixe de commande administrateur exact dépend de la configuration du mode de jeu. Vérifiez la documentation du mode de jeu pour sa commande spécifique.

## L'Outil de Diagnostic « Why »

L'un des outils administrateur les plus utiles est la commande `why`. Si un joueur signale qu'il ne peut pas faire quelque chose sur son île (ou qu'il *peut* faire quelque chose qu'il ne devrait pas), exécutez :

```
/[admin_command] why <player>
```

Après cela, la console du serveur enregistrera la raison de chaque action que ce joueur prend — si elle a été autorisée ou bloquée, et quel drapeau de protection l'a causée. Cela facilite le diagnostic des permissions mal configurées sans deviner.

Pour arrêter le suivi, exécutez à nouveau la commande.

## Panneau des Paramètres Administrateur

Le panneau des paramètres administrateur (ouvert avec `/[admin] settings`) contrôle les défauts à l'échelle mondiale — les paramètres qui s'appliquent partout dans le monde du mode de jeu, pas seulement sur une île. Cela inclut :

- Drapeaux de protection par défaut pour les nouvelles îles
- Restrictions à l'échelle mondiale (par ex. dégâts d'explosion creeper, comportement du piston)
- Paramètres de visibilité du panneau de paramètres du joueur (masquez les drapeaux que vous ne voulez pas que les joueurs changent)

Voir [Protection](Protections.md) pour une explication complète du système de drapeaux.

## Contrôle Basé sur les Permissions

BentoBox est fortement basé sur les permissions. Presque tout — du nombre de foyers qu'un joueur peut avoir, à s'il peut voler, à la taille de son île — peut être contrôlé en accordant ou en refusant les permissions via votre plugin de permissions (par ex. LuckPerms).

!!! tip
    Exécutez `/bentobox perms` dans la console pour voir une liste de toutes les permissions enregistrées par BentoBox et ses compléments au format YAML. C'est utile pour configurer votre plugin de permissions.

## Gestion de la Base de Données

BentoBox supporte plusieurs bases de données pour stocker les données des îles et des joueurs :

- **JSON (fichier plat)** — la valeur par défaut ; facile à configurer, aucun logiciel supplémentaire nécessaire
- **MySQL** (5.7+)
- **MariaDB** (10.2.3+)
- **MongoDB** (3.6+)
- **SQLite** (3.28+)
- **PostgreSQL**

Le type de base de données est défini dans le `config.yml` BentoBox. Pour migrer d'un type de base de données à un autre sans perdre de données, utilisez :
```
/bentobox migrate
```

!!! warning
    Faites toujours une sauvegarde complète avant de migrer les bases de données.

## Rechargement sans Redémarrage

Après avoir modifié un fichier de configuration, vous pouvez l'appliquer sans redémarrer entièrement le serveur :
```
/bentobox reload
```
Cela recharge BentoBox et tous les compléments, y compris les locales. Notez que certains changements (comme les paramètres de génération de monde) nécessitent toujours un redémarrage complet pour prendre effet.

## Journal des modifications

!!! warning "Nouveautés dans v3.18.0 — Support Minecraft 26.2 nécessite Java 25 (serveur)"
    **Publié :** 27 juin 2026

    - 🔺 **Support Minecraft 26.2 + Java 25.** BentoBox fonctionne désormais sur la ligne Minecraft 26.x (26.2 supporté à l'exécution) et la compilation a migré vers la chaîne d'outils Java 25. **Votre serveur doit fonctionner sur une build Paper capable de Java 25 pour la ligne 26.x.** Les jars d'addon déjà compilés continuent à fonctionner sans modification — seuls les *développeurs* d'addon recompilant contre cette version doivent passer leur propre compilation à Java 25. Compatibilité : Paper Minecraft 1.21.5 – 26.2, Java 25+.
    - ⚙️ **Bascules de marqueur/zone Dynmap pour île.** Une nouvelle section `dynmap` dans `config.yml` ajoute les interrupteurs `island-markers` (l'icône maison au centre de chaque île) et `island-areas` (la boîte de bordure de zone protégée). Les deux sont par défaut `true`, préservant le comportement existant ; réglez l'un d'eux à `false` et exécutez `/bbox reload` pour masquer ces superpositions sur les serveurs où les îles denses inondent la carte.
    - **Gestion des bonus de plage d'administration.** Nouvelles commandes `/[admin] range removebonus` et `/[admin] range purgebonus` qui effacent les bonus de plages de protection d'une île ou de toutes les îles — idéal après désinstallation d'un addon qui les accordait (voir le tableau des Commandes d'Administration par Mode de Jeu ci-dessus).
    - 🐛 `/is team setowner` n'est plus bloqué par la limite d'île lors du transfert à un membre d'équipe existant.
    - 🐛 Le crochet Vault réessaye maintenant après l'activation des addons, corrigeant l'intégration d'économie qui dépendait de l'ordre de chargement.

    [Release v3.18.0](https://github.com/BentoBoxWorld/BentoBox/releases/tag/3.18.0)

??? note "Nouveautés dans v3.18.1"
    **Publié :** 1er juillet 2026

    Maintenance release.

    - 🐛 **Les titres et noms multilignes conservent leur couleur.** Le texte après la première ligne d'une infobulle GUI ne retombe plus sur le violet par défaut — le sérialiseur réémet désormais la couleur active (et les décorations) après chaque nouvelle ligne, corrigeant les infobulles sur tous les addons.

    [Release v3.18.1](https://github.com/BentoBoxWorld/BentoBox/releases/tag/3.18.1)
