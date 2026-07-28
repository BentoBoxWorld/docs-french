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

!!! warning "`default-biome` et `make-structures` sont des paramètres de génération de monde"
    Ces deux options sont figées au moment où un chunk est généré. BentoBox ne prend pas en charge leur modification en cours de partie — les chunks existants conservent leur apparence actuelle, attendez-vous donc à une jointure visible aux frontières des anciens chunks, sauf si vous démarrez un monde neuf. `sulfur-vent-chance` fait exception : depuis la 2.1.0, elle peut être modifiée sur un serveur en fonctionnement, elle n'affecte simplement que les chunks générés à partir de ce moment-là.

??? note "world.default-biome"
    Le biome par défaut de l'Overworld. `SULFUR_CAVES` (Minecraft 26.2+) donne une eau vert acide avec un brouillard vert correspondant. Sur les serveurs plus anciens, ce biome n'existe pas et `WARM_OCEAN` est utilisé à la place.

    Par défaut : `SULFUR_CAVES` (était `WARM_OCEAN` avant la 2.0.0)

??? note "world.sulfur-vent-chance"
    Chance (0–100) par chunk qu'une cheminée de soufre se génère juste sous la surface de la mer. Les cheminées sont constituées de soufre puissant au-dessus d'un bloc de magma et bouillonnent, gazent et entrent en éruption sous forme de geysers. Elles se déclinent en quatre formes naturelles — cheminée, monticule, jumelle et éperon hérissé — avec des variations aléatoires. Nécessite Minecraft 26.2 ou une version ultérieure ; ignoré sur les serveurs plus anciens.

    Depuis la 2.1.0, cette option peut être modifiée sans réinitialiser le monde — la nouvelle valeur ne s'applique qu'aux chunks générés à partir de ce moment-là.

    Par défaut : `10`

??? note "world.make-structures"
    Génère les structures vanilla dans les mondes. Les chambres d'épreuves et autres structures souterraines se génèrent enfouies sous le fond de l'océan, donnant aux joueurs une raison de creuser vers le bas, et rendant la clé d'épreuve du kit de départ gagnable.

    Par défaut : `true` (était `false` avant la 2.0.0)

### Offrandes aux geysers

!!! new "Ajouté dans AcidIsland 2.1.0, complété en 2.1.1"
    Jetez des objets dans l'eau autour d'une cheminée de soufre et le geyser les engloutit en guise d'offrandes. Lors de sa prochaine éruption, la cheminée recrache des récompenses hors du panache — transmutées, et non restituées. Ce que vous lui donnez détermine ce qui en ressort : sacrifiez des minerais et elle penchera vers les gemmes, sacrifiez du bois et elle penchera vers les êtres vivants. Ce mécanisme nécessite Minecraft 26.2 ou une version ultérieure (là où les cheminées de soufre existent) et se désactive discrètement sur les serveurs plus anciens.

    Depuis la 2.1.1, une cheminée **commerce au lieu de jouer aux dés** : elle calcule ce que valait votre offrande et rend des récompenses d'une valeur à peu près équivalente, si bien qu'un diamant revient en gemmes et qu'une pile de pierre taillée revient en babioles de la même trempe. Les objets qui flottent près d'une cheminée dérivent vers son bassin, une offrande n'a donc pas besoin d'être précise, et une cheminée nourrie est provoquée pour entrer en éruption quelques secondes plus tard, afin que la récompense arrive pendant que le joueur regarde encore.

    Seuls les objets lancés par un joueur comptent — les objets tombés à la mort, ceux issus de blocs et ceux lâchés par les monstres qui dérivent dans un bassin sont ignorés. Les objets que l'acide dissout à l'intérieur du bassin d'une cheminée comptent comme des offrandes au lieu d'être perdus, et les récompenses recrachées sont marquées afin de ne jamais pouvoir être recyclées en nouvelles offrandes. Une cheminée minée fait perdre les offrandes qu'elle avait en attente.

??? note "world.geyser-offerings.enabled"
    Interrupteur principal du mécanisme d'offrandes aux geysers.

    Par défaut : `true`

??? note "world.geyser-offerings.max-rewards"
    Nombre maximal de récompenses qu'une seule éruption peut recracher, quel que soit le nombre d'objets offerts.

    Par défaut : `12`

??? note "world.geyser-offerings.match-value"
    Répond à une offrande par des récompenses de valeur à peu près équivalente, au lieu d'une récompense aléatoire par objet. Une cheminée transmute plutôt qu'elle ne détruit : donnez-lui un diamant et elle vous doit la valeur d'un diamant, donnez-lui de la pierre taillée et elle vous doit de la pierre taillée. La valeur provient de `geyser-values.yml`, qui peut se rabattre sur les valeurs de blocs de l'addon Level. Désactivez cette option pour retrouver le paiement d'un tirage par objet de la 2.1.0.

    Par défaut : `true` (ajouté en 2.1.1)

??? note "world.geyser-offerings.exchange-rate"
    Fraction de la valeur offerte qu'une cheminée rembourse lorsqu'elle aligne les valeurs. `1.0` correspond à un échange équitable, en dessous de `1.0` la cheminée prend une commission, au-dessus de `1.0` faire une offrande devient rentable en soi — ce que les joueurs ne manqueront pas d'exploiter, augmentez donc cette valeur avec prudence.

    Par défaut : `1.0` (ajouté en 2.1.1)

??? note "world.geyser-offerings.reward-ceiling"
    Valeur maximale d'une seule récompense, exprimée en multiple de la valeur de l'objet le plus précieux offert. Une pile de pierre taillée vaut une émeraude et un générateur de pierre est infini : sans ce plafond, une cheminée devient une imprimante à gemmes. Les récompenses nommées dans une liste `from:` de `geyser-loot.yml` ignorent ce plafond — une transmutation que l'administrateur a lui-même écrite est toujours autorisée. Mettez `0` pour ne pas fixer de limite.

    Par défaut : `8.0` (ajouté en 2.1.1)

??? note "world.geyser-offerings.erupt-on-offering"
    Provoque une cheminée nourrie pour qu'elle entre en éruption quelques secondes après avoir été alimentée, au lieu d'attendre le cycle d'éruption vanilla, afin que la récompense suive l'offrande pendant que le joueur est encore là pour la voir. Désactivez cette option pour laisser entièrement le rythme des éruptions à vanilla — les offrandes sont alors conservées jusqu'à ce que la cheminée entre en éruption.

    Par défaut : `true` (ajouté en 2.1.1)

#### geyser-loot.yml

Les récompenses sont définies dans `geyser-loot.yml`, copié dans `plugins/BentoBox/addons/AcidIsland/` au premier démarrage. Chaque entrée est soit un objet, soit une commande console :

```yaml
loot:
  - {item: RAW_IRON, weight: 30, channel: mineral, amount: {min: 1, max: 3}}
  - {item: OBSIDIAN, weight: 10, channel: nether, from: [MAGMA_BLOCK, BASALT, LAVA_BUCKET]}
  - {item: MUSIC_DISC_13, weight: 1, from: [BONE, GUNPOWDER]}
  - {command: "give %player% cod 1", weight: 1, value: 4}
```

| Clé | Signification |
| --- | --- |
| `item` / `command` | La récompense. Les commandes sont exécutées depuis la console ; `%player%` est remplacé par le nom du joueur. |
| `weight` | Probabilité relative que l'entrée soit tirée — plus la valeur est élevée, plus elle est fréquente. |
| `channel` | Facultatif. L'un de `gems`, `nether`, `mineral`, `forestry`, `husbandry`. Les offrandes attirent la table vers leur propre canal, à hauteur de la part de la *valeur* de l'offrande qui y a été versée. |
| `from` | Liste facultative de matériaux qui se transmutent en cette récompense. Offrez l'un d'entre eux et l'entrée devient huit fois plus probable — et elle ignore `reward-ceiling`, ce qui en fait le seul moyen pour une cheminée de rendre quelque chose de bien plus précieux que ce qui y est entré. |
| `amount` | Quantité facultative, fixe ou sous forme d'intervalle `{min, max}`. `1` par défaut. |
| `value` | Valeur facultative d'une unité de cette récompense, qui remplace la valeur du matériau. Les récompenses de type commande sont gratuites tant qu'elles ne définissent pas cette valeur : donnez donc une valeur aux commandes payantes, sinon elles apparaîtront à chaque paiement. |

!!! warning "Mise à niveau depuis la 2.1.0"
    `geyser-loot.yml` n'est écrit que lorsqu'il est absent : un exemplaire laissé par la 2.1.0 n'obtiendra donc ni les transmutations `from:` ni les champs `value:`, et aucune des transmutations nommées ne fonctionnera. Supprimez le fichier pour qu'il soit régénéré, puis réappliquez vos modifications.

#### geyser-values.yml

`geyser-values.yml` indique ce qu'un matériau vaut aux yeux d'une cheminée. L'échelle est arbitraire — seuls les rapports comptent — et elle est calée sur le lingot de fer `6`, le lingot d'or `12`, l'émeraude `15` et le diamant `45`, si bien qu'un diamant revient sous la forme de trois émeraudes, ou d'une émeraude et de deux lingots d'or.

La valeur est résolue dans cet ordre, le premier résultat l'emportant :

1. la table `values:` du fichier
2. les valeurs de blocs de l'**addon Level** pour ce monde, si Level est installé et que `use-level-addon: true` — ainsi, un serveur qui a déjà réglé Level n'a pas à tout régler une deuxième fois. Supprimez une entrée de `values:` pour confier ce matériau à Level.
3. la valeur `default:`, pour tout ce qu'aucune autre source ne connaît

La valeur dépend uniquement du matériau : les enchantements, les noms personnalisés et le contenu des boîtes de Shulker ne sont pas comptés, l'équipement vaut donc son matériau de base.

Le fichier est créé automatiquement au premier démarrage.

## Permissions

Les permissions peuvent être trouvées [ici](Permissions).

## Commandes

Les commandes peuvent être trouvées [ici](Commands).

## Placeholders

Les placeholders peuvent être trouvés [ici](Placeholders).

## API

Les autres addons peuvent se greffer sur le mécanisme d'offrandes aux geysers grâce à deux évènements, tous deux ajoutés en 2.1.0 :

- `GeyserSacrificeEvent` — déclenché lorsqu'une cheminée engloutit une offrande. Annulable.
- `GeyserTransmuteEvent` — déclenché lorsqu'une cheminée recrache une récompense.

## Journal des modifications

!!! warning "Nouveautés dans v2.1.1 — les cheminées commercent au lieu de jouer aux dés (supprimez `geyser-loot.yml`)"
    **Publié :** 26 juillet 2026

    La 2.1.0 a livré le mécanisme d'offrandes aux geysers, mais pas l'économie qui devait l'accompagner : une cheminée tirait une récompense par objet jeté, si bien qu'une pile de pierre taillée et un diamant achetaient le même tirage, et le mécanisme ne disait jamais un mot au joueur. La 2.1.1 le complète. Compatibilité : BentoBox API 3.14.0 · Minecraft 1.21.5 – 26.2 (les fonctionnalités liées aux geysers nécessitent 26.2+) · Java 21.

    - ⚙️ 🔺 **Alignement des valeurs.** Un nouveau fichier `geyser-values.yml` indique ce qu'un matériau vaut aux yeux d'une cheminée, calé sur le lingot de fer 6, le lingot d'or 12, l'émeraude 15 et le diamant 45. Une cheminée additionne ce dont elle a été nourrie et continue de tirer des récompenses qu'elle peut encore s'offrir jusqu'à ce que cette valeur soit épuisée. Quatre nouvelles options sous `world.geyser-offerings` : `match-value`, `exchange-rate`, `reward-ceiling` et `erupt-on-offering` (voir la Configuration ci-dessus). Là où le fichier reste muet, la valeur peut se rabattre sur les valeurs de blocs de l'**addon Level** via `use-level-addon: true`.
    - ⚙️ **Transmutations nommées.** Les entrées de butin de `geyser-loot.yml` acceptent désormais une liste `from:` des matériaux qui se transmutent en elles — les blocs de magma donnent de l'obsidienne, le fer donne de l'or, les os avec de la poudre à canon donnent des disques de musique. Une entrée `from:` est huit fois plus probable et ignore `reward-ceiling`, ce qui en fait l'endroit idéal pour les récompenses qui nécessiteraient autrement une ferme à monstres.
    - 🔡 **La cheminée prend enfin la parole.** Une nouvelle section de langue `acidisland.geyser` ajoute les messages d'offrande, de bouillonnement et de paiement ainsi que les noms d'affichage des cinq canaux de récompense, dans les 24 langues. Ce sont des messages de barre d'action par défaut — retirez la balise `[actionbar]` pour les envoyer dans le chat.
    - **Les lancers n'ont plus besoin d'être précis.** Les objets qui flottent près d'une cheminée dérivent vers son bassin, et une cheminée nourrie est provoquée pour entrer en éruption quelques secondes plus tard, afin que le paiement arrive pendant que le joueur regarde encore.
    - **Orientation des canaux par la valeur.** Les offrandes attirent toujours la table des récompenses vers leur propre canal, mais cette attraction est désormais pondérée par la valeur plutôt que par le nombre d'objets — un diamant oriente aussi fermement que la pile de pierre taillée qu'il vaut.

    🔺 **Supprimez `geyser-loot.yml`** de `plugins/BentoBox/addons/AcidIsland/` si vous avez utilisé la 2.1.0. Le fichier n'est écrit que lorsqu'il est absent : un exemplaire existant n'obtiendra donc ni les transmutations `from:` ni les champs `value:`. Réappliquez vos modifications au fichier régénéré.

    ⚙️ `geyser-values.yml` est créé automatiquement au premier démarrage, et les quatre nouvelles options sont ajoutées à `config.yml` au lancement, vos réglages existants étant préservés. 🔡 Régénérez ou mettez à jour vos fichiers de langue pour récupérer les chaînes `acidisland.geyser`. Les serveurs qui préféraient le paiement de la 2.1.0 peuvent mettre `match-value: false` et conserver tout le reste.

    [Release v2.1.1](https://github.com/BentoBoxWorld/AcidIsland/releases/tag/2.1.1)

??? note "Nouveautés dans v2.1.0 — offrandes aux geysers"
    **Publié :** 26 juillet 2026

    AcidIsland 2.1.0 transforme les cheminées de soufre, qui passent du décor à une véritable économie. Jetez des objets dans l'eau autour d'une cheminée et le geyser les consomme en guise d'offrandes, puis vous rembourse lors de sa prochaine éruption en recrachant des récompenses transmutées hors du panache. Compatibilité : BentoBox API 3.14.0 · Minecraft 1.21.11 – 26.2 (les offrandes aux geysers nécessitent 26.2+) · Java 21.

    - ⚙️ **Offrandes aux geysers.** Les objets qui flottent dans le bassin autour d'une cheminée de soufre sont consommés dans un grésillement en guise d'offrandes — n'importe quel endroit du bassin convient, nul besoin de viser au pixel près. Lors de la prochaine éruption de la cheminée, une récompense par objet offert (plafonnée, configurable) est recrachée du panache en une fontaine radiale.
    - **Canaux.** Les offrandes sont réparties entre les canaux **gems**, **nether**, **mineral**, **forestry** et **husbandry**, et orientent la table des récompenses vers ce qui a été sacrifié.
    - ⚙️ **Nouveau fichier `geyser-loot.yml`**, copié dans le dossier de données de l'addon au premier démarrage : des entrées d'objets pondérées avec des intervalles de quantité, ainsi que des récompenses sous forme de commandes console avec substitution de `%player%`.
    - ⚙️ **Nouvelle section de configuration `world.geyser-offerings`** : `enabled` (`true` par défaut) et `max-rewards` par éruption (`12` par défaut).
    - **Nouveaux évènements d'API** pour les autres addons : `GeyserSacrificeEvent` (annulable) et `GeyserTransmuteEvent`.
    - **Compatible avec la destruction d'objets par l'acide.** Les objets que l'acide dissout à l'intérieur du bassin d'une cheminée comptent comme des offrandes au lieu d'être perdus, quel que soit votre temps de destruction `acid.damage.acid.item` — et les récompenses recrachées sont marquées afin de ne jamais pouvoir être recyclées en nouvelles offrandes. Les cheminées minées font perdre leurs offrandes en attente : le geyser n'est pas un coffre de stockage.
    - ⚙️ **`world.sulfur-vent-chance` n'exige plus de réinitialiser le monde** pour être modifiée. Elle n'affecte que les chunks nouvellement générés, les administrateurs peuvent donc ajuster la densité des cheminées sur un serveur en fonctionnement.

    **Aucune réinitialisation du monde nécessaire.** Les offrandes fonctionnent sur n'importe quelle cheminée de soufre existante — cette version n'apporte aucun changement de génération de monde.

    [Release v2.1.0](https://github.com/BentoBoxWorld/AcidIsland/releases/tag/2.1.0)

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
