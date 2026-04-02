# API de Configuration BentoBox

Ceci est une API optionnelle qui améliore l'API de configuration Bukkit pour les fichiers YAML. L'API de Configuration BentoBox ajoute les fonctionnalités suivantes :

1. Le fichier de configuration peut conserver les commentaires même après la sauvegarde
2. Le fichier de configuration peut être mis à jour avec de nouveaux paramètres quand vous mettez à jour votre complément
3. La classe de configuration est aussi l'endroit où vous allez pour obtenir et définir les paramètres

Si vous ne voulez pas utiliser cette API, vous pouvez utiliser les méthodes d'API Bukkit standard telles que saveDefaultConfig(), getConfig(), etc.

## Démarrage — un exemple

Disons que nous voulons créer un fichier de configuration pour notre nouveau plugin. Peut-être qu'il ressemblera à ceci :

```yaml
# Ceci est mon fichier config.yml
# C'est pour mon complément

world:
  # Ceci est le nom du monde.
  name: My_world_name
  # Taille - minimum 10, max 100
  size: 100
```

### ConfigObject
Pour utiliser l'API de configuration, nous créons une nouvelle classe qui implémente `ConfigObject` :

```java
public class Settings implements ConfigObject {

}
```

Nous devons maintenant spécifier où cet objet de configuration sera enregistré. L'emplacement est relatif au dossier de données du complément.

```java
@StoreAt(filename="config.yml") // Appelez explicitement le nom que cela devrait avoir.
public class Settings implements ConfigObject {

}
```

### @ConfigEntry
Ensuite, nous devons ajouter les champs de données que nous voulons dans la configuration. Pour cela, nous utilisons l'annotation `@ConfigEntry` :

```java
@StoreAt(filename="config.yml") // Appelez explicitement le nom que cela devrait avoir.
public class Settings implements ConfigObject {
    @ConfigEntry(path = "world.name")
    private String worldName = "My_world_name";

    @ConfigEntry(path = "world.size")
    private int worldSize = 100;
}
```

Remarquez comment les champs ont une valeur par défaut assignée.

### Getters et Setters
Ensuite, nous devons ajouter les getters et setters pour accéder à ces champs. Les noms des getters et setters et les noms des paramètres doivent respecter les [Conventions de Nommage JavaBeans](https://www.oreilly.com/library/view/javaserver-pages-3rd/0596005636/ch20s01s01.html) :

```java
@StoreAt(filename="config.yml") // Appelez explicitement le nom que cela devrait avoir.
public class Settings implements ConfigObject {
    @ConfigEntry(path = "world.name")
    private String worldName = "My_world_name";

    @ConfigEntry(path = "world.size")
    private int worldSize = 100;

    public String getWorldName() {
        return worldName;
    }
    public void setWorldName(String worldName) {
        this.worldName = worldName;
    }
    public int getWorldSize() {
        return worldSize;
    }
    public void setWorldSize(int worldSize) {
        this.worldSize = worldSize;
    }
}
```

### `@ConfigComment`
Ensuite, nous pouvons ajouter des commentaires en utilisant l'annotation `@ConfigComment` :

```java
@StoreAt(filename="config.yml") // Appelez explicitement le nom que cela devrait avoir.
@ConfigComment("Ceci est mon fichier config.yml") // Remarquez que le commentaire sera automatiquement
@ConfigComment("C'est pour mon complément") // procédé avec un # et un espace
public class Settings implements ConfigObject {
    @ConfigEntry(path = "world.name")
    @ConfigComment("Ceci est le nom du monde.")
    private String worldName = "My_world_name";

    @ConfigEntry(path = "world.size")
    @ConfigComment("Taille - minimum 10, max 100")
