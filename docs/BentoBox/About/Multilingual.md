# Support Multilingue

BentoBox et ses compléments supportent une large gamme de langues directement. Tous les messages en jeu, le texte des interfaces graphiques et les noms d'objets que les joueurs voient peuvent être affichés dans leur propre langue — aucun plugin supplémentaire nécessaire.

## Langues Supportées

BentoBox est actuellement livré avec des traductions pour :

| Langue | Code |
|---|---|
| Anglais (par défaut) | `en-US` |
| Chinois (Simplifié) | `zh-CN` |
| Chinois (Traditionnel, HK) | `zh-HK` |
| Chinois (Traditionnel, TW) | `zh-TW` |
| Croate | `hr` |
| Tchèque | `cs` |
| Néerlandais | `nl` |
| Français | `fr` |
| Allemand | `de` |
| Hongrois | `hu` |
| Indonésien | `id` |
| Italien | `it` |
| Japonais | `ja` |
| Coréen | `ko` |
| Letton | `lv` |
| Polonais | `pl` |
| Portugais | `pt` |
| Roumain | `ro` |
| Russe | `ru` |
| Espagnol | `es` |
| Turc | `tr` |
| Ukrainien | `uk` |
| Vietnamien | `vi` |

Les compléments individuels peuvent supporter un sous-ensemble différent de langues. Vérifiez la page de chaque complément pour son statut de traduction spécifique.

## Définition de la Langue par Défaut

Pour définir la langue que tous les joueurs voient par défaut, éditez le `config.yml` BentoBox :

```yaml
# Langue par défaut pour les nouveaux joueurs.
# Référez-vous au dossier /locale dans le dossier du plugin BentoBox pour les langues disponibles.
default-language: en-US
```

Définissez cela à n'importe quel code de langue du tableau ci-dessus. Après l'avoir changé, rechargez le serveur ou exécutez `/bentobox reload`.

## Sélection de la Langue des Joueurs

Si activé, les joueurs peuvent basculer vers leur langue préférée en utilisant :
```
/bentobox locale
```

C'est utile sur les serveurs internationaux où la base de joueurs parle plusieurs langues.

## Les Traductions Sont Créées par la Communauté

Les traductions pour BentoBox et ses compléments sont contribuées par la communauté. L'équipe BentoBox ne peut pas examiner chaque traduction en profondeur, mais toutes les contributions sont vérifiées pour la qualité avant d'être acceptées.

!!! note "Qualité des Traductions"
    Parce que les traductions sont contribuées par la communauté, la qualité varie. Si vous repérez des erreurs dans une traduction, aidez à l'améliorer !

## Comment Contribuer une Traduction

La plupart des traductions sont désormais générées avec l'aide de l'IA, donc
l'essentiel du travail est déjà fait — mais **l'IA n'est pas parfaite**. La
chose la plus utile que la communauté puisse faire est de **signaler les
erreurs** et de **suggérer des corrections**.

* **Vous avez repéré une erreur ?** Ouvrez une issue ou une PR sur le dépôt
  concerné via [bentobox.world](https://bentobox.world) (un lien court vers
  notre organisation GitHub), ou prévenez-nous sur
  [Discord](https://discord.bentobox.world).
* **Vous voulez corriger une chaîne ?** Modifiez le fichier de locale dans
  `src/main/resources/locales/` du dépôt concerné et ouvrez une PR. Ne
  **traduisez pas** le texte à l'intérieur de crochets — par ex. `[name]`
  doit rester tel quel.
* **Vous voulez ajouter une toute nouvelle langue ?** Ouvrez une PR ajoutant
  un nouveau fichier de locale à côté des existants, ou demandez sur Discord
  et nous vous aiderons à démarrer.

Un outil d'assistance à la traduction est disponible sur
[download.bentobox.world/translate.html](https://download.bentobox.world/translate.html)
— il s'exécute entièrement dans votre navigateur. Les traducteurs gagnent un badge de communauté spécial !

Voir la liste complète des pages de traduction des compléments sur [Traduire BentoBox et les Compléments](../Translate-BentoBox-and-addons.md).
