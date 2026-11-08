# SkyGrid

Chaque quatrième bloc dans chaque direction est un vrai bloc. Tout le reste est de l'air.

Cela signifie du gravier flottant au-dessus du vide. Des flaques de lave suspendues dans le néant. Un creeper sur un bloc de sable à douze mètres au-dessus de vous. Aller n'importe où nécessite de la planification, de la précision et un respect sain de ce qui se passe si vous manquez un saut.

**SkyGrid** a été créé par SethBling en 2012 et est devenu l'une des meilleures cartes de défi Minecraft jamais faites. Ceci est la version BentoBox — même grille chaotique, s'exécutant désormais en tant qu'expérience d'île multijoueur complète avec toute la progression, les défis et les tableaux de classement que les joueurs attendent.

Créé et maintenu par [tastybento](https://github.com/tastybento).

{{ addon_description("SkyGrid") }}

## Installation

0. Installez BentoBox et exécutez-le sur le serveur au moins une fois pour créer ses dossiers de données.
1. Placez ce jar dans le dossier addons du plugin BentoBox.
2. Redémarrez le serveur.
3. L'addon créera des mondes et un dossier de données contenant un fichier config.yml.
4. Arrêtez le serveur.
5. Modifiez le fichier config.yml selon vos préférences.
6. Supprimez tous les mondes créés par défaut si vous avez apporté des modifications qui les affecteraient.
7. Redémarrez le serveur.

## Permissions

Les permissions peuvent être trouvées [ici](Permissions).

## Commandes

Les commandes peuvent être trouvées [ici](Commands).

## Placeholders

Les placeholders peuvent être trouvés [ici](Placeholders).

## Journal des modifications

??? warning "Nouveautés dans v2.2.4 — correctif de la génération du monde"
    **Publié :** 5 novembre 2026

    Compatibilité : BentoBox API 3.3.1 · Minecraft 1.21.x (testé sur Paper 26.3) · Java 21.

    - 🔺 **La grille n'est plus remplie de pierre et d'herbe.** Le terrain vanilla était généré sous la grille et la génération de surface vanilla remplaçait des blocs par de l'herbe. Les emplacements de la grille ne reçoivent désormais que les blocs de votre configuration. [PR #88](https://github.com/BentoBoxWorld/SkyGrid/pull/88)
    - 🔺 **Les chunks ne se répètent plus.** Chaque chunk partait de la même séquence aléatoire, si bien que le même motif se répétait tous les 16 blocs. Chaque chunk a désormais la sienne. [PR #88](https://github.com/BentoBoxWorld/SkyGrid/pull/88)
    - **La canne à sucre a maintenant de l'eau.** Elle se trouve dans un petit bassin de grès pour que l'eau reste en place. L'eau du bassin peut geler dans les biomes froids. [PR #89](https://github.com/BentoBoxWorld/SkyGrid/pull/89)
    - **Les cactus et les buissons morts ne flottent plus.** Ils reposent désormais sur du sable, posé sur du grès. [PR #89](https://github.com/BentoBoxWorld/SkyGrid/pull/89)

    🔺 **Mondes existants :** les chunks déjà générés ne changent pas, il y aura donc une démarcation visible là où les anciens et les nouveaux chunks se rejoignent. Pour une grille homogène, supprimez vos mondes SkyGrid et laissez-les se régénérer — **cela supprime toutes les îles de ces mondes**, alors planifiez-le avec vos joueurs et faites d'abord une sauvegarde.

    [Release v2.2.4](https://github.com/BentoBoxWorld/SkyGrid/releases/tag/2.2.4)

## Traductions

{{ translations("SkyGrid") }}
