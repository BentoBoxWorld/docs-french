# Vos Premiers 30 Minutes avec BentoBox

Vous avez installé BentoBox et un complément de mode de jeu. Et maintenant ? Ce guide vous guide à travers tout ce que vous devez vérifier et faire avant d'ouvrir votre serveur aux joueurs.

---

## Étape 1 — Confirmez que Tout a Chargé

Démarrez votre serveur et cherchez les messages d'erreur dans la console. Puis exécutez :

```
/bentobox version
```

Vous devriez voir le numéro de version de BentoBox, suivi d'une liste de chaque complément chargé et de ses versions. Si votre complément de mode de jeu apparaît dans cette liste, BentoBox l'a trouvé et chargé correctement.

!!! warning "Si un complément manque de la liste"
    Vérifiez que le fichier `.jar` est dans `plugins/BentoBox/addons/` et **pas** dans `plugins/`. Puis vérifiez la console pour tous les messages d'erreur lors du démarrage. Les causes courantes sont les incompatibilités de versions ou une dépendance manquante.

---

## Étape 2 — Testez la Création d'Île en Tant que Joueur

Rejoignez votre serveur en tant que joueur régulier (utilisez un compte alt ou demandez à un ami) et exécutez la commande de joueur principale du mode de jeu. Pour BSkyBlock :

```
/island
```

Une nouvelle île devrait être créée et vous devriez être téléporté. Si cela fonctionne, la configuration de base est correcte.

Essayez quelques choses à partir de l'île :

- Cassez un bloc ✅ (devrait fonctionner — c'est votre île)
- Placez un bloc ✅
- Vérifiez les informations de votre île : `/island info`

---

## Étape 3 — Testez la Protection

Tenez-vous sur votre île et demandez à un autre joueur (ou utilisez un alt) de visiter. En tant que visiteur, il ne devrait **pas** être capable de :

- Casser des blocs
- Ouvrir des coffres
- Interagir avec la plupart des objets

Si les visiteurs peuvent casser des blocs, vérifiez les drapeaux de protection de l'île. Le propriétaire de l'île ouvre l'interface graphique des paramètres avec :
```
/island settings
```

Et en tant qu'administrateur, vous pouvez ouvrir les paramètres mondiaux avec :
```
/[admin_command] settings
```

---

## Étape 4 — Examinez les Paramètres de Configuration Clé

Avant l'arrivée des joueurs, ouvrez le `config.yml` du mode de jeu (trouvé dans `plugins/BentoBox/addons/[GameMode]/`) et examinez ces paramètres :

| Paramètre | Qu'est-ce qu'il contrôle | Recommandation |
|---|---|---|
| `distance-between-islands` | Espace entre les centres des îles | Définissez ceci **avant** que toute île ne soit créée — cela ne peut pas être changé plus tard |
| `island-protection-range` | Rayon de protection par défaut | Devrait être inférieur à la moitié de la distance ci-dessus pour donner de l'espace à la croissance |
| `reset-limit` | Combien de fois les joueurs peuvent réinitialiser leur île | `-1` pour illimitée, ou un nombre comme `3` |
| `max-team-size` | Nombre maximum de joueurs par équipe d'île | `4` est le défaut ; augmentez pour un jeu plus coopératif |

!!! warning "La distance d'île ne peut pas être changée plus tard"
    Une fois que toute île a été créée, changer `distance-between-islands` causera à BentoBox de refuser de démarrer. Choisissez votre valeur et définissez-la avant d'ouvrir aux joueurs. Le défaut (rayon 400 blocs = 800 blocs entre les centres) fonctionne bien pour la plupart des serveurs.

---

## Étape 5 — Configurez les Permissions

BentoBox utilise le plugin de permissions de votre serveur (comme LuckPerms) pour contrôler ce que les joueurs peuvent faire. Les joueurs recevront généralement un ensemble de permissions par défaut, qui incluent :

```
[gamemode].island.create       # Créer une île
[gamemode].island.home         # Se téléporter à leur île
[gamemode].island.settings     # Ouvrir l'interface graphique des paramètres de l'île
[gamemode].island.team         # Utiliser les commandes d'équipe
```

Remplacez `[gamemode]` par le préfixe du mode de jeu (par ex. `bskyblock`, `acidisland`, `oneblock`).

Pour voir la liste complète des permissions, exécutez :
```
/bentobox perms
```

---

## Étape 6 — Installez les Compléments Recommandés

Un mode de jeu BentoBox nu fonctionne, mais les joueurs s'attendront à quelques extras. Envisagez d'ajouter ceux-ci avant d'ouvrir :

- **Warps** — Les joueurs peuvent créer des panneaux warp sur leur île pour que d'autres puissent facilement les visiter
- **Level** — Calcule un score d'île et affiche un classement ; donne aux joueurs quelque chose vers lequel travailler
- **Challenges** — Donne aux joueurs des tâches et des récompenses ; améliore considérablement la rétention
- **InvSwitcher** — Essentiel si vous gérez plus d'un mode de jeu ou avez d'autres mondes ; garde les inventaires séparés

Téléchargez les compléments à partir de [BentoBoxWorld](https://download.bentobox.world), mettez le `.jar` dans `plugins/BentoBox/addons/`, et redémarrez le serveur.

---

## Étape 7 — Personnalisez Votre Île de Démarrage (Optionnel)

L'île de démarrage par défaut est fonctionnelle mais générique. Pour donner à votre serveur une atmosphère unique, construisez une île de démarrage personnalisée et enregistrez-la en tant que Blueprint.

Résumé rapide :
1. Construisez l'île que vous voulez quelque part dans le monde
2. Utilisez `/[admin_command] blueprint pos1` et `pos2` pour la sélectionner
3. Utilisez `/[admin_command] blueprint copy` puis `save myisland`
4. Ouvrez `/[admin_command] blueprint` pour gérer les bundles

Voir [Blueprints](About/BlueprintsSummary.md) pour la procédure complète.

---

## Étape 8 — Ouvrez aux Joueurs

Vous êtes prêt. Quelques dernières choses à vérifier avant d'annoncer :

- [ ] Testez que les nouveaux joueurs peuvent créer une île sans erreurs - surtout si vous utilisez d'autres plugins
- [ ] Confirmez que la protection fonctionne (les visiteurs ne peuvent pas griffer)
- [ ] Confirmez que le mode de jeu apparaît dans `/bentobox version`
- [ ] Lisez la [FAQ](../FAQ.md) pour les pièges courants

---

## Obtenir de l'Aide

Si quelque chose ne fonctionne pas :

1. Exécutez `/bentobox version` et copiez la sortie
2. Vérifiez la console pour les messages d'erreur
3. Cherchez dans la [FAQ](../FAQ.md)
4. Demandez sur le [Discord BentoBox](https://discord.bentobox.world) — incluez votre sortie `/bentobox version` et les erreurs de console
5. Signalez les bogues à [github.com/BentoBoxWorld/BentoBox/issues](https://github.com/BentoBoxWorld/BentoBox/issues)
