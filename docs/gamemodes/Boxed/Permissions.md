# Permissions Boxed

| **Permission**                          | **Autoriser pour** | **Description**                                                |
|------------------------------------------|----------------|----------------------------------------------------------------|
| boxed.admin.clearresetall                | op             | Autoriser la suppression de la limite de réinitialisation de toutes les îles des joueurs             |
| boxed.admin.delete                       | op             | Autoriser un joueur à supprimer complètement un joueur (y compris l'île)      |
| boxed.admin.deleteisland                 | op             | Autoriser un joueur à supprimer complètement l'île sur laquelle se trouve le joueur      |
| boxed.admin.noban                        | op             | Le joueur ne peut pas être banni d'une île                         |
| boxed.admin.noexpel                      | op             | Le joueur ne peut pas être expulsé d'une île                       |
| boxed.admin.purge                        | op             | Autoriser un joueur à purger les anciennes îles                  |
| boxed.admin.register                     | op             | Autoriser un joueur à enregistrer l'île la plus proche auprès d'un autre joueur      |
| boxed.admin.reload                       | op             | Recharger le config.yml                                           |
| boxed.admin.reserve                      | op             | Réserver un emplacement vide pour la prochaine île d'un joueur               |
| boxed.admin.setlanguage                  | op             | Réinitialiser les langues de tous les joueurs et définir la langue par défaut       |
| boxed.admin.setrange                     | op             | Autoriser la définition de la plage de protection de l'île                      |
| boxed.admin.setspawn                     | op             | Autoriser l'utilisation des outils de spawn                                       |
| boxed.admin.settingsreset                | op             | Réinitialiser tous les paramètres de protection de l'île à la valeur par défaut           |
| boxed.admin.tp                           | op             | Autoriser la téléportation vers une île                                    |
| boxed.admin.tpuser                       | op             | Autoriser la téléportation d'un joueur vers l'île d'un autre joueur          |
| boxed.admin.getrank                      | op             | Autoriser la récupération du rang d'un joueur dans sa boîte                  |
| boxed.admin.setrank                      | op             | Autoriser la définition du rang d'un joueur dans sa boîte                    |
| boxed.admin.version                      | op             | Afficher les versions de BentoBox et des addons                          |
| boxed.admin.blueprint                    | op             | Autoriser la manipulation des blueprints                               |
| boxed.admin.blueprint.load               | op             | Charger le blueprint dans le presse-papiers                               |
| boxed.admin.blueprint.paste              | op             | Coller le presse-papiers à votre emplacement                            |
| boxed.admin.blueprint.origin             | op             | Définir l'origine du blueprint à votre position                     |
| boxed.admin.blueprint.copy               | op             | Copier le presse-papiers défini par pos1 et pos2                         |
| boxed.admin.blueprint.save               | op             | Enregistrer le presse-papiers copié                                       |
| boxed.admin.blueprint.rename             | op             | Renommer un blueprint                                              |
| boxed.admin.blueprint.delete             | op             | Supprimer le blueprint                                            |
| boxed.admin.blueprint.pos1               | op             | Définir le 1er angle du presse-papiers cubique                              |
| boxed.admin.blueprint.pos2               | op             | Définir le 2ème angle du presse-papiers cubique                              |
| boxed.admin.blueprint.list               | op             | Lister les blueprints disponibles                                       |
| boxed.admin.range                        | op             | Commande de portée de boîte admin                                         |
| boxed.admin.range.display                | op             | Afficher/masquer les indicateurs de portée de la boîte                     |
| boxed.admin.range.set                    | op             | Définir la plage de protection de la boîte                       |
| boxed.admin.range.reset                  | op             | Réinitialiser la plage protégée à la valeur par défaut mondiale                 |
| boxed.admin.range.add                    | op             | Augmenter la plage de protection de la boîte                            |
| boxed.admin.range.remove                 | op             | Diminuer la plage de protection de la boîte                            |
| boxed.admin.resets                       | op             | Modifier les valeurs de réinitialisation du joueur                                        |
| boxed.admin.resets.set                   | op             | Définir le nombre de réinitialisations de l'île d'un joueur              |
| boxed.admin.resets.add                   | op             | Ajouter au nombre de réinitialisations de l'île du joueur                            |
| boxed.admin.resets.remove                | op             | Réduire le nombre de réinitialisations de l'île du joueur                |
| boxed.admin.delete                       | op             | Supprimer l'île d'un joueur et régénérer sa boîte                      |
| boxed.admin.why                          | op             | Basculer le rapport de débogage de protection console                       |
| boxed.admin.deaths                       | op             | Modifier les décès des joueurs                                          |
| boxed.admin.deaths.reset                 | op             | Réinitialiser les décès du joueur                                      |
| boxed.admin.deaths.set                   | op             | Définir les décès du joueur                                        |
| boxed.admin.deaths.add                   | op             | Ajouter des décès au joueur                                      |
| boxed.admin.deaths.remove                | op             | Retirer des décès au joueur                                |
| boxed.admin.setspawnpoint                | op             | Définir l'emplacement actuel comme point de spawn pour cette île             |
| boxed.admin.resetflags                   | op             | Réinitialiser tous les paramètres de drapeaux de l'île au config.yml par défaut        |
| boxed.admin.level                        | op             | Calculer le niveau de l'île pour un joueur                           |
| boxed.admin.top                          | op             | Afficher la liste du top dix                                           |
| boxed.admin.top.remove                   | op             | Retirer un joueur du Top Dix                                      |
| boxed.admin.levelstatus                  | op             | Afficher le nombre d'îles dans la file d'attente pour analyse             |
| boxed.admin.level.sethandicap            | op             | Définir ou modifier le handicap de l'île                               |
| boxed.admin.stats                        | op             | Afficher les statistiques sur les îles de ce serveur                    |
| boxed.mod.bypasscooldowns                | op             | Autoriser le modérateur à ignorer les délais d'attente                             |
| boxed.mod.bypassdelays                   | op             | Autoriser le modérateur à ignorer les délais                                |
| boxed.mod.bypassexpel                    | op             | Autoriser le modérateur à ignorer l'expulsion de l'île                      |
| boxed.mod.bypasslock                     | op             | Ignorer un verrouillage d'île                                         |
| boxed.mod.bypassban                      | op             | Ignorer le bannissement de l'île                                             |
| boxed.mod.switch                         | op             | Autoriser le modérateur à basculer la protection bypass                 |
| boxed.mod.bypassprotect                  | op             | Autoriser le modérateur à ignorer la protection de l'île                     |
| boxed.mod.clearreset                     | false          | Autoriser la suppression de la limite de réinitialisation de l'île                            |
| boxed.mod.info                           | op             | Permettre à un modérateur de voir les informations d'un joueur et de son île                 |
| boxed.mod.lock                           | op             | Verrouiller ou déverrouiller une île                                      |
| boxed.mod.resethome                      | op             | Autoriser la définition ou la réinitialisation de la position d'accueil d'un joueur         |
| boxed.mod.name                           | false          | Autoriser le nommage des îles d'un joueur                              |
| boxed.mod.resetname                      | false          | Autoriser la réinitialisation des noms des îles d'un joueur                          |
| boxed.mod.team                           | false          | Autoriser la modification des équipes via les commandes kick et add         |
| boxed.mod.tp                             | op             | Autoriser la téléportation vers une île                                    |
| boxed.island                             | true           | Autoriser l'utilisation de la commande d'île                                      |
| boxed.island.ban                         | true           | Autoriser le bannissement de visiteurs                                      |
| boxed.island.create                      | true           | Autoriser la création d'une île                                           |
| boxed.island.expel                       | true           | Autoriser l'expulsion de visiteurs                                      |
| boxed.island.home                        | true           | Autoriser la téléportation vers l'île du joueur                              |
| boxed.island.info                        | true           | Permettre au joueur d'utiliser la commande d'information de l'île                      |
| boxed.island.language                    | true           | Le joueur peut sélectionner une langue                                    |
| boxed.island.lock                        | false          | Autoriser le verrouillage de l'île                                           |
| boxed.island.name                        | true           | Le joueur peut définir le nom de son île                         |
| boxed.island.number                      | false          | x définit le nombre d'îles que le joueur peut créer                     |
| boxed.island.reset                       | true           | Le joueur peut utiliser la commande de réinitialisation ou de redémarrage de l'île              |
| boxed.island.sethome                     | true           | Permettre au joueur d'utiliser la commande sethome                          |
| boxed.island.settings                    | true           | Le joueur peut voir les paramètres du serveur                                  |
| boxed.island.spawn                       | true           | Le joueur peut utiliser la commande spawn de l'île si le spawn existe         |
| boxed.island.team.*                      | true           | Permettre à un joueur d'utiliser toutes les commandes d'équipe (Recommandé)                |
| boxed.island.team                        | true           | Permettre à un joueur d'utiliser la commande d'équipe                                   |
| boxed.island.team.invite                 | true           | Permettre à un joueur d'inviter d'autres                                      |
| boxed.island.team.accept                 | true           | Le joueur peut accepter les invitations d'équipe                                  |
| boxed.island.team.reject                 | true           | Le joueur peut rejeter les invitations d'équipe                                  |
| boxed.island.team.coop                   | true           | Permettre à un joueur de rendre d'autres joueurs coop                                 |
| boxed.island.team.trust                  | true           | Permettre à un joueur de faire confiance à d'autres joueurs                                 |
| boxed.island.team.promote                | true           | Permettre à un joueur de promouvoir d'autres                                      |
| boxed.island.team.kick                   | true           | Permettre à un joueur de retirer un autre joueur de son équipe                |
| boxed.island.team.leave                  | true           | Permettre à un joueur de quitter une équipe                                   |
| boxed.island.team.setowner               | true           | Permettre à un joueur de définir un autre joueur comme propriétaire de l'île              |
| boxed.settings.*                         | true           | Autoriser l'utilisation des paramètres sur l'île.                                |
| boxed.team.maxsize.[NUMBER]              | false          | Permettre à un joueur d'avoir une taille d'équipe plus grande que la valeur par défaut          |
| boxed.island.maxhomes.[NUMBER]           | false          | Permettre à un joueur d'avoir plus de maisons que la valeur par défaut                 |
| boxed.island.range.[NUMBER]              | false          | Permettre à un joueur d'avoir une plage de protection plus grande que la valeur par défaut. Non recommandé pour Boxed! |
