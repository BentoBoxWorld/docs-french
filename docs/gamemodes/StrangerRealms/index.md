# Stranger Realms : Un mode de jeu BentoBox

Une expérience de survie frissonnante où le monde familier est ombragé par une dimension terrifiante et inversée. *Stranger Realms* est un mode de jeu BentoBox personnalisé qui remplace le Nether par une copie noire et déformée du monde principal — le **À l'envers**.

## Concept du jeu : Bienvenue au pays À l'envers

Plongez dans un monde où la réalité est tordue. Inspirée par la dimension frissonnante d'une émission télévisée populaire, la dimension À l'envers est un monde de pénombre constante et de danger.

* **L'inversion :** Le À l'envers est une copie sombre et déformée du monde principal, bloc par bloc. Elle est générée dynamiquement quand un joueur entre pour la première fois dans un endroit de la dimension.
* **Mobs corrompus :** La faune du monde principal a été corrompue. La plupart des mobs du monde principal sont transformés en leurs équivalents du Nether, créant des rencontres uniques et dangereuses.
* **Le scintillement (Lien dimensionnel) :** Attention à ce avec quoi vous interagissez ! Activer un levier ou appuyer sur un bouton au pays À l'envers peut déclencher la même action dans le bloc correspondant du monde principal.

## Commandes

*Stranger Realms* utilise la structure de commande robuste de BentoBox. Les commandes peuvent être trouvées [ici](Commands).

La commande joueur principale est `/strange` ou `/st` et la commande admin est `/stranger`.

## Permissions

Les permissions peuvent être trouvées [ici](Permissions).

??? note "Nouveautés de la v1.0.4"
    **Publié :** 2026-05-16

    Version de correction de bugs pour la bordure dynamique du monde. Voir les notes complètes : [Release 1.0.4](https://github.com/BentoBoxWorld/StrangerRealms/releases/tag/1.0.4)

    - Correction d'une `NullPointerException` sporadique dans `getBorderSize()` lors du premier rétrécissement de la bordure dynamique (par ex. quand le nombre de joueurs baissait) qui spammait la console et bloquait la bordure jusqu'au prochain redémarrage. Le chemin d'annulation utilise désormais le helper `cancelBorderTask()` protégé contre les nulls.
    - L'avertissement de démarrage indiquant de ne pas utiliser l'addon `Border` de BentoBox référençait par erreur "the Crowdbound world" ; il indique maintenant `StrangerRealms has its own Border, so do not use Border addon.`
    - Construit et testé avec l'API Paper 1.21.11 pour suivre la branche de suivi de MockBukkit.

    **Compatibilité :** BentoBox API 3.9.0+, Minecraft 1.21.10+, Java 21.

!!! warning "Nouveautés de la v1.0.5 — Correctif urgent"
    **Publié :** 2026-05-19

    Correctif pour un bug pouvant corrompre les îles d'autres modes de jeu partageant le même serveur. Voir les notes complètes : [Release 1.0.5](https://github.com/BentoBoxWorld/StrangerRealms/releases/tag/1.0.5)

    - 🔺 **Correction de `TeamListener` corrompant la plage des îles d'autres modes de jeu.** Quand un joueur quittait une équipe ou était expulsé, le code de réinitialisation de revendication affectait les îles appartenant à d'autres modes de jeu (par ex. AOneBlock) sur le même serveur. Mettez à niveau immédiatement si vous exécutez StrangerRealms aux côtés d'un autre mode de jeu.

    **Récupération pour les serveurs affectés.** Si une version précédente de StrangerRealms a corrompu les îles d'autres modes de jeu, ces îles échoueront toujours à charger au démarrage avec une erreur `Island distance mismatch`. Pour récupérer, choisissez l'une des options suivantes :

    - Éditez `plugins/BentoBox/database/Island/*.json` et restaurez `range` à la `distance-between-islands` configurée du mode de jeu affecté (par ex. `400` pour AOneBlock / BSkyBlock, `320` pour Boxed), **ou**
    - Supprimez les fichiers JSON d'île concernés si vous acceptez de les perdre.

    **Compatibilité :** BentoBox API 3.9.0+, Minecraft 1.21.10+, Java 21.

## Traductions

{{ translations("StrangerRealms") }}
