# ChunkBlock

Un bloc magique. Un chunk. Un mur que vous ne pouvez pas traverser.

**ChunkBlock** reprend la boucle OneBlock que tout le monde connaît — miner le bloc magique, il revient sous une autre forme, les phases se succèdent — et ajoute une bordure dure à 16 blocs de distance. Tout ce qui se trouve en dehors de votre chunk de départ est une zone interdite : vous ne pouvez pas marcher, voler, planer, jeter de perles, monter ou creuser pour y accéder. La seule façon de s'échapper est de devenir *plus riche*.

Les niveaux d'île sont la monnaie. Augmentez votre niveau, allez à la bordure et **frappez-la dans la direction où vous voulez vous étendre**. Le chunk de l'autre côté s'ouvre et la bordure recule d'un pas. Perdez des niveaux et la bordure revient — les chunks les plus récents d'abord — et votre ferme se retrouve derrière jusqu'à ce que vous les regagniez.

Créé et maintenu par [tastybento](https://github.com/tastybento). Le moteur du bloc magique provient de [AOneBlock](../AOneBlock/index.md), donc les fichiers de phases sont interchangeables ; le verrouillage des chunks est original à ChunkBlock.

{{ addon_description("ChunkBlock") }}

## Pourquoi les joueurs sont accrochés

- 🔒 **Une bordure que vous ne pouvez vraiment pas franchir.** La marche, le sprint-saut, l'élytre, les tridents de courant violent, les perles de l'Ender (remboursées), le fruit du choeur, les chevaux, les bateaux, les minecarts et le vol créatif sont tous bloqués — à *chaque* hauteur, du vide au-dessus de la limite de construction. Il n'y a pas de couloir de survol et pas de creusement sous.
- 💰 **Les niveaux sont le territoire.** Pas une boutique, pas un rang, pas un minuteur. La chose que vos joueurs optimisent déjà — le niveau d'île — est la chose qui achète de l'espace. Chaque bloc placé est un acompte sur le prochain chunk.
- 👊 **L'expansion est un geste physique.** Pas de GUI, pas de `/buy chunk`. Le propriétaire se tient à la bordure, la frappe et le monde s'ouvre avec un son et une vague de particules vertes. Ils choisissent la direction, donc pas deux îles ne se développent de la même manière.
- ⚠️ **La perte a des conséquences — sans être cruelle.** Les baisses de niveau reverrouillent les chunks les plus récemment réclamés dans l'ordre inverse exact. Rien à l'intérieur n'est touché : les constructions, les coffres, les mobs sont tous toujours là quand les niveaux reviennent. Préférez un jeu plus doux ? Une seule ligne de configuration rend le territoire une cliquette qui ne rétrécit jamais.
- 🗺️ **Vous pouvez voir la frontière.** Un rideau de particules par joueur marque chaque face verrouillée près de vous (éventuellement avec des blocs de barrière côté client) et `/ch chunks` affiche une carte colorée de ce que vous possédez, ce que vous pouvez réclamer ensuite et ce que cela coûte.
- 🧱 **Rien ne fuit à travers.** Les pistons, les liquides qui coulent, les distributeurs, la croissance des arbres, la propagation du feu et de l'herbe, les explosions et les apparitions naturelles de mobs s'arrêtent tous à la ligne, et les objets tombés rebondissent plutôt que d'être perdus dans la zone interdite.
- ⛏️ **Le jeu complet OneBlock en dessous.** 20 phases thématisées, 15 500 blocs de contenu, pools de blocs et de mobs pondérés, coffres de rareté, hologrammes, barre de boss et progression de la barre d'action — tout cela, dans une boîte qui s'agrandit.

## Comment se déroule une session

Vous apparaissez sur un bloc d'herbe au milieu de nulle part avec un mur rouge dans toutes les directions. Minez. Minez encore. Du pavé, de la terre, un poulet qui descend immédiatement. Vers le cinquantième bloc, le chat dit que vous avez du crédit, alors vous vous tournez vers le côté du lever du soleil, frappez le mur et il *disparaît* — deux fois le monde que vous aviez il y a une seconde, et maintenant vous pouvez vraiment construire une ferme de blé sans renverser votre propre tour.

Cinquante niveaux plus tard, votre île est un carré de 3×3 chunks et vous choisissez délibérément les directions : la phase océan arrive, et vous voulez de la place pour elle du côté est où la pente est. Puis vous mourez mal dans la phase Donjon, perdez un chunk de niveaux, et le chunk le plus récent se referme avec votre banque de fourneaux dedans. Ce n'est pas parti. C'est juste *derrière le mur* jusqu'à ce que vous regagniez ces niveaux.

## Configuration

!!! warning "L'addon Level est requis"
    Le niveau d'île est la seule monnaie de chunk, donc ChunkBlock ne fonctionnera pas sans [Level](../../addons/Level/index.md). Si Level est absent, ChunkBlock se désactive avec un message clair dans la console plutôt que de démarrer partiellement.

0. Installez BentoBox et exécutez le serveur une fois pour que ses dossiers existent.
1. Installez l'addon **Level** dans `plugins/BentoBox/addons/`.
2. Déposez le jar **ChunkBlock** dans `plugins/BentoBox/addons/` et redémarrez.
3. ChunkBlock crée `chunkblock_world`, un dossier de données, un `config.yml`, un dossier `phases` et `phases_index.yml`.
4. Arrêtez le serveur, modifiez `config.yml` selon vos préférences et supprimez n'importe quel monde qu'il a créé si vos modifications affectent la génération.
5. Redémarrez.

ChunkBlock fonctionne bien à côté d'AOneBlock, CaveBlock et des autres — son propre monde, ses commandes (`/ch`, `/chadmin`), ses permissions (`chunkblock.*`), ses drapeaux et sa table de base de données.

!!! tip "Compagnons recommandés"
    - **Level** — requis et vaut la peine d'être accordé : sa pénalité de mort et ses valeurs de blocs sont, dans ChunkBlock, des *paramètres de territoire*.
    - **Border** — compatible. Il dessine la limite de protection globale de l'île ; la frontière des chunks à l'intérieur est le rideau propre à ChunkBlock.
    - **InvSwitcher** — garde les inventaires séparés de vos autres modes de jeu.
    - Les défis, les warps, les j'aimes, les biomes, les serres et les amis fonctionnent tous comme d'habitude dans les chunks déverrouillés.

## Compatibilité

| Fonction | Supportée |
|---|---|
| Serveur | ✅ Paper / Spigot, Minecraft 1.21+ |
| Version BentoBox | ✅ 3.13.0 ou version ultérieure |
| Version Java | ✅ Java 21 |
| Addon Level | ⚠️ Requis — le niveau d'île est la monnaie des chunks |
| Nether / End | ⚪ Désactivés par défaut ; voir ci-dessous |

## Configuration

`config.yml` est le fichier mode de jeu BentoBox standard plus un bloc spécifique à ChunkBlock. Chaque option est commentée dans le fichier lui-même ; la dernière copie se trouve à [config.yml](https://github.com/BentoBoxWorld/ChunkBlock/blob/develop/src/main/resources/config.yml).

### Les paramètres des chunks

```yaml
chunkblock:
  # Combien de niveaux d'île un chunk coûte pour être réclamé. Minimum 1.
  levels-per-chunk: 1
  # Nombre maximum de chunks qu'une île peut réclamer, y compris le chunk central.
  # 441 est un carré complet 21 x 21 chunks. -1 signifie « tout ce que la plage de protection contient ».
  max-chunks: 441
  # Perdre des niveaux en dessous de ce qui a été dépensé reverrouille les chunks, les plus récents d'abord.
  # false = 'mode cliquet' : les chunks ne se reverrouillent jamais une fois réclamés.
  relock-on-level-loss: true
  # Éjectez les joueurs d'un chunk qui se reverrouille sous leurs pieds.
  eject-players-on-relock: true
  # Annulez l'apparition naturelle de mobs dans les chunks verrouillés.
  deny-mob-spawns-in-locked: true
  # Faites rebondir les objets tombés à la bordure au lieu de les perdre.
  bounce-back-items: true
  border:
    # Rideau de particules par joueur sur les faces des chunks verrouillés.
    show-particles: true
    particle-color:
      ==: Color
      ALPHA: 255
      RED: 255
      GREEN: 0
      BLUE: 0
    # Envoyez également des blocs de barrière côté client. Purement visuel ; le monde n'est jamais modifié.
    client-side-barrier-blocks: false
```

!!! abstract "Guide complet : [Réclamation de chunks](Chunks.md)"
    Ce que fait chaque paramètre sur la sensation du jeu, des exemples de crédit travaillés, les règles de reverrouillage et comment accorder le rythme pour un serveur décontracté ou hardcore.

### Paramètres mondiaux qui importent plus que d'habitude

=== "distance-between-islands"
    !!! summary "Doit être un multiple de 8"
        Les centres d'îles doivent atterrir au milieu d'un chunk (x ≡ 8, z ≡ 8) sinon le bloc magique s'assiérait sur une couture de chunk. ChunkBlock aligne cette valeur au multiple de 8 le plus proche au chargement, donc un `250` édité à la main devient silencieusement `248`. La valeur par défaut est `256`.

=== "protection-range"
    !!! summary "Un second plafond dur"
        Les chunks réclamés doivent tenir entièrement dans la plage de protection de l'île, donc la plage plafonne le territoire peu importe ce que dit `max-chunks`. Le plus grand rayon d'anneau qui rentre est `(protection-range − 8) ÷ 16`, arrondi vers le bas, donnant `(2r + 1)²` chunks.

        Avec les valeurs par défaut — `protection-range: 240` — c'est un rayon de 14, ou 841 chunks, donc `max-chunks: 441` est le paramètre qui mord réellement. Si vous relevez `max-chunks`, vérifiez que la plage le contient, et n'oubliez pas que la plage ne peut jamais dépasser `distance-between-islands`.

=== "offset-x / offset-z"
    !!! summary "Délibérément absent"
        D'autres modes de jeu exposent les décalages mondiaux. ChunkBlock les calcule en interne à partir de `start-x`/`start-z` pour que le bloc magique soit toujours centré sur un chunk, et n'offre pas du tout les paramètres.

=== "nether and end"
    !!! summary "Désactivés par défaut"
        `nether.generate` et `end.generate` sont tous deux définis par défaut à `false`. Activez l'un ou l'autre et cette dimension obtient son propre chunk central et les mêmes règles de réclamation, pilotées par le même niveau d'île. Le bloc magique n'existe que dans le monde normal.

### Phases

Le bloc magique, les fichiers de phases et `phases_index.yml` se comportent exactement comme dans AOneBlock — les formats sont compatibles octet pour octet, donc les packs de phases communautaires entrent directement.

!!! abstract "Guide complet : [Le bloc magique et les phases](Phases.md)"
    La progression de 20 phases expédiée, l'index de phase, l'éditeur de phase administrateur et où trouver la référence de champ complète.

### Interfaces graphiques personnalisables

ChunkBlock utilise l'API de panneau à modèle BentoBox pour son interface graphique de phases. À la première exécution, il crée un dossier `panels` sous `plugins/BentoBox/addons/ChunkBlock` contenant `phases_panel.yml`. Voir [Interfaces graphiques personnalisables](../../Tutorials/generic/Customizable-GUI.md) pour les mécaniques ; les types de bouton `PREVIOUS`, `NEXT` et `PHASE` fonctionnent comme décrit dans la [documentation d'AOneBlock](../AOneBlock/index.md#customizable-guis).

## Commandes

!!! tip
    La commande du joueur par défaut est `/ch` (alias `/chunkblock`) et la commande administrateur par défaut est `/chadmin` (alias `/chunkblockadmin`, `/cha`). Les deux sont configurables sous `chunkblock.command` dans `config.yml`.

=== "Commandes uniques de joueur ChunkBlock"
    - `/ch chunks` — votre nombre de chunks, crédit dépensable et une carte de chat de votre territoire.
    - `/ch count` — le comptage actuel du bloc magique et la phase.
    - `/ch phases` — l'interface graphique des phases.
    - `/ch setcount <number>` — rejouez une phase que vous avez déjà atteinte.
    - `/ch check` — réapparaître le bloc magique ou afficher ses particules.
    - `/ch bossbar` / `/ch actionbar` — basculez les affichages de progression de phase.

=== "Commandes uniques d'administrateur ChunkBlock"
    - `/chadmin chunks <player> [reset]` — inspectez les chunks, les dépenses et le crédit d'un joueur, ou reverrouillezles de retour au chunk central.
    - `/chadmin bypass` — basculez l'application du verrouillage des chunks pour vous-même.
    - `/chadmin setcount <player> <number> [lifetime]` — définis le compteur de blocs d'un joueur.
    - `/chadmin setchest <phase> <rarity>` — enregistrez le coffre que vous regardez dans une phase.
    - `/chadmin sanity [<phase>]` — vérifiez les probabilités de phase dans la console.
    - `/chadmin phases` — l'éditeur d'ordre de phase.

[Liste complète des commandes ChunkBlock](Commands.md)

## Permissions

!!! tip
    Chaque permission ChunkBlock est préfixée par `chunkblock.`.

!!! warning "`chunkblock.mod.bypasschunks` ne sont pas donnés aux ops"
    Le contournement du verrouillage des chunks est défini par défaut à `false` — **pas** `op` — donc le personnel joue selon les mêmes règles que tout le monde jusqu'à ce que vous l'accordiez explicitement dans votre plugin de permissions. C'est délibérément un nœud séparé de `chunkblock.mod.bypasslock` du BentoBox, qui contourne le *verrouillage* de l'île et est une fonction différente.

=== "Permissions des joueurs"
    - `chunkblock.island.chunks` — utilisez `/ch chunks`. Par défaut `true`.
    - `chunkblock.count` — utilisez `/ch count`. Par défaut `true`.
    - `chunkblock.phases` — utilisez `/ch phases`. Par défaut `false`.
    - `chunkblock.island.setcount` — utilisez `/ch setcount`. Par défaut OP.
    - `chunkblock.respawn-block` — utilisez `/ch check`. Par défaut `true`.
    - `chunkblock.island.bossbar` / `chunkblock.island.actionbar` — basculez les affichages de progression. Par défaut `true`.

=== "Permissions administrateur"
    - `chunkblock.admin.chunks` — utilisez `/chadmin chunks`. Par défaut OP.
    - `chunkblock.mod.bypasschunks` — exempté du verrouillage des chunks et utilisez `/chadmin bypass`. **Par défaut `false`.**
    - `chunkblock.admin.setcount`, `chunkblock.admin.setchest`, `chunkblock.admin.sanity`, `chunkblock.admin.phases` — par défaut OP.

[Liste complète des permissions ChunkBlock](Permissions.md)

## Drapeaux

ChunkBlock enregistre ses propres ID de drapeaux pour pouvoir s'exécuter à côté d'AOneBlock sans que l'un ou l'autre addon ne perde ses drapeaux à une enregistrement dupliqué.

| Drapeau | Type | Description | Par défaut |
|---|---|---|---|
| `CHUNKBLOCK_START_SAFETY` | Paramètre mondial | Les joueurs ne peuvent pas se déplacer pendant une courte période après la création d'une île, ils ne peuvent donc pas immédiatement tomber. La durée est `starting-safety-duration` dans la config. | false |
| `CHUNKBLOCK_BOSSBAR` | Paramètre d'île | Afficher la barre de boss de progression de phase. Disponible uniquement avec `bossbar: true` dans la config. | true |
| `CHUNKBLOCK_ACTIONBAR` | Paramètre d'île | Afficher la barre d'action de progression de phase. Disponible uniquement avec `actionbar: true` dans la config. | true |
| `MAGIC_BLOCK` | Protection | Rang d'île minimum requis pour casser le bloc magique. | COOP |

!!! warning "Mise à niveau à partir de 1.0.0"
    Ces drapeaux s'appelaient `START_SAFETY`, `ONEBLOCK_BOSSBAR` et `ONEBLOCK_ACTIONBAR` en 1.0.0. Si vous en avez modifié par rapport à la valeur par défaut, réappliquez le paramètre une fois après la mise à niveau — les anciennes valeurs ne sont plus lues.

## Espaces réservés

En plus des espaces réservés de phase hérités du moteur du bloc magique, ChunkBlock ajoute cinq espaces réservés de territoire :

| Espace réservé | Description |
|---|---|
| `%chunkblock_island_chunks%` | Nombre de chunks déverrouillés, y compris le chunk central |
| `%chunkblock_island_max_chunks%` | Chunks maximum que cette île peut réclamer |
| `%chunkblock_island_chunk_credit%` | Crédit de niveau disponible à dépenser maintenant |
| `%chunkblock_island_next_chunk_level%` | Niveau d'île total nécessaire pour se permettre le prochain chunk |
| `%chunkblock_island_ring%` | Numéro d'anneau du chunk revendiqué le plus éloigné |

[Liste complète des espaces réservés ChunkBlock](Placeholders.md)

## FAQ

??? question "Pourquoi ne puis-je pas passer le mur rouge brillant ?"
    Ce chunk est toujours verrouillé. Si vous êtes le propriétaire de l'île et que vous avez du crédit de niveau, frappez le mur et il s'ouvre. `/ch chunks` affiche votre crédit et ce qui est réclaimable.

??? question "Les membres de l'équipe peuvent-ils réclamer des chunks ?"
    Non — réclamer est la décision du propriétaire de l'île. Tous les membres de l'équipe bénéficient de l'espace, voient les annonces de crédit et peuvent utiliser `/ch chunks`, mais seul le coup du propriétaire à la bordure dépense les niveaux.

??? question "J'ai perdu des niveaux et ma ferme est maintenant derrière le mur. Est-elle partie ?"
    Non. Rien à l'intérieur d'un chunk reverrouillé n'est touché — les blocs, coffres et mobs sont exactement comme vous les avez laissés. Récupérez les niveaux et réclamez-le ; le reverrouillage prend toujours les chunks les plus récents en premier, vous les récupérez donc dans l'ordre où vous les avez perdus. Les administrateurs peuvent désactiver complètement le reverrouillage avec `relock-on-level-loss: false`.

??? question "Un chunk s'est reverrouillé pendant que j'y étais. Qu'est-ce qui m'arrive ?"
    Vous êtes déplacé vers le spot le plus proche déverrouillé à l'intérieur de votre propre île — l'état du vol est préservé, les dégâts de chute annulés et un bloc d'atterrissage créé sous vous si le spot n'était pas sûr. Personne n'est jamais abandonné ou jeté dans le vide. Les joueurs qui n'appartiennent pas à cette île sont envoyés à la maison de leur propre île à la place.

??? question "Comment puis-je obtenir plus de chunks plus rapidement ?"
    Augmentez votre niveau d'île : placez davantage et des blocs plus précieux. Réduisez `levels-per-chunk` si vous voulez que l'expansion semble généreuse, ou relevez-le si vous voulez que la carte s'ouvre lentement.

??? question "Puis-je réclamer en diagonale ?"
    Pas directement. Un nouveau chunk doit partager une **face** avec le territoire que vous possédez déjà, donc un chunk de coin a besoin d'un de ses deux voisins orthogonaux reclamés d'abord.

??? question "Quelle taille peut atteindre une île ?"
    Lequel est le plus petit : `max-chunks` (par défaut 441, un carré 21×21) ou le plus grand carré de chunks qui rentre dans la plage de protection de l'île. `/ch chunks` affiche le maximum effectif.

??? question "Pourquoi ne cesse-t-je de tomber et de mourir ?"
    Un chunk n'est pas beaucoup d'espace au début. Construisez d'abord avant de construire vers le haut — et n'oubliez pas que les morts peuvent coûter des niveaux, et les niveaux sont le territoire.

??? question "Quelles phases y a-t-il ?"
    La même progression qu'AOneBlock : Plaines, Sous-sol, Hiver, Océan, Jungle, Marais, Donjon, Désert, Le Nether, Pléthore, Désolation, Deep Dark, L'End, Grottes luxuriantes, Grottes de stalactite, Marais de palétuvier, Prairie, Bosquet de cerisier, Pics dentelés et Grottes de soufre. Voir [Phases](Phases.md).

??? question "Y a-t-il un Nether ou un End ?"
    Les deux sont désactivés par défaut. Activez-les dans `config.yml` et chacun obtient son propre chunk central et les mêmes règles de réclamation. Le bloc magique n'existe que dans le monde normal.

??? question "Ai-je besoin de l'addon Border ?"
    Non, et vous n'avez pas non plus besoin de l'enlever. Border dessine la limite de protection extérieure de l'île ; ChunkBlock dessine la frontière des chunks à l'intérieur. Ils montrent des choses différentes et coexistent bien.

??? question "J'ai un bug ou une idée de fonctionnalité. Où est-ce que je le mets ?"
    Sur le [suivi des problèmes](https://github.com/BentoBoxWorld/ChunkBlock/issues).

## Traductions

{{ translations("ChunkBlock") }}

## API

ChunkBlock stocke ses données dans sa propre table de base de données, `ChunkBlockIslands`, et expose son état de territoire via des événements, un gestionnaire de requête et la classe addon.

Ajoutez-le à votre projet en tant que dépendance fournie :

```xml
<dependency>
    <groupId>world.bentobox</groupId>
    <artifactId>chunkblock</artifactId>
    <version>1.0.1</version>
    <scope>provided</scope>
</dependency>
```

### Objet de données

=== "OneBlockIslands"
    !!! summary "Description"
        État par île : la progression du bloc magique héritée du moteur AOneBlock, plus le territoire des chunks.

        Lien vers la source : [OneBlockIslands](https://github.com/BentoBoxWorld/ChunkBlock/blob/develop/src/main/java/world/bentobox/chunkblock/dataobjects/OneBlockIslands.java)

    !!! question "Variables"
        - `uniqueId` — l'ID unique de l'île, égal à l'ID unique de l'Island.
        - `blockNumber` — le numéro du bloc cassé actuel.
        - `lifetime` — le nombre total de blocs jamais cassés.
        - `phaseName` — le nom de la phase actuelle.
        - `hologram` — le texte hologramme en cours d'affichage.
        - `unlockedChunks` — la liste de réclamation ordonnée `"dx,dz"`, relative au chunk central. `"0,0"` est toujours d'abord et ne peut jamais être supprimé.
        - `lastKnownLevel` — le niveau d'île tel qu'au dernier calcul, utilisé pour détecter les gains et les pertes.

    !!! example "Exemple de code"
        ```java
        public void accessChunkBlockData(@NonNull Island island) {
            BentoBox.getInstance().getAddonsManager().<ChunkBlock>getAddonByName("ChunkBlock")
                .ifPresent(chunkBlock -> {
                    OneBlockIslands data = chunkBlock.getOneBlocksIsland(island);
                    int chunks = data.getUnlockedChunkCount();
                    List<String> claimOrder = data.getUnlockedChunks();

                    ChunkManager cm = chunkBlock.getChunkManager();
                    long credit = cm.getCredit(island);
                    long spent = cm.getSpentLevels(island);
                    int max = cm.getMaxChunks(island);
                    boolean here = cm.isUnlocked(island, someLocation);
                });
        }
        ```

### Événements

ChunkBlock déclenche les événements du bloc magique AOneBlock (`BlockClearEvent`, `MagicBlockEntityEvent`, `MagicBlockEvent`, `MagicBlockPhaseEvent` — voir la [section API d'AOneBlock](../AOneBlock/index.md#events), les mêmes champs, dans le package `world.bentobox.chunkblock.events`) plus deux des siens.

=== "ChunkUnlockEvent"
    !!! summary "Description"
        Déclenché une fois pour chaque chunk qu'une île réclame. **Non annulable** — la réclamation a déjà été décidée et payée ; c'est une notification.

        Lien vers la classe : [ChunkUnlockEvent](https://github.com/BentoBoxWorld/ChunkBlock/blob/develop/src/main/java/world/bentobox/chunkblock/events/ChunkUnlockEvent.java)

    !!! question "Variables"
        - `@NonNull Island island` — l'île qui a réclamé le chunk.
        - `@NonNull Vector chunkOffset` — le décalage du chunk par rapport au chunk central de l'île (x et z ; y est toujours 0).
        - `int unlockIndex` — la position du chunk dans l'ordre de réclamation de l'île. Le chunk central est 0.

    !!! example "Exemple de code"
        ```java
        @EventHandler(priority = EventPriority.MONITOR)
        public void onChunkUnlock(ChunkUnlockEvent event) {
            Island island = event.getIsland();
            Vector offset = event.getChunkOffset();
            int index = event.getUnlockIndex();
        }
        ```

=== "ChunkRelockEvent"
    !!! summary "Description"
        Déclenché une fois pour chaque chunk qu'une île perd quand son niveau baisse. **Non annulable.** Les événements arrivent les plus récemment réclamés en premier, correspondant à l'ordre dans lequel les chunks sont réellement repris.

        Lien vers la classe : [ChunkRelockEvent](https://github.com/BentoBoxWorld/ChunkBlock/blob/develop/src/main/java/world/bentobox/chunkblock/events/ChunkRelockEvent.java)

    !!! question "Variables"
        - `@NonNull Island island` — l'île qui a perdu le chunk.
        - `@NonNull Vector chunkOffset` — le décalage du chunk par rapport au chunk central de l'île.
        - `int unlockIndex` — la position que le chunk tenait dans l'ordre de réclamation.

    !!! example "Exemple de code"
        ```java
        @EventHandler(priority = EventPriority.MONITOR)
        public void onChunkRelock(ChunkRelockEvent event) {
            Island island = event.getIsland();
            Vector offset = event.getChunkOffset();
            int index = event.getUnlockIndex();
        }
        ```

### Gestionnaires de requête

Les plugins qui ne veulent pas de dépendance au moment de la compilation peuvent utiliser l'[API de requête d'addon](../../BentoBox/Request-Handler-API---How-plugins-can-get-data-from-addons.md). ChunkBlock enregistre `island-stats` et `location-stats` du moteur du bloc magique, plus :

=== "unlocked-chunks"
    !!! summary "Description"
        Informations de territoire pour l'île d'un joueur. Soumettez `"player"` → `UUID`. Retourne une carte vide si le joueur n'a pas d'île dans le monde ChunkBlock.

    !!! question "Carte retournée"
        - `count` — `Integer`, chunks déverrouillés y compris le central.
        - `max` — `Integer`, le maximum que cette île peut déverrouiller.
        - `ring` — `Integer`, le numéro d'anneau du chunk déverrouillé le plus éloigné.
        - `spent` — `Long`, niveaux déjà dépensés sur les chunks.
        - `credit` — `Long`, crédit de niveau disponible à dépenser.
        - `chunks` — `List<String>`, les décalages `"dx,dz"` dans l'ordre de réclamation.

    !!! example "Exemple de code"
        ```java
        Map<String, Object> request = Map.of("player", player.getUniqueId());
        @SuppressWarnings("unchecked")
        Map<String, Object> result = (Map<String, Object>) new AddonRequestBuilder()
                .addonName("ChunkBlock")
                .label("unlocked-chunks")
                .addMetaData(request)
                .request();
        int chunks = (int) result.getOrDefault("count", 0);
        ```

## Journal des modifications

??? note "Quoi de neuf dans la v1.0.0"
    **Libéré :** 2026-07-28

    La première version. La boucle OneBlock, dans un chunk qui s'agrandit quand vous payez pour cela.

    - **Réclamez des chunks en frappant la bordure.** Les niveaux d'île sont du crédit dépensable (`levels-per-chunk` par réclamation, par défaut 1). Le propriétaire vise le mur et frappe ou clique à droite pour ouvrir le prochain chunk, dans n'importe quelle direction.
    - **Le territoire a des conséquences.** Chaque réclamation est enregistrée dans l'ordre ; si le niveau d'île chute en dessous de ce qui a été dépensé, les chunks les plus récemment réclamés se reverrouillent, les plus récents d'abord. Les constructions à l'intérieur sont intactes. `relock-on-level-loss: false` donne le mode cliquet.
    - **Une bordure que vous ne pouvez vraiment pas franchir.** La marche, le sprint-saut, l'élytre, le courant violent, les perles de l'Ender (remboursées), le fruit du choeur, les montures, les bateaux et le vol sont bloqués à n'importe quelle hauteur. Les pistons, les liquides, les distributeurs, la croissance des arbres, la propagation et les explosions ne peuvent pas atteindre au-delà, et les objets tombés rebondissent.
    - **Une frontière que vous pouvez voir.** Un rideau de particules par joueur marque les faces des chunks verrouillés, avec des blocs de barrière côté client optionnels, plus des effets de célébration quand le crédit est gagné et les chunks sont réclamés. Le monde lui-même n'est jamais modifié.
    - **`/ch chunks`** — une carte de chat colorée de votre territoire, ce que vous pouvez réclamer ensuite et votre crédit.
    - **Sûr par design.** Les joueurs pris dans un chunk qui se reverrouille sont déplacés vers le spot déverrouillé le plus proche avec le vol préservé et aucun dégât de chute.
    - **Nécessite l'addon Level** — le niveau d'île est la seule et unique monnaie des chunks.

    [Version 1.0.0](https://github.com/BentoBoxWorld/ChunkBlock/releases/tag/1.0.0)

!!! warning "Quoi de neuf dans la v1.0.1 — ID de drapeau et commandes par défaut modifiés"
    **Libéré :** 2026-07-30

    Patch libérant tous les bugs signalés contre 1.0.0, plus deux problèmes de compatibilité qui n'apparaissent que lors de l'exécution de ChunkBlock aux côtés d'autres modes de jeu.

    - 🐛 **L'exploitation minière près de la bordure ne spamme plus les messages de réclamation.** La détection de réclamation ignorait le bloc sur lequel vous avez réellement cliqué et passait à travers les murs, donc l'exploitation minière d'un générateur à quelques blocs d'un chunk verrouillé vous ennuyait *« Vous avez besoin de X autres niveaux) de crédit »* à chaque coup. Les réclamations ne se déclenchent maintenant que sur un visage vrai de la bordure, et les commentaires d'échec sont limités en taux. Corrige [#14](https://github.com/BentoBoxWorld/ChunkBlock/issues/14).
    - 🐛 **Les réapparitions ne peuvent plus abandonner les joueurs sur l'île d'un étranger.** Une réapparition atterrissant dans un chunk verrouillé d'une île ancienne ou abandonnée utilisée pour relocaliser le joueur *dans cette île*, en générant un bloc d'atterrissage. Les joueurs qui n'appartiennent pas à l'île sont maintenant envoyés à la maison de leur propre île. Corrige [#13](https://github.com/BentoBoxWorld/ChunkBlock/issues/13).
    - 🔡 **L'interface graphique des phases respecte la permission de défini du compte.** *« Cliquez pour modifier »* n'est plus proposé aux joueurs sans `chunkblock.island.setcount`, et le titre de l'interface graphique dit *Phases ChunkBlock*. Corrige [#11](https://github.com/BentoBoxWorld/ChunkBlock/issues/11).
    - 🔺 ⚙️ **ID de drapeau propre, pas plus de collision AOneBlock.** Les drapeaux de la barre de boss, de la barre d'action et de sécurité de démarrage sont maintenant `CHUNKBLOCK_BOSSBAR`, `CHUNKBLOCK_ACTIONBAR` et `CHUNKBLOCK_START_SAFETY`. Ils partageaient auparavant les ID d'AOneBlock, et BentoBox rejette les enregistrements de drapeaux dupliqués — donc sur les serveurs exécutant les deux, le plugin qui s'est chargé en second a silencieusement perdu ses drapeaux.
    - 🔺 ⚙️ **Les commandes par défaut sont passées de `/cb` à `/ch`.** CaveBlock utilise déjà `/cb` et `/cbadmin`, donc les valeurs par défaut sont maintenant `ch chunkblock` (joueur) et `chadmin chunkblockadmin cha` (admin). Les serveurs existants conservent tous les alias qui se trouvent dans leur `config.yml` ; seules les nouvelles installations obtiennent les nouvelles valeurs par défaut.
    - **Arrêt propre quand Level est absent.** ChunkBlock se désactive maintenant avec un message clair au lieu de laisser des écouteurs semi-enregistrés qui ont spammé les erreurs à chaque jointure et déplacement.

    🔺 **Après la mise à niveau :** si vous avez changé les paramètres mondiaux de la barre de boss, de la barre d'action ou de sécurité de démarrage à partir de leurs valeurs par défaut, réappliquez-les une fois — les anciennes valeurs `ONEBLOCK_*` / `START_SAFETY` ne sont plus lues.

    🔡 **Remarque de localisation :** les clés ont été renommées (`protection.flags.CHUNKBLOCK_*`, titres de l'interface graphique des phases). Régénérez ou mettez à jour les fichiers de paramètres régionaux personnalisés.

    **Compatibilité :** API BentoBox 3.13.0+, Minecraft 1.21+, Java 21.

    [Version 1.0.1](https://github.com/BentoBoxWorld/ChunkBlock/releases/tag/1.0.1)
