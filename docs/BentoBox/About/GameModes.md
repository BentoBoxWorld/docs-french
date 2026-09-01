# Modes de Jeu

BentoBox est un cadre — il fournit les outils de base (gestion des îles, protection, équipes) mais ne crée pas de monde par lui-même. Vous ajoutez un ou plusieurs **modes de jeu** pour définir quel type d'expérience les joueurs auront.

Un mode de jeu est un complément qui définit les règles : à quoi ressemble le monde, comment les joueurs commencent et quel est l'objectif global. Vous pouvez exécuter plusieurs modes de jeu sur le même serveur en même temps.

!!! tip "Pas sûr lequel choisir ?"
    Voir la page [Comparaison des Modes de Jeu](../../gamemodes/Comparison.md) pour un aperçu côte à côte.

---

## Modes de Jeu Disponibles

### BSkyBlock — Skyblock Classique

Les joueurs commencent sur une petite île flottante haut dans le ciel, au-dessus de rien d'autre que des nuages et du vide. Le défi est de survivre et de grandir en utilisant seulement les ressources limitées dont ils disposent.

**Meilleur pour :** Les serveurs qui veulent l'expérience Skyblock classique et bien connue. Idéal pour tous les âges.

---

### AOneBlock — One Block Skyblock

Les joueurs commencent avec un seul bloc magique flottant dans le vide. Chaque fois qu'ils le minent, il se régénère en tant que bloc ou créature différent. Les phases progressent au fur et à mesure qu'ils minent plus, déverrouillant graduellement de nouveaux matériaux et défis.

**Meilleur pour :** Les serveurs qui veulent une nouvelle approche du Skyblock avec un système de progression intégré.

---

### ChunkBlock — Un Bloc dans un Chunk Muré

Les joueurs commencent sur le même bloc magique qui se régénère qu'AOneBlock, mais le monde est un seul chunk 16×16 avec une bordure que rien ne peut traverser — pas marcher, voler, perler ou creuser. Le niveau d'île est la devise du territoire : construisez le niveau, marchez vers le mur et frappez-le dans la direction où vous voulez, et le prochain chunk s'ouvre. Perdez les niveaux et les derniers chunks se verrouillent à nouveau (les constructions sont intactes) jusqu'à ce que les niveaux reviennent. Nécessite le module [Level](../../addons/Level/index.md).

**Meilleur pour :** Les serveurs qui veulent la boucle d'un bloc avec une raison solide de continuer à monter de niveau, et l'expansion que les joueurs gagnent un chunk à la fois.

---

### AcidIsland — Survie dans l'Acide

Similaire à Skyblock, mais l'océan entourant les îles est rempli d'acide qui endommage les joueurs. La natation est dangereuse, donc les joueurs doivent construire avec soin et éviter de tomber dedans.

**Meilleur pour :** Les serveurs qui veulent Skyblock avec un défi de survie supplémentaire et une tournure unique.

---

### CaveBlock — Survie Souterraine

Au lieu d'une île flottante dans le ciel, les joueurs reçoivent une petite grotte dans un monde souterrain solide. Ils doivent creuser et agrandir leur espace, le monde lui-même étant le défi.

**Meilleur pour :** Les serveurs qui veulent une sensation Skyblock inversée — l'exploration souterraine et l'extraction axées.

---

### SkyGrid — Survie Basée sur les Blocs Éparpillés

Le monde est généré comme une vaste grille de blocs uniques espacés — un bloc de terre ici, un bloc de bois là. Les joueurs doivent voyager à travers la grille pour collecter des ressources, sans sol solide sur lequel se tenir.

**Meilleur pour :** Les serveurs qui veulent un défi de survie extrême nécessitant l'exploration et le mouvement de précision.

---

### Boxed — Survie en Espace Confiné

Les joueurs sont confinés à une petite boîte qui voyage avec eux. La boîte s'agrandit à mesure que les joueurs complètent les avancées. Le défi est de survivre et de progresser dans un espace toujours limité mais en expansion.

**Meilleur pour :** Les serveurs qui veulent un mode survie axé sur les avancées avec une mécanique unique.

---

### Poseidon — Survie Aquatique

Les joueurs commencent à la surface de l'océan ou dessous et doivent construire et survivre dans un monde entièrement aquatique. Le défi est d'adapter la survie standard Minecraft à un environnement sous-marin.

**Meilleur pour :** Les serveurs qui veulent une expérience de survie visuellement distincte et à thème aquatique.

---

### Stranger Realms — Survie avec l'Envers

Les joueurs survivent dans l'Overworld tout en gérant une dimension miroir sinistre — l'Envers — qui est une copie sombre et dangereuse de leur monde. Les interactions entre les deux dimensions créent des défis uniques.

**Meilleur pour :** Les serveurs qui veulent une expérience de survie plus complexe et inspirée par une histoire avec des mécaniques dimensionnelles.

---

### TradeWinds — Commerce Maritime

Les joueurs commencent avec un bateau à rames et un peu de charbon sur un océan infini généré procéduralement parsemé d'îles de commerce PNJ. Le bateau est la cargaison : achetez bon marché à un port, vendez cher à un autre, améliorez la coque, cartographiez les nouvelles îles pour monter les rangs de Marin, et finalement réclamez votre propre îlot. Nécessite Vault et un module d'économie.

**Meilleur pour :** Les serveurs qui veulent un jeu d'économie axé sur le commerce — les eaux sûres près du spawn conviennent aux joueurs occasionnels, tandis que la contrebande, les pirates et les primes PvP attendent plus loin.

---

## Installation d'un Mode de Jeu

Les modes de jeu sont téléchargés en tant que fichiers `.jar` et placés dans :
```
plugins/BentoBox/addons/
```

Ils ne sont **pas** placés dans le dossier principal `plugins/`. Après avoir placé le fichier, redémarrez le serveur et le mode de jeu créera ses propres fichiers de configuration pour vous.

Voir [Comment Installer BentoBox](../Install-Bentobox.md) pour le guide de configuration complet.

## Exécution de Plusieurs Modes de Jeu

Vous pouvez exécuter autant de modes de jeu que vous le souhaitez simultanément. Chaque mode de jeu obtient ses propres mondes distincts et ses propres données de joueur, donc l'île BSkyBlock d'un joueur et son île AcidIsland sont complètement indépendantes.
