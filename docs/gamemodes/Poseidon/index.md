# Poseidon

Créé et maintenu par [tastybento](https://github.com/tastybento).

**Poseidon** est une expérience de survie immersive sous-marine pour Minecraft. Échoué après un naufrage mystérieux, vous vous réveillez avec l'étrange capacité de respirer sous l'eau — mais il y a une prise. Comme un requin, vous devez continuer à vous déplacer pour survivre.

Bienvenue dans un monde où l'océan est à la fois votre sanctuaire et votre plus grande menace. Des ruines des profondeurs aux villes de corail fluorescent, Poseidon vous met au défi de survivre, construire et explorer dans un royaume où la mer est votre seule constante — jusqu'à ce que vous osiez mettre un pied sur la terre redoutée et brûlante au-dessus.

## 🐚 Fonctionnalités

- 🧭 **Survie réimaginée** : Continuez à vous déplacer pour rester en vie. L'immobilité invite le danger.
- 🏰 **Construction du royaume sous-marin** : Construisez des châteaux couverts de corail et des villes aquatiques dans les profondeurs.
- ⚔️ **Rencontres défiant** : Affrontez les noyés impitoyables, les monstres marins et les secrets enfouis.
- 🌋 **Le Nether rempli d'eau** : Découvrez une version immergée de l'enfer.
- 📖 **Défis inspirés par une histoire** : Complétez des quêtes multi-niveaux et débloquez des livres mystérieux qui élargissent l'univers de Poseidon.
- 🏝️ **Royaumes de démarrage personnalisés** : Choisissez votre début — épave simple, petit monument, ou un grand domaine couvert de corail.

## 🔧 Instructions de configuration

> Recommandé : Installer aux côtés de l'[addon BentoBox Challenges](https://github.com/BentoBoxWorld/Challenges) pour la pleine fonctionnalité de Poseidon.

1. **Téléchargez et installez l'addon Poseidon.**
2. **Placez-le dans votre dossier `/plugins/BentoBox/addons/`.**
3. **Démarrez votre serveur** – les nouveaux mondes pour Poseidon seront générés automatiquement.
4. **Laissez la pré-génération s'exécuter.** Elle ne fonctionne que lorsqu'aucun joueur n'est en ligne. Plus de chunks sont pré-générés, meilleure est la performance.
5. **Connectez-vous et configurez les défis** :
    - Utilisez `/padmin challenges`
    - Cliquez sur l'icône 🕸️ web pour télécharger les **Défis Poseidon**
6. **Choisissez un royaume de démarrage** :
    - Épave avec corail
    - Épave avec un petit monument
    - Épave avec les petits et grands monuments
    - Personnalisez les royaumes en utilisant `/padmin bp`
7. **(Optionnel)** Modifiez `config.yml` ou utilisez l'interface graphique des paramètres admin.
    - Les modifications majeures peuvent nécessiter la suppression de la base de données et la réinitialisation des mondes.

## ⚠️ Notes

- Le monde du End est actuellement **sous-développé**.
- Des ralentissements peuvent survenir si les royaumes ne sont pas pré-générés. Attendez la fin de la pré-génération avant d'inviter des joueurs.

## ✅ Compatibilité

| Fonctionnalité          | Prise en charge                    |
|---------------------|------------------------------------|
| Version Minecraft   | ✅ 1.21.4+ (incompatible avec les versions antérieures) |
| Version BentoBox    | ✅ 3.3.0 ou ultérieure              |
| Version Java        | ✅ Java 21                         |

## Commande joueur

La commande joueur par défaut est `/poseidon` ou `/po` pour faire court.

## Config.yml

Le fichier config.yml est similaire à d'autres modes de jeu en ce sens qu'il y a une section spécialement pour les paramètres de Poseidon, et d'autres paramètres génériques du monde et de l'île. Dans Poseidon, les îles sont appelées royaumes. Les paramètres Poseidon uniques sont :

```
poseidon:
  air-effect:
    # Le temps qu'un joueur peut passer hors de l'eau sans souffrir en secondes.
    grace-period: 3
    # Dégâts par seconde d'être dans l'air.
    damage: 2
    # Le temps que boire de l'eau préviendra les dégâts de l'air en secondes. Boire de l'eau est le même que boire une potion de respiration aquatique.
    water-effect-time: 30
  # Probabilité que les mobs d'eau ignoreront les enfants de Poseidon. En pourcentage.
  # Facilite le jeu.
  water-mob-ignore: 50
```

## Permissions

Les permissions peuvent être trouvées [ici](Permissions).

## Commandes

Les commandes peuvent être trouvées [ici](Commands).

## Placeholders

Les placeholders peuvent être trouvés [ici](Placeholders).

## Journal des modifications

??? note "Nouveautés dans v1.1.1"
    **Publié :** 28 juin 2026

    Version de correction de bugs — remplaçable direct, pas de modification de configuration ou de locale.

    - 🔺 🐛 **Plantage du serveur corrigé pendant la création du monde sur difficulté Paisible (Paper 26.2).** Le générateur Nether essayait de faire apparaître des monstres (Noyé / Gardien / Gardien Aîné), ce qui n'est pas autorisé sur Paisible et causait un plantage du système de chunk. Les apparitions de monstres sont maintenant ignorées sur Paisible et gardées de façon défensive pour que la génération du monde ne puisse jamais planter.

    [Release v1.1.1](https://github.com/BentoBoxWorld/poseidon/releases/tag/1.1.1)

## Traductions

{{ translations("Poseidon") }}
