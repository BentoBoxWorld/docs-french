# Commandes ChunkBlock

La commande du joueur par défaut est **`/ch`** (alias `/chunkblock`) et la commande d'administrateur par défaut est **`/chadmin`** (alias `/chunkblockadmin`, `/cha`). Les deux, et plusieurs des étiquettes de sous-commande, sont configurables sous `chunkblock.command` dans `config.yml` :

```yaml
chunkblock:
  command:
    island: ch chunkblock
    admin: chadmin chunkblockadmin cha
    # Sous-commande exécutée sur le tout premier /ch d'un joueur
    new-player-action: create
    # Sous-commande exécutée à chaque /ch ultérieur
    default-action: go
    count-command: count
    phases-command: phases
    set-count-command: setCount
    bossbar-command: bossbar
    actionbar-command: actionbar
    respawn-block-command: respawnBlock check
```

Un `/ch` nu crée une île la première fois et téléporte le joueur à la maison par la suite.

!!! note "Pourquoi `/ch` et pas `/cb`"
    Les valeurs par défaut de ChunkBlock étaient `/cb` et `/cbadmin` en 1.0.0, qui entrent en collision avec CaveBlock. Depuis 1.0.1, les nouvelles installations obtiennent `/ch` et `/chadmin`. Les serveurs qui ont déjà un `config.yml` conservent tous les alias qui s'y trouvent.

## Commandes de joueur uniques ChunkBlock

Il s'agit des sous-commandes uniques à ChunkBlock. Tout le reste — `go`, `create`, `reset`, `sethome`, `team`, `ban`, `expel`, `settings`, `language`, `info`, `near` et le reste — est l'ensemble de mode de jeu BentoBox standard.

| Commande | Description | Permission |
|---------|-------------|------------|
| `/ch chunks` | Votre nombre de chunks déverrouillés, maximum, crédit de niveau dépensable et une carte de chat colorée de votre territoire montrant les chunks que vous pouvez réclamer ensuite. | `chunkblock.island.chunks` |
| `/ch count` | Le comptage actuel du bloc magique de l'île et la phase. | `chunkblock.count` |
| `/ch phases` | Ouvrir le GUI des phases — parcourir les phases et, avec permission, en rejouez une déjà atteinte. Désactivé par défaut. | `chunkblock.phases` |
| `/ch setcount <number>` | Sauter le compteur de blocs à la valeur de démarrage d'une phase précédemment complétée. Soumis à `set-count-cooldown` (5 minutes par défaut). | `chunkblock.island.setcount` |
| `/ch check` (alias `respawnBlock`) | Afficher les particules du bloc magique ou le réapparaître s'il a disparu. | `chunkblock.respawn-block` |
| `/ch bossbar` | Basculez la barre de boss de progression de phase. Nécessite `bossbar: true` dans la config. | `chunkblock.island.bossbar` |
| `/ch actionbar` | Basculez la barre d'action de progression de phase. Nécessite `actionbar: true` dans la config. | `chunkblock.island.actionbar` |

## Commandes administrateur uniques ChunkBlock

`/chadmin` porte l'ensemble standard BentoBox complet (`version`, `tp`, `info`, `getrank`, `setrank`, `range`, `resets`, `deaths`, `purge`, `blueprint`, `register`, `delete`, `settings`, `reload`, `why`, `switch`, `team` et ainsi de suite) plus les commandes spécifiques à ChunkBlock ci-dessous.

| Commande | Description | Permission |
|---------|-------------|------------|
| `/chadmin chunks <player>` | Afficher le nombre de chunks déverrouillés d'un joueur, son maximum effectif, les niveaux qu'il a dépensés et son crédit restant. | `chunkblock.admin.chunks` |
| `/chadmin chunks <player> reset` | Reverrouiller tout de retour au chunk central et effacer le dossier de dépenses. Les constructions sont intactes — le territoire doit simplement être regagné. | `chunkblock.admin.chunks` |
| `/chadmin bypass` | Basculez l'application du verrouillage des chunks pour vous-même. Lors du contournement, vous pouvez vous déplacer à travers les chunks verrouillés et le rideau de bordure est caché pour vous. | `chunkblock.mod.bypasschunks` |
| `/chadmin setcount <player> <number> [lifetime]` | Définissez le compteur de blocs magiques d'un joueur ou leur compteur de vie. | `chunkblock.admin.setcount` |
| `/chadmin setchest <phase> <rarity>` | Enregistrez le coffre que vous regardez dans un fichier de coffre de phase avec la rareté donnée (`COMMON`, `UNCOMMON`, `RARE`, `EPIC`). Le coffre doit être un coffre unique rempli. | `chunkblock.admin.setchest` |
| `/chadmin sanity [<phase>]` | Imprimer une vérification de santé des probabilités de phase à la console. | `chunkblock.admin.sanity` |
| `/chadmin phases` | Ouvrir l'éditeur d'ordre de phase — réorganiser, redimensionner, activer et désactiver les phases. | `chunkblock.admin.phases` |

!!! tip "Le `/chadmin bypass` a besoin d'une permission que les ops n'ont pas"
    `chunkblock.mod.bypasschunks` est défini par défaut à `false`, donc même un op doit l'accorder explicitement avant que la commande fonctionne. C'est intentionnel : le personnel joue selon les mêmes règles jusqu'à ce qu'ils s'y inscrivent. Le mode spectateur est toujours exempté indépendamment.

!!! tip "Utilisation de l'éditeur d'ordre de phase"
    `/chadmin phases` répertorie chaque phase dans l'ordre avec son bloc de démarrage calculé, sa longueur et son état, et écrit `phases_index.yml`.

    - **Clic gauche** prend une phase ; cliquez où elle devrait aller, ou l'emplacement de dépôt à la fin, pour la placer. Cliquez n'importe où ailleurs ou fermez le panneau pour la remettre inchangée.
    - **Clic droit** bascule une phase activée ou désactivée.
    - **Maj-clic gauche** définit la longueur d'une phase via une invite de chat. La première édition de longueur écrit `adminLengths: true` dans l'index pour que vos longueurs ne soient jamais recalculées.

    Les phases désactivées apparaissent en gris de verre et celles verrouillées par version en tant que barrières ; les deux peuvent toujours être réordonnées. Voir [Phases](Phases.md) pour l'image complète.

## Lecture `/ch chunks`

```
Chunks : 9/441. Crédit : 3 niveaux) — un chunk coûte 1.
Votre territoire d'île (9/441 chunks) :
□ □ □ □ □
□ ▣ ▣ ▣ □
□ ▣ ■ ■ ▣
□ ▣ ■ ◆ ▣
□ □ ▣ ▣ □
■ les vôtres  ▣ réclaimable (1 niveaux) chacun)  □ verrouillé
```

| Glyphe | Signification |
|---|---|
| `■` vert | Un chunk que vous possédez |
| `▣` jaune | Réclaimable maintenant — adjacent, dans la plage, en dessous de la limite |
| `□` gris | Verrouillé et pas encore réclaimable |
| `◆` bleu | Le chunk dans lequel vous vous tenez |

La carte s'élargit au fur et à mesure que l'île grandit, jusqu'à une vue de 15 × 15.
