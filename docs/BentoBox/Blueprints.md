# Blueprints
Les **Blueprints** sont un moyen simple et rapide de faire vos propres îles de démarrage personnalisées dans le jeu.

Les Blueprints *ressemblent à* les schematics WorldEdit mais ne sont **pas** compatibles. Les Blueprints sont optimisés pour les compléments BentoBox et ne nécessitent aucun autre plugin ou bibliothèque à utiliser.

Les Blueprints sont gérés avec le **Gestionnaire de Blueprint** et peuvent être regroupés dans un **Bundle de Blueprint** pour contenir un ensemble de jusqu'à 3 îles pour chaque dimension - monde normal, monde nether et monde end. Les Bundles de Blueprint ont leur propre icône, description et peuvent contenir d'autres paramètres, comme exiger la permission d'utilisation.

### FAQ : J'ai beaucoup de schematics - comment les convertir en Blueprints ?

C'est assez facile, mais vous devez le faire en jeu car vous devrez ajouter des panneaux.

Étapes :

1. Chargez le schematic en utilisant WorldEdit
2. Collez-le quelque part, je recommande un espace dans le monde BSKyBlock loin de tout
3. Trouvez où vous voulez que le joueur apparaisse et placez un panneau là-bas avec le texte [spawn_here] dessus.
4. (Optionnel) Placez un panneau de bienvenue faisant face à l'endroit qui a le texte [start] dessus. Pour les détails sur ces panneaux, regardez ci-dessous
5. Sélectionnez l'île en utilisant les commandes de positionnement administrateur blueprint pos1 et pos2 (Souvenez-vous d'utiliser la commande blueprint et pas WE !)
6. Copiez l'île en utilisant la commande de copie administrative blueprint
7. Enregistrez l'île en utilisant la commande de sauvegarde administrative blueprint
8. Répétez pour toutes vos îles y compris les îles Nether et End.

Conseils : Assurez-vous d'avoir un bloc de bedrock au centre de l'île. C'est où l'île sera centrée.

## Asynchrone
Tous les copies et collages de Blueprint sont faits async et ne devraient **jamais** décaler le serveur peu importe la taille du Blueprint. Cela peut prendre plusieurs secondes pour coller de très grands Blueprints. Vous pouvez définir combien de blocs seront copiés ou collés en éditant la vitesse de collage dans le config.yml BentoBox. La valeur par défaut devrait être acceptable pour la plupart des systèmes. Si vous exécutez les timings, vous pouvez voir le processus de collage prendre longtemps, mais il ne fait que des blocs d'environ 1000 par tick et ne devrait pas décaler votre système.

## Opération
Le flux de base pour faire une île personnalisée :

1. Créez une boîte de délimitation en définissant deux positions aux coins opposés de la boîte - définissez pos1 et pos2
2. Copiez le contenu de la boîte dans le presse-papiers
3. Enregistrez le contenu. Si vous voulez juste remplacer les îles par défaut, enregistrez comme « island », « nether-island » ou « end-island » - on vous demandera de confirmer le remplacement.
4. Ouvrez le Gestionnaire de Blueprint, par ex., /bsb blueprint pour faire un nouveau Bundle, définir les icônes, regrouper les Blueprints, etc.

### Vidéo
*Cliquez sur la vignette !*
[![vignette](https://user-images.githubusercontent.com/20014332/62939503-be4c5980-bdd1-11e9-8814-2253845cecd0.png)](https://youtu.be/4gvaG89uxAs)

## Commandes
Les commandes sont presque les mêmes que les commandes de schematic WorldEdit. Vous devez être Op ou un administrateur avec des permissions pour utiliser les blueprints. Utilisez la commande administrative et **blueprint** ou son alias **bp** :

* /bsb bp pos1 - définissez un coin de la boîte de délimitation à la position de votre joueur
* /bsb bp pos2 - définissez l'autre coin
* /bsb bp copy - copiez les blocs et les entités à l'intérieur de la boîte dans le presse-papiers
* /bsb bp copy air - copiez les blocs, les entités et l'air à l'intérieur de la boîte dans le presse-papiers. C'est important si vous prévoyez de coller l'île dans l'eau (AcidIsland) ou la roche (CaveBlock).
* /bsb bp paste - collez le presse-papiers à votre emplacement
* /bsb bp save <name> - enregistre le presse-papiers dans un fichier (sauvegardé en tant que fichier `.blueprint` JSON brut)
* /bsb bp load <name> - chargez un fichier blueprint (n'ajoutez pas le suffixe `.blueprint` ou `.blu`)
* /bsb bp - ouvrez l'Interface Graphique du Gestionnaire de Blueprint

Pour AcidIsland, utilisez /acid à la place de /bsb.

## Interface Graphique du Gestionnaire de Blueprint
L'Interface Graphique du Gestionnaire de Blueprint vous permet de créer, éditer et configurer les ensembles d'îles que les joueurs peuvent sélectionner quand ils commencent une nouvelle île ou réinitialisent. Les ensembles d'îles (monde normal, monde nether et monde end) s'appellent « bundles ». Il y a un bundle par défaut qui peut être personnalisé, mais ne peut pas être supprimé.

Pour créer un nouveau bundle, cliquez sur la bannière verte dans le coin inférieur gauche de l'Interface Graphique. L'entrée de texte se fait via l'interface de discussion. Entrez un nom pour le nouveau bundle. Vous pouvez le changer plus tard.

Le nouveau bundle aura une icône de laine rouge par défaut et un nom. Il a trois emplacements à droite qui représentent les endroits où vous pouvez mettre 3 blueprints :

* Panneau de verre vert - c'est l'emplacement du blueprint du monde normal
* Panneau de verre rouge - c'est l'emplacement du blueprint du monde nether
* Panneau de verre jaune - c'est l'emplacement du blueprint du monde end

Cliquez avec le bouton droit sur ces emplacements pour les effacer.

Sous la ligne de panneaux de verre gris foncé, vous verrez un certain nombre de blueprints à choisir. Cliquez sur celui que vous voulez et il brillera. Ensuite, cliquez sur l'emplacement où vous voulez le mettre. Vous pouvez mettre le même blueprint dans les trois emplacements ou avoir des blueprints différents pour chacun, c'est à vous de décider.

Pour ajouter une description au bundle, cliquez avec le bouton droit sur l'icône du bundle et entrez une description dans le chat. Gardez chaque ligne courte pour que l'Interface Graphique ne devienne pas trop grande. Vous pouvez définir la couleur du texte en utilisant les codes de couleur Bukkit, comme &c pour rouge.

Pour changer l'icône d'un bundle, cliquez sur un objet dans votre inventaire et il remplacera l'icône du bundle. Pour changer l'icône d'un blueprint, sélectionnez le blueprint, puis cliquez sur l'objet d'inventaire.

Pour limiter un bundle aux joueurs avec la permission appropriée, cliquez sur l'objet image pour basculer si la permission est requise ou non. L'icône affichera quelle permission est requise dans son texte (elle est basée sur le nom du bundle). La permission est `GameModeAddonName.island.create.uniqueId` du bundle de blueprint. par exemple `bskyblock.island.create.vip`.

Pour supprimer un bundle, cliquez avec le bouton droit sur le TNT.

Les Bundles et les Blueprints doivent être renommés dans l'Interface Graphique. N'essayez pas de les renommer en utilisant le système de fichiers.

## Fichiers et Édition
Quand vous utilisez des blueprints dans le jeu, utilisez toujours juste le nom du blueprint. Sur le système de fichiers, les blueprints sont désormais enregistrés en tant que **fichiers texte JSON brut** avec le suffixe `.blueprint`. Les bundles de blueprint sont également enregistrés en tant que fichiers texte `.json`. Les fichiers `.blueprint` et les bundles `.json` peuvent être édités avec n'importe quel éditeur de texte.

!!! note "Anciens fichiers `.blu`"
    Les fichiers Blueprint utilisaient auparavant un format binaire compressé `.blu`. BentoBox chargera automatiquement les anciens fichiers `.blu` pour la compatibilité ascendante, mais tous les nouveaux blueprints sont sauvegardés au format `.blueprint` (JSON brut). Vous pouvez versionner et comparer les fichiers `.blueprint` normalement. N'essayez pas de créer ou d'éditer des fichiers `.blu` à la main.

## Bundles Incomplets
Les Bundles doivent toujours avoir un blueprint du monde Overworld/Normal. S'ils ne l'ont pas, le blueprint d'île par défaut sera utilisé et une erreur sera enregistrée dans la console.
Les Bundles ne doivent pas avoir de blueprints du monde Nether ou End, mais s'ils ne l'ont pas, aucune île ne sera collée dans ces mondes (évidemment).

## Entités

!!! new "À venir dans BentoBox 1.14.0"
    Dans cette prochaine version, vous pourrez également utiliser `[name]`, qui sera remplacé par le nom du propriétaire de l'île lors de la création de l'île.

Vous pouvez utiliser des placeholders dans les noms des entités.
Renommez une étiquette de nom avec le placeholder dans une enclume, puis appliquez l'étiquette de nom à l'entité.

## Panneaux
Les Blueprints peuvent avoir deux panneaux spéciaux pour vous aider à placer où un joueur apparaîtra et pour leur donner un message de bienvenue.

### Panneau Apparaître Ici
Placez un panneau avec la première ligne comme [spawn_here] (en anglais) où vous voulez que le joueur apparaisse. Il apparaîtra à cette position et le panneau ne sera pas collé. Cela s'applique à toutes les îles mondes, pour que vous puissiez spécifier où les joueurs apparaîtront dans le Nether quand ils passent par un portail, par exemple.

### Panneau de Bienvenue
Le panneau de bienvenue offre un moyen convivial de donner aux joueurs un conseil sur le jeu et ce qu'ils peuvent faire, ou ne pas faire ! Placez un panneau avec [start] (en anglais) sur la première ligne. Le texte du panneau sera remplacé par le texte du panneau dans le fichier de localisation du GameModeAddon.

## Conseils et Recommandations
* Nous recommandons de garder les îles de démarrage petites pour rendre le jeu un défi. Mettez juste assez d'objets et de blocs sur une île pour que les joueurs puissent développer leur île.
* Essayez de faire des îles divisées (pensez haut et bas, côté à côté) pour donner aux joueurs une cible à construire quand ils ont les ressources.
* Si vous copiez avec l'air, essayez de faire votre boîte de délimitation aussi petite que possible pour garder la taille du fichier petite.
* Après avoir copié un blueprint, essayez de le coller pour vérifier qu'il a été copié correctement. Puis enregistrez-le.
