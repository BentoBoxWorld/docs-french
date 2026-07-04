# Bank

**Bank** fournit une **banque d'île** pour permettre aux membres de l'île de partager de l'argent.

Créé et maintenu par [tastybento](https://github.com/tastybento).

{{ addon_description("Bank") }}

## Introduction

Chaque île a un compte bancaire. Les joueurs peuvent déposer ou retirer de l'argent de leurs comptes d'économie réguliers vers le compte d'île où il est mis en commun. Le propriétaire de l'île peut décider quel rang de membre de l'équipe peut accéder au compte via le menu des paramètres. Il existe une commande `baltop` que les joueurs peuvent utiliser pour voir quelle île a le plus, ou le moins d'argent.

### Fonctionnalités

* Économiser ou dépenser de l'argent en équipe d'île
* Concourir pour avoir le solde le plus élevé du jeu
* Voir l'historique complet des transactions du compte

### Exigences
**Bank** nécessite qu'une économie soit installée sur le serveur qui utilise Vault. Idéalement, l'économie devrait être consciente des mondes multiples sinon l'argent pourrait finir par être partagé entre les mondes et les modes de jeu.

## Commandes
### Commandes du joueur

La commande par défaut est `bank` et elle peut être modifiée dans le config.yml. Donc pour utiliser la banque, vous faites `/island bank` par exemple.

* `bank deposit <amount>` - déposer de l'argent dans la banque d'île
* `bank withdraw <amount>` - retirer de l'argent de la banque d'île
* `bank balance` - voir le solde de votre banque d'île
* `bank statement` - voir un relevé élégant des dépôts/retraits, etc. sur votre compte bancaire d'île

### Commandes Admin

La commande admin par défaut est `bank` et elle peut être modifiée dans le config.yml.

Les commandes admin créent de l'argent par magie.
* `bank give <player> <amount>` - déposer de l'argent dans la banque d'île du joueur
* `bank take <player> <amount>` - retirer de l'argent de la banque d'île du joueur
* `bank set <player> <amount>` - définir le solde de la banque d'île du joueur à un montant
* `bank balance <player>` - voir le solde de la banque d'île d'un joueur
* `bank statement <player>` - voir un relevé élégant des dépôts/retraits, etc. sur le compte bancaire d'île du joueur

## Placeholders

Les placeholders peuvent être trouvés [ici](Placeholders).


## Configuration

```
bank:
  # BentoBox GameModes that can use Bank
  game-modes:
  - BSkyBlock
  - AOneBlock
  - AcidIsland
  - SkyGrid
  - CaveBlock
  commands:
    # User command
    user: bank
    # Admin command
    admin: bank
  placeholders:
    # This is how many ranks will be registered with the placeholder API.
    # There are two placeholders per rank:
    # %Bank_[gamemode]_top_name_1% with island level: %Bank_[gamemode]_top_value_1%
    # [gamemode] is bskyblock, acidisland, etc.
    number-of-ranks: 10
```

## Permissions

```
permissions:
  '[gamemode].bank.user':
    description: Le joueur peut utiliser la commande de banque
    default: true
  '[gamemode].bank.user.balance':
    description: Le joueur peut utiliser la commande d'équilibre bancaire
    default: true
  '[gamemode].bank.user.deposit':
    description: Le joueur peut utiliser la commande de dépôt bancaire
    default: true
  '[gamemode].bank.user.withdraw':
    description: Le joueur peut utiliser la commande de retrait bancaire
    default: true
  '[gamemode].bank.user.statement':
    description: Le joueur peut utiliser la commande de relevé bancaire
    default: true
  '[gamemode].bank.user.baltop':
    description: Le joueur peut utiliser la commande baltop de la banque
    default: true
  '[gamemode].bank.admin':
    description: Le joueur peut utiliser la commande admin
    default: op
  '[gamemode].bank.admin.balance':
    description: Le joueur peut utiliser la commande d'équilibre admin
    default: op
  '[gamemode].bank.admin.give':
    description: Le joueur peut utiliser la commande de don admin
    default: op
  '[gamemode].bank.admin.take':
    description: Le joueur peut utiliser la commande de retrait admin
    default: op
  '[gamemode].bank.admin.statement':
    description: Le joueur peut utiliser la commande de relevé admin
    default: op
  '[gamemode].bank.admin.set':
    description: Le joueur peut utiliser la commande de définition admin
    default: op

```

## Aimez cet addon?
Vous pouvez [sponsoriser](https://github.com/sponsors/tastybento) pour obtenir plus d'addons comme celui-ci et l'améliorer!

## Journal des modifications

??? note "Nouveautés dans v1.10.1"
    **Publié :** 21 juin 2026

    Version de correction de bugs — remplaçable sans modification de configuration ou de locale.

    - 🐛 **Bank ne se désactive plus quand l'économie est fournie par un addon.** BentoBox accroche Vault pendant sa phase d'accrochage précoce, avant l'activation des addons. Si aucun plugin d'économie n'avait enregistré de fournisseur à ce moment, cet accrochage précoce était abandonné — donc quand l'économie venait d'un addon (ex. [InvSwitcher](../InvSwitcher/index.md), qui enregistre une économie Vault par monde dans son propre `onEnable()`), Bank ne trouvait pas de fournisseur Vault et se désactivait avec *"Vault est nécessaire"*. Bank réessaye maintenant l'accrochage Vault avant d'abandonner, et déclare `InvSwitcher` comme une `softdepend` pour qu'il s'active en premier quand présent, rendant l'ordre de chargement déterministe.

    [Release v1.10.1](https://github.com/BentoBoxWorld/Bank/releases/tag/1.10.1)

??? note "Nouveautés dans v1.9.1"
    **Publié :** 28 mars 2026

    - **Placeholders de nom d'île pour le classement.** `%Bank_[gamemode]_top_island_<number>%` expose maintenant le nom de l'île (pas seulement le nom du propriétaire) pour chaque position du classement. Les noms d'île sont mis en cache avec les noms de propriétaires et les soldes.
    - ⚙️ Documentation de la composition des intérêts et commentaires de configuration corrigés — le calcul de `compound-periods-per-year` avait une erreur qui causait des intérêts composés légèrement incorrects.

    [Release v1.9.1](https://github.com/BentoBoxWorld/Bank/releases/tag/1.9.1)

## Traductions

{{ translations("Bank") }}
