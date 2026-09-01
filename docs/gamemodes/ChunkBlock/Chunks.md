# Réclamation de chunks

C'est la partie de ChunkBlock qui n'est pas AOneBlock. Le bloc magique est le moteur ; **le chunk est le jeu**.

Chaque île commence exactement un chunk — 16 × 16 blocs, de la roche mère au ciel, avec le bloc magique au milieu. Tout le reste dans la plage de protection de l'île est verrouillé. Le propriétaire de l'île l'ouvre un chunk à la fois en dépensant des niveaux d'île à la bordure.

---

## Le modèle de monnaie

Le niveau d'île est la monnaie. Il n'y a pas de solde séparé à suivre, pas de boutique et pas de cooldown.

```
crédit = niveau d'île − niveaux déjà dépensés
dépensé = (chunks réclamés) × levels-per-chunk
```

Le chunk central est gratuit et ne compte pas comme une dépense. Avec le `levels-per-chunk: 1` par défaut :

| Niveau d'île | Chunks possédés | Dépensé | Crédit | Peut réclamer ? |
|---:|---:|---:|---:|:--|
| 0 | 1 | 0 | 0 | Non — rien à dépenser |
| 1 | 1 | 0 | 1 | Oui, un chunk |
| 1 | 2 | 1 | 0 | Pas jusqu'à ce que le niveau augmente |
| 7 | 3 | 2 | 5 | Oui, cinq chunks de plus |
| 4 | 6 | 5 | −1 | **Dépensé en trop** — un chunk se reverrouille |

Parce que le crédit est dérivé plutôt que stocké, il n'y a rien à désynchroniser : changez `levels-per-chunk` dans la config et chaque île est repricée lors du prochain calcul de niveau.

!!! tip "Régler le rythme"
    `levels-per-chunk` est le cadran unique le plus important sur la sensation du jeu.

    - `1` (par défaut) — généreux. L'expansion précoce est rapide et la carte s'ouvre aussi vite que les joueurs peuvent construire.
    - `5`–`10` — délibéré. Les joueurs choisissent les directions avec soin et un chunk est un événement.
    - `50`+ — un jeu long. Convient aux serveurs où le niveau d'île s'élève déjà aux milliers.

    N'oubliez pas qu'il interagit avec les valeurs de bloc du plugin Level : doubler la valeur des blocs que vos joueurs cultivent réduit de moitié le coût réel d'un chunk.

---

## Réclamer : frappez la bordure

L'expansion est un geste, pas un menu.

1. Le **propriétaire de l'île** se tient à l'intérieur de son propre territoire.
2. Ils font face au chunk verrouillé qu'ils veulent.
3. Ils **cliquent à gauche ou à droite vers le mur**.

Si tout est en ordre, le chunk s'ouvre avec un son, une vague de particules vertes et un message de chat indiquant à tous les membres de l'équipe la taille de l'île et le crédit restant.

!!! note "Seul le propriétaire peut réclamer"
    Les membres de l'équipe partagent le territoire, voient les annonces de crédit et peuvent exécuter `/ch chunks`, mais dépenser les niveaux de l'île est la décision du propriétaire.

### Ce qui est coché, dans l'ordre

| Vérification | Échec | Ce que le joueur voit |
|---|---|---|
| Déjà le tien ? | `ALREADY_UNLOCKED` | Rien — c'est juste un clic normal |
| À l'intérieur de la plage de protection et en dessous de `max-chunks` ? | `BEYOND_LIMIT` | *« Ce chunk dépasse la zone de protection de votre île. »* |
| Partage une face avec un chunk que vous possédez ? | `NOT_ADJACENT` | Rien — les visées diagonales sont silencieusement ignorées |
| Assez de crédit ? | `NO_CREDIT` | *« Vous avez besoin de N niveaux) de crédit supplémentaires pour réclamer ce chunk. »* |

L'adjacence est par **face, pas coin** : un chunk diagonal a besoin d'un de ses deux voisins orthogonaux réclamés d'abord. Le territoire reste donc toujours un seul blob connecté.

### Comment le visée est lue

L'écouteur fait attention à ne pas transformer l'exploitation minière ordinaire en tentatives de réclamation accidentelles :

- Cliquer sur un bloc qui est à l'intérieur de votre propre territoire n'est jamais une réclamation, peu importe ce qui est derrière. L'exploitation minière d'un générateur de pavé à deux blocs du mur ne fait rien.
- Cliquer sur un bloc qui est lui-même dans un chunk verrouillé cible ce chunk directement.
- Cliquer sur l'air trace un court rayon (5 blocs) le long de votre ligne de mire et prend le premier chunk verrouillé qu'il entre — s'arrêtant au premier bloc solide, donc vous ne pouvez pas réclamer à travers vos propres murs.
- Regarder droit vers le haut ou vers le bas ne réclame jamais.
- Les messages d'échec sont limités à un taux d'un tous les deux secondes par joueur, donc un coup d'exploitation minière ne peut pas spammer le chat.

!!! tip "Frapper le mur vous dit quoi faire"
    Entrer dans un chunk verrouillé donne au propriétaire un indice contextuel plutôt qu'un refus plat : *« Frappez la bordure pour réclamer ce chunk pour N niveaux) ! »* s'ils peuvent se le permettre, ou combien de niveaux il leur faut encore s'ils ne peuvent pas. Tout le monde d'autre obtient juste *« Ce chunk est verrouillé. »*

---

## Perdre des chunks

Si le niveau d'île tombe en dessous de ce qui a été dépensé, les chunks les plus récemment réclamés se reverrouillent — **dernier réclamé, d'abord perdu** — jusqu'à ce que la dépense s'adapte au nouveau niveau. C'est pourquoi l'ordre de réclamation est enregistré.

Rien à l'intérieur d'un chunk reverrouillé n'est touché. Les constructions, les coffres, les mobs, les fermes sont tous exactement où ils étaient ; ils sont simplement inaccessibles jusqu'à ce que les niveaux reviennent. Parce que le reverrouillage est strictement en ordre inverse, regagner les niveaux les donne en l'ordre où ils ont été perdus.

La perte de niveau provient généralement de trois endroits :

- **Morts**, si la pénalité de mort du plugin Level est activée — dans ChunkBlock, cette pénalité est un paramètre de *territoire*, donc examinez-la délibérément.
- **Supprimer des blocs** — extraire une grande tour de pavé peut genuinely réduire l'île.
- **Administrateurs** recalculant ou ajustant un niveau.

### Joueurs debout dans un chunk qui se ferme

Avec `eject-players-on-relock: true` (la valeur par défaut), quiconque est coincé à l'intérieur est déplacé à la position déverrouillée la plus proche dans sa propre île :

- Le spot est le point le plus proche à l'intérieur d'un chunk qu'ils possèdent, bloqué à un bloc dedans afin qu'ils ne se posent pas sur la ligne.
- Si le spot n'est pas sûr et le joueur n'est pas en vol, un bloc d'atterrissage est créé sous eux. C'est la **seule** fois que ChunkBlock modifie le monde, et c'est toujours dans un chunk *déverrouillé*.
- L'état du vol est préservé à travers le déplacement, et les dégâts de chute sont annulés pendant quelques secondes après. Une éjection ne tue jamais.
- Un joueur qui n'est pas membre de cette île est envoyé à la maison de sa propre île, donc personne n'est jamais posé sur l'île d'un étranger.

Avec `eject-players-on-relock: false`, ils peuvent sortir mais pas revenir dedans.

### Mode cliquet

```yaml
chunkblock:
  relock-on-level-loss: false
```

Le territoire ne rétrécit jamais. Les chunks coûtent des niveaux à réclamer, mais une fois réclamés, ils sont permanents. Bon pour les serveurs familiaux, ou si vous préférez ne pas avoir à expliquer la pénalité de mort à tout le monde.

---

## La bordure que vous ne pouvez pas franchir

Un chunk verrouillé est verrouillé à **chaque y**, du dessous du vide au-dessus de la limite de construction. Il n'y a pas de couloir de survol et pas de creusement en dessous par construction — la vérification est 2D à dessein.

=== "Joueurs"
    Le mouvement dans un chunk verrouillé est annulé *et* le joueur est téléporté le court saut en arrière, car l'annulation seule ne tient pas à la vitesse (sprint-saut, élytre, tridents de courant violent peuvent percer un mouvement annulé). Les planeur interceptés en vol reçoivent une chute lente afin qu'ils ne soient pas lâchés comme une pierre.

    Les perles de l'Ender et le fruit du choeur dans les chunks verrouillés sont annulés — et la perle est remboursée, car le lancer était une honnête erreur. Tout autre téléportage qui se termine dans le territoire verrouillé (maisons de plugin, respawn anchors, commandes) est autorisé à se déclencher puis sont silencieusement corrigés une tick plus tard.

    Rejoindre et réapparaître sont tous deux revérifiés une tick tard, donc « le chunk s'est reverrouillé pendant que j'étais hors ligne » se résout.

=== "Montures et véhicules"
    Les chevaux, les porcs, les striders et les bateaux ne font pas de manière fiable les événements de mouvement des joueurs gated, donc un joueur à cheval est surveillé une fois par seconde et est démonté et remis en arrière si la monture traverse la ligne.

    Les bateaux et les minecarts — montés ou à la dérive — rebondissent à la bordure du chunk. Un véhicule transportant un joueur exempté passe librement.

=== "Blocs et physique"
    Rien ne franchit la bordure :

    - Les pistons ne peuvent pas pousser ou tirer les blocs au-delà de cela.
    - Les liquides s'arrêtent de couler à cela.
    - Les distributeurs et les droppers ne peuvent pas tirer à travers.
    - Les arbres ne poussent pas dedans, et le feu, l'herbe, les vignes et la sculk ne se propagent pas dedans.
    - Les explosions ne endommagent pas les blocs de l'autre côté.
    - Placer, casser, mettre en seau et interagir à l'intérieur d'un chunk verrouillé sont tous refusés — y compris les tentatives de portée depuis un chunk déverrouillé.

=== "Mobs et objets"
    L'apparition naturelle de mobs à l'intérieur des chunks verrouillés est annulée quand `deny-mob-spawns-in-locked: true` (la valeur par défaut), donc la zone interdite ne s'emplit pas silencieusement de mobs hostiles attendant le jour où elle s'ouvre.

    Les objets tombés sont suivis pendant 20 secondes et rebondissent le moment où ils franchissent la ligne, donc un lancer mal chronométré ou une mort près du mur ne nourrit pas votre équipement au vide. Désactivez-le avec `bounce-back-items: false`.

---

## Voir la frontière

`border.show-particles: true` dessine un rideau de poussière sur chaque face entre votre territoire et un chunk verrouillé, pour tout joueur à moins de 5 blocs de celui-ci, redessiné quelques fois par seconde pour être visible même en se tenant immobile. La couleur est configurable ; la section du rideau au-dessus de la limite de hauteur du monde est dessinée en orange afin que les planeur puissent voir où le mur continue.

`border.client-side-barrier-blocks: true` ajoute une couche de blocs de barrière sur ces mêmes faces. Ils sont envoyés par joueur avec `sendBlockChange` — **le monde n'est jamais modifié**, et les vrais blocs sont restaurés quand le joueur s'éloigne, se téléporte, change de monde ou se déconnecte.

Les deux sont purement cosmétiques. Les désactiver ne rend pas la bordure plus franchissable ; ça la rend juste invisible.

### `/ch chunks`

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

- **`■` vert** — un chunk que vous possédez.
- **`▣` jaune** — réclaimable maintenant : adjacent, dans la plage, en dessous de la limite.
- **`□` gris** — verrouillé et pas encore réclaimable.
- **`◆` bleu** — le chunk dans lequel vous vous tenez.

La carte grandit avec votre île jusqu'à une vue de 15 × 15, qui est aussi large que le chat le permet confortablement.

---

## Limites

Deux plafonds s'appliquent et le plus petit gagne.

**`max-chunks`** — un plafond plat y compris le chunk central. La valeur par défaut `441` est un carré complet 21 × 21. `-1` signifie « pas de limite au-delà de la plage de protection ».

**La plage de protection** — les chunks réclamés doivent s'adapter entièrement à l'intérieur. Le plus grand rayon d'anneau qui rentre est `(protection-range − 8) ÷ 16` arrondi vers le bas, donnant `(2r + 1)²` chunks :

| `protection-range` | Rayon d'anneau | Chunks |
|---:|---:|---:|
| 120 | 7 | 225 |
| 168 | 10 | 441 |
| 240 (par défaut) | 14 | 841 |
| 400 | 24 | 2401 |

Avec les valeurs par défaut expédiées (`protection-range: 240`, `max-chunks: 441`), le plafond plat est celui qui mord, et une île culmine à un carré 21 × 21. Quand une île atteint sa taille maximale, la dernière réclamation est annoncée avec *« Votre île a atteint sa taille maximale ! »*

!!! warning "Relever le plafond"
    `protection-range` ne peut jamais dépasser `distance-between-islands`, et ni l'un ni l'autre ne peut être changé en jeu sans réinitialiser les mondes et les bases de données. Décidez du plafond avant d'ouvrir le serveur.

!!! note "Pourquoi les centres d'îles sont centrés sur les chunks"
    Les centres d'îles atterrissent toujours à x ≡ 8, z ≡ 8 dans un chunk pour que le bloc magique se tienne au milieu de son chunk plutôt que sur une couture. ChunkBlock calcule les décalages mondiaux pour cela lui-même et aligne `distance-between-islands` à un multiple de 8 au chargement — c'est pourquoi il n'y a pas de paramètres `offset-x`/`offset-z` à mal faire.

---

## Outils administrateur

=== "/chadmin chunks &lt;player&gt;"
    Affiche le nombre de chunks du joueur et le maximum effectif, les niveaux qu'il a dépensés et son crédit actuel. Le premier arrêt pour *« le jeu dit que je ne peux pas réclamer et je ne sais pas pourquoi »*.

=== "/chadmin chunks &lt;player&gt; reset"
    Reverrouille tout de retour au chunk central et efface le dossier de dépenses. Leurs constructions sont intactes — ils doivent simplement regagner le territoire. Utile pour les tests et pour nettoyer après un accident de calcul de niveau.

=== "/chadmin bypass"
    Bascule l'application du verrouillage des chunks pour vous-même. Nécessite `chunkblock.mod.bypasschunks`, qui n'est **pas** accordé à ops par défaut — vous devez l'accorder explicitement. Lors du contournement, vous pouvez vous déplacer librement à travers les chunks verrouillés et le rideau de bordure est caché pour vous, ce qui facilite l'inspection d'une construction signalée.

    Le mode spectateur est toujours exempté, permission ou pas.

---

## Pour les développeurs

Deux événements se déclenche sur chaque changement de territoire, tous deux après coup et ni l'un ni l'autre annulable :

- **`ChunkUnlockEvent`** — une fois par chunk réclamé.
- **`ChunkRelockEvent`** — une fois par chunk perdu, le plus récemment réclamé en premier.

Les deux portent l'île, le décalage du chunk par rapport au chunk central et l'index que le chunk tient dans l'ordre de réclamation.

Le gestionnaire de requête **`unlocked-chunks`** donne les mêmes informations aux plugins sans dépendance au moment de la compilation sur ChunkBlock. Voir la [section API](index.md#api) pour tous deux.
