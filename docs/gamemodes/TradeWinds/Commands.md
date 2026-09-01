# Commandes TradeWinds

La commande joueur est **`/tw`** (alias `/tradewinds`) ; la commande administrateur est **`/twadmin`**. Exécuter bare `/tw` effectue l'action par défaut, `go`.

## Commandes joueur

| Commande | Description | Permission |
|---------|-------------|------------|
| `/tw go` (alias : `spawn`, `sail`) | Levez l'ancre — entrez dans l'océan où vous l'avez quitté. Sur votre propre île : marchez jusqu'à votre point d'accueil. En mer : bascule un cap vers la maison (gisement le jour, distance exacte sous les étoiles la nuit). Jamais une course à travers la mer. | `tradewinds.island.spawn` |
| `/tw chart` | Élever le compas de la carte — marqueurs holographiques pour les îles cartographiées, le dock, vos bateaux et la maison. `/tw chart list` imprime la version texte. | `tradewinds.island.chart` |
| `/tw starchart` | Recevez une carte Étoile de vos îles cartographiées. | `tradewinds.island.starchart` |
| `/tw rank` (alias : `ranks`) | Votre rang de Marin et les dix meilleurs marins par îles cartographiées. | `tradewinds.island.rank` |
| `/tw claim` | Réclamez l'îlot sauvage sur lequel vous vous tenez en tant qu'île personnelle (les portes de rang et de prix s'appliquent). | `tradewinds.island.claim` |
| `/tw sethome` | Définissez votre point d'accueil — uniquement en vous tenant sur votre propre île. | `tradewinds.island.sethome` |
| `/tw home` | Marchez vers votre point d'accueil — uniquement en vous tenant déjà sur votre propre île. | `tradewinds.island.home` |
| `/tw unclaim` | Donnez votre îlot réclamé retour à l'état sauvage. Propriétaire uniquement, l'équipe doit d'abord être vidée, pas de remboursement ; chaque bloc reste exactement comme il a été laissé. | `tradewinds.island.unclaim` |
| `/tw fine` | Régler votre casier criminel à un port (vous ramène à Propre). | `tradewinds.island.fine` |
| `/tw restart` | Redémarrer votre carrière commerciale (utilisations limitées, plafonnées par la config). | `tradewinds.island.restart` |
| `/tw info` | Informations sur l'île sur laquelle vous vous trouvez. | `tradewinds.island.info` |
| `/tw settings` | Voir les paramètres de l'île. | `tradewinds.island.settings` |
| `/tw language` | Sélectionnez votre langue. | `tradewinds.island.language` |
| `/tw warp` | Ouvrir le dialogue de téléportation de n'importe où dans les eaux de l'île. **Op par défaut** — le chemin prévu est de naviguer jusqu'à la limite de l'île, qui offre le dialogue automatiquement. | `tradewinds.island.warp` |
| `/tw trade` | Ouvrir le marché de l'île de n'importe où dans sa plage de protection. **Op par défaut** — le chemin prévu est de vous amarrer et clic-droit un commerçant sur la plaza. | `tradewinds.island.trade` |
| `/tw prices` | Votre carnet de prix — quels ports vous avez visités étaient payants, et depuis combien de temps. Enregistré uniquement quand la fonctionnalité `economy.price-logbook-enabled` est activée (désactivée par défaut). | `tradewinds.island.prices` |

## Commandes administrateur

`/twadmin` porte toutes les commandes administrateur BentoBox standard (`version`, `tp`, `getrank`, `setrank`, blueprints, et ainsi de suite), plus l'ensemble spécifique à TradeWinds :

| Commande | Description | Permission |
|---------|-------------|------------|
| `/twadmin islands` | Répertoriez les îles commerciales les plus proches avec type, niveau technologique, bande et distance. | `tradewinds.admin.islands` |
| `/twadmin tpisland <#>` | Téléportez-vous à une île commerciale de la liste des îles. | `tradewinds.admin.tpisland` |
| `/twadmin boat <player>` | Inspectez les records de bateau d'un joueur directement depuis la base de données : matériau, cargaison, carburant, dernière position observée, et si une coque est réellement chargée là ou dans le pack de quelqu'un. | `tradewinds.admin.boat` |
| `/twadmin boat <player> restore` | Régénérez un bateau actif perdu comme article estampillé dans le pack du joueur, record de cargaison intact. Refuse tant que la vraie coque est chargée ou portée. | `tradewinds.admin.boat` |
| `/twadmin rank <player>` | Montrez le rang de Marin d'un joueur : îles effectives, vrai nombre cartographié et ajustement. | `tradewinds.admin.rank` |
| `/twadmin rank <player> <rank\|islands\|reset>` | Définissez le rang d'un joueur par slug de rang ou nombre d'îles, ou réinitialisez l'ajustement. La cartographie réelle continue à compter par-dessus. | `tradewinds.admin.rank` |
| `/twadmin customs` | Montrez ce que les douanes pensent de vous où vous vous trouvez : contrebande à bord, probabilités de scan, force de patrouille. | `tradewinds.admin.customs` |
| `/twadmin priceaudit` | Auditez la couverture des prix — ce qui peut être vendu, ce qui est du butin, ce qui est invendable — et écrivez le rapport complet dans `price-audit.txt`. | `tradewinds.admin.priceaudit` |
| `/twadmin warpfail <player>` | Pirater le prochain téléportation d'un joueur pour échouer dans l'Interstice (exécutez à nouveau pour effacer). Pour tester le chemin du mauvais tir à la demande. | `tradewinds.admin.warpfail` |
| `/twadmin reflag` | Ré-appliquer les drapeaux de bande de sécurité à toutes les îles commerciales. | `tradewinds.admin.reflag` |
