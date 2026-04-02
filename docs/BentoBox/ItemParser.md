# Analyseur d'Objet BentoBox

Il n'y a pas de bonne façon de définir une pile d'objet à partir des fichiers de configuration.
Puisque chaque objet a des métadonnées différentes qui peuvent être assignées.
Donc BentoBox utilise un format très étrange qui vient des temps ASkyBlock.

## Exemple Rapide

### Traductions d'Objet Minecraft Générique

Depuis BentoBox 2.0.0, vous pouvez utiliser les traductions d'objet Minecraft comme dans la commande give :

    - minecraft:diamond_sword{display:{Lore:["\"A legendary weapon\""]}}
    - minecraft:stone
    - diamond_chestplate{Enchantments:[{id:mending,lvl:1},{id:protection,lvl:4},{id:unbreaking,lvl:3}]}

### Traduction Générale

Par défaut, tous les objets sont traduits au format :

    - [TYPE]<:QUANTITY>

La Quantité n'est pas nécessaire, cependant, si vous la fournissez, vous devez ajouter `:` avant.

Tous les types que vous pouvez trouver ici : [Material](https://hub.spigotmc.org/javadocs/bukkit/org/bukkit/Material.html)

Cependant, il y a quelques exceptions qui ont quelques personnalisations disponibles. Vous pouvez les vérifier ci-dessous.

### Objets Dommageables

Vous pouvez également définir des objets dommageables en suivant ce format :

    - [TYPE]:<DAMAGE_AMOUNT>:<QUANTITY>

Le Montant des Dégâts et la Quantité sont optionnels.

### Potions et Flèches Empoisonnées

Les Potions, Potions de Splash, Potions Flottantes et Flèches Empoisonnées suivent le même motif :

    - [TYPE]:<POTION_TYPE>:QUANTITY

[TYPE] vous pouvez remplacer par POTION, SPLASH_POTION, LINGERING_POTION ou TIPPED_ARROW.
Tous les types de potions que vous pouvez trouver par ce lien : [PotionTypes](https://hub.spigotmc.org/javadocs/spigot/org/bukkit/potion/PotionType.html)

Exemples :

    - POTION:STRENGTH:1 - Créera une potion de splash avec l'effet étendu de force 1.
    - SPLASH_POTION:INSTANT_DAMAGE:2 - Créera 2 potions de splash avec l'effet de dégâts instantanés 2
    - LINGERING_POTION:STRONG_LEAPING:1 - Créera une potion flottante de Saut 2.
    - TIPPED_ARROW:WEAKNESS:1 - Créera une flèche empoisonnée de faiblesse 1.

### Bannières

Les Bannières ont des options d'analyse personnalisées qui suivent le schéma :

    - [color]_BANNER:QUANTITY<:PatternType:DyeColor>

Vous pouvez spécifier autant de motifs que vous le souhaitez, mais ils doivent suivre la séquence donnée, le motif, puis la couleur de teinture.

Vous pouvez trouver tous les types de motif ici : [PatternType](https://hub.spigotmc.org/javadocs/spigot/org/bukkit/block/banner/PatternType.html)

Vous pouvez trouver toutes les couleurs de teinture ici : [DyeColor](https://hub.spigotmc.org/javadocs/spigot/org/bukkit/DyeColor.html)


### Têtes de Joueur

Les Têtes de Joueur ont des options d'analyse personnalisées. Il suit ce schéma :

 - PLAYER_HEAD:<Name|Trimmed UUID|UUID|Texture>:<QUANTITY>

PLAYER_HEAD - indique que l'objet sera une Tête de Joueur.
Dans la partie suivante, vous pouvez spécifier :

    - Nom du Joueur
    - UUID Taillé du Joueur (sans -)
    - UUID du Joueur (avec -)
    - Lien de Texture

À la fin, vous pouvez spécifier le montant des têtes de joueur dans la pile.
Comme exemple : `PLAYER_HEAD:BONNe1704` - donnera 1 tête de joueur avec la peau BONNe1704.

### Données de Modèle Personnalisé

Les données de modèle personnalisé peuvent être ajoutées à toute pile d'objet analysable. Le texte des données de modèle personnalisé peut être ajouté à n'importe quelle partie de la chaîne analysable. Le schéma pour les données de modèle personnalisé :

- `CMD-[number]`

Exemples :

- IRON_INGOT:2:CMD-12345678 => Crée une pile d'objet avec 2 lingots de fer et données de modèle personnalisé `12345678`
- GOLD_INGOT:CMD-12345678 => Crée une pile d'objet avec lingot d'or et données de modèle personnalisé `12345678`
- PLAYER_HEAD:BONNe1704:CMD-12345678 => Crée une pile d'objet avec tête de joueur BONNe1704 et données de modèle personnalisé `12345678`
