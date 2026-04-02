# Tutoriel Vidéo

[![Vignette vidéo](https://i.ytimg.com/vi/01MagYDuOCk/hqdefault.jpg?sqp=-oaymwEjCPYBEIoBSFryq4qpAxUIARUAAAAAGAElAADIQj0AgKJDeAE=&rs=AOn4CLCzVNO0ObSEMOOpYtUEtv4LjsMhBA)](https://www.youtube.com/watch?v=01MagYDuOCk)

# Introduction

BentoBox est un plugin puissant mais spécifique à installer et exécuter sur votre serveur. Nous chez BentoBoxWorld avons discuté longuement de la méthode d'installation la plus conviviale qui correspondrait le mieux aux fonctionnalités déterminantes de BentoBox.

Comparé à la plupart des plugins Spigot, l'installation de BentoBox prendra un peu plus de temps qu'une simple glisser-déposer dans le dossier plugins de votre serveur ; mais les innombrables possibilités qu'elle vous apportera en valent la peine.

Commençons !

***

# Téléchargez BentoBox

Vous pouvez télécharger BentoBox **gratuitement** sur différents sites Web. Les versions officielles peuvent être trouvées sur la page Spigot du plugin ou dans l'[onglet GitHub `Releases`](https://github.com/BentoBoxWorld/bentobox/releases), tandis que les builds de développement **non testés** peuvent être téléchargés depuis [Jenkins](https://ci.codemc.io/job/BentoBoxWorld/job/BentoBox/).

# Configurez BentoBox

Une fois que vous avez téléchargé BentoBox, vous devez le mettre dans le dossier `plugins` de votre serveur. Contrairement à ASkyBlock, il n'y a pas de dépendances requises : BentoBox se connectera automatiquement aux plugins qu'il trouve (comme Vault, PlaceholderAPI, Multiverse-Core, ...) pour étendre sa capacité.

Démarrez votre serveur et attendez que tous les plugins soient complètement activés. Si vous vous connectez à votre serveur, vous remarquerez que BentoBox ne fait rien de spécial. En fait, **BentoBox ne fait rien par lui-même** : il a besoin que vous ajoutiez des [Compléments](https://github.com/BentoBoxWorld/bentobox/wiki/Addons) pour qu'il puisse « apprendre » à gérer par ex. le mode de jeu Skyblock.

Maintenant, éteignez votre serveur. Vous pouvez jeter un coup d'œil au fichier `config.yml` BentoBox.

# Installer les Compléments

Les [Compléments](/BentoBox/Addons) sont ce qui rend BentoBox spécial. Cependant, remarquez que ceux-ci ne sont **pas des plugins** : ils **ne lanceront pas** si vous les mettez juste dans le dossier `plugins`.

Premièrement, vous devez télécharger les Compléments que vous voulez ajouter à votre serveur. Les officiels peuvent être trouvés dans la [liste des dépôts BentoBoxWorld](https://github.com/BentoBoxWorld) et peuvent être téléchargés à partir de leur onglet `Releases` (ou depuis [Jenkins](https://ci.codemc.io/job/BentoBoxWorld/) pour les **non testés** builds de développement). Nous allons configurer un site web à un certain point pour vous rendre plus facile de les télécharger plus tard.

Une fois que vous avez téléchargé tout ce dont vous avez besoin, il vous suffit de les mettre tous dans le dossier `plugins\BentoBox\addons`, de démarrer votre serveur pour que les fichiers de configuration et les dossiers se créent, et enfin de l'éteindre à nouveau pour pouvoir éditer tout ce dont vous avez besoin sans causer de dégâts à votre serveur.

Veuillez noter que les Compléments peuvent parfois être incompatibles avec la version de BentoBox que vous utilisez. Les Compléments Officiels seront **toujours** fournis avec une déclaration claire des versions qu'ils supportent. Cependant, remarquez qu'ils supportent souvent les versions plus récentes sans avoir besoin d'être mis à jour.

# Conclusion

Vous devriez être bon d'aller !
Nous sommes heureux que vous utilisiez notre plugin, et nous espérons que vous l'apprécierez autant que nous apprécions l'améliorer.
