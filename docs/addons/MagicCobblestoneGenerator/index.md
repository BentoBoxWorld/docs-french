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
