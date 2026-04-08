# Upgrades

**Upgrades** vous permet de mettre à niveau la taille de votre île, les limites des entités/blocs au coût de l'argent et du niveau de l'île.

Cet addon a été créé pour ajouter une courbe de progression et une utilisation de l'argent pour l'île.

Créé et maintenu par [Ikkino](https://github.com/Guillaume-Lebegue)

{{ addon_description("Upgrades", true) }}

## Installation

1. Placez le fichier jar du addon Upgrades dans le dossier des addons du plugin BentoBox
2. Redémarrez le serveur
3. L'addon créera un dossier de données et à l'intérieur du dossier se trouvera un config.yml
4. Modifiez le config.yml comme vous le souhaitez.
5. Redémarrez le serveur si vous apportez une modification

## Commandes

!!! tip
    `[player_command]` est une commande qui diffère selon le mode de jeu que vous exécutez.
    Le fichier `config.yml` des modes de jeu contient des options qui vous permettent de modifier cette valeur.
    Par exemple, sur BSkyBlock, la `[player_command]` par défaut est `island`.

Il y a une commande d'utilisateur pour ouvrir une interface graphique avec les mises à niveau.

`/[Player command] upgrade`

## Setup - Config.yml

Le config.yml a les sections suivantes :

* range-upgrade
* block-limits-upgrade
* entity-limits-upgrade
* command-upgrade
* gamemodes
* entity-icon
* command-icon

!!! tip
    Tous les champs `upgrade`, `island-min-level` et `vault-cost` sont des expressions mathématiques. Donc:

    * +,-,*,/,^,(,) peuvent être utilisés
    * sqrt(), sin(), cos(), tan() peuvent être utilisés
    * `[level]` est remplacé par le niveau réel pour cette mise à niveau
    * `[islandLevel]` est remplacé par le niveau de l'île du addon de niveau **(Peut être 0)**
    * `[numberPlayer]` est remplacé par le nombre de joueurs dans l'équipe


### Général

Une mise à niveau est divisée par « tier » qui peut être nommé à volonté

Exemple:
```yml
tier1:
  max-level: 5
  upgrade: "5"
  island-min-level: "2"
  vault-cost: "[level]*100"
  permission-level: 1
```

* `max-level` est le niveau maximum de ce tier.
* `upgrade` est le montant donné à chaque niveau.
* `island-min-level` est le niveau d'île minimum nécessaire pour acheter cette mise à niveau. Il est donné par [Level Addon](/addons/Level)
* `vault-cost` est le coût pour acheter cette mise à niveau **(>= 0)**
* `permission-level` est le niveau de permission nécessaire pour acheter cette mise à niveau (cf. Permission)


### Mise à niveau de plage

Cette mise à niveau augmente la taille de protection de l'île.

L'augmentation de taille est donnée dans le champ `upgrade`

Exemple:
```yaml
range-upgrade:
  tier1:
    max-level: 5
    upgrade: "5"
    island-min-level: "2"
    vault-cost: "[level]*100"
  tier2:
    max-level: 10
    upgrade: "3"
    island-min-level: "4"
    vault-cost: "[level]*[numberPlayer]*200"
```

!!! warning "Plage maximale"
    Vous devriez toujours vérifier que, même au niveau de mise à niveau maximum, la taille de protection n'excède jamais la taille entre les îles.

### Mise à niveau des limites de blocs

Cette mise à niveau augmente les limites des blocs définis dans le [Addon Limits](/addons/Limits)

Le nombre à ajouter aux limites est donné par le champ `upgrade`.

Exemple:
```yaml
block-limits-upgrade:
  HOPPER:
    tier1:
      max-level: 2
      upgrade: "1"
      island-min-level: "2"
      vault-cost: "[level]*100"
    tier2:
      max-level: 5
      upgrade: "1"
      island-min-level: "4"
      vault-cost: "([level]-2)*[numberPlayer]*700"
      permission-level: 1
```

!!! tip "Blocs"
    Une liste de blocs peut être trouvée [ici](https://hub.spigotmc.org/javadocs/bukkit/org/bukkit/Material.html)


### Mise à niveau des limites d'entités

Cette mise à niveau augmente les limites des entités définies dans le [Addon Limits](/addons/Limits)

Toutes les entités doivent avoir une icône correspondante (CF: [entity-icon](#entity-icon))

Le nombre à ajouter aux limites est donné par le champ `upgrade`.

Exemple:
```yaml
entity-limits-upgrade:
  CHICKEN:
    tier1:
      max-level: 2
      upgrade: "1"
      island-min-level: "2"
      vault-cost: "[level]*100"
    tier2:
      max-level: 5
      upgrade: "1"
      island-min-level: "4"
      vault-cost: "([level]-2)*[numberPlayer]*700"
      permission-level: 3
```

!!! tip "Entités"
    Une liste d'entités peut être trouvée [ici](https://hub.spigotmc.org/javadocs/spigot/org/bukkit/entity/EntityType.html)

## Traductions

{{ translations("Upgrades") }}
