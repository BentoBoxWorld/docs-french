# Bienvenue dans la Documentation pour Développeurs BentoBox !

BentoBox est un plugin de plateforme qui supporte une suite d'API pour les Compléments qui s'exécutent dessus. L'architecture est pratiquement identique au système de plugin Bukkit. Vous pouvez créer GameModeAddons comme BSkyBlock qui fournissent aux joueurs votre propre expérience de mode de jeu, ou vous pouvez développer des Compléments utilitaires, comme Warps qui permettent aux joueurs d'utiliser les panneaux warp dans ces modes de jeu.

## Pladdons

En raison des changements dans la façon dont les serveurs fonctionnent (remappage du code lors du chargement), il est maintenant recommandé que tous les Compléments maintenant exécutés à l'intérieur d'une enveloppe de Plugin Bukkit, qui est fournie par BentoBox et appelée Pladdon -
Pladdons = Plugin + Addon. en étant un Plugin, ils seront correctement remappés quand chargés, ce qui est important pour les serveurs comme Paper.

Le travail du wrapper Pladdon est de générer l'instance Addon et de la fournir à chaque fois qu'elle est demandée via la méthode `getAddon`.

En conséquence des Compléments étant des Plugins, ils seront listés comme tels par le serveur, cependant ils doivent toujours être placés dans le dossier `Bentobox/Addons`.

# JavaDocs
Les Javadocs sont ici : [https://javadocs.bentobox.world](https://ci.codemc.io/job/BentoBoxWorld/job/BentoBox/javadoc/)

Le paquet API principal est `world.bentobox.bentobox.api.*`. Les méthodes dans ces paquets sont maintenues aussi stables que possible à long terme. Les méthodes et les classes en dehors du paquet api peuvent changer beaucoup ou plus fréquemment.

# Exemple de Complément

@BONNe maintient un exemple de complément ici : [https://github.com/BONNePlayground/ExampleAddon](https://github.com/BONNePlayground/ExampleAddon)
