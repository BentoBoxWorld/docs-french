# Greenhouses

Greenhouses est un addon BentoBox pour booster votre monde d'île! Il permet aux joueurs de construire leurs propres serres de biome complètes avec météo, génération de mobs amicaux, croissance unique des plantes, et même l'érosion des blocs!

Les serres sont faites de verre et doivent contenir les blocs trouvés dans la recette du biome pour être valides. Il existe une interface graphique de recette. Une fois construite, la serre peut être utilisée pour cultiver des plantes avec de la farine d'os, et elle peut générer des mobs spécifiques au biome. Si vous incluez un entonnoir avec de l'eau dedans, la neige se formera à l'intérieur de la serre quand il pleut. Si vous mettez de la farine d'os dans l'entonnoir, les plantes spécifiques au biome pousseront. Certains blocs peuvent également se transformer au fil du temps en raison de l'« érosion ».

Créé et maintenu par [tastybento](https://github.com/tastybento).

{{ addon_description("Greenhouses") }}

## Fonctionnalités

* Créez votre propre serre de biome autonome sur une île (ou ailleurs si vous le souhaitez)
* Les serres peuvent cultiver des plantes qui ne peuvent normalement pas être cultivées, comme les tournesols
* Les mobs amicaux peuvent générer si votre serre est bien conçue - vous avez besoin de slimes? Construisez une serre de marais!
* Les blocs changent dans les biomes au fil du temps - la terre devient du sable dans un désert, la terre devient de l'argile dans une rivière, par exemple.
* Les serres peuvent fonctionner dans plusieurs mondes.
* Interface graphique facile à utiliser qui affiche les recettes de serre (par exemple **/is greenhouses**)
* Les administrateurs peuvent personnaliser entièrement les biomes et les recettes

## Comment construire une serre

Cet exemple s'applique quand vous êtes dans le monde BSkyBlock. Pour AcidIsland, utilisez simplement /ai au lieu de /island.

1. Fabriquez des blocs de verre et construisez un ensemble rectangulaire de murs avec un toit plat.
2. Placez un entonnoir dans le mur ou le toit.
3. Placez une porte dans le mur pour pouvoir entrer et sortir.
4. Tapez **/island greenhouses** et lisez les règles pour la serre que vous voulez.
5. Quittez l'interface graphique et placez des blocs, de l'eau, de la lave et de la glace pour créer votre biome souhaité.
6. Tapez **/island greenhouses** à nouveau et cliquez sur le biome pour le créer.
7. Tapez **/island greenhouses help** pour voir d'autres options.

### Une fois créée :

* Utilisez de la farine d'os pour cultiver des petites plantes sur les blocs d'herbe immédiatement dans la serre.
* Ou placez de la farine d'os dans l'entonnoir pour que la serre vaporise automatiquement de la farine d'os. Revenez plus tard pour voir ce qui pousse!
* Placez un seau d'eau (ou plus) dans l'entonnoir pour faire tomber la neige dans les biomes froids. La neige tombera quand il pleut dans le monde. Chaque chute de neige vide un seau d'eau.
* Les mobs amicaux spécifiques au biome peuvent générer dans votre serre - les règles habituelles s'appliquent (être à plus de 24 blocs de distance).

## FAQ

* Puis-je utiliser du verre teinté? Oui, vous pouvez. C'est joli.
* Puis-je remplir ma serre complètement d'eau? Oui. C'est un océan.
* Un calmar va-t-il générer là-bas? Peut-être... d'accord, oui, il va générer si c'est un océan assez grand.
* Comment puis-je placer une porte haut dans le mur si le mur est tout en verre? Placez-la sur un entonnoir.
* Comment puis-je placer une porte sur un entonnoir? Accroupissez-vous et ensuite placez-la.
* Puis-je utiliser des portes en métal? Oui.
* Puis-je utiliser une trappe? Oui.
* Puis-je cultiver des fleurs de marais avec cela? Oui. Créez un biome de marais et utilisez de la farine d'os.
* Combien de farine d'os est utilisé pour cultiver des plantes? Une pour chaque plante réussie.
* Combien d'eau dois-je mettre dans l'entonnoir pour qu'il neige? Un seau d'eau (juste l'eau) est utilisé à chaque fois qu'il pleut. Cela ne se produit que dans les biomes froids.
* Puis-je construire une serre du Nether? Essayez et voyez... (En fait, vous avez peut-être besoin d'une permission)
* Puis-je construire des serres dans le Nether? Oui. Vous pouvez coloniser le Nether avec elles.
* Quel type de mobs spawner dans les biomes? C'est ce que vous attendriez, des loups dans Taiga froid, des chevaux dans les plaines, etc.
* Comment un administrateur peut-il mettre à jour la serre du Nether pour avoir une chance de générer des Wither Skeletons ? Ajoutez le mob à la recette `NETHER` dans `biomes.yml` — consultez [Personnaliser les spawns de mobs](#personnaliser-les-spawns-de-mobs-exemple-wither-skeletons) ci-dessous.

## Plugin requis

Cette version de Greenhouses est un addon pour BentoBox et ne fonctionne pas de manière autonome!

1. BentoBox - assurez-vous d'utiliser la dernière version ! Greenhouses 1.11.0 nécessite BentoBox 3.24.0 ou une version ultérieure, Paper 1.21.11 à 26.3 et Java 25.

## Installation et configuration

1. Téléchargez et installez BentoBox si vous ne l'avez pas déjà fait
2. Téléchargez l'addon
3. Placez-le dans le dossier des addons de BentoBox
4. Redémarrez votre serveur
5. L'addon créera un dossier de données appelé greenhouses. Ouvrez ce dossier.
6. Vérifiez **config.yml** et modifiez-le comme vous le souhaitez, notez la liste des noms de mondes.
7. Configurez le **biomes.yml** si vous le souhaitez (avancé).
8. Tapez **/bsbadmin greenhouses reload** dans le jeu pour recharger la configuration ou redémarrez le serveur.
9. Fait!

Une option de `config.yml` a été ajoutée dans Greenhouses 1.11.0 :

??? note "sample-ticks"
    Ajoutée dans Greenhouses 1.11.0. Fréquence, en ticks serveur (20 = 1 seconde), à laquelle des emplacements aléatoires de chaque serre sont choisis pour l'apparition des mobs et la conversion des blocs. Des valeurs plus basses répartissent la charge plus uniformément. Cela ne change pas les taux globaux, définis par `mobtick` et `blocktick` : en moyenne, chaque emplacement a toujours une chance par `mobtick` ou `blocktick`, si bien que les mobs arrivent progressivement plutôt que tous en même temps.

    Par défaut : `20`

Pour construire votre première serre, construisez une boîte de verre et tapez **/is greenhouses make** pour voir quel type de serre vous obtenez. Tapez **/is greenhouses** pour voir les recettes.

## Mise à niveau

Lisez le fichier notes de version pour les modifications et les instructions de mise à niveau.

## Commandes du joueur

Ajoutez ces commandes à /island, /ai. Le libellé de la commande est `greenhouse`, avec les alias `gh` et `greenhouses`.

* **greenhouses** - ouvre l'interface graphique des recettes ; cliquer sur une recette essaie de créer cette serre
* **greenhouses help** - répertorie ces commandes
* **greenhouses make [recipe]**: Essaie de créer une serre, en trouvant la première recette valide ou en utilisant celle qui est nommée
* **greenhouses remove**: Supprime une serre dans laquelle vous vous tenez si vous êtes le propriétaire

!!! warning "`list` et `recipe` ont été supprimées en 1.10.0"
    Ces deux commandes du joueur étaient documentées mais n'ont jamais été réellement enregistrées — c'étaient des ébauches inaccessibles, et les appeler n'a jamais produit qu'une erreur de commande inconnue. Elles ont été supprimées en 1.10.0. `/is greenhouses` sans argument ouvre l'interface graphique des recettes, ce qui est ce qu'elles étaient censées faire.

## Commandes Admin

!!! new "Ajouté dans Greenhouses 1.10.0"
    Avant la 1.10.0, l'addon n'avait aucune arborescence de commandes admin. Si l'enregistrement d'une serre devenait invalide, la seule option était d'arrêter le serveur et de modifier la base de données à la main.

Enregistrées sous la commande admin de votre mode de jeu, par exemple `/bsbadmin greenhouses` ou `/acid greenhouses`. Le libellé est `greenhouses`, avec les alias `greenhouse` et `gh`.

| Commande | Rôle |
|---|---|
| `list [player] [page]` | Liste paginée des serres, éventuellement celles d'un seul joueur. Les enregistrements qui n'ont pas pu être chargés sont **toujours** listés eux aussi, avec la raison. |
| `info [id]` | Recette, propriétaire, monde, emplacement, boîte englobante, superficie, biome d'origine, entonnoir, état de dégradation et blocs manquants. Sans identifiant, utilise la serre dans laquelle vous vous tenez. |
| `delete <id>` | Supprime un enregistrement — chargé ou non — après vous avoir demandé de confirmer. |
| `tp <id>` | Vous téléporte au milieu du sol de la serre. Alias : `teleport`. |
| `verify [id]` | Revérifie une serre ou toutes les serres par rapport à leur recette et signale ce qui manque. Alias : `check`. |
| `reload` | Relit `biomes.yml`, puis recharge les serres depuis la base de données. |
| `edit [recipe]` | Ouvre l'[éditeur de recette](#in-game-recipe-editor), ou l'éditeur d'une recette. Depuis la 1.11.0. |
| `build <recipe> [x y z] [WxDxH] [keep\|clear]` | Construit une [serre de test](#test-greenhouse-builder) pour une recette, autour de vous ou centrée sur le point du sol indiqué. Depuis la 1.11.0. |

- Les identifiants proviennent de `list` et peuvent être abrégés en n'importe quel préfixe ne correspondant qu'à **une seule** serre. Un préfixe ambigu est traité comme une absence de correspondance plutôt que comme une supposition, car la suppression d'une mauvaise serre est irréversible.
- Tout fonctionne depuis la console du serveur, sauf `tp`, `edit` et `build`.
- Les enregistrements de serres qui ne peuvent pas être chargés — chevauchement, recette inconnue, monde absent, aucun emplacement — sont conservés en mémoire avec la raison au lieu d'être silencieusement ignorés. C'est ce qui les rend listables et supprimables.
- Les enregistrements ne sont jamais supprimés automatiquement. Retirer la serre d'un joueur sans qu'on le demande serait pire qu'un avertissement récurrent.

!!! tip "Serres qui se chevauchent"
    Si deux serres enregistrées se chevauchent, l'une est ignorée au démarrage et nommée dans le journal, avec l'enregistrement qu'elle chevauche. Utilisez `/bsbadmin greenhouses list` pour voir les enregistrements ignorés et pourquoi, puis `/bsbadmin greenhouses delete <id>` pour retirer celui que vous ne voulez pas. Aucune modification de base de données et aucun redémarrage nécessaires.

### Hub d'administration { #admin-hub }

*Ajouté dans Greenhouses 1.11.0.*

Exécuter `/bsbadmin greenhouses` sans argument ouvre une interface graphique qui donne accès à tous les outils d'administration. Depuis la console, la commande affiche toujours l'aide. Le hub comporte ces boutons :

- **Recettes** ouvre l'éditeur de recettes.
- **Serres** ouvre le navigateur de serres.
- **Construire une serre de test** construit une serre de test à l'endroit où vous vous trouvez.
- **Vérifier toutes les serres** revérifie chaque serre.
- **Recharger** effectue le rechargement, après confirmation.

Chaque bouton n'apparaît que si vous avez la permission de la sous-commande correspondante, et il exécute la même commande que celle que vous taperiez : les vérifications de permission et les messages sont donc identiques.

Le navigateur liste toutes les serres, y compris celles qui n'ont pas pu être chargées, et peut être filtré par propriétaire. Dans le navigateur :

| Clic | Effet |
|---|---|
| Clic gauche | Téléporte à la serre |
| Clic droit | La vérifie |
| Maj+clic | Affiche ses détails |
| ++q++ | La supprime, après une boîte de dialogue de confirmation |

### Éditeur de recettes en jeu { #in-game-recipe-editor }

*Ajouté dans Greenhouses 1.11.0.*

`/bsbadmin greenhouses edit [recipe]` (permission `[gamemode].greenhouses.admin.edit`) crée, modifie, duplique et supprime des recettes de biome sans toucher à `biomes.yml` ni redémarrer. Vous pouvez modifier chaque partie d'une recette :

- icône, nom et description ;
- biome, priorité et permission ;
- couverture d'eau, de lave et de glace ;
- [limites de mobs par habitat](#mob-limits-per-habitat) ;
- blocs, plantes et mobs requis (variantes comprises) et conversions de blocs.

Les blocs peuvent être choisis dans une liste avec recherche ou en cliquant sur un objet de votre inventaire.

Quand vous enregistrez :

- La recette est d'abord vérifiée.
- `biomes.yml` est sauvegardé dans `backups/`, et les 10 dernières sauvegardes sont conservées.
- Seule la recette modifiée est réécrite, et les commentaires sont conservés.
- Les serres appliquent immédiatement les nouvelles règles, sans redémarrage.

Les modifications non enregistrées de chaque admin sont conservées jusqu'à ce qu'il les enregistre ou les abandonne. Si un autre admin enregistre la même recette pendant que vous la modifiez, vous pouvez écraser sa version ou repartir de celle-ci. Supprimer une recette ne supprime jamais de serres : les serres qui l'utilisaient apparaissent alors comme non chargées.

### Constructeur de serre de test { #test-greenhouse-builder }

*Ajouté dans Greenhouses 1.11.0.*

`/bsbadmin greenhouses build <recipe> [x y z] [WxDxH] [keep|clear]` (permission `[gamemode].greenhouses.admin.build`) construit une serre fonctionnelle pour une recette et l'enregistre :

- des murs de verre ;
- une porte d'un style adapté au biome, du côté vers lequel vous regardez ;
- un entonnoir dans le toit, rempli de poudre d'os ;
- les blocs, l'eau et la lave dont la recette a besoin (les serres océaniques sont inondées, et celles du Nether reçoivent de la lave).

`keep` construit autour de ce qui se trouve déjà là, comme un arbre. `clear` vide d'abord l'espace, après confirmation. Les coordonnées `~ ~ ~` fonctionnent.

## Personnaliser les spawns de mobs (exemple : Wither Skeletons) { #personnaliser-les-spawns-de-mobs-exemple-wither-skeletons }

Chaque mob qu'une serre peut générer est défini par recette dans `plugins/BentoBox/addons/Greenhouses/biomes.yml`, donc ajouter un nouveau mob c'est juste éditer la configuration. Chaque entrée de la section `mobs:` d'une recette a le format :

```
ENTITY_TYPE: chance:BLOCK_TO_SPAWN_ON
```

Par exemple, pour donner à la serre du Nether une chance de générer des Wither Skeletons, trouvez la recette `NETHER:` et ajoutez une ligne à sa section `mobs:` :

```yaml
NETHER:
  # ...
  mobs:
    ZOMBIFIED_PIGLIN: 10:NETHERRACK
    PIGLIN: 10:NETHERRACK
    STRIDER: 10:LAVA
    ENDERMAN: 5:NETHERRACK
    WITHER_SKELETON: 5:NETHERRACK
```

Cela donne 5% de chance par tentative de génération pour un Wither Skeleton d'apparaître sur un bloc de netherrack à l'intérieur de la serre. Le bloc sur lequel générer peut être n'importe quel bloc de la serre — pour une atmosphère plus de forteresse, vous pourriez utiliser `WITHER_SKELETON: 10:NETHER_BRICKS` à la place, mais alors les joueurs ont besoin de briques du Nether à l'intérieur de la serre pour que cela se déclenche.

Appliquez le changement avec **/bsbadmin greenhouses reload** (ou l'équivalent de votre mode de jeu, par ex. **/acid greenhouses reload**), ou redémarrez le serveur. Les serres existantes reprennent le nouveau mob sans être reconstruites.

Choses à garder à l'esprit :

* **Toutes les chances dans une recette doivent ajouter jusqu'à 100 ou moins.** Si une nouvelle entrée pousse le total au-delà de 100, ce mob est ignoré et une erreur est enregistrée au chargement (`Mob chances add up to > 100% in NETHER biome recipe! Skipping ...`). Avant la 1.11.0, une erreur d'arrondi pouvait faire rejeter des chances totalisant exactement 100.
* La génération est également limitée par les valeurs `moblimit` et `maxmobs` de la recette, et par l'intervalle de tick de mob dans `config.yml` — donc un pourcentage bas peut sembler rare en pratique.
* Le `ENTITY_TYPE` doit être un nom [Bukkit EntityType](https://jd.papermc.io/paper/1.21.5/org/bukkit/entity/EntityType.html) valide ; les noms inconnus sont ignorés avec un avertissement.
* Sur Minecraft 26.x, le mooshroom est `MOOSHROOM`, pas `MUSHROOM_COW`. Renommez toutes les entrées `MUSHROOM_COW` dans votre `biomes.yml`.
* Depuis la 1.11.0, les mêmes changements peuvent être effectués en jeu avec l'[éditeur de recettes](#in-game-recipe-editor).

### Limites de mobs par habitat { #mob-limits-per-habitat }

*Ajouté dans Greenhouses 1.11.0.*

`moblimit` est le nombre de blocs de sol dont chaque mob a besoin, ce qui n'est pas la bonne mesure pour un océan profond, un lac de lave ou des mobs volants. Une recette peut définir trois clés facultatives supplémentaires dans `biomes.yml`. Chacune compte ses propres mobs, et chaque valeur est le nombre de blocs par mob :

| Clé | Mobs comptés | Espace de référence |
|---|---|---|
| `moblimit-water` | Mobs qui apparaissent sur l'eau | Blocs d'eau |
| `moblimit-lava` | Mobs qui apparaissent sur la lave | Blocs de lave |
| `moblimit-air` | Mobs volants : allays, chauves-souris, abeilles, ghasts, perroquets, phantoms et vex | Le volume intérieur de la serre |

Les mobs terrestres continuent d'utiliser `moblimit`, et `maxmobs` plafonne toujours le total. Si une limite n'est pas indiquée, ces mobs partagent `moblimit` avec les mobs terrestres, si bien que les recettes sans les nouvelles clés se comportent comme avant. Le `biomes.yml` fourni définit :

- `moblimit-water` : plages, plage enneigée et océan (9), et rivière (1) ;
- `moblimit-lava` : nether et forêt biscornue (9) ;
- `moblimit-air` : jungle et grottes de spéléothèmes (27), et vallée des âmes (64).

`moblimit` est exact depuis la 1.11.0 : 81 blocs à 9 blocs par mob donnent 9 mobs, et non 10. Les apparitions naturelles (vanilla) à l'intérieur d'une serre sont aussi annulées depuis la 1.11.0 : seuls les mobs propres à la recette apparaissent.

## Permissions

Une liste complète des permissions est [ici](Permissions).

La permission pour utiliser des biomes spécifiques peut être ajoutée dans biomes.yml.

Par exemple, la permission pour le biome Nether est **greenhouses.biome.nether** et est définie ici :

 NETHER:

    permission: greenhouses.biome.nether

La permission peut être n'importe quoi que vous aimez, par exemple, une permission de rang, **myserver.VIP**.

### Les permissions générales sont :

  greenhouses.player:

     description: Donne accès aux commandes du joueur
     default: true

  greenhouses.admin:

     description: Donne accès aux commandes admin
     default: op

Depuis la 1.10.0, chaque sous-commande admin possède également son propre nœud — `greenhouses.admin.list`, `.info`, `.delete`, `.tp`, `.verify` et `.reload` — tous avec `op` par défaut. La 1.11.0 ajoute `.edit` et `.build`. Les opérateurs n'ont rien à faire, mais si vous accordez l'accès admin via un plugin de permissions, vous voudrez les ajouter. Ils étaient totalement absents de `addon.yml` avant cette version, ce qui explique pourquoi seul l'accès op fonctionnait.

## Traductions

{{ translations("Greenhouses") }}

!!! warning "Nouveautés dans v1.11.0 — hub d'administration et éditeur de recettes ; nécessite BentoBox 3.24.0"
    **Publié :** 22 novembre 2026

    Compatibilité : API BentoBox 3.24.0 ou version ultérieure · Paper 1.21.11 à 26.3 · Java 25.

    - 🔡 **Hub d'administration.** `/[admin_command] greenhouses` ouvre désormais une interface graphique qui donne accès à tous les outils d'administration : modifier les recettes, parcourir les serres, construire des serres de test, toutes les vérifier et recharger. Voir [Hub d'administration](#admin-hub).
    - 🔡 **Éditeur de recettes en jeu.** `/[admin_command] greenhouses edit [recipe]` crée, modifie, duplique et supprime des recettes de biome sans toucher à `biomes.yml` ni redémarrer. Voir [Éditeur de recettes en jeu](#in-game-recipe-editor).
    - 🔡 **Constructeur de serre de test.** `/[admin_command] greenhouses build <recipe>` construit, à l'endroit où vous vous trouvez, une serre fonctionnelle pour n'importe quelle recette. Voir [Constructeur de serre de test](#test-greenhouse-builder).
    - ⚙️ **Apparition des mobs et conversion des blocs plus régulières.** Les deux parcouraient auparavant chaque bloc de chaque serre en un seul tick, si bien qu'une serre atteignait d'un coup sa limite de mobs. Elles s'exécutent désormais tous les `sample-ticks` ticks (nouveau paramètre, `20` par défaut) sur un échantillon aléatoire d'emplacements. Les taux moyens sont inchangés, et les mobs sont comptés dans la zone propre à chaque serre plutôt que dans le monde entier.
    - **Limites de mobs distinctes pour l'eau, la lave et l'air.** Nouvelles clés de recette facultatives `moblimit-water`, `moblimit-lava` et `moblimit-air`. Voir [Limites de mobs par habitat](#mob-limits-per-habitat).
    - 🐛 **Les apparitions naturelles à l'intérieur des serres sont bloquées.** La protection contre les apparitions ne reconnaissait que les blocs des murs et du toit, si bien que les serres de taïga se remplissaient de loups, et celles du Nether de ghasts, de cubes de magma et de piglins zombifiés.
    - 🐛 `moblimit` autorisait un mob de trop ; les plantes ne sont désormais placées que là où elles peuvent survivre ; les chances totalisant exactement 100 % ne sont plus rejetées.
    - 🔡 **Descriptions de recettes et couleurs MiniMessage** dans le panneau des recettes, traduites dans les 22 langues.
    - Nouvelles permissions `[gamemode].greenhouses.admin.edit` et `[gamemode].greenhouses.admin.build`, toutes deux `op` par défaut.

    🔺 **Nécessite BentoBox 3.24.0 et Paper 1.21.11+.** L'éditeur de recettes et le hub d'administration utilisent la nouvelle API de dialogues et de panneaux paginés de BentoBox ; les versions plus anciennes de BentoBox refusent donc de charger cet addon. Mettez d'abord BentoBox à jour.

    🔺 **`biomes.yml` n'est pas remplacé.** Le fichier livré a changé : les recettes ont des descriptions et des noms MiniMessage, les limites de mobs par habitat sont définies, et `MUSHROOM_COW` est maintenant `MOOSHROOM`. Votre fichier est conservé tel quel. Pour utiliser les nouvelles valeurs par défaut, fusionnez vous-même les changements ou renommez votre fichier pour qu'un nouveau soit généré. Dans les deux cas, renommez toutes les entrées `MUSHROOM_COW` en `MOOSHROOM`, car l'ancien nom n'est pas valide en 26.x.

    🔡 **Fichiers de locale.** Pour bénéficier de toutes les corrections de texte, supprimez `plugins/BentoBox/locales/Greenhouses/` avant de démarrer le serveur. BentoBox ajoute de nouvelles clés de locale aux fichiers existants, mais ne met pas à jour les clés qui ont changé.

    [Release v1.11.0](https://github.com/BentoBoxWorld/Greenhouses/releases/tag/1.11.0)

??? warning "Nouveautés dans v1.10.2 — correction d'un plantage sur Paper 26.2"
    **Publié :** 2026-09-06

    Compatibilité : API BentoBox 2.7.1 · Minecraft 1.21.5+ · Java 21. Aucun changement de config ou de locale.

    - 🐛 **La croissance des plantes ne plante plus lorsqu'un entonnoir manque de farine d'os.** Lorsque l'entonnoir du toit contenait une seule farine d'os et qu'au moins une plante a grandi, Greenhouses a écrit le reste sous la forme d'un objet avec zéro quantité. Les anciens serveurs toléraient cela silencieusement ; Paper 26.2 lance `IllegalArgumentException: amount must be greater than 0` depuis `EcoSystemManager.setBoneMeal` à chaque tick de plante et interrompt la passe de croissance pour cette serre. La dernière farine d'os est maintenant simplement retirée de l'entonnoir.

    🔺 **Si vous êtes sur Paper 26.2 ou plus récent, cette mise à jour est fortement recommandée.** Chaque serre dont l'entonnoir se vide enregistrera sinon cette erreur à chaque tick et arrêtera la croissance des plantes jusqu'à ce que de la farine d'os soit ajoutée à nouveau.

    [Release v1.10.2](https://github.com/BentoBoxWorld/Greenhouses/releases/tag/1.10.2)

??? warning "Nouveautés dans v1.10.1 — recompter si vous exécutez Limits"
    **Publié :** 2026-09-01

    Compatibilité : API BentoBox 2.7.1 · Minecraft 1.21.5+ · Java 21. Aucun changement de config ou de locale.

    - 🐛 **Greenhouses ne laisse plus les mobs contourner l'addon Limits.** Lorsque Limits a annulé une génération à la limite d'une entité, Greenhouses a continué avec l'entité jamais générée, a exécuté son contrôle « ce mob s'adapte-t-il à l'intérieur du verre ? » et, lorsqu'il ne s'adaptait pas (les ghasts sont 4×4×4, donc souvent), a appelé `remove()` sur lui. Paper déclenche un `EntityRemoveEvent` pour cela même si le mob n'a jamais entré le monde, et Limits l'a comptabilisé comme une vraie suppression, donc son compteur a diminué lentement et la prochaine génération a été autorisée — le cas signalé était des ghasts à 4/3. Les générations annulées sont maintenant complètement ignorées.

    🔺 **Si vous avez vu cela,** le compteur de Limits pour l'île affectée est toujours faux jusqu'à sa reconstruction. Faites que le joueur exécute `/[player_command] limits recount` (ou exécutez l'admin `/[admin_command] limits calc <joueur>`) une fois après la mise à jour.

    [Release v1.10.1](https://github.com/BentoBoxWorld/Greenhouses/releases/tag/1.10.1)

??? note "Nouveautés de la v1.10.0 — commandes admin"
    **Publié le :** 2026-07-26

    Greenhouses dispose enfin d'une arborescence de commandes admin. Compatibilité : API BentoBox 2.7.1 · Minecraft 1.21.5+ · Java 21.

    - 🛠️ **Commandes admin.** `list`, `info`, `delete`, `tp`, `verify` et `reload`, enregistrées sous la commande admin de votre mode de jeu (par exemple `/bsbadmin greenhouses`). Voir la section Commandes Admin ci-dessus. Les enregistrements de serres qui ne peuvent pas être chargés — chevauchement, recette inconnue, monde absent, aucun emplacement — sont désormais conservés en mémoire avec la raison au lieu d'être silencieusement ignorés, ce qui est ce qui les rend affichables et supprimables. Les enregistrements ne sont toujours jamais supprimés automatiquement.
    - ⚙️ **Nouvelles permissions.** Les six sous-commandes possèdent chacune leur propre nœud sous `greenhouses.admin.*`, tous avec `op` par défaut. Ils étaient totalement absents de `addon.yml` avant cette version, ce qui explique pourquoi seul l'accès op fonctionnait.
    - 🐛 **Vérifier une serre dont la recette n'existe plus ne lève plus de NPE.** Quand un enregistrement de la base de données nomme une recette absente de `biomes.yml`, la vérification signale désormais `FAIL_UNKNOWN_RECIPE`.
    - 🐛 **`getFloorHeight` ne lève plus d'exception sur un enregistrement sans emplacement** — précisément les enregistrements les plus susceptibles d'être invalides. Il retombe sur la boîte englobante.
    - 🔺 **La neige signale désormais un succès depuis chaque colonne analysée,** et non seulement depuis la dernière. `SnowTracker` écrasait son résultat à chaque colonne, donc une serre qui produisait de la neige dans quatre-vingt-dix colonnes et échouait sur la dernière signalait un échec — et cette valeur détermine si l'eau est consommée depuis l'entonnoir.
    - 🧹 Les 68 problèmes SonarCloud ouverts ont été résolus, cinq méthodes refactorisées sous le seuil de complexité cognitive, code mort supprimé, et la suite de tests est passée de 177 à 224 tests.

    🔡 **Traducteurs recherchés.** Les commandes admin ajoutent des messages sous `greenhouses.commands.admin.*`, actuellement en anglais uniquement. Les 24 autres fichiers de locale retombent sur les noms de clés jusqu'à ce qu'ils soient traduits.

    🔺 **Trois commandes du joueur ont été supprimées — mais aucune ne fonctionnait.** `InfoCommand`, `ListCommand` et `RecipeCommand` étaient des ébauches non enregistrées avec des corps factices. `InfoCommand` se déclarait même sous le libellé `make`, ce qui serait entré en collision avec la véritable commande make si quelqu'un l'avait un jour activée. Cette page listait auparavant `greenhouses list` et `greenhouses recipe` comme des commandes du joueur fonctionnelles ; elles ne l'étaient pas, et cela a été corrigé. `/is greenhouses` sans argument ouvre toujours l'interface graphique des recettes.

    [Release v1.10.0](https://github.com/BentoBoxWorld/Greenhouses/releases/tag/1.10.0)

??? warning "Nouveautés de la v1.9.6 — les serres qui se chevauchent sont désormais diagnosticables"
    **Publié le :** 2026-07-25

    - 🐛 **Les serres qui se chevauchent sont désormais diagnosticables.** Si deux serres enregistrées se chevauchent, l'une est ignorée au démarrage — mais la ligne de journal ne disait auparavant que `Greenhouse overlaps with another greenhouse. Skipping...`, ce qui ne donnait rien sur quoi agir et se répétait à chaque redémarrage. L'avertissement nomme désormais **les deux** enregistrements avec leur `uniqueId`, recette, propriétaire, monde, emplacement et boîte englobante, et vous indique comment corriger le problème. La ligne de synthèse indique `Loaded 63 greenhouses out of 65 in the database.` et se termine par un décompte du nombre de serres ignorées.
    - 🔺 **L'ordre de chargement des serres est désormais déterministe.** Les serres étaient chargées dans l'ordre renvoyé par la base de données, donc avec deux enregistrements qui se chevauchent, l'un ou l'autre pouvait gagner, et cela pouvait changer d'un redémarrage à l'autre. Elles sont désormais triées par `uniqueId` avant chargement, donc le résultat est stable jusqu'à ce que vous retiriez l'un des enregistrements.
    - ⚙️ **Entrée `SQUID` en double retirée de la recette `OCEAN`** dans `biomes.yml`. Elle était listée deux fois, ce qui déclenche un avertissement de clé en double de SnakeYAML sur les versions de serveur récentes. YAML conserve la dernière occurrence, donc la valeur effective (`20:WATER`) est préservée et l'apparition des mobs est inchangée.

    ⚙️ **Le correctif de `biomes.yml` ne s'applique pas tout seul.** Votre serveur possède déjà son propre `biomes.yml` sur le disque et l'addon ne l'écrasera pas. Si vous voyez un avertissement de clé en double SnakeYAML pour `SQUID`, ouvrez `plugins/BentoBox/addons/Greenhouses/biomes.yml`, trouvez la section `OCEAN`, et supprimez la première des deux lignes `SQUID:`. Les nouvelles installations reçoivent automatiquement le fichier corrigé.

    🔺 **Cette version signale les serres qui se chevauchent mais ne les retire pas.** Les enregistrements ignorés sont volontairement laissés dans la base de données — supprimer silencieusement la serre d'un joueur serait pire qu'un avertissement récurrent. En 1.9.6, vous deviez retirer vous-même l'enregistrement obsolète en utilisant les `uniqueId` désormais affichés dans le journal ; la 1.10.0 ajoute des commandes admin qui le font en jeu.

    [Release v1.9.6](https://github.com/BentoBoxWorld/Greenhouses/releases/tag/1.9.6)

??? note "Nouveautés de la v1.9.5"
    **Publié le :** 2026-06-03

    Une version de correction de bugs axée sur la croissance des plantes et l'interface de recettes. Voir les notes complètes de la [Release v1.9.5](https://github.com/BentoBoxWorld/Greenhouses/releases/tag/1.9.5).

    - 🔡 Correction d'une fuite de couleur dans l'interface : le code couleur rouge de l'entrée de recette du Nether n'était jamais réinitialisé, ce qui rendait rouge le reste du texte du panneau de recettes. Les plantes hautes/doubles (tournesols, lilas, rosiers, etc.) placent désormais correctement leur moitié supérieure.
    - Le lichen lumineux pousse désormais sur les blocs terrestres (par exemple `GLOW_LICHEN: 10:STONE`) au lieu d'être traité comme uniquement sous-marin.
    - La limite `maxmobs` est désormais appliquée à chaque génération, de sorte que les serres ne peuvent plus dépasser le maximum de mobs configuré.
