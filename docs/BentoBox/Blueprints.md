# Îles de Démarrage (Blueprints) { #starter-islands-blueprints }

Quand un joueur crée une île, BentoBox colle une île de démarrage pour lui. Ces îles de démarrage sont des **blueprints**, que vous construisez et sauvegardez en jeu. Un **bundle** groupe un blueprint Overworld, Nether et End en un seul choix dans le menu Créer une Île, avec sa propre icône, nom et description.

Chaque mode de jeu est livré avec quelques bundles. Vous pouvez les modifier, ajouter les vôtres, offrir des îles VIP uniquement, les facturer, et exécuter des commandes quand l'une est choisie.

!!! info "Commandes sur cette page"
    Les commandes sont affichées pour BSkyBlock (`/bsbadmin`). Utilisez la commande d'administration de votre mode de jeu à la place, par exemple `/oba` pour AOneBlock ou `/acid` pour AcidIsland. `blueprint` peut être raccourci à `bp`.

## Créer une île de démarrage { #make-a-starter-island }

1. **Construisez-la.** Construisez l'île quelque part dans le monde du mode de jeu, loin des autres îles. Mettez au moins un bloc de **bedrock** dedans : le bloc de bedrock le plus élevé devient le centre de l'île, et BentoBox n'enregistrera pas un blueprint sans un.
2. **Ajouter les panneaux (optionnel).** Placez une pancarte avec `[spawn_here]` sur la première ligne où les joueurs doivent apparaître, face à la direction qu'ils doivent regarder. Ajoutez une pancarte avec `[start]` sur la première ligne pour un message de bienvenue. Voir [Panneaux](#signs).
3. **Sélectionnez-la.** Tenez-vous à un coin et exécutez `/bsbadmin bp pos1`, puis au coin opposé `/bsbadmin bp pos2`. Utilisez ceux-ci, pas la sélection de WorldEdit.
4. **Copiez-la.** `/bsbadmin bp copy`. Ajoutez `air` si l'île sera collée dans l'eau ou la pierre (AcidIsland, CaveBlock, Poseidon), ainsi l'air autour est aussi collé. Ajoutez `biome` pour garder les biomes, ou `nowater` pour laisser de côté les blocs d'eau.
5. **Vérifiez-la.** Allez quelque part vide et exécutez `/bsbadmin bp paste` pour voir ce que vous avez copié.
6. **Enregistrez-la.** `/bsbadmin bp save <name>`, par exemple `/bsbadmin bp save vip_island`.
7. **Offrez-la aux joueurs.** Ouvrez `/bsbadmin bp` et mettez le blueprint dans un bundle (section suivante).

Pour remplacer l'île par défaut du mode de jeu au lieu d'en ajouter une nouvelle, enregistrez-la sur son blueprint (généralement `island`, `nether-island` et `end-island`). On vous demandera de confirmer.

!!! tip "Gardez-la petite"
    Le plaisir des modes de jeu d'îles est de grandir à partir de très peu. Commencez les joueurs avec juste assez de blocs et d'objets pour commencer.

**Conversion de schematics WorldEdit :** les blueprints ne sont pas des schematics, mais vous pouvez coller un schematic avec WorldEdit, ajouter le bedrock et les panneaux, puis sélectionner, copier et enregistrer avec les commandes blueprint comme ci-dessus. Faites ceci pour chaque île Nether et End aussi.

## Bundles : les choix du menu Créer une Île { #bundles-the-choices-in-the-create-island-menu }

Ouvrez le Gestionnaire de Blueprint avec **`/bsbadmin bp`**. Il liste les bundles ; cliquez sur un pour le modifier.

| Pour… | Faites ceci |
|---|---|
| Créer un bundle | Cliquez sur la bannière verte, puis tapez un nom dans le chat |
| Mettez un blueprint dans un bundle | Cliquez sur un blueprint en bas pour qu'il brille, puis cliquez sur l'emplacement vert (Overworld), rouge (Nether) ou jaune (End) |
| Videz un emplacement | Clic droit dessus |
| Changez l'icône du bundle | Cliquez sur un objet de votre propre inventaire |
| Renommez-le | Clic droit sur le bundle dans la liste principale, puis tapez le nom dans le chat |
| Changez la description | À l'intérieur du bundle, cliquez sur son icône (en haut à gauche), puis tapez dans le chat. Les codes de couleur comme `&c` fonctionnent |
| Choisissez où il apparaît dans le menu | Clic gauche sur l'icône d'emplacement pour le déplacer plus tard, clic droit pour le déplacer plus tôt |
| Rendez-le VIP uniquement | Cliquez sur la peinture pour exiger une permission. La permission est affichée sur l'icône, par exemple `bskyblock.island.create.vip_island` |
| Facturez-le | Cliquez sur l'lingot d'or : clic gauche/droit ajoute/supprime 1, clic maj 100. Nécessite Vault et un plugin économique |
| Exécutez des commandes quand c'est choisi | Cliquez sur le bloc de commande et tapez des commandes dans le chat |
| Limitez le nombre de fois qu'un joueur peut le choisir | Cliquez sur l'horloge. Uniquement affiché quand les joueurs peuvent posséder plus d'une île |
| Supprimez-le | Clic droit sur le TNT |

Chaque mode de jeu a un bundle appelé `default`, qui ne peut pas être supprimé. Il est utilisé quand un joueur ne choisit pas (par exemple quand les îles sont créées automatiquement à la première connexion).

Un bundle **doit** avoir un blueprint Overworld ; s'il n'en a pas, l'île par défaut est utilisée et une erreur est enregistrée. Les blueprints Nether et End sont optionnels ; sans eux, rien n'est collé dans ces mondes.

**Renommez les bundles et blueprints dans le gestionnaire ou avec `/bsbadmin bp rename`**, pas en renommant des fichiers.

### Commandes quand un bundle est choisi { #commands-when-a-bundle-is-chosen }

Les commandes s'exécutent chaque fois qu'une île est créée avec le bundle, par exemple pour donner un kit de démarrage ou définir un rang. `[player]` et `[owner]` sont remplacés par le nom du joueur. Les commandes s'exécutent depuis la console sauf si elles commencent par `[SUDO]`, qui les exécute en tant que joueur :

```
lp user [player] parent add skyblock-starter
[SUDO] kit starter
```

### Facturer un bundle { #charging-for-a-bundle }

Définissez un coût sur le bundle avec l'lingot d'or. Le joueur paie quand il crée ou réinitialise une île avec, et ne peut pas le choisir s'il n'a pas les moyens. Cela nécessite `use-economy: true` dans le `config.yml` de BentoBox et Vault avec un plugin économique ; sans eux l'lingot d'or n'est pas affiché.

## Panneaux { #signs }

| Première ligne de la pancarte | Ce qui se passe |
|---|---|
| `[spawn_here]` | Les joueurs apparaissent à cet endroit, face à la direction que la pancarte regarde. La pancarte est supprimée. Fonctionne dans les blueprints Nether et End aussi |
| `[start]` | Remplacé par le texte de bienvenue du fichier de locale du mode de jeu (`bskyblock.sign.line0` à `line3`), dans la langue du propriétaire. `[name]` dans ce texte devient le nom du propriétaire |
| N'importe quoi d'autre | Collé tel que écrit |

**Mobs nommés :** renommez une balise de nom pour inclure `[name]` dans une enclume et mettez-la sur un mob dans votre île avant de copier. Le mob est nommé d'après le propriétaire de l'île quand l'île est collée.

## Toutes les commandes blueprint { #all-blueprint-commands }

| Commande | Ce qu'elle fait |
|---|---|
| `/bsbadmin bp` | Ouvrir le Gestionnaire de Blueprint |
| `/bsbadmin bp pos1`, `pos2` | Définissez les coins de la zone à copier |
| `/bsbadmin bp copy [air] [biome] [nowater]` | Copiez la zone dans votre presse-papiers |
| `/bsbadmin bp origin` | Définissez l'origine du collage sur le bloc auquel vous regardez |
| `/bsbadmin bp paste` | Collez votre presse-papiers où vous vous tenez |
| `/bsbadmin bp save <name>` | Enregistrez votre presse-papiers comme un blueprint |
| `/bsbadmin bp load <name>` | Chargez un blueprint dans votre presse-papiers pour le modifier |
| `/bsbadmin bp list` | Listez les blueprints |
| `/bsbadmin bp rename <name> <new name>` | Renommez un blueprint |
| `/bsbadmin bp delete <name>` | Supprimez un blueprint |
| `/bsbadmin bp sink` | Basculez si ce blueprint s'enfonce au fond de la mer quand collé |

## Les fichiers { #the-files }

Les blueprints et bundles sont stockés par mode de jeu dans `plugins/BentoBox/addons/<GameMode>/blueprints/` :

- `<name>.blueprint` : un blueprint, en JSON simple. Les anciens fichiers `.blu` (compressés) se chargent toujours.
- `<bundle>.json` : un bundle, en JSON simple.

Vous pouvez copier ces fichiers entre serveurs, les garder sous contrôle de version, ou les modifier. Pour chaque champ, voir [Format de Fichier Blueprint](Blueprint-Format.md).

## Vitesse de collage { #pasting-speed }

La copie et le collage se produisent un peu à la fois, donc les grandes îles ne gèlent pas le serveur ; une grande île peut prendre quelques secondes. Si la création d'îles cause du lag, baissez `paste-speed` (blocs par tick) dans le `config.yml` de BentoBox.

## Dépannage { #troubleshooting }

**« Au moins un bloc de bedrock doit être dans un blueprint ! »**
Ajoutez un bloc de bedrock à l'île, copiez à nouveau, puis enregistrez.

**Les joueurs apparaissent au mauvais endroit, ou tombent.**
Ajoutez une pancarte `[spawn_here]`, avec de l'air au-dessus pour le joueur.

**L'île est entourée de lacunes d'eau (ou de pierre) qui ne devraient pas être là**, ou l'eau du monde s'écoule dedans.
Copiez avec `air` afin que l'espace autour de l'île fasse partie du blueprint. Gardez la sélection serrée, car l'air rend le fichier plus grand.

**Mon nouveau bundle ne s'affiche pas dans le menu Créer une Île.**
Vérifiez qu'il a un blueprint Overworld, qu'il n'exige pas une permission que le joueur n'a pas, et, s'il a une limite d'utilisation, que le joueur ne l'a pas épuisée. Avec `hide-used-blueprints: true` dans le `config.yml` de BentoBox, les bundles utilisés sont masqués.

**La pancarte de bienvenue affiche `[start]`.**
Le texte `[start]` vient du fichier de locale du mode de jeu. Vérifiez que `<gamemode>.sign.line0` à `line3` existent dedans.

## Voir aussi { #see-also }

- [Îles](About/IslandManagement.md) : création, réinitialisation et dimensionnement des îles
- [Agrandir le menu de création d'île](../Tutorials/generic/Bigger-Create-Island-Menu.md) et [Personnalisation des Menus](../Tutorials/generic/Customizable-GUI.md) : le menu que les joueurs choisissent
- [Format de Fichier Blueprint](Blueprint-Format.md) : pour éditer les fichiers
