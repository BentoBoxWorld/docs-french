#### Permissions LikesAddon (à partir de 1.7.0)

| Permission                      | Permission parent     | Valeur par défaut | Description                                          |
|---------------------------------|-----------------------|---------------|------------------------------------------------------|
| [gamemode].likes                |                       | true          | Permet d'utiliser `/[gamemode_user] likes`               |
| [gamemode].likes.top            | [gamemode].likes      | true          | Permet d'utiliser `/[gamemode_user] likes top`           |
| [gamemode].likes.view           | [gamemode].likes      | true          | Permet d'utiliser `/[gamemode_user] likes view`          |
| [gamemode].likes.view.others    | [gamemode].likes.view | op            | Permet d'utiliser `/[gamemode_user] likes view <player>` |
| [gamemode].likes.bypass-cost    | [gamemode].likes      | op            | Permet de contourner le paiement pour aimer et ne pas aimer   |
| [gamemode].likes.admin          |                       | op            | Permet d'utiliser `/[gamemode_admin] likes`              |
| [gamemode].likes.admin.settings | [gamemode].likes.admin| op            | Permet d'utiliser `/[gamemode_admin] likes settings`     |
| [gamemode].likes.icon.X         |                       |               | Permet de définir l'icône personnalisée (x est Material) pour le joueur |
