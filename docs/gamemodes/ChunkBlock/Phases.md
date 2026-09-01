# Le bloc magique et les phases

Le bloc magique de ChunkBlock est le moteur AOneBlock, porté délibérément inchangé. Tout ce qui concerne les fichiers de phases — les pools de blocs et de mobs pondérés, `fixedBlocks`, hologrammes, coffres et raretés, blocs personnalisés, gating de version, commandes de démarrage et de fin, exigences, index de phase — fonctionne exactement comme dans AOneBlock, et les formats de fichier sont identiques.

Cela signifie :

- **Les packs de phases communautaires fonctionnent littéralement.** Un fichier de phase écrit pour AOneBlock se dépose dans le dossier `phases` de ChunkBlock et s'exécute.
- **Vous pouvez copier vos propres phases AOneBlock** sans les modifier.
- **Les correctifs et les fonctionnalités en amont arrivent ici aussi**, car le moteur est maintenu en phase plutôt que forké.

!!! abstract "Référence de champ complète : [Personnalisation des phases AOneBlock](../AOneBlock/Phases.md)"
    Ce guide est la procédure complète — ce que chaque nombre signifie, comment la raffle pondérée fonctionne avec des exemples travaillés, coffres, blocs personnalisés, gating de version et comment construire une phase à partir de zéro. Tout cela s'applique ici inchangé.

    Seuls les **noms de commande** diffèrent : lisez `/oba` comme `/chadmin` et `/ob` comme `/ch` partout.

Cette page couvre ce qui est spécifique à ChunkBlock.

---

## Ce qui s'expédie

Vingt phases, 15 500 blocs de contenu sur un serveur Minecraft 26.2+ :

| # | Phase | Longueur | Commence à |
|---:|---|---:|---:|
| 1 | Plaines | 700 | 0 |
| 2 | Sous-sol | 1 300 | 700 |
| 3 | Hiver | 1 000 | 2 000 |
| 4 | Océan | 1 000 | 3 000 |
| 5 | Jungle | 1 000 | 4 000 |
| 6 | Marais | 1 000 | 5 000 |
| 7 | Donjon | 1 000 | 6 000 |
| 8 | Désert | 500 | 7 000 |
| 9 | Le Nether | 1 000 | 7 500 |
| 10 | Pléthore | 1 000 | 8 500 |
| 11 | Désolation | 1 000 | 9 500 |
| 12 | Deep Dark | 1 000 | 10 500 |
| 13 | L'End | 500 | 11 500 |
| 14 | Grottes luxuriantes | 500 | 12 000 |
| 15 | Grottes de stalactite | 500 | 12 500 |
| 16 | Marais de palétuvier | 500 | 13 000 |
| 17 | Prairie | 500 | 13 500 |
| 18 | Bosquet de cerisier | 500 | 14 000 |
| 19 | Pics dentelés | 500 | 14 500 |
| 20 | Grottes de soufre | 500 | 15 000 |

**Grottes de soufre a besoin de Minecraft 26.2 ou version ultérieure.** Elle déclare `requiredMinecraftVersion: '26.2'` dans l'index, donc sur les serveurs plus anciens, elle est ignorée avec une seule ligne de journal d'info — la phase ne prend aucun bloc du tout et Pics dentelés s'exécute simplement jusqu'au point de boucle à la place. Ce serveur a 19 phases et 15 000 blocs.

Après la dernière phase, le compteur de blocs saute de retour à `gotoAtEnd` dans `phases_index.yml`, qui est `0` par défaut, donc la progression boucle.

---

## Où vivent les fichiers

```
plugins/BentoBox/addons/ChunkBlock/
├── config.yml
├── phases_index.yml          ← ordre, longueur, activé, gating de version
├── panels/
│   └── phases_panel.yml      ← le modèle GUI /ch phases
└── phases/
    ├── 0_plains.yml          ← blocs, mobs, hologrammes, commandes
    ├── 0_plains_chests.yml   ← le butin pour cette phase
    ├── 700_underground.yml
    └── …
```

Les fichiers dans `phases/` sont **jamais écrasés** lors de la mise à niveau, donc vos éditions survivent. Les nouvelles phases expédiées dans un jar ultérieur sont restaurées dans l'index automatiquement par réconciliation.

---

## L'index de phase

`phases_index.yml` est la source de vérité pour les phases qui se chargent, dans quel ordre, la longueur de chacune et quelle version Minecraft chacune a besoin. Il est lu **avant** n'importe quel fichier de phase n'est analysé, donc une phase qui nécessite une version Minecraft plus récente est ignorée sans son YAML — ou n'importe quel article à l'intérieur — jamais être touchée.

Chaque entrée prend ces champs :

| Champ | Signification |
|---|---|
| `file` | Nom de base du fichier de phase dans le dossier `phases`, sans `.yml`. Le fichier de coffre est `<file>_chests.yml`. |
| `section` | La clé de haut niveau à l'intérieur du fichier de phase (historiquement le bloc de démarrage). |
| `name` | Nom d'affichage, utilisé dans les journaux et dans le panneau `/chadmin phases`. |
| `length` | Nombre de blocs dans la phase. |
| `enabled` | Optionnel, par défaut `true`. Définissez `false` pour laisser une phase dehors. |
| `requiredMinecraftVersion` | Optionnel. La phase est ignorée — ne prenant aucun bloc du tout — sur les serveurs plus anciens que cette version. |

Les blocs de démarrage sont **calculés** : la somme courante des longueurs des phases activées ci-dessus, commençant à 0. Les phases peuvent être réordonnées librement, et une phase ignorée s'effondre hors de la progression.

Un `adminLengths: true` de niveau supérieur est écrit automatiquement la première fois que vous modifiez une longueur dans le panneau. À partir de là, la réconciliation ne recompute jamais les longueurs, donc vos valeurs survivent aux ajouts, renommages et mises à niveau de fichiers ultérieurs.

### Réconciliation

L'index est réconcilié contre les fichiers réellement sur disque à chaque charge et à chaque sauvegarde depuis le panneau d'administration, donc ce que `/chadmin phases` affiche est ce que votre serveur exécute vraiment. Regardez le journal de démarrage pour les lignes commençant par `Phase index:` — elles disent exactement ce qui a changé.

- Une entrée dont le fichier a été **renommé dans les versions du plugin** est re-pointée vers votre fichier par nom de phase.
- Une entrée dont le fichier est **manquant mais expédié dans le jar** est restaurée automatiquement. C'est ainsi que les nouvelles phases apparaissent sur les serveurs mis à niveau, étant donné que `phases/` n'est jamais écrasé.
- **Les fichiers de phase personnalisés** déposés dans le dossier sont ajoutés automatiquement. Une clé numérique s'insère à son bloc de démarrage hérité ; tout le reste est ajouté à la fin pour vous organiser dans le panneau.
- Les entrées dont les fichiers sont partis pour de bon sont supprimées avec un avertissement.

!!! warning "Suppression d'une phase"
    Pour supprimer une phase de manière permanente, supprimez ses fichiers ou basculez-la dans `/chadmin phases`. Supprimer seulement son entrée d'index ne fonctionne pas — la réconciliation re-ajoute tout fichier de phase qu'elle trouve dans le dossier.

    Un index malformé tombe en arrière sur le chargement de fichier direct, donc une mauvaise édition ne peut pas laisser le plugin bloqué.

!!! tip "Les chiffres dans les noms de fichiers sont optionnels"
    Un `desert.yml` personnalisé avec une section `desert:` fonctionne bien. Les fichiers de coffre s'accouplent toujours par nom de fichier (`<file>_chests.yml`). Les chiffres dans les fichiers expédiés sont historiques : avec l'index en charge, les valeurs de démarrage et de longueur du panneau sont la vérité.

---

## L'éditeur d'ordre de phase

`/chadmin phases` (permission `chunkblock.admin.phases`, OP par défaut) affiche chaque phase dans l'ordre avec son bloc de démarrage calculé, sa longueur et son état. Il modifie `phases_index.yml` et les chutes et les basculements enregistrent l'index et rechargent les phases immédiatement.

- **Clic gauche** une phase pour la prendre — le reste rétrécit à gauche. Cliquez où elle devrait aller pour pousser les autres à droite et la déposer, ou utilisez l'emplacement de dépôt à la fin. Cliquez n'importe où ailleurs ou fermez le panneau pour la remettre sans enregistrer.
- **Clic droit** bascule une phase activée ou désactivée.
- **Maj-clic gauche** définit la longueur d'une phase. Le panneau se ferme et une invite de chat affiche la longueur actuelle ; tapez un nombre entier pour l'appliquer ou `cancel` pour le garder. L'entrée invalide relance l'invite et l'invite expire après 60 secondes. La première édition de longueur écrit `adminLengths: true` dans l'index.

Les phases désactivées apparaissent en gris de verre et celles verrouillées par version en tant que barrières — les deux peuvent toujours être réordonnées. Une phase sans icône configurée utilise son premier bloc.

---

## Joueurs et phases

- `/ch count` — le comptage de blocs actuel et la phase, en chat.
- `/ch phases` — le GUI des phases. Nécessite `chunkblock.phases`, qui est **désactivé par défaut**.
- `/ch setcount <number>` — rejouez une phase déjà atteinte. Nécessite `chunkblock.island.setcount` (OP par défaut) et obéit à la valeur `set-count-cooldown` config, 5 minutes par défaut.
- `/ch check` — réapparaître le bloc magique s'il a disparu, ou afficher ses particules pour pouvoir le trouver.
- `/ch bossbar` / `/ch actionbar` — bascule les affichages de progression, si `bossbar` / `actionbar` sont activés dans `config.yml`.

Les hologrammes au-dessus du bloc magique sont activés par défaut (`world.holograms: true`), utilisent les entités de texte Minecraft natif et disparaissent après `hologram-duration` secondes.

---

## Outils de phase administrateur

- `/chadmin setcount <player> <number> [lifetime]` — définir le comptage de blocs d'un joueur ou leur comptage de vie.
- `/chadmin setchest <phase> <rarity>` — le moyen facile de construire du butin. Remplissez un coffre en jeu avec ce que vous voulez, regardez-le et exécutez la commande avec le nom de phase et une rareté de `COMMON`, `UNCOMMON`, `RARE` ou `EPIC`. Le coffre est écrit dans le fichier de coffre de cette phase, prêt à l'emploi. La suppression de coffres signifie toujours l'édition du fichier et le rechargement.
- `/chadmin sanity [<phase>]` — rapporte les probabilités de phase dans la console, pour que vous puissiez voir ce que vos poids s'ajoutent réellement.
- `/chadmin phases` — l'éditeur de commande décrit ci-dessus.

---

## Notes spécifiques à ChunkBlock

!!! warning "Le bloc magique est dans le chunk central, toujours"
    Le chunk central ne peut jamais être verrouillé, donc le bloc magique est toujours accessible. C'est garanti par le modèle de données plutôt que par une vérification : la liste de réclamation commence toujours par le chunk central et le reverrouillage ne peut jamais l'enlever.

!!! note "L'effacement des blocs de frai de mobs respecte la bordure"
    `mobs-clear-blocks: true` permet aux mobs qui réapparaissent de casser les blocs pour se faire de la place — une prévention de triche portée en avant d'AOneBlock afin que les joueurs ne puissent pas mettre le bloc magique en boîte et suffoque tout. Les chunks verrouillés ne sont jamais modifiés, donc cela n'affecte que votre propre territoire.

!!! tip "Les phases et le territoire tirent l'un contre l'autre"
    Les blocs que le bloc magique produit augmentent le niveau d'île, et le niveau d'île achète des chunks — donc une phase généreuse est aussi une phase d'expansion rapide. Si l'expansion semble trop rapide sur votre serveur, augmenter `levels-per-chunk` est généralement un meilleur levier que de rééquilibrer les poids de phase.

!!! note "Les phases Nether et End s'exécutent toujours"
    Les phases Nether et The End font partie de la progression indépendamment du fait que les mondes *Nether* et *End* soient générés (tous deux sont désactivés par défaut). Ils livrent des blocs et des mobs nether et end à travers le bloc magique du monde normal.
