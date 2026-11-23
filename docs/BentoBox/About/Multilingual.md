# Langues et Messages { #languages-messages }

Chaque message, menu et nom d'objets dans BentoBox et ses add-ons provient de **fichiers de locale** : un fichier YAML par langue. Les joueurs choisissent leur propre langue, et vous pouvez changer n'importe quel texte, couleur ou comment un message est affiché (chat, barre d'action, titre, son).

## Langues { #languages }

BentoBox est livré avec 25 langues :

| Langue | Fichier | Langue | Fichier |
|---|---|---|---|
| Anglais (défaut) | `en-US` | Italien | `it` |
| Chinois (Simplifié) | `zh-CN` | Japonais | `ja` |
| Chinois (Traditionnel, Hong Kong) | `zh-HK` | Coréen | `ko` |
| Chinois (Traditionnel, Taïwan) | `zh-TW` | Letton | `lv` |
| Croate | `hr` | Polonais | `pl` |
| Tchèque | `cs` | Portugais | `pt` |
| Néerlandais | `nl` | Portugais (Brésil) | `pt-BR` |
| Français | `fr` | Roumain | `ro` |
| Allemand | `de` | Russe | `ru` |
| Hongrois | `hu` | Espagnol | `es` |
| Indonésien | `id` | Turc | `tr` |
| | | Ukrainien | `uk` |
| | | Vietnamien | `vi` |

Les add-ons peuvent en avoir moins. Chaque page de [mode de jeu](../../gamemodes/Comparison.md) et d'[add-on](Addons.md) a un tableau montrant combien chaque langue est complète.

### La langue par défaut du serveur { #the-servers-default-language }

Les nouveaux joueurs voient la langue par défaut jusqu'à ce qu'ils en choisissent une. Définissez-le dans le `config.yml` de BentoBox, en utilisant un nom de fichier du tableau :

```yaml
general:
  default-language: en-US
```

Puis redémarrez ou exécutez `/bentobox reload`. BentoBox ne détecte pas automatiquement la langue Minecraft d'un joueur.

### Joueurs choisissant une langue { #players-choosing-a-language }

Les joueurs changent de langue avec **`/island language`** (ou la propre commande du mode de jeu), qui ouvre un menu des langues installées. Leur choix s'applique à BentoBox et tous les add-ons, dans chaque mode de jeu.

Si un message manque dans la langue du joueur, BentoBox utilise la langue par défaut du serveur, puis l'anglais.

## Changer les messages { #changing-messages }

Les fichiers de locale sont dans :

| Texte de | Dossier |
|---|---|
| BentoBox | `plugins/BentoBox/locales/BentoBox/` |
| Un mode de jeu ou un add-on | `plugins/BentoBox/locales/<AddonName>/`, par exemple `locales/BSkyBlock/` |

Pour changer un message :

1. Trouvez-le : recherchez dans le fichier de langue (par exemple `en-US.yml`) le texte que les joueurs voient.
2. Changez le texte après la clé, en gardant la clé et l'indentation. Laissez tout entre crochets, comme `[name]`, `[number]` ou `[prefix_island]`, tel quel ; ceux-ci sont remplis par BentoBox. (`[prefix_island]` devient le mot du mode de jeu pour une île, comme « île », « grotte » ou « boîte ».)
3. Exécutez `/bentobox reload locales`.

```yaml
commands:
  island:
    create:
      creating-island: "<green>Construction de votre [prefix_island], tenez bon...</green>"
```

Changez chaque langue utilisée par vos joueurs, sinon les autres afficheront toujours l'ancien texte.

**Vos modifications sont conservées lors de la mise à jour.** Quand BentoBox ou un add-on est mis à jour, les nouveaux messages sont ajoutés aux fichiers sur votre serveur, mais les messages déjà présents ne sont pas écrasés. Cela signifie aussi que si une mise à jour améliore le libellé d'un message, vous ne le verrez pas jusqu'à ce que vous supprimiez cette ligne (ou le fichier entier) et que vous rechargiez.

**Pour masquer un message**, définissez-le sur une chaîne vide : `creating-island: ""`. Les messages vides ne sont pas envoyés.

**Pour vérifier les traductions manquantes**, exécutez `/bentobox locale`. Il compare chaque fichier de langue, pour BentoBox et chaque add-on, avec l'anglais et rapporte ce qui manque.

## Couleurs et formatage { #colours-and-formatting }

Les messages utilisent les balises [MiniMessage](https://docs.advntr.dev/minimessage/format.html) :

```yaml
example: "<green>Bienvenue sur l'île !</green>"
example: "<bold><red>Attention !</red></bold> Quelque chose s'est produit."
example: "<gradient:gold:yellow>Nom de l'Île</gradient>"
```

Les anciens codes de couleur (`&a`, `&l`, `§c`) fonctionnent toujours.

## Comment un message est affiché { #how-a-message-is-shown }

Par défaut, un message va au chat. Commencez-le par une balise pour l'afficher ailleurs :

| Balise | Affiche le message |
|---|---|
| `[actionbar]` | Au-dessus de la barre d'outils |
| `[title]` | Comme un grand titre au milieu de l'écran. Ajouter `[subtitle]` pour mettre du texte dans une ligne plus petite en dessous |
| `[sound:name:volume:pitch]` | Joue aussi un son. Le volume et la hauteur sont optionnels. Utilisez les noms de sons Minecraft avec des tirets bas, par exemple `entity_experience_orb_pickup` |

```yaml
example: "[actionbar]Téléportation..."
example: "[title]Téléportation...[subtitle]Attendre une seconde."
example: "[sound:entity_experience_orb_pickup:1:1][title]Téléportation...[subtitle]Attendre une seconde."
```

Les messages à la console vont toujours au journal de la console.

### Messages cliquables { #clickable-messages }

Ajouter ces éléments n'importe où dans un message pour rendre le message entier cliquable ou afficher du texte au survol :

| Balise | Effet |
|---|---|
| `[run_command: /command]` | Cliquer exécute la commande |
| `[suggest_command: /command]` | Cliquer met la commande dans la boîte de chat |
| `[open_url: https://...]` | Cliquer ouvre un lien |
| `[copy_to_clipboard: text]` | Cliquer copie le texte |
| `[hover: text]` | Affiche le texte quand le joueur survole le message |

```yaml
example: "Vous n'êtes pas sur votre île. Cliquez pour aller à la maison ![run_command: /island go][hover: Retour à la maison]"
```

## Texte du menu { #menu-text }

Les titres du menu et le texte des boutons sont également dans les fichiers de locale, référencés à partir des modèles de menu. Voir [Personnalisation des Menus](../../Tutorials/generic/Customizable-GUI.md#change-the-title-or-button-text).

## Corriger ou ajouter des traductions { #fixing-or-adding-translations }

Les traductions sont faites avec l'aide de l'IA et corrigées par la communauté. Si vous repérez une erreur, corrigez-la dans le fichier de locale dans le référentiel GitHub du projet et ouvrez une demande de fusion, ou dites-le nous sur [Discord](https://discord.bentobox.world). Voir [Traduire BentoBox](../Translate-BentoBox-and-addons.md) pour les directives et l'état de traduction de chaque projet.

## Dépannage { #troubleshooting }

**Mon changement n'a pas été affiché.**
Exécutez `/bentobox reload locales`. Vérifiez que vous avez modifié la langue du joueur (il n'utilise peut-être pas l'anglais) et le bon dossier (les messages propres de BentoBox sont dans `locales/BentoBox/`, les messages du mode de jeu dans `locales/<GameMode>/`).

**Le serveur affiche `commands.island...` au lieu d'un message.**
La clé manque dans la langue du joueur, la langue par défaut du serveur et l'anglais. Supprimez le fichier pour que BentoBox écrive une copie fraîche, ou rajoutez la clé.

**Après une mise à jour, un message a toujours l'ancien libellé.**
Votre fichier conserve l'ancien texte. Supprimez cette ligne ou le fichier entier et exécutez `/bentobox reload locales`.

**Tous les rangs de l'info-bulle d'un drapeau de protection ont la même couleur, ou les drapeaux n'affichent pas les indications « Clic gauche / Clic droit ».**
Les fichiers de locale ont été écrits à l'origine par une ancienne version de BentoBox et contiennent encore l'ancien texte. BentoBox 3.23.7 affiche de nouveau correctement les couleurs des rangs avec les anciens fichiers, mais seuls des fichiers neufs comportent les indications de clic et toutes les corrections de formulation ultérieures. Pour les rafraîchir : arrêtez le serveur, renommez `plugins/BentoBox/locales/BentoBox/` (par exemple en `BentoBox-old`), démarrez le serveur pour que les fichiers actuels soient écrits, puis reportez-y vos propres modifications. La même méthode fonctionne pour le dossier d'un add-on dans `plugins/BentoBox/locales/<AddonName>/`.

**Le fichier YAML ne se charge pas après édition.**
Généralement un guillemet manquant ou une mauvaise indentation. Mettez les messages contenant `:` ou `#` entre guillemets, et vérifiez la console pour le numéro de ligne.
