# Choisir un mode de jeu

Vous ne savez pas quel mode de jeu lancer sur votre serveur ? Cette page compare tous les modes de jeu BentoBox officiels pour vous aider à décider.

Vous pouvez aussi lancer **plusieurs modes à la fois** — de nombreux serveurs proposent deux ou trois modes de jeu afin que les joueurs puissent choisir leur expérience préférée.

---

## Comparaison rapide

| Mode de jeu | Environnement | Difficulté | Défi principal | Focus multijoueur |
|---|---|---|---|---|
| **BSkyBlock** | Ciel (îles flottantes) | Moyen | Étendre une minuscule île dans le vide | Moyen |
| **AOneBlock** | Ciel (vide) | Moyen | Miner un seul bloc magique qui ne s'épuise jamais | Faible à Moyen |
| **ChunkBlock** | Ciel (vide, un chunk) | Moyen | Miner le bloc magique et dépenser les niveaux d'île pour frapper les murs | Faible à Moyen |
| **AcidIsland** | Mer (océan acide) | Moyen à Difficile | Skyblock avec eau acide dangereuse | Moyen |
| **CaveBlock** | Souterrain | Moyen | Creuser l'espace dans un monde de pierre solide | Moyen |
| **SkyGrid** | Ciel (blocs dispersés) | Difficile | Collecter les ressources dans une grille de blocs individuels | Faible |
| **Boxed** | Monde normal | Facile à Moyen | Compléter les avancements pour agrandir votre espace confiné | Moyen |
| **Poseidon** | Océan | Moyen | Survivre entièrement sous l'eau | Moyen |
| **StrangerRealms** | Monde principal + À l'envers | Moyen à Difficile | Réclamer des terres en gérant une dimension miroir dangereuse | Moyen à Élevé |
| **TradeWinds** | Mer (océan infini de commerce) | Facile à Difficile (par région) | Naviguer entre les îles de commerce PNJ, acheter bas et vendre haut | Moyen |

---

## Lequel choisir ?

### Je veux l'expérience la plus populaire et la plus connue
**BSkyBlock** — Le Skyblock classique est ce que la plupart des joueurs connaissent déjà. Il a la plus grande communauté, le plus de ressources et constitue un choix sûr pour n'importe quel serveur.

### Je veux quelque chose de nouveau mais toujours accessible
**AOneBlock** — Le concept (un bloc magique) est facile à expliquer et immédiatement engageant. La progression des phases intégrée garde les joueurs motivés pendant longtemps.

### Je veux la boucle d'un bloc avec une raison de continuer à monter de niveau
**ChunkBlock** — Le même bloc magique qu'AOneBlock (les fichiers de phase sont interchangeables), mais le monde est un chunk 16×16 derrière une bordure que rien ne peut traverser. Le niveau d'île est la devise : construisez votre niveau, marchez vers le mur, et frappez-le dans la direction où vous voulez grandir. Perdez les niveaux et les derniers chunks se verrouillent à nouveau, les constructions intactes, jusqu'à ce que vous les regagniez — ou désactivez cela dans la config si vous voulez que le territoire soit un cliquet. Nécessite le module [Level](../addons/Level/index.md).

### Je veux Skyblock mais plus difficile
**AcidIsland** — La même atmosphère que BSkyBlock mais tomber dans l'océan est vraiment dangereux. Bon pour les joueurs qui trouvaient le Skyblock ordinaire trop facile.

### Je veux un thème souterrain / minier
**CaveBlock** — Au lieu de construire vers le haut dans le ciel, les joueurs creusent depuis le sol solide. L'expérience se sent très différente malgré le partage de la plupart des mécaniques de BentoBox.

### Je veux accueillir les joueurs avancés / hardcore
**SkyGrid** — Le monde des blocs dispersés est impitoyable. Les ressources sont étalées, les mouvements sont dangereux et la survie nécessite une véritable compétence. Non recommandé comme seule option sur un serveur avec des nouveaux joueurs.

### Je veux quelque chose lié à la progression vanilla
**Boxed** — Le mécanisme d'expansion basé sur les avancements connecte le jeu directement aux objectifs de Minecraft vanilla. Bon pour les joueurs qui aiment la progression structurée.

### Je veux un thème visuel unique
**Poseidon** — Un monde entièrement aquatique est magnifique et joue très différemment. Excellent comme option secondaire pour les joueurs qui veulent quelque chose de visuellement distinct.

### Je veux une expérience inspirée par une histoire avec des mécaniques complexes
**StrangerRealms** — La dimension miroir À l'envers ajoute une couche de stratégie. Mieux adapté aux joueurs à l'aise avec Minecraft et prêts pour quelque chose de plus complexe.

### Je veux un jeu d'économie axé sur le commerce
**TradeWinds** — Achetez bon marché et vendez cher dans un océan infini généré procéduralement composé de ports de commerce PNJ. La difficulté est géographique : les eaux près du spawn sont patrouillées et calmes, tandis que la contrebande, les pirates et l'espace des primes PvP attendent plus loin — donc cela fonctionne pour un serveur familial et un serveur impitoyable à la fois. Nécessite Vault et un module d'économie.

---

## Support des fonctionnalités par mode de jeu

La plupart des addons BentoBox fonctionnent avec tous les modes de jeu. Quelques-uns ont des exigences de compatibilité spécifiques.

| Fonctionnalité | BSkyBlock | AOneBlock | ChunkBlock | AcidIsland | CaveBlock | SkyGrid | Boxed | Poseidon | StrangerRealms | TradeWinds |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| Addon Level | ✅ | ✅ | ⚠️**** | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Défis | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Warps | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| InvSwitcher | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Addon Border | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ❌* | ✅ |
| Monde Nether | ✅ | ✅ | ⚠️***** | ✅ | ✅ | ✅ | ✅ | ✅ | ❌** | ❌*** |
| Monde End | ✅ | ✅ | ⚠️***** | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ❌*** |

\* StrangerRealms possède son propre système de bordure intégré — n'utilisez pas l'addon Border avec lui.

\*\* StrangerRealms remplace le Nether par la dimension À l'envers.

\*\*\* TradeWinds remplace le Nether par l'Interstice (une mer nether hostile atteinte par les ratés de warp) et n'a délibérément pas de monde End. TradeWinds nécessite également Vault plus un module d'économie.

\*\*\*\* ChunkBlock **nécessite** le module Level — le niveau d'île est la devise utilisée pour réclamer les chunks, et ChunkBlock se désactive lui-même si Level est manquant.

\*\*\*\*\* ChunkBlock génère le Nether et l'End désactivés par défaut. Activez l'un ou l'autre et il obtient son propre chunk central et les mêmes règles de réclamation basées sur le niveau ; le bloc magique n'existe que dans l'overworld.

---

## Lancer plusieurs modes de jeu

Chaque mode de jeu fonctionne complètement indépendamment — mondes séparés, bases de données d'îles séparées, configurations séparées. Les joueurs peuvent avoir une île dans chaque mode de jeu en même temps.

Si vous lancez plusieurs modes de jeu, nous vous recommandons vivement d'installer l'addon **InvSwitcher**. Sans cela, les joueurs partagent le même inventaire, expérience et santé dans tous les mondes des modes de jeu, ce qui peut causer de la confusion et des exploits.
