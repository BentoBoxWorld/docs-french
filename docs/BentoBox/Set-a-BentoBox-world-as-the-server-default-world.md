## Introduction

**Définir un monde BentoBox comme le monde par défaut du serveur** permet d'éviter la génération des **mondes vanille par défaut**.

!!! warning
    Dans cet exemple pas à pas/tutoriel, nous considérons que vous faites cela pour `BSkyBlock`.
    Le processus est le même pour les autres modes de jeu, mais **faites attention aux noms des mondes** !

## Préparations

1. La procédure entière doit être exécutée pendant que le serveur est **éteint**.
2. Supprimez les mondes vanille (`world`, `world_nether`, `world_the_end`) en supprimant leurs dossiers.

![mondes à supprimer](https://user-images.githubusercontent.com/20014332/62977233-bebf1180-be1e-11e9-9ec8-ddcfd3352b13.png)

*Les dossiers en surbrillance sont ceux du monde par défaut. Ils doivent être supprimés.*

## server.properties

Ouvrez le fichier `server.properties`.

Trouvez la ligne suivante :
```properties
level-name=world
```

Remplacez `world` par le nom du monde BentoBox. C'est généralement `[gamemode]_world`, où `[gamemode]` est le nom du mode de jeu en minuscules (par ex. `bskyblock` ou `caveblock`). Cependant, cela peut être modifié dans le fichier `config.yml` du mode de jeu, donc assurez-vous que c'est le bon.

Par souci de simplicité, nous supposerons que le nom du monde reste inchangé et reste donc génériquement `bskyblock_world`.

La ligne devrait maintenant ressembler à ceci :
```properties
level-name=bskyblock_world
```

## bukkit.yml

Ouvrez le fichier `bukkit.yml` : nous devons dire à Bukkit que le monde par défaut utilise un générateur personnalisé, **sinon il gâtera la génération du monde**. Remarquez que si vous voulez utiliser le nether ou la fin vanille, ne les listez pas dans ce fichier.

La section de configuration que nous ajoutons n'existe probablement pas déjà dans votre fichier `bukkit.yml`, vous devez donc la créer. Voir le [Wiki Bukkit](https://bukkit.fandom.com/wiki/Bukkit.yml) officiel pour plus de détails sur la section.

Ajoutez la section suivante à votre fichier. Les noms listés **doivent** être les noms des mondes :
```yaml
worlds:
  bskyblock_world:
    generator: BentoBox
  bskyblock_world_nether:
    generator: BentoBox
  bskyblock_world_the_end:
    generator: BentoBox
```

Si vous allez utiliser le nether ou la fin vanille, ne les listez pas. Listez juste le surmondes. Par exemple :
```yaml
worlds:
  bskyblock_world:
    generator: BentoBox
```
