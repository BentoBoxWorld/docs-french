# MagicCobblestoneGenerator

**MagicCobblestoneGenerator** transforme les générateurs de roche de plain et ennuyeux en une source géniale et fiable de blocs configurables!

Créé et maintenu par [BONNe](https://github.com/BONNe).

{{ addon_description("MagicCobblestoneGenerator") }}

## Installation

1. Placez le fichier jar de l'addon dans le dossier des addons du plugin BentoBox
2. Redémarrez le serveur
3. Exécutez la commande `/[admincmd] generator` pour configurer l'addon

## Configuration

Par défaut, l'addon tente d'importer toutes les données du fichier modèle, pour simplifier la première configuration. De nombreux paramètres du addon sont exposés dans l'interface graphique Admin, cependant, certains ne le sont pas.
Les dernières options de configuration et leurs explications détaillées se trouvent [ici](https://github.com/BentoBoxWorld/MagicCobblestoneGenerator/blob/develop/src/main/resources/config.yml).

Les fichiers modèles sont principalement pour les utilisateurs qui n'aiment pas utiliser l'interface graphique d'édition en jeu. Cependant, le fichier modèle n'est pas automatiquement importé à chaque modification. Cela nécessite une importation via une commande ou l'interface graphique Admin.

??? question "Structure du fichier modèle"
    ```
    # Commencez à répertorier tous les niveaux de générateur.
    tiers:
      # Id unique pour le générateur. Utilisé dans le stockage interne et l'accès à chaque donnée du générateur.
      generator_unique_id:
        # Nom d'affichage pour les utilisateurs. Supporte les codes de couleur.
        # Valeur par défaut: generator_unique_id sans _
        name: "Something fancy"
        # Description en message de lore. Supporte les codes de couleur.
        # Peut être défini vide en remplaçant tout par [].
        # Valeur par défaut: []
        description: -|
          First Line Of lore Message
          &2Second Line Of lore Message
        # Icône utilisée dans les interfaces graphiques. Le nombre à la fin permet de spécifier la taille de la pile pour l'article.
        # Valeur par défaut: Paper.
        icon: "PAPER:1"
        # Type de générateur: COBBLESTONE, STONE ou BASALT. Auto-explicatif.
        # Valeur par défaut: COBBLESTONE
        type: COBBLESTONE
        # Indique si le générateur est le générateur par défaut. Les générateurs par défaut ignorent la section des conditions.
        # Il est activé pour chaque nouvelle île. Il ne peut y en avoir qu'un par type de générateur.
        # Valeur par défaut: false
        default: false
        # Les utilisateurs sélectionnent les générateurs actifs.
        # La priorité indique quel générateur sera utilisé
        # si plusieurs d'entre eux remplissent les conditions.
        # Valeur par défaut: 1
        priority: 1
        # Il existe plusieurs exigences qui peuvent être définies ici.
        requirements:
          # Peut définir le niveau d'île minimum pour que le générateur fonctionne. Addon de niveau requis.
          # Valeur par défaut: 0
          island-level: 10
          # Liste des permissions requises pour que les utilisateurs sélectionnent ce générateur.
          # Valeur par défaut: []
          required-permissions: []
          # Liste des biomes requis pour que le générateur fonctionne.
          # Vide signifie qu'il n'y a pas de limitation dans quel biome le générateur fonctionne.
          # Valeur par défaut: [].
          required-biomes: []
          # Coût pour acheter ce générateur. Nécessite Vault et n'importe quel plugin d'économie.
          # Actuellement implémenté en cliquant sur l'icône d'achat dans l'interface graphique de visualisation du générateur.
          # Valeur par défaut: 0
          purchase-cost: 5.0
        # Coût pour activer le niveau de générateur actuel. Nécessite Vault et n'importe quel plugin d'économie.
        # Sera payé uniquement lors du changement actif entre les générateurs.
        # Valeur par défaut: 0.
        activation-cost: 0.0
        # Matériaux et leurs chances. Utilisez les blocs réels s'il vous plaît.
        # La chance supporte n'importe quel nombre positif, y compris la valeur double.
        # Tout à la fin sera normalisé.
        # Valeur par défaut: []
        blocks:
          FIRST_BLOCK_NAME_ID: NUMBER
          SECOND_BLOCK_NAME_ID: NUMBER
        # Trésor qui a une chance d'être lâché quand le bloc est généré.
        # SEULEMENT à la génération, pas au cassage de bloc.
        # Valeur par défaut: []
        treasure:
          # Chance de 0 till 1. 0 - ne sera pas possible d'obtenir un trésor.
          # Valeur par défaut: 0
          chance: 0.001
          # Matériaux qui peuvent être lâchés. S'applique aux mêmes règles que la section des blocs.
          # Valeur par défaut: []
          material:
            FIRST_BLOCK_NAME_ID: NUMBER
            SECOND_BLOCK_NAME_ID: NUMBER
          # Montant maximal d'articles lâchés.
          # Il sera de 1 till montant défini.
          # Valeur par défaut: 1
          amount: 1

    # Commencez à répertorier tous les bundles
    bundles:
      # bundle_id
      bundle_unique_id:
        # Nom d'affichage pour les utilisateurs
        name: "Something fancy"
        # Description en message de lore. Supporte les codes de couleur.
        # Peut être défini vide en remplaçant tout par [].
        # Valeur par défaut: []
        description: -|
          First Line Of lore Message
          &2Second Line Of lore Message
        # Icône utilisée dans les interfaces graphiques. Le nombre à la fin permet de spécifier la taille de la pile pour l'article.
        # Valeur par défaut: Paper.
        icon: "PAPER:1"
        # Liste des générateurs auxquels le bundle aura accès.
        generators:
          - generator_id_1
          - generator_id_2
    ```

### Épuisement du générateur (limitation du débit)

Depuis **2.8.0** les générateurs peuvent être plafonnés pour ne produire qu'un nombre défini de blocs dans une période donnée avant de passer en cooldown — utile pour décourager les fermes AFK entièrement automatisées. La fonctionnalité est **opt-in et désactivée par défaut** (une limite de `0`), donc les configurations existantes ne sont pas affectées jusqu'à ce que vous l'activiez. Quand un générateur est temporairement en cooldown, les joueurs reçoivent un message `generator-exhausted`.

=== "exhaustion.limit"
    !!! summary "Description"
        Le nombre par défaut de blocs qu'un générateur peut produire au cours d'une seule période d'épuisement. `0` ou moins désactive la limitation (la valeur par défaut). Chaque niveau de générateur peut remplacer ceci via la clé `exhaustion-limit` par niveau (voir ci-dessous).

        Défaut : `0`

=== "exhaustion.period"
    !!! summary "Description"
        La durée de la période d'épuisement, en **minutes**. Le comptage des blocs se réinitialise à la fin de chaque période.

        Défaut : `60`

=== "exhaustion.cooldown"
    !!! summary "Description"
        Combien de temps, en **minutes**, un générateur reste en cooldown après avoir atteint sa limite d'épuisement.

        Défaut : `1440` (24 heures)

=== "exhaustion.notification-cooldown"
    !!! summary "Description"
        Le temps minimum, en **secondes**, entre deux messages d'avertissement d'épuisement affichés au même joueur.

        Défaut : `60`

!!! tip "Limite par niveau"
    Chaque niveau de générateur peut remplacer la limite globale avec une clé `exhaustion-limit` dans le modèle de générateur (et dans l'interface graphique admin), de sorte que différents niveaux peuvent être étranglés indépendamment.

### Plages de hauteur par bloc

Également depuis **2.8.0**, les générateurs — et les blocs individuels au sein d'un générateur — peuvent être limités à un niveau Y minimum et maximum, de sorte que différents matériaux sont produits à différentes hauteurs. De nouveaux boutons de l'interface graphique permettent aux admins de définir et d'effacer la plage, et la lore du générateur montre aux joueurs où chaque générateur opère. Les modèles hérités sans plage de hauteur restent pleinement compatibles.

## Commandes

!!! tip
    `[player_command]` et `[admin_command]` sont les commandes qui diffèrent selon le mode de jeu que vous exécutez.
    Le fichier `config.yml` des Gamemodes contient des options qui vous permettent de modifier ces valeurs.
    Par exemple, sur BSkyBlock, le `[player_command]` par défaut est `island`, et l'`[admin_command]` par défaut est `bsbadmin`.

=== "Commandes joueur"
    - `/[player_command] generator`: Accédez à l'interface graphique du générateur.

=== "Commandes admin"
    - `/[admin_command] generator`: Accédez à l'interface graphique admin du générateur.

## Journal des modifications

!!! warning "Nouveautés dans v2.8.0 — nécessite BentoBox 3.14.0 / Java 21"
    **Publié :** 3 juillet 2026

    - ⚙️ **Épuisement du générateur.** Limitation optionnelle du nombre de blocs qu'un générateur produit par période, avec un cooldown une fois la limite atteinte. Configurable globalement (`exhaustion.*` dans `config.yml`) et par niveau de générateur (`exhaustion-limit` dans le modèle). Opt-in et désactivé par défaut. Voir la section Configuration ci-dessus.
    - **Plages de hauteur par bloc.** Limitez les générateurs et les blocs individuels à un niveau Y minimum/maximum, avec de nouveaux contrôles de l'interface graphique et une lore de face utilisateur.
    - 🔡 **Nouveaux placeholders** `[gamemode]_magiccobblestonegenerator_generator_exhaustion_status` et `[gamemode]_magiccobblestonegenerator_exhausted_generator_names` exposent l'état d'épuisement.
    - 🔡 🔺 **Locales MiniMessage + 13 nouvelles langues.** Chaque fichier de locale a été converti des codes couleur `&` legacy vers MiniMessage (que BentoBox 3.14 rend nativement), et des traductions ont été ajoutées pour cs, hr, hu, id, it, ja, ko, lv, nl, pt, pt-BR, ro et zh-HK — 24 locales au total, correspondant à BentoBox core. Si vous avez conservé vos propres modifications à n'importe quel fichier `locales/*.yml`, réappliquez-les au format MiniMessage (ou supprimez le fichier pour régénérer un frais).
    - 🔺 **Modernisé pour BentoBox 3.14 / Java 21.** Mis à jour vers l'API BentoBox et Paper actuels, avec la suite de tests migrée vers MockBukkit. Cette version ne se chargera pas sur les anciennes versions de BentoBox ou Java — mettez d'abord à jour BentoBox.

    [Release v2.8.0](https://github.com/BentoBoxWorld/MagicCobblestoneGenerator/releases/tag/2.8.0)

## Traductions

{{ translations("MagicCobblestoneGenerator") }}
