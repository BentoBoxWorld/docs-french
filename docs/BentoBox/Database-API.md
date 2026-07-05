# Introduction

BentoBox fournit une API de base de données pour les développeurs pour que vous n'ayez pas à en créer une vous-même. La base de données BentoBox peut être choisie pour stocker les données dans un fichier plat, MySQL, Mongo, SQLite, PostGreSQL, MariaDB, etc. Vous n'avez pas besoin de vous soucier ou de prendre soin de laquelle est utilisée. Remarquez que YAML n'est plus supportée en tant que base de données, cependant elle est utilisée pour les fichiers de configuration via l'API Config.

## Philosophie

Nous avons adopté une approche « NoSQL » à la base de données BentoBox. C'est à dire que nous enregistrons les objets Java sérialisés en tant que blobs JSON dans la base de données. Chaque tableau dans la base de données est assigné pour enregistrer un objet Java spécifique, par ex., îles, joueurs, défis, etc. et chaque entrée dans le tableau est un objet. Les tableaux ont deux colonnes - un ID unique et l'objet JSON. Les bases de données comme PostgreSQL peuvent enregistrer ces objets JSON sous une forme binaire, ce qui les rend gérer cette approche efficacement.

### Comment accéder aux données en dehors de BentoBox ?
La plupart des bases de données supportées, par ex., MySQL, PostgreSQL, etc. supportent les requêtes sur les données JSON directement. Les seules qui ne le font pas sont les fichiers plats, c'est à dire JSON et SQLite. Par conséquent, vous devriez consulter la documentation sur comment faire des requêtes JSON pour votre base de données.

## Comment Faire

Pour enregistrer une classe dans la base de données BentoBox, faites ce qui suit :

1. Créez une classe qui étend DataObject
2. Définissez les champs de la classe
3. Un champ doit être une chaîne appelée **uniqueId**. C'est l'id unique (clé) de l'objet qui sera utilisé par la base de données pour identifier l'objet
5. Exposez chaque champ que vous voulez enregistrer dans la base de données avec une annotation @Expose
6. Assurez-vous que la classe a un [constructeur sans argument](https://en.wikipedia.org/wiki/Nullary_constructor)
7. Créez un getter et un setter pour chaque champ - la plupart des IDEs devraient être capable de faire cela automatiquement

**ATTENTION :** Le nom canonique complet de la classe est utilisé pour créer le tableau dans la base de données, mais la longueur maximale de ce nom ne peut être que de **64 caractères**. Donc quand vous définissez la classe d'objet de données, assurez-vous que le paquet et les noms de classe sont assez courts pour s'adapter. **AUSSI** puisque BentoBox permet aux tableaux de base de données d'avoir un préfixe, assurez-vous que votre nom canonique est moins d'environ 60 caractères au total pour permettre un préfixe.

Pour certains types de champ, en particulier les personnalisés, vous devrez peut-être définir votre propre classe Adapter qui gérera la sérialisation et la désérialisation des données du champ.

## Exemple
```
public class Names implements DataObject {

    @Expose
    private String uniqueId = ""; // nom
    @Expose
    private UUID uuid;

    public Names() {}

    public Names(String name, UUID uuid) {
        this.uniqueId = name;
        this.uuid = uuid;
    }

    @Override
    public String getUniqueId() {
        return uniqueId;
    }

    @Override
    public void setUniqueId(String uniqueId) {
        this.uniqueId = uniqueId;
    }

    /**
     * @return l'uuid
     */
    public UUID getUuid() {
        return uuid;
    }

    /**
     * @param uuid l'uuid à définir
     */
    public void setUuid(UUID uuid) {
        this.uuid = uuid;
    }


}
```

## uniqueID

L'interface DataObject exige que vous surchargiez les méthodes getUniqueId() et setUniqueID(). L'uniqueId est une chaîne qui est utilisée pour identifier l'objet de données dans la base de données. Un uniqueId typique est l'UUID du joueur (converti en String). S'il ne va jamais y avoir qu'un seul objet de base de données, cet uniqueId peut être une constante, par ex., « TopTen ». L'uniqueId seulement besoin d'être unique dans la portée des objets de données du type que vous avez créé. Il n'a pas besoin d'être unique pour tous les objets de données jamais.

# Instanciation de l'objet de base de données

Une fois que vous avez créé l'objet de données, vous devez l'instancier pour l'utiliser. Vous le faites en créant un nouvel objet BSBDatabase avec BSkyBlock comme premier argument et votre classe comme second. Par exemple :

`BSBDatabase<Names> names = new BSBDatabase<>(plugin, Names.class);`

# Sauvegarde de données dans la base de données

Pour écrire des données dans la base de données, faites ce qui suit :

1. Créez une instance de votre objet de base de données, dans cet exemple, la classe Names
2. Mettez des données dedans, soit via le constructeur soit en utilisant les setters
3. Enregistrez-le dans la base de données en utilisant la méthode saveObject()

Par exemple :

`names.saveObject(new Names(user.getName(), user.getUniqueId()));`

Vous pouvez enregistrer plusieurs objets dans la base de données en répétant les appels de la méthode saveObject. Si l'objet a le même uniqueId qu'un objet précédemment enregistré, il sera automatiquement remplacé.

# Chargement de données à partir de la base de données

Il y a deux façons de charger les données - charger des enregistrements spécifiques (objets) par uniqueId, ou charger tous les objets de ce type d'un seul coup.

## Chargement d'un seul objet

Pour cela, vous devez connaître l'uniqueId de l'enregistrement que vous voulez. Puis utilisez la méthode loadObject avec l'uniqueId comme argument. Par exemple :

`Names loadedName = names.loadObject("tastybento");`

Si vous savez quelles données vous voulez à partir de l'objet chargé et que vous êtes sûr qu'il existe, vous pouvez l'obtenir directement :

`UUID uuid = names.loadObject(string).getUuid();`

## Chargement de tous les objets

Parfois, vous avez besoin de charger toute la base de données dans la mémoire pour pouvoir y accéder tout le temps. Essayez de ne pas le faire à moins que vous n'en ayez besoin. Pour charger tous les objets, utilisez la méthode loadObjects(). Cela les chargera tous comme une Liste. Par exemple :

`List<UUID> uuids = names.loadObjects();`

Remarquez que charger à partir d'une base de données peut prendre longtemps et donc ne devrait pas être fait sur le thread principal pendant le jeu. Vous devriez être capable de charger les objets dans un thread async.

# Vérification de l'existence d'un objet dans la base de données

Pour vérifier si un objet existe, vous devez avoir son uniqueId. Vérifiez-le comme cet exemple :

`return names.objectExists("tastybento") ? "il existe dans la db" : "qui?";'

Vérifier l'existence d'un objet peut aussi prendre longtemps, donc ne le faites pas sur le thread principal si vous pouvez l'éviter.

# Suppression d'un objet dans la base de données

La suppression d'un objet nécessite que vous connaissiez l'uniqueId. Supprimez les objets comme ceci :

`names.deleteObject("tastybento");`

La méthode enregistrera une erreur dans la console si elle ne peut pas supprimer l'objet, mais sinon elle sera silencieuse.

Actuellement, il n'y a aucun moyen de supprimer tous les objets dans la base de données.

# Fermeture de la base de données

Les connexions à la base de données sont définies pour se fermer automatiquement quand le plugin est désactivé, mais si vous souhaitez fermer explicitement la connexion pour économiser les ressources, utilisez cette méthode :

`names.close()`

Cela libérera l'objet de connexion de la base de données et toutes les ressources JDBC immédiatement au lieu d'attendre qu'elles soient automatiquement libérées.

# Support du type d'objet

*La base de données YAML n'est plus supportée !*
La base de données utilise GSON pour sérialiser l'objet. Cela gère la plupart des types d'objets génériques et toutes les classes Bukkit qui implémentent l'interface [ConfigurationSerializable](https://hub.spigotmc.org/javadocs/spigot/org/bukkit/configuration/serialization/ConfigurationSerializable.html), par exemple :

* World
* Location
* Vector (Vector de Bukkit)
* PotionEffectType
* etc.

Si vous implémentez un objet qui doit être sérialisé et enregistré dans la base de données, il devrait implémenter l'interface [ConfigurationSerializable](https://hub.spigotmc.org/javadocs/spigot/org/bukkit/configuration/serialization/ConfigurationSerializable.html) de Bukkit.
