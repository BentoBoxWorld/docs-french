# Spécification de Blueprint BentoBox

**Version 1**

Les mots clés « MUST », « MUST NOT », « REQUIRED », « SHALL », « SHALL NOT », « SHOULD », « SHOULD NOT », « RECOMMENDED », « MAY » et « OPTIONAL » dans ce document doivent être interprétés tel que décrit dans [RFC 2119](http://www.ietf.org/rfc/rfc2119.txt).

## Introduction

Cette spécification définit un format qui décrit une région (composée de blocs et d'entités) d'un monde [Minecraft](https://minecraft.net) à des fins de sérialisation et de stockage sur disque ou dans une base de données basée sur JSON. Il est conçu pour permettre une compatibilité maximale entre les plates-formes, les versions et les divers états de modification.

L'objectif du format Blueprint BentoBox est de nous donner la possibilité de sérialiser les régions d'un monde Minecraft sur disque ou sur n'importe quelle méthode de stockage choisie par l'utilisateur pour être placées ultérieurement dans le monde, tout en évitant de s'appuyer sur des logiciels ou des plugins tiers pour nous fournir les capacités de sérialisation et de désérialisation.

## Historique des Révisions

| Version | Date | Version de BentoBox | Description
|---|---|---|---|
| 1 | 2019-06-09 | [1.5.0](https://github.com/BentoBoxWorld/BentoBox/releases/tag/1.5.0) | Version initiale, dérivée du format BentoBox Schem
| 1.1 | 2026 | 2.x | Le format de stockage est passé du binaire compressé (zippé) au JSON brut ; `.blueprint` est désormais l'extension principale ; les anciens fichiers `.blu` (zippés) restent chargeables pour assurer la compatibilité ascendante

## Définitions

### <a name="defMaterial"></a>Matériau

Un [Matériau](https://hub.spigotmc.org/javadocs/spigot/org/bukkit/Material.html) est un ID fourni par l'[API Bukkit](https://dev.bukkit.org/) qui définit le type littéral d'un bloc ou d'un objet. Il affecte diverses options de rendu côté client comme la lumière, la transparence ou l'affichage. Ils représentent un raccourci programmatique vers la NamespacedKey correspondante actuelle.

## Spécifications

### Format

La structure spécifiée par cette spécification est persistante à la méthode de stockage choisie par l'utilisateur en utilisant le format [JavaScript Object Notation](https://json.org) (JSON). Depuis BentoBox 2.x, les fichiers Blueprint sont stockés en **JSON brut (non compressé)** avec l'extension `.blueprint`.

Les anciens fichiers Blueprint utilisaient un format binaire compressé (zippé) avec l'extension `.blu`. BentoBox continue de charger les fichiers `.blu` pour la compatibilité ascendante, mais tous les nouveaux Blueprints sauvegardés utilisent le format JSON brut `.blueprint`.

Les fichiers utilisant cette spécification doivent utiliser l'une des extensions de fichier suivantes :
* `.blueprint` — JSON brut (actuel, recommandé)
* `.blu` — JSON zippé/compressé (ancien)

Tous les noms de champs dans la spécification sont **sensibles à la casse**.

### Schéma

#### Champs

| Nom du champ | Type | Description |
|---|---|---|
| name | `String` | Nom d'affichage du Blueprint |
| icon | `String` | [Matériau](#defMaterial) de l'objet représentant le Blueprint en jeu comme une icône |
| attached | `Array` | |
| entities | `Array` | |
| blocks | `Array` | |
| xSize | `integer` | |
| ySize | `integer` | |
| zSize | `integer` | |
| bedrock | `Array` | |
