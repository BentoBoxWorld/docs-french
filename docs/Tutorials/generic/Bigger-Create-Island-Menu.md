# Agrandir le menu de création d'île (plus de lignes)

**Question :** « Est-il possible d'avoir un menu *Créer une île* plus grand — jusqu'à 5 ou 6 lignes au lieu des 3 par défaut ? »

**Réponse :** Oui. Le menu de création d'île est une [interface utilisateur entièrement personnalisable](Customizable-GUI.md). Vous contrôlez le nombre de lignes et le nombre de lots de blueprints qui apparaissent sur chaque page en modifiant le modèle `island_creation_panel.yml`. Cette page vous montre exactement comment.

Décidez d'abord lequel de ces cas vous concerne vraiment, car ils nécessitent des modifications différentes :

- **Vous voulez juste que le menu *paraisse* plus grand** (plus de lignes d'espace, par exemple pour un look encadré/spacieux) → utilisez le raccourci d'une seule ligne [`force-shown`](#vous-voulez-juste-un-menu-plus-grand-force-shown) ci-dessous. Les rangées supplémentaires seront remplies de fond vide.
- **Vous voulez plus d'îles visibles à la fois / moins de pages** → vous devez [ajouter plus de boutons de lot](#exemple-un-menu-6-lignes). `force-shown` seul ne fera pas cela.

## Vous voulez juste un menu plus grand ? (`force-shown`)

Si vous voulez juste un menu plus grand — plus de lignes visibles, sans forcément montrer plus d'îles — c'est une modification en une seule ligne. Ajoutez (ou modifiez) la ligne `force-shown` dans `island_creation_panel.yml` :

```yaml
force-shown: 6
```

`force-shown: 6` force les lignes 1 à 6 à toujours s'afficher, ce qui vous donne un panneau complet de **6 lignes (54 emplacements)**. Utilisez `5` pour 5 lignes, et ainsi de suite.

**Important :** `force-shown` contrôle uniquement la **hauteur du panneau**. Les rangées supplémentaires qu'il ouvre sont remplies de votre élément `background`/`border` — elles ne **contiennent pas plus de lots d'îles**. Les lots n'apparaissent que là où les entrées `blueprint_bundle_button` existent dans la section `content`. Donc si votre objectif est de montrer *plus d'îles à la fois* (pas juste agrandir la boîte), passez à [l'exemple 6-lignes](#exemple-un-menu-6-lignes), qui ajoute également les boutons de lot supplémentaires.

## Contexte : comment le menu est construit

Le menu de création d'île (et le menu identique affiché quand un joueur réinitialise son île) est généré à partir d'un modèle de panneau appelé `island_creation_panel.yml`. BentoBox expédie une version par défaut avec **3 lignes** et jusqu'à **7 boutons de lot par page** (avec une paire de flèches « précédent »/« suivant » pour la pagination quand il y a plus de lots que de place).

Deux règles décident du nombre de lignes que le joueur voit réellement :

1. **Le panneau grandit pour s'adapter à son contenu.** Une ligne s'affiche si elle contient au moins un bouton. En interne, la grille est toujours de 6 lignes, mais les lignes vides sont supprimées, donc le modèle par défaut ne *ressemble* qu'à 3 lignes parce que les lignes 1, 5 et 6 sont vides.
2. **`force-shown` peut épingler les lignes ouvertes** même quand elles sont vides (utile pour maintenir une mise en page fixe pendant que votre liste de lots grandit).

Donc, pour obtenir un menu plus grand, vous ajoutez simplement plus d'entrées `blueprint_bundle_button` sur plus de lignes. Il y a une limite dure maximale de **6 lignes** (54 emplacements) parce que c'est la plus grande taille qu'un inventaire de coffre Minecraft peut avoir.

## Où placer le fichier

Le menu peut être écrasé à deux niveaux. BentoBox cherche le fichier dans cet ordre :

1. **Par mode de jeu** (recommandé) — `plugins/<GameMode>/panels/island_creation_panel.yml`
   par exemple `plugins/AcidIsland/panels/island_creation_panel.yml`, `plugins/BSkyBlock/panels/island_creation_panel.yml`.
   Cela n'affecte que ce mode de jeu.
2. **Fallback global** — `plugins/BentoBox/panels/island_creation_panel.yml`
   Utilisé pour tout mode de jeu qui n'en a pas sa propre copie.

Si aucun fichier n'existe, la valeur par défaut intégrée (dans le jar de BentoBox) est utilisée.

> **Conseil :** Copiez le fichier par défaut plutôt que d'en écrire un de zéro. Démarrez le serveur une fois pour que BentoBox écrive ses valeurs par défaut, puis copiez `plugins/BentoBox/panels/island_creation_panel.yml` dans le dossier `panels/` de votre mode de jeu et éditez-le là. Rechargez avec `/bentobox reload` (ou redémarrez) après avoir enregistré.

## Exemple : un menu 6-lignes

Ce modèle montre un menu complet de 6 lignes avec une mise en page bordée. Les lignes 2–5 contiennent des boutons de lot de blueprints (jusqu'à **28** lots par page), et la ligne 6 contient les flèches de pagination.

```yaml
island_creation_panel:
  title: panels.island_creation.title
  type: INVENTORY
  background:
    icon: BLACK_STAINED_GLASS_PANE
    title: "&b&r"
  border:
    icon: BLACK_STAINED_GLASS_PANE
    title: "&b&r"
  # Épingle les 6 lignes ouvertes même si certaines sont vides. Utilisez [] pour laisser le panneau
  # s'adapter automatiquement à son contenu à la place.
  force-shown: 6
  content:
    2:
      2: blueprint_bundle_button
      3: blueprint_bundle_button
      4: blueprint_bundle_button
      5: blueprint_bundle_button
      6: blueprint_bundle_button
      7: blueprint_bundle_button
      8: blueprint_bundle_button
    3:
      2: blueprint_bundle_button
      3: blueprint_bundle_button
      4: blueprint_bundle_button
      5: blueprint_bundle_button
      6: blueprint_bundle_button
      7: blueprint_bundle_button
      8: blueprint_bundle_button
    4:
      2: blueprint_bundle_button
      3: blueprint_bundle_button
      4: blueprint_bundle_button
      5: blueprint_bundle_button
      6: blueprint_bundle_button
      7: blueprint_bundle_button
      8: blueprint_bundle_button
    5:
      2: blueprint_bundle_button
      3: blueprint_bundle_button
      4: blueprint_bundle_button
      5: blueprint_bundle_button
      6: blueprint_bundle_button
      7: blueprint_bundle_button
      8: blueprint_bundle_button
    6:
      1:
        icon: tipped_arrow[potion_contents={custom_color:11546150}]
        title: panels.buttons.previous.name
        description: panels.buttons.previous.description
        data:
          type: PREVIOUS
          indexing: true
        actions:
          previous:
            click-type: UNKNOWN
            tooltip: panels.tips.click-to-previous
      9:
        icon: tipped_arrow[potion_contents={custom_color:8439583}]
        title: panels.buttons.next.name
        description: panels.buttons.next.description
        data:
          type: NEXT
          indexing: true
        actions:
          next:
            click-type: UNKNOWN
            tooltip: panels.tips.click-to-next
  reusable:
    blueprint_bundle_button:
      # icon: GRASS_BLOCK   # Décommentez pour forcer une seule icône pour chaque lot ;
                            # sinon chaque lot utilise sa propre icône configurée.
      title: panels.island_creation.buttons.bundle.name
      description: panels.island_creation.buttons.bundle.description
      data:
        type: BUNDLE
      actions:
        select:
          click-type: UNKNOWN
          tooltip: panels.tips.click-to-choose
```

### Vous voulez un menu 5-lignes à la place ?

Supprimez la ligne `5` de `content` et changez `force-shown: 6` à `force-shown: 5`. Déplacez les flèches de pagination jusqu'à la ligne `5` si vous le souhaitez. N'importe quel nombre de lignes de 1 à 6 fonctionne de la même manière — ajoutez ou supprimez simplement des lignes d'entrées `blueprint_bundle_button`.

## Comment les pièces fonctionnent

| Paramètre | Ce qu'il fait |
|---|---|
| lignes `content` `1`–`6` | Chaque clé `1`–`6` est une ligne ; chaque clé imbriquée `1`–`9` est une colonne. Une ligne n'est affichée que si elle a du contenu (ou est forcée). |
| `blueprint_bundle_button` | Un bouton réutilisable de `type: BUNDLE`. **Le nombre de ces boutons dans le modèle = le nombre de lots affichés par page.** Ajoutez-en plus pour afficher plus de lots à la fois. |
| `force-shown` | `force-shown: 6` force les lignes 1 à 6 à toujours s'afficher (hauteur fixe). `force-shown: [2,4]` force uniquement les lignes 2 et 4. `force-shown: []` (ou l'omettre) laisse le panneau s'adapter automatiquement à son contenu. |
| `type: PREVIOUS` / `type: NEXT` | Les flèches de pagination. Elles n'apparaissent que quand il y a plus de lots que la place sur une page, donc il est sûr de toujours les inclure. |
| `unique_id` (facultatif) | Ajouter `unique_id: <bundleId>` sous `data:` d'un bouton épingle un lot spécifique à cet emplacement exact au lieu de remplir les emplacements dans l'ordre. |

## Questions courantes

**« J'ai ajouté des lignes mais le menu est toujours petit. »**
Une ligne ne s'affiche que si elle a un bouton *ou* est listée dans `force-shown`. Assurez-vous que chaque nouvelle ligne contient réellement des entrées `blueprint_bundle_button`, et vérifiez l'indentation YAML (les lignes et colonnes sont des clés numériques imbriquées sous `content`).

**« Puis-je aller au-delà de 6 lignes ? »**
Non. 6 lignes / 54 emplacements est la taille maximale d'une interface utilisateur de coffre Minecraft, donc c'est la limite stricte pour un panneau de type `INVENTORY`.

**« Mes changements n'ont rien fait. »**
Confirmez que le fichier est dans le dossier correct pour le mode de jeu que vous testez (le dossier par mode gagne sur le dossier global de BentoBox), le fichier s'appelle exactement `island_creation_panel.yml`, et vous avez exécuté `/bentobox reload` ou redémarré le serveur après édition. Une erreur de syntaxe YAML fera que BentoBox revient à la valeur par défaut intégrée — vérifiez la console du serveur pour les avertissements au démarrage.

**« Est-ce que cela change aussi le menu quand les joueurs *réinitialisent* leur île ? »**
Oui. Le menu de réinitialisation d'île utilise le même modèle `island_creation_panel.yml`.

## Voir aussi

- [Interfaces graphiques personnalisées](Customizable-GUI.md) — le système général sur lequel ces menus sont construits, y compris la liste complète des options d'élément/icône.
- [ItemParser](https://docs.bentobox.world/en/latest/BentoBox/ItemParser/) — la syntaxe pour le champ `icon:`.
