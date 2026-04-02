# L'API du Gestionnaire de Requêtes

**Remarque :** Cette API est obsolète car la plupart des Compléments sont maintenant chargés en tant que Plugins. Cette page est laissée juste pour référence.

---

Cette API permet aux auteurs de plugins de demander des données des compléments. Les auteurs de compléments peuvent décider exactement quelles données ils souhaitent exposer. Les plugins ne peuvent pas accéder directement à aucune classe à l'intérieur d'un complément en raison des règles de sécurité Java sur les chargeurs de classe.

## Exemple avec le Complément Level

Le complément Level expose deux gestionnaires de requêtes [LevelRequestHandler](https://github.com/BentoBoxWorld/Level/blob/develop/src/main/java/world/bentobox/level/requests/LevelRequestHandler.java) et [TopTenRequestHandler](https://github.com/BentoBoxWorld/Level/blob/develop/src/main/java/world/bentobox/level/requests/TopTenRequestHandler.java). Voici comment un plugin obtiendrait le niveau d'un joueur de LevelRequestHandler :

### LevelRequestHandler

Label : `island-level`

Carte d'entrée :

* Clé : `world-name` -> String
* Valeur : `player` -> UUID

    !!! example "Exemple de code"
        ```java
            /**
             * Retourne le niveau de l'île de ce joueur dans le monde donné.
             * @param playerUUID UUID du joueur, pas null.
             * @param worldName Nom du monde (Overworld) dans lequel se trouve l'île, pas null.
             * @return le niveau de l'île du joueur ou {@code 0L} si l'entrée était invalide ou
             *         si ce joueur n'a pas d'île dans ce monde.
             */
            public long getIslandLevel(UUID playerUUID, String worldName) {
                return (Long) new AddonRequestBuilder()
                    .addon("Level")
                    .label("island-level")
                    .addMetaData("world-name", worldName)
                    .addMetaData("player", playerUUID)
                    .request();
            }
        ```

Vous pouvez découvrir quelles données sont exposées par les compléments en regardant leur code ou leur documentation.

# Exposition des données d'un complément
Pour exposer les données, créez des classes pour chaque élément qui étendent [AddonRequestHandler](https://bentoboxworld.github.io/BentoBox/world/bentobox/bentobox/api/addons/request/AddonRequestHandler.html). Enregistrez ensuite les gestionnaires de requêtes dans votre complément. Par exemple :

```
        // Enregistrez les gestionnaires de requêtes
        registerRequestHandler(new LevelRequestHandler(this));
        registerRequestHandler(new TopTenRequestHandler(this));
```

Le gestionnaire doit définir son label dans son constructeur, par exemple :

```
    public LevelRequestHandler(Level addon) {
        super("island-level"); // le label est "island-level"
        this.addon = addon;
    }
```

Le label doit être unique pour votre complément.

Ensuite, remplacez la méthode `handle` qui prend une carte comme paramètre :

```
    @Override
    public Object handle(Map<String, Object> map) {
```

Vous pouvez définir le contenu de la carte mais l'Object ne doit **JAMAIS** être aucune classe unique dans votre complément. Il ne peut être que les classes qui existent pour tous les plugins. Si vous essayez de référencer une classe cachée, le plugin générera une exception. Donc, les entiers, les longs, les Emplacements Bukkit, les mondes, etc. vont bien.

C'est une bonne pratique de documenter ce que votre carte sera parce que les auteurs de plugins l'utiliseront :

```
        /*
            Ce dont nous avons besoin dans la carte :
            0. "world-name" -> String
            1. "player" -> UUID
            Ce que nous allons retourner :
            - 0L si entrée invalide/le joueur n'a pas d'île
            - le niveau de l'île sinon (qui peut être 0)
         */
```

Après cela, traitez la carte et fournissez le résultat :

```

        if (map == null || map.isEmpty()
                || map.get("world-name") == null || !(map.get("world-name") instanceof String)
                || map.get("player") == null || !(map.get("player") instanceof UUID)
                || Bukkit.getWorld((String) map.get("world-name")) == null) {
            return 0L;
        }

        return addon.getIslandLevel(Bukkit.getWorld((String) map.get("world-name")), (UUID) map.get("player"));
    }
```

Remarquez que vous retournez un `Object` donc l'auteur du plugin devra le caster à la forme correcte, dans ce cas, une `long`. C'est une bonne pratique de protéger votre complément des formats de carte erronés en effectuant un niveau approprié de vérification des paramètres.
