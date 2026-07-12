# CaveBlock

Pas de ciel. Pas de surface. Juste de la pierre dans toutes les directions et une pioche dans votre main.

**CaveBlock** renverse le jeu des îles sur sa tête : au lieu de construire vers l'air ouvert, les joueurs creusent leur monde à partir de pierre solide souterraine. Excavez pour trouver des minerais, creusez un espace habitable, développez-vous à travers l'obscurité. C'est la même progression d'îles satisfaisante — défis, niveaux, coéquipiers — mais tout se joue sous terre. ~~Les nains~~ Les joueurs adorent ça.

Créé et maintenu par [BONNe](https://github.com/BONNe).

{{ addon_description("CaveBlock") }}

## Installation

0. Installez BentoBox et exécutez-le sur le serveur au moins une fois pour créer ses dossiers de données.
1. Placez ce jar dans le dossier addons du plugin BentoBox.
2. Redémarrez le serveur.
3. L'addon créera des mondes et un dossier de données contenant un fichier config.yml.
4. Arrêtez le serveur.
5. Modifiez le fichier config.yml selon vos préférences.
6. Supprimez tous les mondes créés par défaut si vous avez apporté des modifications qui les affecteraient.
7. Redémarrez le serveur.

## Configuration

Le fichier principal `config.yml` contient les informations de base sur la configuration de l'addon du mode de jeu.

### config.yml

Après que l'addon soit installé avec succès, il créera un fichier config.yml. Chaque option de ce fichier est accompagnée de commentaires. Veuillez vérifier le fichier pour plus d'informations.

Vous pouvez trouver le dernier fichier config : [config.yml](https://github.com/BentoBoxWorld/CaveBlock/blob/develop/src/main/resources/config.yml)

!!! info "Génération du monde remaniée dans 1.21.0"
    Depuis la version **1.21.0**, l'Overworld est taillé par le propre générateur de bruit vanilla 1.18+ de Minecraft, donc les îles traversent de véritables cavernes fromage, spaghetti, luxuriantes, pierre à stalactite et ombre profonde — complètes avec des minerais vanilla, des décorations, des structures et des biomes souterrains. Chaque colonne est ensuite plafonnée pour que le monde reste du roc solide sans ciel ouvert. Parce que le serveur gère désormais la taille, les minerais et les biomes, les anciennes options de génération de remplacement de blocs (`generation-tries`, `use-new-material-generator`, les listes `blocks` par dimension et les bascules `natural-*`) ont été supprimées. Le Nether et l'End conservent une approche de remplissage-et-décoration avec un nouveau générateur de veines de minerai. Consulter le journal des modifications au bas de cette page avant de mettre à jour.

=== "world.world-depth"
    !!! summary "Description"
        La profondeur du monde indique jusqu'à quelle hauteur les blocs seront générés dans le monde. Définir cette valeur à -64 créera simplement un monde vide.

        Permet de créer un peu d'air frais au-dessus de votre caverne.

=== "world.structures"
    !!! summary "Description"
        *Ajoutée dans la v1.23.0.* Une carte des structures vanilla qui peuvent générer dans le monde souterrain de l'**Overworld**. Définissez une structure sur `false` pour arrêter sa génération ; les structures non listées ici se génèrent normalement. Utilisez la clé de structure vanilla, par exemple `ancient_city`, `trial_chambers`, `mineshaft`, `mineshaft_mesa`, `stronghold`, `mansion`, `monument`, `pillager_outpost`, `ruined_portal`, `trail_ruins`, `village_plains`, `desert_pyramid`, `jungle_pyramid`, `igloo`, `swamp_hut`.

        Les grandes structures comme les Villes Antiques et les Salles d'Épreuve peuvent remplir ou déséquilibrer un monde souterrain solide, c'est pourquoi elles sont **désactivées par défaut**. N'affecte que les chunks de l'Overworld nouvellement générés.

        Par défaut :
        ```yaml
        structures:
          ancient_city: false
          trial_chambers: false
          mansion: false
          mineshaft: true
          stronghold: true
        ```

=== "world.overworld-cave-fill"
    !!! summary "Description"
        *Ajoutée dans la v1.23.0.* Densité des cavernes de l'Overworld. Vanilla génère un réseau de cavernes dense 1.18+ (cavernes fromage et spaghetti) qui, dans un monde souterrain solide, peut sembler « rien que des passages ». Ceci re-solidifie une fraction de cet air de caverne après la génération en utilisant un champ de bruit à basse fréquence, de sorte que des régions entières se ferment en chambres séparées plutôt que de créer des trous uniques aléatoires.

        - `0.0` conserve chaque caverne vanilla (la plus dense, le comportement original).
        - `1.0` remplit presque toutes les cavernes (presque solide).
        - Essayez `0.4` – `0.6` pour les réduire.

        Les biomes souterrains, les minerais, les décorations et les structures sont conservés de toute façon. N'affecte que les chunks nouvellement générés.

        Par défaut : `0.0`

=== "world.overworld-carvers"
    !!! summary "Description"
        *Ajoutée dans la v1.23.0.* Générer les cavernes de carver vanilla (grandes ravines et longs tunnels ronds) dans l'Overworld. Celles-ci se superposent aux cavernes de bruit. Définissez sur `false` pour supprimer les ravines et tunnels larges tout en conservant les cavernes de bruit.

        !!! warning
            BentoBox ne supporte pas de changer cette valeur en milieu de partie. Si vous avez besoin de le changer, effectuez une réinitialisation complète de vos mondes et bases de données.

        Par défaut : `true`

=== "world.normal.roof"
    !!! summary "Description"
        Autoriser le basculement si le bloc supérieur de l'Overworld doit être un bloc de bedrock. Sinon, il sera composé de pierre.

=== "world.normal.floor"
    !!! summary "Description"
        Autoriser le basculement si le bloc inférieur de l'Overworld doit être un bloc de bedrock. Sinon, il sera composé de pierre.

=== "world.normal.main-block"
    !!! summary "Description"
        Bloc principal utilisé pour combler les lacunes du ciel au-dessus du terrain généré à la vanille. La taille des cavernes vanilla, les minerais, les structures et les biomes souterrains (cavernes luxuriantes, cavernes de pierre à stalactite, ombre profonde) sont produits par le serveur ; ce paramètre n'affecte que le matériau utilisé pour remplir la couche de surface. Définir cette valeur sur AIR laissera un ciel ouvert au-dessus des cavernes.

=== "world.nether.roof"
    !!! summary "Description"
        Autoriser le basculement si le bloc supérieur du nether doit être un bloc de bedrock. Sinon, il sera composé de netherrack.

=== "world.nether.floor"
    !!! summary "Description"
        Autoriser le basculement si le bloc inférieur du nether doit être un bloc de bedrock. Sinon, il sera composé de netherrack.

=== "world.nether.main-block"
    !!! summary "Description"
        Permettre de définir le bloc principal qui sera utilisé pour la génération du monde du nether. Définir cette valeur sur AIR créera un monde vide. Les veines de minerai (débris anciens, quartz du nether, obsidienne, pierre lumineuse et plus) sont placées au-dessus de cela par le générateur de veines.

=== "world.end.roof"
    !!! summary "Description"
        Autoriser le basculement si le bloc supérieur de l'End doit être un bloc de bedrock. Sinon, il sera composé de pierre de l'End.

=== "world.end.floor"
    !!! summary "Description"
        Autoriser le basculement si le bloc inférieur de l'End doit être un bloc de bedrock. Sinon, il sera composé de pierre de l'End.

=== "world.end.main-block"
    !!! summary "Description"
        Permettre de définir le bloc principal qui sera utilisé pour la génération du monde de l'End. Définir cette valeur sur AIR créera un monde vide. Les veines de minerai sont placées au-dessus de cela par le générateur de veines.

## Commandes

!!! tip
    `[player_command]` et `[admin_command]` sont des commandes qui diffèrent selon le mode de jeu que vous exécutez.
    
    Le fichier `config.yml` du mode de jeu contient des options qui vous permettent de modifier ces valeurs.
    
    Par exemple, sur CaveBlock, la `[player_command]` par défaut est `cave`, et la `[admin_command]` par défaut est `cba`.
    
    Soyez conscient que cet addon permet de modifier les alias des commandes de joueur dans le fichier `config.yml` de l'addon.


Par défaut, les addons BentoBox GameMode sont livrés avec l'ensemble de sous-commandes par défaut, cependant, chaque addon peut introduire encore plus de sous-commandes.

[Liste complète des commandes CaveBlock](Commands)

## Permissions

!!! tip
    Le préfixe `[gamemode]` à chaque endroit pour l'addon CaveBlock doit être remplacé par `caveblock`.

Par défaut, les addons BentoBox GameMode sont livrés avec l'ensemble de sous-permissions par défaut, cependant, chaque addon peut introduire encore plus de sous-permissions.

[Liste complète des permissions CaveBlock](Permissions)

## Placeholders

Par défaut, les addons BentoBox GameMode sont livrés avec [l'ensemble de placeholders par défaut](../../BentoBox/Placeholders), cependant, chaque addon peut introduire encore plus de placeholders.

[Liste complète des placeholders CaveBlock](Placeholders)


## Drapeaux

L'addon introduit 1 drapeau de paramètres BentoBox :

- ![feather](https://static.wikia.nocookie.net/minecraft_gamepedia/images/e/e2/Feather_JE3_BE2.png){: loading=lazy width=16px } SKY_WALKER_FLAG: drapeau dans les paramètres du monde qui permet d'activer/désactiver la marche des joueurs sur le toit de la caverne.


## FAQ

??? question "Pouvez-vous ajouter une fonctionnalité X ?"
    Veuillez l'ajouter à la liste [ici](https://github.com/BentoBoxWorld/CaveBlock/issues).

??? question "J'ai un bug, où devrais-je le signaler ?"
    Veuillez l'ajouter à la liste [ici](https://github.com/BentoBoxWorld/CaveBlock/issues).


## Journal des modifications

??? note "Nouveautés dans v1.23.1"
    **Publié :** 9 juillet 2026

    Une version de correction qui comble la faille de suppression des structures introduite en 1.23.0. Recommandée pour tous les serveurs sous 1.23.0 qui désactivent des structures vanilla.

    - 🔺 **Les structures désactivées ne gèlent plus le serveur.** Désactiver une structure n'annulait que son *placement*, pas ses *règles* de placement, de sorte que les recherches de structures (`/locate`, Yeux de l'Ender, cartes d'explorateur/au trésor, dauphins, échanges de cartes de villageois) continuaient à scanner jusqu'au rayon maximal et à geler le thread principal. Un nouveau gestionnaire `StructuresLocateEvent` retire désormais les structures désactivées de la recherche dès le départ, renvoyant « introuvable » instantanément. Corrige [#116](https://github.com/BentoBoxWorld/CaveBlock/issues/116).
    - 🔺 **Les structures ne se faufilent plus dans la zone de spawn.** L'écouteur de suppression est désormais enregistré tôt dans `createWorlds()`, avant que les premiers chunks de spawn ne se génèrent, de sorte qu'une structure désactivée ne peut plus apparaître près du spawn.

    [Release v1.23.1](https://github.com/BentoBoxWorld/CaveBlock/releases/tag/1.23.1)

??? note "Nouveautés dans v1.23.0"
    **Publié :** 7 juillet 2026

    Donne aux administrateurs un contrôle direct sur ce qui remplit le monde souterrain de l'Overworld, en s'appuyant sur le travail de génération 1.22.0.

    - ⚙️ **Structures d'Overworld configurables.** Une nouvelle section `structures:` dans `config.yml` active/désactive les structures vanilla individuelles (Villes Antiques, Salles d'Épreuve, Manoirs, Mineshafts, Forteresses et plus). Les plus grandes structures remplissant le monde sont désactivées par défaut. Corrige [#112](https://github.com/BentoBoxWorld/CaveBlock/issues/112).
    - ⚙️ **Contrôle de la densité des cavernes de l'Overworld.** Un nouveau paramètre `overworld-cave-fill` (`0.0`–`1.0`, par défaut `0.0`) re-solidifie une fraction du réseau de cavernes dense vanilla pour que les mondes ressemblent moins à des passages interminables, tout en conservant les biomes, les minerais, les décorations et les structures intacts. Corrige [#111](https://github.com/BentoBoxWorld/CaveBlock/issues/111).
    - ⚙️ **Bascule des cavernes de carver.** Un nouveau paramètre `overworld-carvers` (par défaut `true`) supprime les ravines vanilla et les tunnels larges tout en conservant les cavernes de bruit. Celui-ci ne peut pas être changé en milieu de partie.

    Les nouvelles options sont écrites dans `config.yml` automatiquement au premier lancement et n'affectent que les chunks **nouvellement générés** ; les valeurs par défaut préservent le comportement 1.22.0, sauf que les plus grandes structures sont maintenant désactivées par défaut. Voir la section Configuration ci-dessus.

    [Release v1.23.0](https://github.com/BentoBoxWorld/CaveBlock/releases/tag/1.23.0)

??? warning "Nouveautés dans v1.22.0 — Génération du Nether et de l'End remaniée"
    **Publié :** 6 juillet 2026

    Reconstruit comment le **Nether** et **l'End** sont générés. Auparavant, les deux dimensions étaient un bloc solide de roche parsemé de blocs individuels aléatoires — y compris du feu flottant qui causait des ralentissements — et n'avaient pas de véritables cavernes.

    - 🔺 **Refonte de la génération du Nether et de l'End.** Les deux dimensions sont maintenant remplies de façon solide et taillées par un générateur de cavernes de bruit 3D en tunnels et chambres connectés, avec une marge solide contre le sol et le toit.
    - 🌋 **Mer de lave du Nether.** Les vides des cavernes les plus basses se remplissent de lave plutôt que d'air ouvert ; le sol et le toit restent solides pour que le monde reste fermé.
    - 🗺️ **Biomes Nether naturels.** Les cinq biomes du Nether sont partagés en régions naturelles, grossièrement égales, de sorte que plusieurs biomes apparaissent dans une seule île.
    - 🌿 **Décorations tenant compte des biomes.** Nylium cramoisi/déformé, racines, champignons et vignes ; vallées de sable de l'âme avec feu de l'âme et os ; deltas de basalte avec colonnes et feu de magma ; taches de plafond de pierre lumineuse ; tiges de fin et chorus dans l'End.
    - ⚡ **Plus de feu flottant qui cause des ralentissements.** Le feu est maintenant clairsemé et enraciné sur la netherrack/magma.

    🔺 **Génération du monde changée :** Le nouveau générateur n'affecte que les chunks **nouvellement générés**. Les chunks Nether/End existants conservent l'ancien apparence, vous pouvez donc voir une couture où l'ancien rencontre le nouveau. Régénérez ces dimensions (ou commencez de nouveaux mondes) si vous voulez un apparence cohérente.

    [Release v1.22.0](https://github.com/BentoBoxWorld/CaveBlock/releases/tag/1.22.0)

??? warning "Nouveautés dans v1.21.0 — Modification : génération du monde remaniée"
    **Publié :** 27 juin 2026

    Un remaniement majeur de la génération. CaveBlock cible désormais **Paper 1.21.11 sur Java 21** et l'**API BentoBox 3.14**.

    - 🔺 **Génération vanilla du monde en cavernes.** L'Overworld se confie au propre générateur de bruit 1.18+ de Minecraft, donc les îles sont taillées à travers de véritables cavernes fromage, spaghetti, luxuriantes, pierre à stalactite et ombre profonde, complètes avec des minerais, décorations, structures (mines, donjons, salles d'épreuve, géodes d'améthyste, villes antiques) et biomes souterrains vanilla. Le ciel est plafonné avec de la pierre pour que le monde reste du roc solide de la bedrock au plafond.
    - 💎 **Veines de minerai Nether & End remaniées.** Le Nether et l'End conservent l'approche de remplissage-et-décoration avec un nouveau générateur de veines qui place des blobs de minerai de taille appropriée (débris anciens, quartz, obsidienne, pierre lumineuse et plus) au lieu de blocs uniques.
    - ⚙️ **Nettoyage de la configuration.** Les paramètres de génération du monde ont été remaniés et les options mortes supprimées — `generation-tries`, `use-new-material-generator`, les listes `blocks` par dimension, les bascules `natural-surface`/`natural-caves`/`natural-bedrock` et les anciens paramètres `netherBlocks`/`endBlocks`/`debug` sont partis. Sauvegardez votre `config.yml` existant avant de laisser l'addon écrire les nouveaux défauts.
    - 🔡 **Locales MiniMessage.** Tous les fichiers de locale ont été migrés des codes couleur legacy vers MiniMessage, et la clé du message de limite de hauteur a été renommée en `caveblock.general.errors.cave-limit-reached`. Régénérez vos fichiers de locale si vous les avez personnalisés.
    - 🧪 Une suite de tests complète JUnit 5 + MockBukkit a été ajoutée pour garder la génération, les limites de hauteur et le cycle de vie de l'addon.

    🔺 **Génération du monde modifiée :** Les chunks nouvellement générés de l'Overworld utilisent maintenant les cavernes de bruit vanilla au lieu de la taille de remplissage solide. Les chunks déjà générés restent inchangés, mais le nouveau terrain aux bords de votre monde aura un aspect différent des zones plus anciennes. Testez d'abord sur une copie si cela importe pour vous.

    [Release v1.21.0](https://github.com/BentoBoxWorld/CaveBlock/releases/tag/1.21.0)

## Traductions

{{ translations("CaveBlock") }}
