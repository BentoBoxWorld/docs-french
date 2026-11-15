# Guide du Joueur { #player-guide }

Nouveau sur un serveur BentoBox ? Cette page couvre les bases : obtenir votre île, inviter des amis, sécuriser votre île et vous déplacer.

!!! info "La commande de votre serveur"
    Cette page utilise `/island`, la commande pour SkyBlock (BSkyBlock). Les autres modes de jeu ont les leurs : par exemple `/ob` pour OneBlock, `/ai` pour AcidIsland, `/cave` pour CaveBlock. Remplacez-la partout où vous voyez `/island`. Votre serveur a peut-être aussi désactivé certaines fonctionnalités ou modifié les valeurs par défaut.

## Commencer { #get-started }

Tapez **`/island`**.

- Si vous n'avez pas encore d'île, on vous demandera d'en choisir une (s'il y a un choix) puis vous serez téléporté dessus.
- Si vous en avez déjà une, `/island` vous ramène à la maison.

C'est tout. Tout le reste est optionnel.

## Se déplacer { #getting-around }

| Commande | Ce qu'elle fait |
|---|---|
| `/island` ou `/island go` | Vous téléporte à votre île |
| `/island sethome` | Définit votre point de départ où vous vous tenez |
| `/island sethome <name>` | Définit une maison supplémentaire nommée, si votre serveur permet plus d'une |
| `/island go <name>` | Téléporte à une maison nommée |
| `/island homes` | Liste vos maisons |
| `/island spawn` | Vous téléporte au spawn du mode de jeu |
| `/island info` | Affiche les détails de l'île sur laquelle vous vous trouvez |
| `/island near` | Affiche les noms des îles à proximité |

## Jouer avec des amis { #playing-with-friends }

Vous avez deux façons de laisser les amis vous aider.

**Rejoindre en tant qu'équipe.** Les membres de l'équipe partagent l'île de manière permanente.

1. Invitez-les : `/island team invite <name>`. Ils doivent être en ligne.
2. Ils acceptent avec `/island team accept` (ou cliquez sur **Accepter** si une fenêtre pop-up apparaît).

!!! warning "Rejoindre l'île de quelqu'un d'autre"
    Quand vous acceptez une invitation d'équipe, vous **perdez généralement votre propre île**. On vous demandera de confirmer d'abord. Selon le serveur, votre inventaire peut aussi être vidé.

**Laissez-les vous aider sans rejoindre.** Ils gardent leur propre île.

- `/island team trust <name>` : ils peuvent vous aider jusqu'à ce que vous les retiriez avec `/island team untrust <name>`.
- `/island team coop <name>` : ils peuvent vous aider jusqu'à ce que tout le monde dans votre équipe se déconnecte.

Ouvrez **`/island team`** pour voir votre équipe, inviter des joueurs et gérer les rangs à partir d'un menu.

| Commande | Ce qu'elle fait |
|---|---|
| `/island team leave` | Quitter l'équipe. Le propriétaire ne peut pas partir sans donner l'île d'abord |
| `/island team kick <name>` | Retirer un membre |
| `/island team promote <name>` | Donner plus de droits à un membre |
| `/island team demote <name>` | Retirer les droits |
| `/island team setowner <name>` | Donner votre île à un autre membre |

## Sécuriser votre île { #keeping-your-island-safe }

Votre île est protégée. Les visiteurs peuvent regarder autour d'eux mais ne peuvent pas casser des blocs, ouvrir des coffres ni faire du mal à vos animaux sauf si vous le permettez.

Ouvrez **`/island settings`** pour choisir ce que les visiteurs, les joueurs en coopération, les joueurs de confiance et les membres de l'équipe peuvent faire. Cliquez sur un paramètre pour parcourir les rangs autorisés.

| Commande | Ce qu'elle fait |
|---|---|
| `/island settings` | Choisir ce que chaque rang peut faire |
| `/island lock` | Verrouiller votre île pour que les visiteurs ne puissent pas entrer (exécutez à nouveau pour déverrouiller) |
| `/island expel <name>` | Renvoyer un visiteur de votre île |
| `/island ban <name>` | Bannir un joueur de votre île |
| `/island unban <name>` | Lever un bannissement |
| `/island banlist` | Voir qui est banni |

Quelque chose est bloqué et vous ne savez pas pourquoi ? Le message le dit généralement. Demandez au propriétaire de votre île, ou vérifiez `/island settings`.

## Votre île { #your-island }

| Commande | Ce qu'elle fait |
|---|---|
| `/island setname <name>` | Nommer votre île |
| `/island resetname` | Supprimer le nom |
| `/island language` | Changer la langue des messages de BentoBox |
| `/island reset` | Recommencer avec une nouvelle île. **Votre ancienne île est supprimée.** Votre serveur peut limiter le nombre de réinitialisations |

## Extras que votre serveur peut avoir { #extras-your-server-may-have }

Les serveurs ajoutent des fonctionnalités avec des add-ons. Voici quelques-uns courants :

| Commande | Add-on | Ce qu'elle fait |
|---|---|---|
| `/island level` | [Level](../addons/Level/index.md) | Calcule le niveau de votre île |
| `/island top` | [Level](../addons/Level/index.md) | Affiche les meilleures îles |
| `/island challenges` | [Challenges](../addons/Challenges/index.md) | Ouvre le menu des défis |
| `/island warps` | [Warps](../addons/Warps/index.md) | Liste les warps des joueurs ; écrivez `[Welcome]` sur la première ligne d'une pancarte pour ajouter la vôtre |
| `/island bank` | [Bank](../addons/Bank/index.md) | La banque partagée de votre île |
| `/island fly` | [IslandFly](../addons/IslandFly/index.md) | Voler sur votre île |

Tapez `/island help` pour voir chaque commande disponible pour vous.
