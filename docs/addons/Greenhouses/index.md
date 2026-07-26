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

## Plugin requis

Cette version de Greenhouses est un addon pour BentoBox et ne fonctionne pas de manière autonome!

1. BentoBox - assurez-vous d'utiliser la dernière version!

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

- Les identifiants proviennent de `list` et peuvent être abrégés en n'importe quel préfixe ne correspondant qu'à **une seule** serre. Un préfixe ambigu est traité comme une absence de correspondance plutôt que comme une supposition, car la suppression d'une mauvaise serre est irréversible.
- Tout fonctionne depuis la console du serveur, sauf `tp`.
- Les enregistrements de serres qui ne peuvent pas être chargés — chevauchement, recette inconnue, monde absent, aucun emplacement — sont conservés en mémoire avec la raison au lieu d'être silencieusement ignorés. C'est ce qui les rend listables et supprimables.
- Les enregistrements ne sont jamais supprimés automatiquement. Retirer la serre d'un joueur sans qu'on le demande serait pire qu'un avertissement récurrent.

!!! tip "Serres qui se chevauchent"
    Si deux serres enregistrées se chevauchent, l'une est ignorée au démarrage et nommée dans le journal, avec l'enregistrement qu'elle chevauche. Utilisez `/bsbadmin greenhouses list` pour voir les enregistrements ignorés et pourquoi, puis `/bsbadmin greenhouses delete <id>` pour retirer celui que vous ne voulez pas. Aucune modification de base de données et aucun redémarrage nécessaires.

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

Depuis la 1.10.0, chaque sous-commande admin possède également son propre nœud — `greenhouses.admin.list`, `.info`, `.delete`, `.tp`, `.verify` et `.reload` — tous avec `op` par défaut. Les opérateurs n'ont rien à faire, mais si vous accordez l'accès admin via un plugin de permissions, vous voudrez les ajouter. Ils étaient totalement absents de `addon.yml` avant cette version, ce qui explique pourquoi seul l'accès op fonctionnait.

## Traductions

{{ translations("Greenhouses") }}

!!! note "Nouveautés de la v1.10.0 — commandes admin"
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
