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
