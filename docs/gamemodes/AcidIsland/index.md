# AcidIsland

C'est SkyBlock — mais l'océan essaie de vous tuer.

**AcidIsland** place les joueurs sur une petite île entourée d'une mer d'acide. Tomber dedans, c'est prendre des dégâts. Cela change tout : agrandir son île devient une opération délicate et très risquée. Construire par-dessus le bord, c'est un pari. Pourtant, les joueurs peuvent toujours naviguer en bateau pour se visiter les uns les autres — s'ils sont assez courageux.

C'est une prémisse familière avec un détail qui garde les joueurs alertes du début à la fin.

Créé et maintenu par [tastybento](https://github.com/tastybento).

{{ addon_description("AcidIsland") }}

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

Le `config.yml` le plus récent est disponible [ici](https://github.com/BentoBoxWorld/AcidIsland/blob/develop/src/main/resources/config.yml).

### Eau purifiée

!!! new "Ajouté dans AcidIsland 1.22.0"
    L'océan reste acide et dangereux, mais il est désormais possible de **purifier** l'eau. Boire une bouteille d'eau acide applique l'effet Poison de vanilla ; boire une bouteille d'eau purifiée soigne le joueur. Chaque objet d'eau porte une description colorée pour qu'on sache d'un coup d'œil ce qu'on a en main. Quatre méthodes permettent de purifier l'eau : cuire une bouteille ou un seau d'eau au four, brasser des bouteilles d'eau avec du charbon, ou récupérer les gouttes d'un stalactite de pointerocher dans un chaudron — à vous de choisir celle qui vous inspire.

??? note "acid.purified-water.enabled"
    Interrupteur maître de la fonctionnalité d'eau purifiée. Mis à `false`, tout s'arrête : le marquage des objets, l'interception des fours/alambics et le suivi des chaudrons.

    Par défaut : `true`

??? note "acid.purified-water.heal-amount"
    Nombre de demi-cœurs restaurés lorsqu'un joueur boit une bouteille d'eau purifiée. `4.0` correspond à 2 cœurs.

    Par défaut : `4.0`

??? note "acid.purified-water.bucket-furnace-enabled"
    Autorise la cuisson d'un seau d'eau au four pour obtenir un seau d'eau purifiée. La cuisson dure 100 secondes (5 fois plus qu'une bouteille). Passez à `false` si cela vous paraît trop facile pour l'équilibre de votre serveur.

    Par défaut : `true`

??? note "acid.purified-water.nether-enabled"
    Active le mécanisme d'eau purifiée dans le Nether géré par l'addon (monde insulaire ou monde vanilla).

    Par défaut : `true`

??? note "acid.purified-water.end-enabled"
    Active le mécanisme d'eau purifiée dans l'End géré par l'addon (monde insulaire ou monde vanilla).

    Par défaut : `true`

### Océan de soufre

!!! new "Ajouté dans AcidIsland 2.0.0"
    À partir de Minecraft 26.2, la mer acide est une eau soufrée vert acide, parsemée de cheminées de soufre bouillonnantes qui gazent la surface avec de la nausée et entrent périodiquement en éruption sous forme de geysers. Le fond de l'océan est un mélange pondéré de sable, de gravier, de grès et de tuf avec des blocs de magma bouillonnants, ainsi que des dépôts de soufre et de cinabre en 26.2+. Le même jar fonctionne toujours sur les serveurs Minecraft 1.21.x, où les fonctionnalités 26.2 se désactivent d'elles-mêmes et où l'eau retombe sur l'océan chaud classique.

!!! warning "Ce sont des paramètres de génération de monde"
    Les trois options ci-dessous sont figées au moment où un chunk est généré. BentoBox ne prend pas en charge leur modification en cours de partie — les chunks existants conservent leur apparence actuelle, attendez-vous donc à une jointure visible aux frontières des anciens chunks, sauf si vous démarrez un monde neuf.

??? note "world.default-biome"
    Le biome par défaut de l'Overworld. `SULFUR_CAVES` (Minecraft 26.2+) donne une eau vert acide avec un brouillard vert correspondant. Sur les serveurs plus anciens, ce biome n'existe pas et `WARM_OCEAN` est utilisé à la place.

    Par défaut : `SULFUR_CAVES` (était `WARM_OCEAN` avant la 2.0.0)

??? note "world.sulfur-vent-chance"
    Chance (0–100) par chunk qu'une cheminée de soufre se génère juste sous la surface de la mer. Les cheminées sont constituées de soufre puissant au-dessus d'un bloc de magma et bouillonnent, gazent et entrent en éruption sous forme de geysers. Elles se déclinent en quatre formes naturelles — cheminée, monticule, jumelle et éperon hérissé — avec des variations aléatoires. Nécessite Minecraft 26.2 ou une version ultérieure ; ignoré sur les serveurs plus anciens.

    Par défaut : `10`

??? note "world.make-structures"
    Génère les structures vanilla dans les mondes. Les chambres d'épreuves et autres structures souterraines se génèrent enfouies sous le fond de l'océan, donnant aux joueurs une raison de creuser vers le bas, et rendant la clé d'épreuve du kit de départ gagnable.

    Par défaut : `true` (était `false` avant la 2.0.0)

## Permissions

Les permissions peuvent être trouvées [ici](Permissions).

## Commandes

Les commandes peuvent être trouvées [ici](Commands).

## Placeholders

Les placeholders peuvent être trouvés [ici](Placeholders).

## Journal des modifications

!!! warning "Nouveautés dans v2.0.0 — océan de soufre (changements de génération de monde)"
    **Publié :** 20 juillet 2026

    AcidIsland adopte les bassins de soufre de Minecraft 26.2 comme apparence emblématique de l'océan acide. Compatibilité : API BentoBox 3.14.0 · Minecraft 1.21.11 – 26.2 (les fonctionnalités de soufre nécessitent la 26.2+) · Java 21.

    - ⚙️ **Eau soufrée vert acide.** Le biome par défaut de l'Overworld est désormais `SULFUR_CAVES`, ce qui rend toute l'eau vert acide avec un brouillard vert correspondant. Sur les serveurs antérieurs à la 26.2, le biome n'existe pas et le monde retombe sur `WARM_OCEAN`.
    - ⚙️ **Cheminées de soufre et geysers.** Des cheminées de soufre puissant se génèrent juste sous la surface de la mer : bulles, nuage de gaz nauséeux à la surface et éruptions périodiques de geysers, en quatre formes naturelles avec des variations aléatoires. La chance par chunk est définie par la nouvelle option `world.sulfur-vent-chance` (10 % par défaut) ; nécessite Minecraft 26.2+.
    - **Fond d'océan varié.** Le fond de sable stérile est désormais un mélange pondéré de sable, de gravier, de grès et de tuf avec des blocs de magma bouillonnants, plus du soufre et du cinabre en 26.2+. Les serveurs plus anciens reçoivent du gravier et du tuf à la place des blocs 26.2.
    - **Nouvelle île de départ « Refuge de la Source Sulfureuse ».** Un affleurement d'épicéas robustes avec litière de feuilles, œilfleurs, une rose de Wither, du podzol, un sanctuaire de tuf en dessous et une chèvre, avec le même kit de départ utilitaire que l'île de la grove de cerisiers. Construite entièrement avec des blocs compatibles 1.21.
    - ⚙️ **Structures activées par défaut.** `world.make-structures` vaut désormais `true` par défaut, donc les chambres d'épreuves et autres structures souterraines se génèrent enfouies sous le fond de l'océan.

    🔺 **Changements de génération de monde.** Le nouveau biome aquatique, les cheminées, le fond d'océan et les structures sont tous figés à la génération des chunks. Les mondes existants conservent leur apparence actuelle dans les chunks déjà explorés ; pour l'expérience 2.0.0 complète, démarrez un monde neuf, ou attendez-vous à une jointure visible aux frontières des anciens chunks.

    ⚙️ **Les configurations existantes ne sont pas modifiées.** Votre `config.yml` conserve ses valeurs enregistrées. Pour adopter les nouvelles valeurs par défaut sur une installation existante, mettez `default-biome: SULFUR_CAVES` et `make-structures: true`, ajoutez `sulfur-vent-chance: 10`, ou supprimez la configuration pour la régénérer.

    🔺 **Nouveaux blueprints sur les installations existantes.** BentoBox n'extrait les blueprints fournis que dans un dossier de blueprints *absent*. Pour voir la nouvelle option d'île sur une installation existante, copiez `sulfur-spring.blueprint` et `sulfur_spring.json` depuis le jar vers `plugins/BentoBox/addons/AcidIsland/blueprints/`.

    [Release v2.0.0](https://github.com/BentoBoxWorld/AcidIsland/releases/tag/2.0.0)

??? note "Nouveautés dans v1.22.1"
    **Publié :** 28 juin 2026

    Version de maintenance. Aucun changement de configuration ni de locale n'est requis.

    - 🐛 **Clés de permission en double corrigées dans `addon.yml`.** Plusieurs commandes partagent légitimement un même nœud de permission — `/ai ban`, `/ai unban` et `/ai banlist` utilisent toutes `acidisland.island.ban` — mais elles étaient écrites comme des entrées YAML distinctes avec des clés identiques. YAML ne conserve que la dernière d'une clé dupliquée, donc les descriptions de permissions précédentes étaient silencieusement perdues et le serveur consignait `duplicate keys found` à chaque chargement. Chaque nœud partagé est désormais une entrée unique avec une description combinée, et les avertissements au démarrage ont disparu.
    - Ajout de Minecraft 26.2 (et ajout rétroactif de 26.1.2) à la liste publiée des versions de jeu.

    [Release v1.22.1](https://github.com/BentoBoxWorld/AcidIsland/releases/tag/1.22.1)

??? note "Nouveautés dans v1.22.0 — Mécanisme d'eau purifiée"
    **Publié :** 15 avril 2026

    L'eau acide peut désormais être purifiée, et les joueurs peuvent enfin la boire sans risque, l'utiliser pour l'agriculture ou la mettre en bouteille en toute sécurité. Tous les objets d'eau portent une description colorée — <span style="color:red">Acid Water</span> ou <span style="color:green">Purified Water</span> — et les chaudrons se souviennent de la pureté de leur contenu entre deux redémarrages du serveur.

    - ⚙️ **Ajout de l'eau purifiée** — quatre manières de purifier : cuire une bouteille d'eau au four (10 s), brasser des bouteilles d'eau avec du charbon, cuire un seau d'eau au four (100 s, activable/désactivable), ou récupérer les gouttes d'un stalactite de pointerocher dans un chaudron.
    - ⚙️ **Effets à la consommation** — une bouteille d'eau acide applique l'effet Poison vanilla ; une bouteille d'eau purifiée restaure des points de vie (quantité configurable via `acid.purified-water.heal-amount`).
    - ⚙️ Nouveau bloc de configuration `acid.purified-water.*` (voir la section Configuration ci-dessus). Contient l'interrupteur maître, la quantité de soin, l'activation de la cuisson de seau et les bascules par dimension Nether/End.
    - 🔡 Deux nouvelles clés de locale sous `acidisland.purified-water.*` ; synchronisées dans les 18 langues traduites.
    - **Nouveaux événements** — `ItemFillWithAcidEvent` et `PlayerDrinkPurifiedWaterEvent` pour permettre à d'autres plugins de s'y accrocher.
    - Hygiène du code : `instanceof` avec pattern matching, `Math.clamp`, réduction de la complexité de `onPlayerMove`/`getWorld`/`findEntities`/`makeNetherRoof`, et modernisation des tests.

    [Release v1.22.0](https://github.com/BentoBoxWorld/AcidIsland/releases/tag/1.22.0)

??? warning "Nouveautés dans v1.21.0 — BentoBox 3.14.0 requis, migration des locales"
    **Publié :** 12 avril 2026

    - **Île de départ Sanctuaire Grove de Cerisiers.** Un nouveau blueprint d'île de départ sur le thème du biome Grove de Cerisiers est inclus pour les serveurs Minecraft 1.21+. Pour l'activer, supprimez `BentoBox/addons/AcidIsland/blueprints/` pour que les blueprints se régénèrent au prochain démarrage.
    - 🔺 **BentoBox API 3.14.0 est maintenant requis.** Mettez à jour BentoBox avant d'installer cette version.
    - 🔡 **Les 24 fichiers de locale migrés des codes `&` vers MiniMessage.** Supprimez `BentoBox/locales/AcidIsland/` et redémarrez pour régénérer. Les codes `&` restants dans les fichiers personnalisés s'afficheront en texte brut.
    - Correction : NullPointerException dans la vérification du mode dieu EssentialsX quand EssentialsX échoue à se charger au démarrage.
    - Plusieurs bugs de locale pré-existants corrigés lors de la migration.

    [Release v1.21.0](https://github.com/BentoBoxWorld/AcidIsland/releases/tag/1.21.0)

## Traductions

{{ translations("AcidIsland") }}
