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

## Permissions

Les permissions peuvent être trouvées [ici](Permissions).

## Commandes

Les commandes peuvent être trouvées [ici](Commands).

## Placeholders

Les placeholders peuvent être trouvés [ici](Placeholders).

## Journal des modifications

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
