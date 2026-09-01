# Introduction

BentoBox repose sur **_les Addons_ pour fournir de nouvelles fonctionnalités ou de nouveaux _Modes de jeu_**.
Ce tutoriel vous guidera à travers le processus de **création de votre premier addon**.

Créer un Addon est souvent plus facile et plus rapide que de créer un addon à partir de zéro, car BentoBox fournit des [wrappers](https://en.wikipedia.org/wiki/Wrapper_function) et des fonctionnalités clés de l'API.
Les Addons ont également accès direct à l'API des autres addons, contrairement aux plugins, en raison du [principe de visibilité des chargeurs de classes Java](https://www.javatpoint.com/classloader-in-java).
De plus, ils ont accès à l'[API Config](../../BentoBox/Config-API.md) et l'[API Base de données](../../BentoBox/Database-API.md) de BentoBox.

Pour suivre confortablement ce tutoriel, vous devez avoir une expérience antérieure en développement d'addons.
Le processus de développement d'addons est en effet très similaire à ce dernier, et nous supposerons tout au long de ce tutoriel que vous compreniez les concepts clés de Java, par souci de concision.

# Préparer le projet

## Utiliser le modèle Addon préfait

Le modèle n'existe actuellement pas.

## Création manuelle du projet

### Importer BentoBox comme dépendance

BentoBox contient toute l'API dont vous aurez besoin pour créer et enregistrer votre addon.
Par conséquent, vous devez l'ajouter en tant que dépendance de votre projet.

BentoBox utilise Maven et notre dépôt Maven est gentiment fourni par [CodeMC](https://codemc.org/).
Cependant, vous pouvez également utiliser Gradle pour récupérer BentoBox.

#### Maven

Ajoutez ce qui suit à votre fichier `pom.xml`.

```xml
<repositories>
  <repository>
    <id>codemc-repo</id>
    <url>https://repo.codemc.io/repository/bentoboxworld/</url>
  </repository>
</repositories>

<dependencies>
  <dependency>
    <groupId>world.bentobox</groupId>
    <artifactId>bentobox</artifactId>
    <version>PUT-VERSION-HERE</version>
    <scope>provided</scope>
  </dependency>
</dependencies>
```

#### Gradle

Ajoutez ce qui suit à votre fichier `build.gradle`.

```groovy
repositories {
  maven { url "https://repo.codemc.io/repository/bentoboxworld/" }
}

dependencies {
  compileOnly 'world.bentobox:bentobox:PUT-VERSION-HERE'
}
```

Si vous avez des problèmes, veuillez consulter la [documentation de Gradle sur la déclaration des dépendances](https://docs.gradle.org/current/userguide/declaring_dependencies.html).

### Configurer l'architecture du projet

# Créer la classe Addon principale

La **classe principale d'un Addon** fonctionne de la même manière que celle d'un addon.
Elle gère notamment le code qui s'exécute lors du chargement, de l'activation, du rechargement et de la désactivation de l'addon.

La classe principale **étend `Addon`**.

*Exemple :*
```java
import world.bentobox.bentobox.api.addons.Addon;

public class MyAddon extends Addon {

}
```

!!! tip
    Lors de la dénomination de votre classe principale, prenez en compte les points suivants :
    Nous vous recommandons de garder son nom aussi proche que possible du nom de l'addon.
    Vous pouvez également ajouter « Addon » au nom de la classe pour mieux lever l'ambiguïté sur son objectif.

*Exemples authentiques* : [Greenhouses](https://github.com/BentoBoxWorld/Greenhouses/blob/develop/src/main/java/world/bentobox/greenhouses/Greenhouses.java),
[Chat](https://github.com/BentoBoxWorld/Chat/blob/develop/src/main/java/world/bentobox/chat/Chat.java),
[Biomes](https://github.com/BentoBoxWorld/Biomes/blob/develop/src/main/java/world/bentobox/biomes/BiomesAddon.java).

## Méthodes obligatoires

Comme les plugins Bukkit, les Addons doivent remplacer quelques méthodes pour être correctement activés.

En tant que tel, votre classe Addon principale devrait ressembler à ceci :

```java
import world.bentobox.bentobox.api.addons.Addon;

public class MyAddon extends Addon {
    @Override
    public void onEnable() {}

    @Override
    public void onDisable() {}
}
```

### onEnable()

Cette méthode est appelée après `#onLoad()`.

### onDisable()

Cette méthode est appelée lors de la désactivation de l'Addon, ce qui se produit généralement à l'arrêt du serveur.

## Méthodes optionnelles

D'autres méthodes peuvent être remplacées si nécessaire.

```java
import world.bentobox.bentobox.api.addons.Addon;

public class MyAddon extends Addon {
    @Override
    public void onLoad() {}

    @Override
    public void onEnable() {}

    @Override
    public void onReload() {}

    @Override
    public void onDisable() {}
}
```

### onLoad()
Le code dans la méthode onLoad() s'exécute lorsque l'Addon est chargé et avant onEnable(). C'est un bon endroit pour charger les configurations et configurer les commandes si cet addon est un mode de jeu :
```
    @Override
    public void onLoad() {
        // Enregistrez la configuration par défaut à partir de config.yml
        saveDefaultConfig();
        // Charger les paramètres à partir de config.yml. Cela vérifiera aussi s'il y a des problèmes.
        loadSettings();
        // Enregistrer les commandes du mode de jeu
        playerCommand = new DefaultPlayerCommand(this)

        {
            @Override
            public void setup()
            {
                super.setup();
                new IslandAboutCommand(this);
            }
        };
        adminCommand = new DefaultAdminCommand(this) {};
    }
```

### onReload()
Le code dans cette méthode s'exécute lorsque (ou si) l'administrateur recharge les Addons en utilisant la commande `bbox reload`.

# Créer le addon.yml
Le addon.yml est requis pour décrire votre addon à BentoBox. C'est presque identique à plugin.yml utilisé par Bukkit. Voici un exemple minimal :

```
name: Bank
main: world.bentobox.bank.Bank
version: 1.0.0
api-version: 1.15.4
authors: tastybento
```
Les balises ci-dessus sont obligatoires et doivent être incluses dans chaque addon.yml.<br>

<table cellspacing="0" cellpadding="4" border="1">
   <caption>Attributs addon.yml
   </caption>
   <tbody>
       <tr>
           <th>Attribut
           </th>
           <th>Requis
           </th>
           <th>Description
           </th>
           <th>Exemple
           </th>
           <th>Notes
           </th>
       </tr>
       <tr style="font-weight: bold;">
           <td>name
           </td>
           <td>oui
           </td>
           <td>Le nom de votre addon.
           </td>
           <td>
               <code>name: MyAddon</code>
           </td>
           <td>
               <ul>
                   <li>Caractères alphanumériques et traits de soulignement (a-z,A-Z,0-9, _)</li>
                   <li>Utilisé pour déterminer le nom du dossier de données de l'addon. Les dossiers de données sont placés dans le répertoire ./addons/ par défaut.</li>
                   <li>C'est une bonne pratique de nommer votre jar de la même manière, par exemple « Bank.jar »</li>
               </ul>
           </td>
       </tr>
       <tr style="font-weight: bold;">
           <td>version
           </td>
           <td>oui
           </td>
           <td>La version de cet addon.
           </td>
           <td>
               <code>version: 1.3.1</code>
           </td>
           <td>
               <ul>
                   <li>La version est une chaîne arbitraire, mais le format le plus courant est MajorRelease.MinorRelease.Build (par exemple : 1.4.1).</li>
                   <li>Généralement, vous l'incrémenterez à chaque fois que vous lancez une nouvelle fonctionnalité ou une correction de bug.</li>
                   <li>
                       Affiché quand un utilisateur tape
                       <code>/bbox version</code>
                   </li>
               </ul>
           </td>
       </tr>
       <tr>
           <td>description
           </td>
           <td>non
           </td>
           <td>Description conviviale de la fonctionnalité fournie par votre addon.
           </td>
           <td>
               <code>description: This addon is so boxy.</code>
           </td>
           <td>
               <ul>
                   <li>La description peut avoir plusieurs lignes.</li>
                   <li>
                       Affiché quand un utilisateur tape
                       <code>/version addonName</code>
                   </li>
               </ul>
           </td>
       </tr>
       <tr>
           <td>authors
           </td>
           <td>oui
           </td>
           <td>Vous permet de lister un ou plusieurs auteurs, s'il s'agit d'un projet collaboratif. Si vous en listez plus d'un, utilisez un format de liste de chaînes YAML.
           C'est effectivement un élément obligatoire.
           </td>
           <td>
<code>authors:
- BONNe
- tastybento</code><br>
ou<br>
<code>authors: tastybento</code>
           </td>
           <td>
               <ul>
                   <li>Vous pouvez lister un auteur ou plusieurs auteurs.</li>
               </ul>
           </td>
       </tr>
       <tr style="font-weight: bold;">
           <td>main
           </td>
           <td>oui
           </td>
           <td>Pointe vers la classe qui étend Addon ou Pladdon
           </td>
           <td>
               <code>main: world.bentobox.acidisland.AcidIsland</code>
           </td>
           <td>
               <ul>
                   <li>Notez que cela doit contenir l'espace de noms complet, y compris le fichier de classe lui-même.</li>
                   <li>
                       Si votre espace de noms est
                       <code>world.bentobox.addon</code>
                       , et votre fichier de classe est appelé
                       <code>Myaddon</code>
                        alors cela doit être
                       <code>world.bentobox.addon.Myaddon</code>
                   </li>
               </ul>
           </td>
       </tr>
       <tr>
           <td>depend
           </td>
           <td>non
           </td>
           <td>Une liste d'addons que votre addon doit charger.
           </td>
           <td>
               <code>depend: Oneaddon, Anotheraddon</code>
           </td>
           <td>
               <ul>
                   <li>
                       La valeur est délimitée par des virgules
                   </li>
                   <li>Utilisez l'attribut « name » de l'addon requis pour spécifier la dépendance.</li>
                   <li>Si un addon listé ici n'est pas trouvé, votre addon échouera au chargement.</li>
                   <li>Si plusieurs addons se listent mutuellement comme dépendance, de sorte qu'il n'y ait pas d'addons sans une dépendance non chargeable, tous échoueront au chargement.</li>
               </ul>
           </td>
       </tr>
       <tr>
           <td>softdepend
           </td>
           <td>non
           </td>
           <td>Une liste d'addons que votre addon peut nécessiter mais qui ne sont pas obligatoires.
           </td>
           <td>
               <code>softdepend: AcidIsland, BSkyBlock, SkyGrid, CaveBock, AOneBlock</code>
           </td>
           <td>
               <ul>
                   <li>
                       La valeur est délimitée par des virgules.
                   </li>
                   <li>Utilisez l'attribut « name » de l'addon souhaité pour spécifier la dépendance.</li>
                   <li>Votre addon se chargera après tous les plugins listés ici.</li>
                   <li>Les dépendances logicielles circulaires sont chargées arbitrairement.</li>
               </ul>
           </td>
       </tr>
       <tr>
           <td>permissions
           </td>
           <td>non
           </td>
           <td>Permissions que l'addon souhaite enregistrer. Chaque nœud représente une permission à enregistrer. Chaque permission peut avoir des attributs supplémentaires.
           </td>
           <td>
               <pre>permissions:
  '[gamemode].intopten':
    description: Player is in the top ten.
    default: true
  '[gamemode].island.level':
    description: Player can use level command
    default: true
  '[gamemode].island.top':
    description: Player can use top ten command
    default: true</pre>
           </td>
           <td>
               <ul>
                   <li>L'enregistrement des permissions est optionnel, peut également être fait à partir du code</li>
                   <li>L'enregistrement des permissions vous permet de définir les descriptions, les valeurs par défaut et les relations parent-enfant</li>
                   <li>Les noms de permissions peuvent inclure la balise <code>[gamemode]</code> pour permettre à la permission de s'appliquer à tous les modes de jeu chargés sur le serveur.</li>
               </ul>
           </td>
       </tr>
   </tbody>
</table>

# Pladdons
Les Pladdons sont une combinaison d'un Plugin Bukkit et d'un Addon. Le principal avantage d'un Pladdon est qu'il est chargé avec le chargeur de classe du serveur Bukkit et que les données qu'il contient peuvent être accédées directement par les Plugins. Si vous écrivez un Addon utilitaire, par exemple un addon Level, d'autres auteurs de Plugins peuvent vouloir accéder aux données qu'il génère dans le code via une API. Le moyen le plus simple de faire cela est de faire un Pladdon et ils peuvent appeler directement des méthodes dans votre code. Si vous **ne voulez pas** que les plugins accèdent aux données de votre addon, gardez-le comme un Addon.

## Faire du Addon un Pladdon
Pour ce faire, créez une classe avec le nom recommandé `MyAddonPladdon.java`, où MyAddon est le même nom que votre Addon, et étendez `Pladdon`. Au lieu de créer un `plugin.yml`, les composants sont déclarés à l'aide d'Annotations. Les annotations doivent être les suivantes. La ApiVersion peut être mise à jour vers la dernière version du serveur si vous l'exigez.

```
@Plugin(name="Pladdon", version="1.0")
@ApiVersion(ApiVersion.Target.v1_16)
@Dependency(value = "BentoBox")
public class LevelPladdon extends Pladdon {
    private Addon addon;

    @Override
    public Addon getAddon() {
        if (addon == null) {
            addon = new Level();
        }
        return addon;
    }
}
```

La seule méthode qui doit être définie est la méthode `getAddon()` qui doit retourner l'instance de votre Addon. Assurez-vous de retourner une seule instance afin que les doublons ne soient pas créés si cette méthode est appelée plusieurs fois.

Une fois cela fait, l'Addon sera chargé tout comme un plugin et sera accessible via d'autres plugins.
