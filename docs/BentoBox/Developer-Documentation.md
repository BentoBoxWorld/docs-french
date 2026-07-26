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

# Événements annulables de réinitialisation de joueur

*Ajouté dans BentoBox 3.17.0.*

Quand un joueur quitte une équipe ou que son île est réinitialisée, BentoBox peut vider son inventaire, son coffre de l'End, son argent, sa santé, sa faim et son XP, et déclasser ses animaux apprivoisés — selon les paramètres `island.reset.on-leave` de chaque mode de jeu. Chacune de ces actions de réinitialisation déclenche désormais un événement **annulable** **avant** son exécution, de sorte qu'un addon peut opposer son veto à une réinitialisation individuelle au lieu de tout ou rien. Si un écouteur annule l'événement, BentoBox ignore cette action.

Ces événements se trouvent dans `world.bentobox.bentobox.api.events.player` :

| Événement | Déclenché avant |
| --- | --- |
| `PlayerTamedRemovalEvent` | le déclassement des animaux apprivoisés du joueur |
| `PlayerResetEnderChestEvent` | le vidage du coffre de l'End |
| `PlayerResetInventoryEvent` | le vidage de l'inventaire |
| `PlayerResetMoneyEvent` | le retrait du solde du joueur |
| `PlayerResetHealthEvent` | la réinitialisation de la santé |
| `PlayerResetHungerEvent` | la réinitialisation de la faim |
| `PlayerResetExpEvent` | la réinitialisation de l'XP |

Tous les événements étendent `PlayerBaseEvent` (qui implémente `Cancellable`) et portent l'UUID du joueur, l'île et le monde. L'écoute est du Bukkit standard :

```java
@EventHandler
public void onInventoryReset(PlayerResetInventoryEvent e) {
    if (shouldKeepInventory(e.getPlayerUUID())) {
        e.setCancelled(true); // l'inventaire ne sera pas vidé
    }
}
```

Les événements sont construits et distribués via une petite API de builder :

```java
PlayerEvent.builder()
    .reason(PlayerEvent.Reason.INVENTORY_RESET)
    .involvedPlayer(uuid)
    .island(island)
    .world(world)
    .build();
```

C'est purement additif — toutes les classes sont nouvelles et aucune API existante n'a changé, donc la 3.17.0 est compatible binairement avec les addons existants. L'[addon Inventory Switcher](../addons/InvSwitcher/index.md) utilise ces événements pour protéger les inventaires et soldes par monde lors des réinitialisations. Voir [Release 3.17.0](https://github.com/BentoBoxWorld/BentoBox/releases/tag/3.17.0).

# Boîtes de dialogue modales

*Ajouté dans BentoBox 3.21.0.*

`world.bentobox.bentobox.api.dialogs` encapsule le système de boîtes de dialogue modales de Paper, qui nécessite **Minecraft 26 ou une version ultérieure**. Les boîtes de dialogue viennent compléter l'API Panels : un panneau est un inventaire que le joueur peut refermer d'un clic, une boîte de dialogue est une fenêtre modale à laquelle le joueur doit répondre. Le cœur les utilise pour les confirmations de commandes, le sélecteur de destination de `/island go`, les invitations d'équipe et le choix du mode de jeu à la première connexion.

| Classe | Rôle |
| --- | --- |
| `Dialogs` | `Dialogs.isSupported()` — indique si ce serveur peut afficher des boîtes de dialogue |
| `DialogBuilder` | Builder fluide : `title`, `body`, `escapable`, `pause`, `confirmation`, `button`, `build` |
| `DialogButton` | Un libellé, une infobulle facultative et un gestionnaire de clic `Consumer<User>` |
| `BBDialog` | La boîte de dialogue construite — `show(User)` pour l'afficher |

`title(...)`, `body(...)` et `DialogButton.of(...)` acceptent chacun soit un `Component` Adventure, soit un `User` accompagné d'une référence de locale (avec des variables facultatives), de sorte que le texte des boîtes de dialogue est traduit comme le reste de votre addon. Tout est basé sur `Component` de bout en bout, donc les actions de clic sont préservées.

```java
if (!Dialogs.isSupported()) {
    // Serveur antérieur à la 26 : repli sur votre flux en chat ou en panneau
    askInChat(user);
    return;
}
new DialogBuilder()
    .title(user, "myaddon.confirm.title")
    .body(user, "myaddon.confirm.body", "[name]", island.getName())
    .confirmation(
        DialogButton.of(user, "myaddon.confirm.yes", u -> doTheThing(u)),
        DialogButton.of(user, "myaddon.confirm.no", u -> u.sendMessage("myaddon.confirm.cancelled")))
    .build()
    .show(user);
```

!!! warning "Prévoyez toujours un repli"
    Vérifiez `Dialogs.isSupported()` et conservez votre comportement précédent en chat ou en panneau pour les serveurs plus anciens, exactement comme le fait le cœur. Les gestionnaires de clic des boutons s'exécutent sur le thread principal, ils peuvent donc utiliser directement l'API Bukkit.

Voir [Release 3.21.0](https://github.com/BentoBoxWorld/BentoBox/releases/tag/3.21.0).
