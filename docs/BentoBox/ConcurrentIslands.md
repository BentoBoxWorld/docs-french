# Îles Concurrentes

Bentobox 2.0.0 et ultérieur permettent aux administrateurs de permettre aux joueurs d'avoir plus d'une île par monde. Cette page explique comment cela fonctionne et certaines des implications de l'autorisation.

## Comment Activer

Par défaut, les joueurs ont une île. Le nombre peut être augmenté globalement via le paramètre `island.concurrent-islands` du `config.yml` BentoBox. Cette valeur peut être remplacée par les paramètres de configuration individuels du mode de jeu s'ils offrent également ce paramètre.

## Comment Utiliser

### Création

Si les joueurs sont autorisés à créer plus d'une île, ils peuvent le faire en utilisant la commande `create`, par exemple :

`/island create`

Cela fonctionne de la même manière que toute autre création d'île et le joueur sera généralement téléporté à l'île après sa création.

### Aller aux Îles

Une fois que les joueurs ont plus d'une île, ils peuvent se téléporter entre elles en utilisant la commande `go`, par exemple :

`/island go`

Cette commande affichera tous les foyers nommés qu'il a le joueur selon avec les noms de toutes les îles qu'il possède. Si le joueur a nommé son île en utilisant la commande `setname`, elle sera dans la liste, mais s'il ne l'a pas fait, l'île sera listée par le nom d'île par défaut suivi d'un nombre, par exemple « l'île de tastybento 2 ». Le nombre de l'île peut changer quand le serveur est redémarré, donc les joueurs devraient être encouragés à nommer leurs îles.

### Définition des Foyers

Les joueurs peuvent définir l'emplacement par défaut de leur île en exécutant la commande `sethome`. Si les joueurs ont la possibilité de définir plusieurs foyers, ils peuvent les définir en utilisant la commande `sethome [home name]`. Le nombre maximum de foyers autorisés dans la configuration pour le monde du jeu est partagé entre toutes les îles que le joueur possède.

### Transfert d'Île

La propriété de l'île peut être transférée à d'autres joueurs dans l'équipe en utilisant la commande `setowner`. La propriété ne peut pas être transférée si le propriétaire a déjà atteint le nombre maximum d'îles concurrentes autorisées.

*NOUVEAU :* Quand un joueur transfère la propriété, maintenant quitter automatiquement l'équipe.

### Équipes

- Les équipes sont basées sur l'île et les équipes ne s'étendent pas sur les îles.
- À partir de BentoBox 2.3.0, il y a un paramètre pour permettre aux membres de l'équipe d'avoir leurs propres îles, auquel cas les joueurs peuvent être membres de plusieurs équipes sur différentes îles.

## Support du Mode de Jeu

Tous les modes de jeu doivent supporter les îles concurrentes.

## Support des Compléments

Cela répertorie les compléments et leur compatibilité avec les îles concurrentes. À partir de 2024-04-03 :

| Complément | Commentaires          |
|-------|-------------------|
| Bank 1.7.0 | Les banques sont par île. L'argent ne s'accumule pas entre les îles |
| Biomes 2.1.1 | Compatible |
| Border 4.1.1 | Compatible  |
| CauldronWitchery 2.0.1 |   |
| Challenges 1.2.0 |   |
| Chat 1.1.4 |   |
| CheckMeOut 1.1.1 | Compatible  |
| DimensionalTrees 1.6.0 |   |
| ExtraMobs 1.12 |   |
| Greenhouses 1.7.3 | Compatible  |
| InvSwitcher 1.11.0 | Compatible  |
| IslandFly 1.11.0 | Compatible  |
| Level 2.11.0 | Les niveaux sont calculés par île. Le Top Ten affichera le score pour la dernière île calculée. Si la téléportation est autorisée lors du clic sur la tête Top Ten, les joueurs iront à l'île actuelle du joueur.  |
| Likes 2.3.1 |   |
| Limits 1.19.1 | Compatible. Les limites sont par île.  |
| MagicCobblestoneGenerator 2.5.1 |   |
| TwerkingForTrees 1.4.3 | Compatible  |
| Visit 1.6.0 |   |
| VoidPortals 1.5.0.0 |   |
| Warps 1.13.0 | Comme d'habitude, les joueurs ne peuvent avoir qu'un seul panneau warp actif.   |
