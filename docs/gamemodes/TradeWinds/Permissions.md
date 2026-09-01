# Permissions TradeWinds

Les paramètres par défaut sont choisis pour qu'une installation vanilla joue le jeu prévu sans plugin de permissions du tout : tout ce qu'un marin a besoin est `true`, les raccourcis qui contournent la navigation sont `op`, et les vraies portes (rang de réclamation, prix de réclamation) se trouvent dans `config.yml` plutôt que dans les permissions.

## Permissions joueur

| Permission | Description | Défaut |
|------------|-------------|---------|
| `tradewinds.island` | Permettre l'utilisation de la commande du joueur TradeWinds | `true` |
| `tradewinds.island.spawn` | Permettre `/tw go` — la porte dans l'océan, et le chemin de retour dans les règles. De l'extérieur, il ramène le joueur à l'eau qu'il a quittée ; sur sa propre île, il le marche vers son point d'accueil ; n'importe où d'autre en mer, il lui dit la direction et la distance à la maison, jamais une course. | `true` |
| `tradewinds.island.chart` | Permettre la visualisation de la carte (hologrammes à flot, liste à terre) | `true` |
| `tradewinds.island.starchart` | Permettre de recevoir la carte Étoile | `true` |
| `tradewinds.island.rank` | Permettre de voir le rang de Marin et le top dix des îles cartographiées | `true` |
| `tradewinds.island.claim` | Permettre de réclamer un îlot sauvage en tant qu'île personnelle. Les vraies portes sont dans la config — rang de Marin (`claims.minimum-rank`) et prix (`claims.price`) — donc celui-ci reste activé par défaut ; le désactiver pour désactiver entièrement la réclamation. | `true` |
| `tradewinds.island.sethome` | Permettre de définir un point d'accueil sur votre propre île — uniquement en vous tenant à l'intérieur de sa plage de protection (propriétaire ou membre de l'équipe). | `true` |
| `tradewinds.island.home` | Permettre de se téléporter vers votre point d'accueil — uniquement en vous tenant déjà sur votre propre île, donc c'est une commodité autour de la base et jamais un chemin de retour à travers la mer. | `true` |
| `tradewinds.island.unclaim` | Permettre au propriétaire de donner un îlot réclamé retour à l'état sauvage. Requiert que l'équipe soit vidée d'abord ; pas de remboursement ; chaque bloc reste exactement comme il a été laissé. | `true` |
| `tradewinds.island.fine` | Permettre de régler un casier criminel à un port. Activé par défaut — un joueur qui ne peut pas payer off une réputation n'a pas d'autre moyen de retour sauf attendre. | `true` |
| `tradewinds.island.restart` | Permettre de redémarrer la carrière commerciale (plafonnée par la config) | `true` |
| `tradewinds.island.prices` | Permettre le carnet du marchand — quels ports vous avez visités étaient payants, et depuis combien de temps. Les prix n'y entrent qu'en visitant un marché ou en achetant un rapport de port, donc ceci relit la connaissance propre d'un joueur. | `true` |
| `tradewinds.island.info` | Permettre l'utilisation de la commande d'information de l'île | `true` |
| `tradewinds.island.settings` | Permettre la visualisation des paramètres de l'île (l'édition est limitée par rang) | `true` |
| `tradewinds.island.language` | Permettre l'utilisation de la commande de langue | `true` |
| `tradewinds.island.warp` | Raccourci : ouvrir le dialogue de téléportation de n'importe où dans les eaux de l'île. Désactivé par défaut — le chemin prévu est de naviguer jusqu'à la limite de l'île, qui offre le dialogue automatiquement. Accorder pour contourner la navigation. | `op` |
| `tradewinds.island.trade` | Raccourci : ouvrir le marché de n'importe où dans la plage de protection d'une île. Désactivé par défaut — le chemin prévu est de vous amarrer et clic-droit un commerçant sur la plaza. Accorder pour contourner la promenade. | `op` |

## Permissions administrateur

| Permission | Description | Défaut |
|------------|-------------|---------|
| `tradewinds.admin` | Permettre l'utilisation de la commande d'administrateur TradeWinds | `op` |
| `tradewinds.admin.islands` | Permettre de répertorier les îles commerciales les plus proches | `op` |
| `tradewinds.admin.tpisland` | Permettre de se téléporter aux îles commerciales | `op` |
| `tradewinds.admin.boat` | Inspectez les records de bateau d'un joueur — cargaison, carburant, dernière position observée, si une coque est réellement chargée là — et restaurez un bateau actif perdu depuis la base de données en tant qu'article dans son pack. | `op` |
| `tradewinds.admin.rank` | Inspectez ou définissez le rang de Marin d'un joueur — stocke un ajustement au-dessus de leur vrai nombre cartographié, donc la promotion, la rétrogradation et la réinitialisation fonctionnent tous et la porte de réclamation et le classement suivent. | `op` |
| `tradewinds.admin.customs` | Montrez l'état des douanes à votre position (contrebande, probabilités de scan, patrouille) | `op` |
| `tradewinds.admin.priceaudit` | Auditez la couverture des prix et écrivez le rapport dans `price-audit.txt` | `op` |
| `tradewinds.admin.warpfail` | Pirater le prochain téléportation d'un joueur pour échouer, le jeter dans l'interstice | `op` |
| `tradewinds.admin.reflag` | Permettre de ré-appliquer les drapeaux de bande de sécurité à toutes les îles | `op` |
| `tradewinds.admin.*` | Toutes les permissions d'administrateur TradeWinds | `op` |
