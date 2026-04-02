# Compléments

BentoBox à lui seul ne fait rien — c'est une plateforme. Les **compléments** sont ce qui le rend vivant. Il y a deux types :

- **Compléments de mode de jeu** — ceux-ci créent le monde de jeu réel dans lequel les joueurs jouent (Skyblock, CaveBlock, etc.)
- **Compléments de fonctionnalités** — ceux-ci ajoutent des extras optionnels sur n'importe quel mode de jeu

Vous choisissez exactement quels compléments installer, donc vous construisez exactement l'expérience serveur que vous voulez.

!!! info "Où vont les compléments ?"
    Les compléments ne sont **pas** placés dans le dossier `plugins/` de votre serveur. Ils vont dans :
    ```
    plugins/BentoBox/addons/
    ```
    Après les y placer, redémarrez le serveur et ils généreront automatiquement leurs fichiers de configuration.

---

## Compléments de Mode de Jeu

Ceux-ci créent le monde dans lequel vos joueurs jouent réellement. Installez-en au moins un.

| Complément | Qu'est-ce que c'est |
|---|---|
| **BSkyBlock** | Skyblock Classique — île flottante dans le ciel |
| **AOneBlock** | Commencez avec un seul bloc magique se régénérant |
| **AcidIsland** | Skyblock où l'océan est de l'acide |
| **CaveBlock** | Survie dans un monde souterrain solide |
| **SkyGrid** | Blocs uniques éparpillés à travers le vide |
| **Boxed** | Une boîte qui s'agrandit quand vous complétez les avancées |
| **Poseidon** | Survie aquatique |
| **StrangerRealms** | Survie avec une dimension en miroir dangereuse |

Voir [Modes de Jeu](GameModes.md) pour des descriptions complètes, ou [les comparer](../../gamemodes/Comparison.md) pour aider à en choisir un.

---

## Compléments de Fonctionnalité

Ceux-ci ajoutent des fonctionnalités optionnelles qui fonctionnent avec n'importe quel mode de jeu. Mélangez et associez ce qui convient à votre serveur.

### Essentiel pour la plupart des serveurs

| Complément | Qu'est-ce qu'il ajoute |
|---|---|
| **Level** | Calcule un score d'île basé sur les blocs placés. Inclut un classement pour que les joueurs puissent concourir. |
| **Challenges** | Une liste de tâches que les joueurs peuvent accomplir pour des récompenses. Idéal pour garder les joueurs engagés. |
| **Warps** | Les joueurs peuvent placer un panneau warp sur leur île pour que d'autres puissent s'y téléporter à partir d'un menu central. |
| **InvSwitcher** | Garde l'inventaire, l'expérience et la santé de chaque joueur séparés entre différents modes de jeu sur le même serveur. Fortement recommandé si vous exécutez plusieurs modes de jeu. |

### Qualité de vie

| Complément | Qu'est-ce qu'il ajoute |
|---|---|
| **IslandFly** | Permet aux joueurs de voler sur leur propre île. |
| **Visit** | Permet aux joueurs de se visiter mutuellement par un menu, sans avoir besoin de panneaux warp. |
| **Border** | Montre aux joueurs une bordure visible autour de leur zone de protection d'île. |
| **Chat** | Ajoute des canaux de chat spécifiques aux îles pour que les membres de l'équipe puissent parler en privé. |
| **Bank** | Donne à chaque île un compte bancaire partagé. Les joueurs mettent l'argent en commun. |
| **CheckMeOut** | Permet aux joueurs de soumettre leur île pour examen administrateur ou vote communautaire. |

### Avancé / Compétitif

| Complément | Qu'est-ce qu'il ajoute |
|---|---|
| **Biomes** | Permet aux joueurs de changer le biome de leur île. |
| **Greenhouses** | Les joueurs peuvent construire des structures de serre en verre qui simulent un biome spécifique à l'intérieur. |
| **Limits** | Permet aux administrateurs de fixer des limites sur le nombre de chaque bloc ou créature qu'un joueur peut avoir sur son île. |
| **MagicCobblestoneGenerator** | Les générateurs de pierre de taille peuvent être configurés pour produire différents blocs (minerais, matériaux) à des taux définis. |
| **Upgrades** | Les joueurs dépensent des ressources pour améliorer les propriétés de l'île comme la taille, la génération de mobs, etc. |
| **TopBlock** | Un classement basé sur le bloc unique le plus élevé placé sur une île. |
| **TwerkingForTrees** | Une mécanique amusante où les joueurs peuvent faire pousser instantanément les semis en dansant (en se faufilant à répétition). |

### Utilitaire / Admin

| Complément | Qu'est-ce qu'il ajoute |
|---|---|
| **VoidPortals** | Les joueurs peuvent voyager au Nether ou à la Fin en tombant dans le vide. |
| **DimensionalTrees** | Les arbres cultivés dans des dimensions spécifiques produisent des butin spéciaux. |
| **ExtraMobs** | Ajoute des défis et des interactions supplémentaires liés aux mobs. |
| **FarmersDance** | Les joueurs peuvent faire pousser les cultures en dansant près d'elles. |
| **ControlPanel** | Fournit un panneau de contrôle GUI pour les administrateurs pour gérer BentoBox. |
| **CauldronWitchery** | Les joueurs fabriquent des potions spéciales en utilisant des chaudrons pour les effets et les objets. |

---

## Trouver et Télécharger des Compléments

Les compléments officiels sont maintenus par l'équipe BentoBoxWorld et peuvent être trouvés sur :

**[github.com/BentoBoxWorld](https://github.com/BentoBoxWorld)**

Téléchargez le fichier `.jar` à partir de l'onglet **Releases** du dépôt de chaque complément. Les builds de développement (non testés) sont disponibles sur le [serveur CodeMC CI](https://ci.codemc.io/job/BentoBoxWorld/).

!!! warning "Compatibilité des versions"
    Chaque complément liste quelles versions de BentoBox il supporte. Vérifiez toujours cela avant de télécharger. L'utilisation d'un complément avec la mauvaise version de BentoBox peut empêcher votre serveur de démarrer correctement.

---

## Vérifier ce qui est Installé

En jeu, exécutez :
```
/bentobox version
```
Cela liste la version de BentoBox et chaque complément actuellement chargé, avec leurs versions. Incluez cette sortie chaque fois que vous signalez un bug ou demandez du support.
