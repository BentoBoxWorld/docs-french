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

Ajoutez ces commandes à /island, /ai:

* **greenhouses help** - répertorie ces commandes
* **greenhouses make**: Essaie de créer une serre en trouvant la première recette valide
* **greenhouses remove**: Supprime une serre dans laquelle vous vous tenez si vous êtes le propriétaire
* **greenhouses list**: Répertorie toutes les recettes disponibles
* **greenhouses recipe**: Affiche l'interface graphique de recette - cliquer sur une recette essayera de créer une serre

## Commandes Admin

Utilisez après la commande admin du mode de jeu, par exemple /bsb ou /acid

* **greenhouses reload** : Recharge les fichiers de configuration
* **greenhouses info <player>**: fournit des informations sur les serres de l'île du joueur
* **greenhouses info**: fournit des informations sur la serre dans laquelle vous êtes

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

## Traductions

{{ translations("Greenhouses") }}
