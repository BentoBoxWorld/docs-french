BentoBox implémente quelques commandes pour vous aider à gérer votre installation entière de BentoBox.

**Commandes Disponibles (à partir de 2.2.0)**

| Commande                                 | Permission                   | Description                                                 |
|-----------------------------------------|------------------------------|-------------------------------------------------------------|
| /bentobox [help/h]                      | bentobox.admin               | Affiche toutes les commandes BentoBox disponibles                    |
| /bentobox about                         | bentobox.about               | Affiche les informations de copyright et de licence                  |
| /bentobox catalog                       | bentobox.admin.catalog       | Affiche le Catalogue                                        |
| /bentobox locale                        | bentobox.admin.locale        | Effectue l'analyse des fichiers de localisation                    |
| /bentobox manage/overview               | bentobox.admin.manage        | Affiche le Panneau de Gestion                               |
| /bentobox migrate                       | bentobox.admin.migrate       | Migre les données d'une base de données à une autre                  |
| /bentobox perms                         | bentobox.admin.perms         | Affiche les perms effectives pour BentoBox et les Compléments au format YAML |
| /bentobox rank [list \| add \| remove] [rank reference] [rank value] | bentobox.admin.rank | liste, ajoute ou supprime des rangs              |
| /bentobox reload/rl                     | bentobox.admin.reload        | Recharge BentoBox et tous les compléments, les paramètres et les locales       |
| /bentobox version/v/versions/addons     | bentobox.version             | Affiche les versions BentoBox et des compléments                       |

Un alias pour `/bentobox` est `/bbox`.

Lors du dépôt de rapports de bugs ou de la demande de support, vous **devez** fournir la sortie de la commande `/bentobox version` pour que nous sachions quelle version du logiciel, de la base de données et des compléments vous utilisez.
