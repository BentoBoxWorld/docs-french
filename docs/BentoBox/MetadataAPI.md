# API de Métadonnées Persistantes BentoBox

BentoBox a une API de métadonnées persistantes qui permet aux métadonnées d'être enregistrées sur les Utilisateurs, les Joueurs ou les Îles de façon persistante.
Cela permet aux compléments qui n'ont pas besoin ou ne veulent pas gérer leur propre stockage de base de données d'enregistrer les données en utilisant cette API à la place.
Par exemple, le complément Border n'a besoin que d'enregistrer un booléen simple qui enregistre si la bordure est allumée ou non
pour l'utilisateur. Ce serait excessif de l'enregistrer dans une table de base de données, donc à la place, le complément peut placer ce booléen dans l'objet Joueur via la classe Utilisateur.

## Exemple Rapide

### Définition des métadonnées
Définissez les métadonnées en fournissant une clé chaîne et une nouvelle `MetaDataValue` avec l'objet que vous voulez enregistrer.
```
// Placez une étiquette booléenne sur l'utilisateur avec la valeur true et nommez-la Border_state
user.putMetaData("Border_state", new MetaDataValue(true));
```

### Vérification des métadonnées
Les métadonnées sont lues en fournissant une clé chaîne. Le retour est un `Optional` que vous pouvez vérifier pour voir s'il existe ou non
```
// Vérifiez si l'utilisateur a les métadonnées appelées Border_state
boolean on = user.getMetaData("Border_state").map(md -> md.asBoolean()).orElse(false);
```

Souvenez-vous, `getMetaData` retourne un `Optional` donc si vous vérifiez une clé de métadonnées et qu'elle n'existe pas, vous obtiendrez un `Optional.empty()`.
Donc si vous souhaitez vérifier explicitement si une étiquette existe ou non, utilisez `isPresent()`:

```
if (user.getMetaData("My_key").isPresent()) {
    // Faites quelque chose
} else {
    // Faites quelque chose d'autre
}
```

Bien sûr, vous pouvez également utiliser la méthode `ifPresent()` pour effectuer une action comme ceci :

```
user.getMetaData("My_key").ifPresent(key -> System.out.println("La valeur de votre clé est " + key.asInt()));
```

Cependant, généralement, vous voulez grabber la valeur et faire quelque chose avec, donc la syntaxe `map()` et `orElse()` est la plus utile.

### Suppression des métadonnées
Les métadonnées peuvent être supprimées d'une Île ou d'un Utilisateur par clé.

Exemple:
```
island.removeMetaData("Bank_balance");
```
Si vous souhaitez vérifier que les données ont été réellement supprimées, alors `removeMetaData` retourne une `MetaDataValue` qui sera les données qui ont été supprimées ou `Optional.empty()` / `null` si cela n'existait pas.

## Valeurs Supportées
Vous pouvez enregistrer les types de métadonnées suivants :

* String
* Integer
* Float
* Double
* Long
* Short
* Byte
* Boolean

## Getters
Bien que vous puissiez enregistrer les données sans avoir à spécifier le type de données, quand vous recevez les données vous devez utiliser le getter correct.
Si vous ne le faites pas, vos données seront `null`. Les getters sont comme suit :

* `asInt()`
* `asFloat()`
* `asDouble()`
* `asLong()`
* `asShort()`
* `asByte()`
* `asBoolean()`
* `asString()`

Exemple:
```
String nameTag = user.getMetaData("Level_nametag").map(MetaData::asString).orElse("No nametag");
```

## Convention de Nommage des Clés
Bien que les clés puissent être nommées n'importe quoi, vous devriez éviter le choc avec d'autres compléments, donc la convention est de préfixer la clé avec le nom de votre complément. Exemples :

* Level_name
* Challenges_latestChallenge
* Border_state
* etc.

## Métadonnées d'Objet Île et Joueur
Les objets Île et Joueur ont la même API pour les métadonnées que la classe Utilisateur. Bien qu'il soit possible de manitfuler les métadonnées d'objet Joueur, c'est mieux fait via l'API de classe Utilisateur.

Les métadonnées d'Île sont enregistrées quand le serveur s'arrête ou quand la base de données est enregistrée périodiquement.
