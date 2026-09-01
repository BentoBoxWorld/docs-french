<!-- Hero screenshot goes here once the game is public:
<img width="600" height="300" alt="TradeWinds" src="..." />
-->

# 🌬️ TradeWinds

Créé et maintenu par [tastybento](https://github.com/tastybento).

**TradeWinds** est un mode de jeu de commerce maritime pour BentoBox : un océan procéduralement généré infini parsemé d'îles commerciales contrôlées par des PNJ. Vos joueurs commencent sans rien d'autre qu'un bateau à rames et une poche pleine de charbon — et le bateau **EST** leur soute à cargaison. Achetez pas cher sur une île agricole, vendez cher dans un port industriel, et regardez l'argent entrer… ou prenez le raccourci par la contrebande, les chasseurs de primes et la piraterie, et affrontez les conséquences.

Si vous avez perdu un week-end sur *Elite* ou *TradeWars 2002*, c'est exactement cette sensation, recréée dans Minecraft. Si ce n'est pas le cas — vos joueurs sont sur le point de découvrir pourquoi vous l'auriez fait.

## 🧭 Pourquoi les joueurs y deviennent accros

- 🏝️ **Un océan infini généré à partir d'une graine.** La position, le type, le niveau technologique, la bande de sécurité, le biome et le nom de chaque île découlent d'une seule graine. Les joueurs peuvent explorer et découvrir de nouveaux endroits. Utilisez la graine par défaut ou choisissez une nouvelle pour avoir un monde unique. Partagez votre graine et un autre serveur obtient exactement le même océan.
- ⛵ **Le bateau EST la soute.** Les marchandises se trouvent dans le navire, le navire peut être amélioré par **20 rangs de coque** (Radeau en Bambou → Bateau en Coffre de Pale Oak), et perdre le navire **signifie quelque chose**. Un joueur, un bateau — chaque décision concernant la coque est importante.
- 📈 **Un marché qui mérite d'être étudié.** Huit types d'îles (fermes, mines, pêcheries, forêts, industrie, luxe, ports gelés…) achètent et vendent différemment, et chaque commerce fait légèrement varier les prix locaux. Les bonnes routes sont *découvertes*, pas affichées.
- ⚡ **Deux façons de voyager, toutes les deux équitables.** Ramer est gratuit, lent, et vous fait traverser des eaux anarchiques, mais potentiellement riches. Se téléporter est instantané mais consomme du carburant de la soute — et un mauvais tir de 5% vous plonge dans l'**Interstice**, une mer de nether hostile où le bloc de verrues du nether, les baguettes de flamme et les tours du Wither guettent. Aucune façon ne l'emporte jamais clairement sur l'autre ; c'est cette tension qui crée le jeu.
- 🗺️ **Cartes, étoiles et rang.** Élever la carte fait flotter un compas holographique de tout ce que vous avez cartographié. Chaque île cartographiée par les joueurs grimpe l'**échelle de Marin** — 19 rangs de Moussaillon à Marin Légendaire, avec un classement intégré des dix meilleurs et des espaces réservés pour votre tableau de bord.
- 🏠 **Une île à vous — gagnée.** Atteindre **Capitaine de la Marée** (36 îles cartographiées) et porter des pièces sérieuses, et n'importe quel îlot sauvage que vous trouvez peut devenir le vôtre : protection, équipe, point d'accueil, un nœud de téléportation réservé aux membres et navigation nocturne par les étoiles. Premier arrivé, premier servi.
- 🚨 **Un crime qui vous paye en vous poussant vers le danger.** La contrebande ne se vend que là où la loi est faible ; un casier judiciaire vous ferme les marchés sûrs et place une prime sur votre tête que les autres joueurs peuvent légalement percevoir. Les contrebandiers les plus riches se trouvent structurellement poussés vers le bord dangereux de la carte — où les pirates se trouvent déjà.
- 🐡 **Une mer qui vous repousse.** Piquets de Gardiens le jour, pillards noyés la nuit, phantômes, créatures des profondeurs, équipages de pirates marins, sorcières de mer — adaptés au caractère anarchique de l'eau. Même les voies sûres obtiennent occasionnellement un banc de poissons-épines, juste pour tenir le timonier éveillé.

**La difficulté est la géographie.** Les eaux près du point d'apparition sont patrouillées et calmes — les joueurs nouveaux et plus jeunes peuvent commercer en paix. Le danger, la contrebande et l'espace PvP avec primes se trouvent tous *ailleurs*, et y aller est toujours un choix. Cela fait de TradeWinds l'un des rares jeux d'économie qui fonctionne à la fois pour un serveur familial et un serveur impitoyable, avec la même configuration.

## ⚓ Comment se déroule une session

Vous levez l'ancre du port d'apparition avec trois emplacements de cargaison et une intuition : le village de pêcheurs deux îles à l'est payait le blé au double. Vous ramez la première étape — le carburant c'est l'argent — et cartographiez un nouvel îlot en chemin, un cran de plus vers Capitaine de la Marée. À la barrière frontalière, le dialogue de téléportation offre la traversée pour 14 unités de charbon ; vous l'acceptez, car le soleil se couche et les pillards noyés possèdent la nuit ici. Le marché paie bien, la soute se remplit de morue bon marché, et sur le chemin du retour vers la carte vous remarquez une île à bande rouge que vous n'avez jamais osé visiter achète du poisson à des prix *ridiculement élevés*. Un seul parcours tranquille suffirait…

Cette boucle — planifier, naviguer, commercer, risquer un peu plus que la dernière fois — c'est tout le jeu, et il ne lâche prise.

## 🔧 Configuration

!!! warning "Vault et un plugin d'économie sont obligatoires"
    Tous les échanges passent par Vault. Installez Vault plus n'importe quelle économie compatible Vault (EssentialsX Economy, CMI, etc.) avant le premier démarrage. TradeWinds formate lui-même l'argent — pièces entières, pas de décimales — en utilisant le `economy.currency-symbol` de sa configuration. Si vous voulez l'option de BentoBox, utilisez InvSwitcher avec l'argent activé - c'est une économie pour BentoBox.

1. **Téléchargez l'addon TradeWinds** et placez-le dans `/plugins/BentoBox/addons/`
2. **Démarrez le serveur** — `tradewinds_world` (l'océan) et `tradewinds_world_nether` (l'Interstice) se génèrent automatiquement. Il n'y a intentionnellement **pas de monde End**.
3. **Connectez-vous en tant qu'Op et regardez autour de vous** : `/twadmin islands` répertorie les îles commerciales les plus proches et `/twadmin tpisland <#>` vous téléporte à l'une d'elles.
4. **Choisissez votre graine du monde** *(optionnel, avant que les joueurs ne rejoignent)* : définissez `ocean.seed` dans `config.yml`. Chaque position d'île, type et nom découle de ce seul nombre — le changer plus tard et c'est un océan différent.
5. **Ajustez l'économie à votre goût** *(optionnel)* : les prix, les coûts des bateaux, les taux de carburant de téléportation, le crime et les tableaux de rencontres sont tous dans `config.yml` avec les valeurs par défaut prévues déjà en place.

!!! tip "Compagnons recommandés"
    - **InvSwitcher** — garde les inventaires, la santé et la faim séparés de vos autres modes de jeu. Inclut une économie.
    - **Bank** — les îles des joueurs réclamées s'attachent automatiquement à l'addon Bank s'il est installé. Permet de mettre en commun l'argent entre les membres de l'équipe.

## ✅ Compatibilité

| Fonctionnalité     | Supportée                          |
|-------------------|------------------------------------|
| Serveur            | ✅ Paper 26.2+                     |
| Version BentoBox   | ✅ 3.18.0 ou version ultérieure                |
| Version Java       | ✅ Java 25                         |
| Économie           | ⚠️ Vault + plugin d'économie requis |

## 🎮 Commandes

La commande joueur est `/tw` (ou `/tradewinds`) ; la commande administrateur est `/twadmin`. Bare `/tw` lève l'ancre — c'est la porte dans l'océan, et le seul téléport prudent du jeu : il vous ramène à l'eau que vous avez quittée, vous marche jusqu'à votre point d'accueil si vous vous tenez sur votre propre île, et n'importe où d'autre en mer, il vous dit le **gisement et la distance** de la maison plutôt que de vous donner une course. Rien dans TradeWinds ne téléporte la cargaison.

La référence complète des commandes est [ici](Commands.md).

## ⚙️ Configuration

Tout ce qui a trait au gameplay se trouve dans `config.yml`, introduit étape par étape avec des commentaires expliquant *pourquoi* chaque défaut est ce qu'il est. Le seul paramètre que chaque administrateur devrait examiner avant le lancement :

```yaml
ocean:
  # La graine de l'océan. Chaque position d'île, type, bande de sécurité, biome, nom et
  # coût de route découlent déterministement de ce seul nombre - partagez-le et un autre
  # serveur obtient le même océan commercial. 0 signifie : utiliser la graine du monde.
  seed: 20260729
```

Autres sections qui méritent un coup d'œil : `boats` (l'échelle des coques et les prix), `travel.warp` (coût du carburant et chance de mauvais tir), `ranks` (l'échelle de Marin), `claims` (le prix d'une île de joueur), `crime` (la couche entière de la loi a un commutateur maître), et `encounters`.

## 📄 Plus de documentation

- **[Le Manuel du Marin](Gameplay.md)** — le guide complet de gameplay : commerce, bateaux, cartes, réclamation, crime et l'Interstice. Lisez celle-ci pour voir ce que vos joueurs verront.
- **[Commandes](Commands.md)** — chaque commande de joueur et d'administrateur.
- **[Permissions](Permissions.md)** — chaque nœud de permission et sa valeur par défaut.
- **[Espaces réservés](Placeholders.md)** — espaces réservés de rang et de classement pour les tableaux de bord.

## Traductions

{{ translations("TradeWinds") }}
