# InvSwitcher

**InvSwitcher** sépare les inventaires des joueurs et d'autres aspects entre les différents mondes.

Créé et maintenu par [tastybento](https://github.com/tastybento).

{{ addon_description("InvSwitcher") }}

Ce qui suit est commuté par monde :

* Inventaire et armure
* Avancées
* Niveau de nourriture
* Expérience
* Santé
* Mode de jeu (créatif, survie, etc.)

## Comment l'utiliser

1. Placez le fichier jar de l'addon dans le dossier des addons du plugin BentoBox
2. Redémarrez le serveur
3. Fait!

## Config.yml

InvSwitcher possède un `config.yml` avec deux sections principales.

### Mondes

Liste les mondes de mode de jeu dans lesquels InvSwitcher opère. Les mondes Nether et End sont inclus automatiquement.

```yml
worlds:
- bskyblock_world
- acidisland_world
- oneblock_world
# ... etc.
```

### Options

Contrôle quels aspects du joueur sont commutés par monde et, optionnellement, par île.

```yml
options:
  inventory: true
  health: true
  food: true
  advancements: true
  gamemode: true       # mode de jeu (Survie/Créatif/etc.)
  experience: true
  ender-chest: true
  statistics: true
  # Commutation d'inventaire par île (ajoutée dans 1.17.0)
  # L'option au niveau du monde doit aussi être true pour que l'option île prenne effet.
  islands:
    active: true       # Activer la commutation par île globalement
    inventory: true    # Donner aux joueurs un inventaire différent sur chaque île qu'ils possèdent
    health: false
    food: false
    advancements: false
    gamemode: false
    experience: false
    ender-chest: true
    statistics: false
```

Définissez `islands.active: true` pour permettre aux joueurs qui possèdent plus d'une île d'avoir des inventaires séparés (et autres aspects) par île, pas seulement par monde de mode de jeu.

## Commandes

Il n'y a pas de commandes.

## Ce qu'il fait
Cet addon donnera aux joueurs un inventaire, une santé, un niveau de nourriture, des avancées et une expérience séparés pour chaque mode de jeu installé et leurs mondes correspondants. Il permet aux joueurs de jouer à chaque mode de jeu indépendamment l'un de l'autre.

## Un exemple
L'inventaire, la santé, le niveau de nourriture, les avancées et l'expérience de **BSkyBlock** sont partagés uniquement entre ses mondes correspondants :
- BSkyBlock_world
- BSkyBlock_world_nether
- BSkyBlock_world_the_end

**Veuillez noter :**
- Ce n'est pas limité aux mondes BentoBox. Cela s'applique à tous les mondes du serveur (pour l'instant).

## Journal des modifications

??? note "Nouveautés dans v1.17.0"
    **Publié :** 31 mars 2026

    - **Commutation d'inventaire par île.** Les joueurs qui possèdent plus d'une île peuvent maintenant avoir des inventaires séparés (et optionnellement santé, nourriture, expérience, coffre de l'end, statistiques) par île dans le même mode de jeu. Activez avec `options.islands.active: true` et configurez chaque sous-option. L'option au niveau du monde doit aussi être `true` pour que son équivalent île prenne effet.
    - ⚙️ Nouvelle section `options.islands` dans `config.yml`.
    - Correction : l'inventaire était perdu lors du retour à l'île d'origine.

    [Release v1.17.0](https://github.com/BentoBoxWorld/InvSwitcher/releases/tag/1.17.0)

## Traductions

{{ translations("InvSwitcher") }}
