= Table des Matières
:toc:

= Introduction
Un mode de jeu est un complément comme BSkyBlock ou AcidIsland. Ce qui en fait un complément de mode de jeu est qu'il créera et enregistrera un *monde* avec BentoBox et fournira à BentoBox un objet de classe WorldSettings.

Actuellement, les mondes enregistrés avec BentoBox doivent être des over-worlds, mais une fois qu'un monde est enregistré, tous les mondes Nether et End associés appartiendront également à ce complément de mode de jeu.

Pour montrer comment cela fonctionne, regardons le code BSkyBlock (certaines lignes supprimées pour la clarté) :

[source,java]
----
    @Override
    public void onLoad() {
        // Enregistrez la configuration par défaut à partir de config.yml
        saveDefaultConfig();
        // Chargez les paramètres à partir de config.yml. Cela vérifiera s'il y a des problèmes avec cela aussi.
        settings = new Config<>(this, Settings.class).loadConfigObject();
        // Chargez ou créez les mondes
        bsbWorlds = new BSkyBlockWorld(this);
    }
----

Les commentaires sont assez clairs, mais les deux premiers appels servent à configurer le fichier config.yml et les paramètres. Dans ce cas, nous utilisons la classe Config de l'API de Configuration BentoBox qui permet la sauvegarde dynamique des fichiers YAML avec commentaires. C'est une API de configuration puissante. Vous n'êtes *pas* obligé de l'utiliser si vous ne le voulez pas. À la place, vous pouvez juste utiliser le système de configuration standard de style Bukkit. Nous l'avons utilisée parce qu'elle nous permet de garder le fichier config.yml à jour automatiquement.

= La Classe des Paramètres

Regardons la classe Settings (à nouveau, certaines lignes ont été supprimées pour la clarté) :

[source,java]
----
@StoreAt(filename="config.yml", path="addons/BSkyBlock") // Appelez explicitement le nom que cela devrait avoir.
@ConfigComment("Configuration BSkyBlock [version]")
@ConfigComment("Ce fichier de configuration est dynamique et enregistré quand le serveur s'arrête.")
@ConfigComment("Vous ne pouvez pas l'éditer pendant que le serveur est en cours d'exécution car les modifications seront")
@ConfigComment("perdues! Utilisez l'interface graphique des paramètres en jeu ou éditez quand le serveur est hors ligne.")
@ConfigComment("")
public class Settings implements DataObject, WorldSettings {

    @ConfigComment("Permettez à l'obsidienne d'être recueillie avec un seau vide dans la lave")
    @ConfigEntry(path = "general.allow-obsidian-scooping")
    private boolean allowObsidianScooping = true;

...
----

Ce que vous voyez ici sont beaucoup de notations suivies par la déclaration de classe, suivi par plus de notations autour d'une déclaration de champ. Prenons-les un par un :

. L'annotation @StoreAt avant la classe définit où ce fichier de configuration sera enregistré. Il est relatif au dossier de données du plugin BentoBox. Les fichiers ne doivent être enregistrés que dans le dossier BentoBox. C'est très important que vous déclariez explicitement cet emplacement !
. L'annotation @Comment est utilisée pour ajouter une ligne de commentaire dans le fichier YAML. Le placeholder « [version] » est automatiquement remplacé par le numéro de version du complément.
. La classe doit implémenter à la fois DataObject et WorldSettings. DataObject est utilisé pour que la classe puisse être enregistrée dans la base de données (via BBConfig) et WorldSettings est utilisé parce que c'est un complément Game Mode
. Le champ « allowObsidianScooping » est déclaré, avec une valeur par défaut et il a une annotation de commentaire et une annotation @ConfigEntry. Celle-ci est utilisée pour définir où cette valeur sera placée dans le fichier YAML. Remarquez que les entrées YAML sont généralement placées dans le même ordre qu'elles sont écrites dans le code sauf si @ConfigEntry force les place ailleurs.
. Après la déclaration du champ, vous devez également créer un getter et un setter pour le champ. (Non affiché dans le code)

Remarquez qu'en implémentant l'interface WorldSetting, vous devrez @Override un certain nombre de getters pour les paramètres mondiaux obligatoires. Dans la classe BSkyBlock Settings, presque tous ceux-ci sont chargés à partir du fichier de configuration. Une exception est le *Optional<Addon> getAddon()*. Cela doit retourner l'instance du complément. En ce moment, le complément doit le définir. À l'avenir, BentoBox peut le faire.

= Enregistrement du Monde avec BentoBox

Maintenant regardons de plus près la classe BSkyBlockWorld mentionnée ci-dessus. Cette classe fait trois choses principales :

. Crée les mondes pour BSkyBlock (crée les mondes et définit les générateurs pour eux)
. Enregistre le monde principal et la classe de paramètres avec BentoBox
. Enregistre les schems qui seront utilisés lors de la création de nouvelles îles avec la classe IslandCreate

Voici comment elle le fait :

[source,java]
----
// Créez le monde s'il n'existe pas
islandWorld = WorldCreator.name(worldName).type(WorldType.FLAT).environment(World.Environment.NORMAL)
    .generator(new ChunkGeneratorWorld(addon)).createWorld();

// Enregistrez le monde et les paramètres avec BentoBox
addon.getPlugin().registerWorld(islandWorld, addon.getSettings());

// Créez les mondes nether et end si nécessaire (non affiché)

// Chargez les schematics
addon.getPlugin().getSchemsManager().loadIslands(islandWorld);
----

Dans ce code, *addon* est l'instance du complément. getPlugin() est utilisé pour obtenir BentoBox et registerWorld() est utilisé pour enregistrer le monde. Remarquez que vous **n'enregistrez pas** les mondes nether et end avec BentoBox. BentoBox supposera que tout Nether ou End associé est également possédé par votre complément s'il existe.

Pour les schems (le format propriétaire de fichiers schematics de BentoBox), vous devriez avoir des schems pour l'île par défaut pour chaque monde de votre complément dans le dossier schems du complément. Ils doivent être nommés comme suit :

* island.schem (Obligatoire)
* nether-island.schem (Optionnel)
* end-island.schem (Optionnel)

Pour créer des schems, utilisez la commande schem de BentoBox (ou la commande schem de BSkyBlock ou AcidIsland).

= Enregistrement des Commandes

Après avoir enregistré le monde, les paramètres du mode de jeu associé et les schems, l'étape suivante est de faire faire quelque chose à votre complément. S'il nécessite des commandes, vous pouvez les créer en étendant CompositeCommand. Regardons comment BSkyBlock enregistre sa commande de haut niveau */island* et les sous-commandes qu'elle contient :

[source,java]
----
public class IslandCommand extends CompositeCommand {

    public IslandCommand(BSkyBlock addon) {
