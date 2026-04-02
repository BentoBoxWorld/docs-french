# Transition de Base de Données
La base de données par défaut pour BentoBox est celle qui enregistre les fichiers sur le système de fichiers en utilisant JSON (elle avait l'habitude d'être YAML, mais depuis 1.5.0 c'est JSON). JSON devrait fonctionner pour la plupart des serveurs. Cependant, il est possible que votre serveur ait grandi au point où avoir la base de données sur une autre machine aidera. Alternativement, vous pouvez avoir d'autres logiciels qui veulent accéder à ces données, par ex., un site web. BentoBox offre la possibilité de migrer vos données d'un type de base de données à un autre de manière transparente. Si vous souhaitez passer de JSON à une autre base de données, vous pouvez le faire facilement en utilisant une option de base de données de transition comme JSON2MYSQL.

## Étapes

1. Arrêtez le serveur
2. Faites une sauvegarde de votre base de données. S'il s'agit d'une base de données de fichier plat, cela signifie copier le dossier de la base de données entière dans un endroit sûr.
3. Éditez le fichier config.yml BentoBox et sélectionnez une option de base de données de transition. Ils ont toujours le chiffre 2 en eux, par exemple JSON2MYSQL.
4. Assurez-vous également d'avoir configuré le nom de la base de données, la connexion et le mot de passe, si nécessaire. Si vous transiez vers MYSQL, vous devez vous assurer que le serveur a la base de données et c'est une version suffisamment récente (5.7 ou ultérieure)
5. Si vous avez une très grande base de données, alors une transition peut prendre plus longtemps que votre délai d'attente du serveur. Donc éditez *spigot.yml* timeout-time et définissez-la à un grand nombre pour que le serveur ne s'écrase pas.
6. Démarrez le serveur. BentoBox transférera immédiatement tous les îles et certains autres fichiers vers la base de données car ceux-ci sont chargés au démarrage.
7. Après que le serveur est complètement actif et fonctionnant, exécutez la commande *bbox migrate* dans la console. Cela copiera tous les joueurs, les noms et toutes les données des compléments dans la base de données.
8. Vous avez terminé !
9. Vous pouvez laisser la base de données comme la base de données de transition, ou vous pouvez maintenant la modifier à l'option de base de données unique, par ex., MYSQL.
