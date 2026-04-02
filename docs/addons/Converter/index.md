# Addon du convertisseur ASkyBlock vers BSkyBlock

## Compatibilité

Le convertisseur devrait être utilisé avec la dernière version de BentoBox et BSkyBlock. Le convertisseur est un addon que vous téléchargez et placez dans le dossier des addons de BentoBox. Pour exécuter la conversion, lisez toutes ces instructions.

## Introduction

Le convertisseur prend les fichiers de données ASkyBlock et crée de nouvelles versions dans la base de données BSkyBlock/BentoBox. Les éléments suivants sont convertis :

* Joueurs et équipes
* Îles
* Panneaux de téléportation
* La plupart des paramètres Config.yml
* Défis

Les éléments suivants ne sont pas convertis :

* Schematics - non supportés dans BSkyBlock. Utilisez les blueprints BentoBox à la place.
* Biomes - non supportés dans BSkyBlock lui-même. Utilisez le addon Biomes à la place.
* Magic Cobblestone - non supportés dans BSkyBlock lui-même. Un addon pour ceci est en cours.
* Paramètres d'eau acide ou de pluie - non supportés dans BSkyBlock.
* Chat d'équipe - non supporté dans BSkyBlock.
* Conversion de coopération - les coops sont gérées différemment dans BSkyBlock, donc ils devront être refaits manuellement par les joueurs.
* Paramètres liés au niveau - non supportés dans BSkyBlock lui-même. Utilisez le addon Level.

## Sauvegarde

**Avertissement!** Ce logiciel est fourni TEL QUEL sans garantie. Utilisez-le à vos risques et périls et assurez-vous de faire une copie de sauvegarde de vos fichiers et dossiers de serveur. C'est très important de le faire!

## Préparation de la conversion

**Remarque:** Aucune modification n'est apportée au monde ASkyBlock sauf par la mise à niveau du serveur vers la dernière version. Vous utiliserez le même monde qu'avant avec BSkyBlock après la conversion. Cela signifie qu'il aura le même nom.

Si votre serveur actuel fonctionne sur 1.12.2, vous devez mettre à niveau votre serveur vers la dernière version de Minecraft.

## Étapes

**Remarque:** que si votre monde est GRAND, vous devrez modifier le délai d'expiration du serveur afin que le minuteur de chien de garde n'arrête pas le serveur pendant la conversion.

*Vous vous souvenez de faire une sauvegarde de vos données, n'est-ce pas?*

0. Modifiez spigot.yml et modifiez **timeout-time:** en quelque chose de grand, comme 60000 pour empêcher le minuteur de chien de garde d'arrêter le serveur pendant la conversion.
1. Arrêtez le serveur et ajoutez le fichier jar Spigot 1.14.4 (ou ultérieur) à votre dossier de serveur.
2. Supprimez le ASkyBlock.jar de votre dossier de plugins. NE supprimez PAS le dossier ASkyBlock ou les mondes.
3. Installez BentoBox Version 1.12.0 (ou supérieur) dans votre dossier de plugins.
4. Démarrez le nouveau serveur avec l'option **--forceUpgrade**. Cela mettra à niveau tous vos mondes vers le nouveau format.
5. Une fois que tout est entièrement chargé et que vous voyez le logo BentoBox, arrêtez le serveur.
6. Placez le addon **BSkyBlock**, le addon **Challenges**, le addon **Warps** et le addon **Converter** dans le dossier des addons de BentoBox.
7. Redémarrez le serveur, à nouveau avec l'option **--forceUpgrade**.
8. Une fois que le serveur est chargé et que vous voyez le logo BentoBox, démarrez la conversion dans la console en entrant: **bsb convert**.
9. Une fois la conversion terminée, arrêtez le serveur. **TRÈS IMPORTANT. ARRÊTEZ LE SERVEUR! NE PAS RECHARGER!!!** Cela enregistrera le générateur de monde correct.
10. Modifiez le config.yml de BSkyBlock comme bon vous semble dans les paramètres.
11. Modifiez spigot.yml et retournez **timeout-time:** à quelque chose de petit, comme 60.
12. Supprimez le addon convertisseur et les dossiers du monde BSkyBlock par défaut qui ont été créés.
13. Redémarrez le serveur. Vous n'avez pas besoin d'utiliser l'option forceUpgrade plus longtemps. L'addon BSkyBlock utilisera le monde ASkyBlock.

**Remarque:** Bentobox utilise PAPI ou MVdW pour les placeholders. Si vous êtes intéressé par l'utilisation de placeholders, lisez la documentation sur les placeholders.

**Remarque:** Challenges et Warps ne sont pas nécessaires. Le convertisseur peut fonctionner sans eux, mais les données ne seront pas converties.
