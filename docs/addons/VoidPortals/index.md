# VoidPortals

**VoidPortals** permet aux joueurs de voyager entre les dimensions en tombant dans le vide. Lorsqu'un joueur tombe dans le vide dans un monde où l'indicateur est activé, il est téléporté en toute sécurité vers l'emplacement correspondant dans la dimension suivante — **Surmonde → Nether → l'End → Surmonde** — au lieu de mourir.

Créé et maintenu par [BONNe](https://github.com/BONNe).

{{ addon_description("VoidPortals", beta=True) }}

!!! info "Compatibilité"
    Nécessite **BentoBox 3.14.0** ou plus récent, **Minecraft 1.21+**, et **Java 21**.

## Installation

1. Placez le fichier jar de l'addon dans le dossier des addons du plugin BentoBox.
2. Redémarrez le serveur.
3. L'indicateur « Téléportation du monde du vide » est **désactivé par défaut** — activez-le par monde dans le panneau des paramètres d'administration du mode de jeu.

## Indicateurs

VoidPortals ajoute un unique indicateur de paramètre de monde. Activez-le par monde depuis le panneau des paramètres d'administration du mode de jeu.

{{ flags_source("VoidPortals", "WORLD_SETTING") }}

## Traductions

{{ translations("VoidPortals") }}

??? note "Nouveautés de la v1.6.1"
    **Publié le :** 2026-06-01

    Une version de correction de bugs. Voir les notes complètes de la [Release v1.6.1](https://github.com/BentoBoxWorld/VoidPortals/releases/tag/1.6.1).

    - La chute dans le vide ne vous tue plus à l'arrivée. Tomber dans le vide accumulait une vélocité vers le bas qui se transmettait à travers la téléportation, vous projetant au sol au moment de votre arrivée dans la dimension suivante. Votre vélocité et votre distance de chute sont désormais réinitialisées à l'arrivée, vous atterrissez donc en toute sécurité.

??? warning "Nouveautés de la v1.6.0 — Changements majeurs"
    **Publié le :** 2026-06-01

    Première version depuis 2019 — VoidPortals est entièrement modernisé pour l'écosystème BentoBox actuel. Voir les notes complètes de la [Release v1.6.0](https://github.com/BentoBoxWorld/VoidPortals/releases/tag/1.6.0).

    - 🔺 **Nécessite Java 21, Paper 1.21.11 et BentoBox 3.14.0** (auparavant Spigot 1.13.2 / BentoBox 1.5.0). Cette version ne se chargera pas sur des serveurs plus anciens.
    - Livre désormais un `Pladdon` et un `plugin.yml` afin que le jar se charge correctement sur les serveurs Paper modernes.
    - 🔡 Ajout de 14 nouvelles langues et conversion de chaque fichier de langue au format **MiniMessage**. Si vous avez personnalisé les fichiers de langue, régénérez-les ou reportez vos modifications — les anciens codes couleur `&` ne sont plus utilisés.
    - Ajout d'une suite de tests JUnit 5 / MockBukkit, comprenant un test de régression garantissant que les chutes diagonales dans le vide téléportent toujours.
