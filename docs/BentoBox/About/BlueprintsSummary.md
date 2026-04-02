# Blueprints (Îles de Démarrage Personnalisées)

Quand un joueur crée une nouvelle île, BentoBox colle une île de démarrage pré-construite pour eux. Ces modèles s'appellent **Blueprints**. Par défaut, chaque mode de jeu est livré avec une île de démarrage basique, mais vous pouvez concevoir la vôtre.

## Pourquoi Personnaliser Votre Île de Démarrage ?

- Donnez à votre serveur un look et un ressenti uniques
- Contrôlez exactement les ressources avec lesquelles les joueurs commencent
- Créez différents niveaux de difficulté (démarrage facile, démarrage difficile) que les joueurs peuvent choisir
- Ajoutez des panneaux de bienvenue et des conseils pour les nouveaux joueurs

## Comment Ça Marche en Bref

Les Blueprints sont créés entièrement dans le jeu. Le processus de base est :

1. Construisez l'île que vous voulez que les joueurs commencent quelque part dans le monde.
2. Utilisez les commandes administrateur Blueprint pour sélectionner la zone, la copier et la sauvegarder.
3. Utilisez le Gestionnaire de Blueprint pour l'assigner à un **Bundle** (un ensemble nommé d'îles de démarrage).
4. Les joueurs verront les bundles disponibles quand ils créent une nouvelle île et peuvent en choisir un.

Vous pouvez avoir différents blueprints pour l'Overworld, le Nether et la Fin, tous dans le même bundle.

!!! tip
    Gardez les îles de démarrage petites. Le plaisir des jeux de type Skyblock est dans la lutte pour grandir. Trop de ressources au début supprime le défi.

## Gestionnaire de Blueprint

Le Gestionnaire de Blueprint est une interface graphique en jeu ouverte avec :
```
/[admin_command] blueprint
```

De là, vous pouvez créer de nouveaux bundles, assigner des blueprints, définir des icônes, ajouter des descriptions et exiger une permission pour des bundles spécifiques (par ex. une île de démarrage VIP).

## Performance

Le collage de Blueprint se fait de manière asynchrone — cela ne gèlera pas votre serveur peu importe la taille du blueprint. Si vous remarquez un lag lors de la création d'île, réduisez le paramètre `paste-speed` dans le `config.yml` BentoBox.

## Documentation Complète

Pour les instructions étape par étape, la référence des commandes et les conseils pour travailler avec les schematics WorldEdit, voir la [page Blueprints complète](../Blueprints.md).
