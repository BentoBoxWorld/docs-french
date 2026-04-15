# DimensionalTrees

**DimensionalTrees** est un addon qui fait en sorte que les arbres qui poussent dans le Nether/End deviennent un arbre de cette dimension.

Créé par [Awakened-Redstone](https://github.com/Awakened-Redstone) et maintenu par [tastybento](https://github.com/tastybento).

{{ addon_description("DimensionalTrees") }}

## Configuration

Le `config.yml` le plus récent est disponible [ici](https://github.com/BentoBoxWorld/DimensionalTrees/blob/develop/src/main/resources/config.yml).

Chaque emplacement de matériau (`logs` / `leaves`) accepte maintenant une **carte pondérée `material: weight`** au lieu d'une simple chaîne. Lorsque la somme des poids vaut exactement 100, les probabilités s'appliquent telles quelles ; au-delà de 100, elles sont mises à l'échelle proportionnellement ; en dessous de 100, le reste est laissé en AIR. Dans les deux cas, un avertissement est consigné dans les logs au démarrage.

```yaml
nether:
  logs:
    gravel: 80
    netherrack: 20
  leaves:
    glowstone: 70
    soul_sand: 30
```

Ordre de résolution quand un arbre pousse : **surcharge par espèce d'arbre → surcharge par mode de jeu → valeur globale par défaut**.

??? note "nether.logs / end.logs"
    Matériau(x) de remplacement global pour les rondins d'arbres dans le Nether / End. Accepte soit un nom de matériau unique (ancienne syntaxe), soit une carte pondérée.

??? note "nether.leaves / end.leaves"
    Matériau(x) de remplacement global pour les feuilles d'arbres dans le Nether / End.

??? note "nether.per-tree / end.per-tree"
    Surcharges facultatives par espèce. Permet d'attribuer à `oak`, `acacia`, `birch`, `jungle`, `spruce` et `dark_oak` leurs propres cartes `logs` / `leaves`. Les entrées manquantes ou invalides reviennent silencieusement aux valeurs globales.

??? note "nether.per-gamemode / end.per-gamemode"
    Surcharges facultatives par mode de jeu BentoBox, utiles si vous faites tourner plusieurs modes de jeu côte à côte (par exemple BSkyBlock + CaveBlock). Le mode de jeu est résolu au moment de l'événement via `IWM.getAddon(world)`.

!!! tip "Migration automatique depuis 1.8.0"
    Les anciennes valeurs en chaîne unique (par exemple `logs: gravel`) sont automatiquement converties vers la nouvelle forme de carte pondérée (`logs: {gravel: 100}`) au premier démarrage avec 1.9.0. Un message de confirmation est écrit dans les logs ; aucune édition manuelle n'est nécessaire.

## Journal des modifications

??? note "Nouveautés dans v1.9.0 — Surcharges par arbre, par mode de jeu et matériaux pondérés"
    **Publié :** 14 avril 2026

    - ⚙️ **Surcharges par espèce d'arbre** — configurez des remplacements de rondins/feuilles distincts pour chacune des six espèces d'arbres dans le Nether et l'End (`per-tree.logs`, `per-tree.leaves`).
    - ⚙️ **Surcharges par mode de jeu** — les serveurs faisant tourner plusieurs modes de jeu BentoBox peuvent désormais configurer des remplacements différents par mode (`per-gamemode.logs`, `per-gamemode.leaves`).
    - ⚙️ 🔺 **Mélange pondéré de plusieurs matériaux** — chaque emplacement de matériau accepte une carte `material: weight` pour mélanger plusieurs types de blocs.
    - ⚙️ **Migration automatique de la configuration** — les anciennes valeurs en chaîne unique de 1.8.0 sont converties en silence vers la nouvelle carte pondérée au premier démarrage.
    - Mise à jour vers Java 21, Paper 1.21.11 et BentoBox 3.14.0. Ajout du support Pladdon pour un packaging compatible standalone.
    - Ajout d'une suite de tests JUnit 5 + MockBukkit.
    - Remplacement de `Material.matchMaterial` (déprécié) par l'API Registry moderne.
    - 🔡 Mise à jour des fichiers de locale pour utiliser les codes couleur MiniMessage dans les messages d'erreur.

    [Release v1.9.0](https://github.com/BentoBoxWorld/DimensionalTrees/releases/tag/1.9.0)

## Traductions

{{ translations("DimensionalTrees") }}
