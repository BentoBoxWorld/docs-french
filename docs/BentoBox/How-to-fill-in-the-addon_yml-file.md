# Comment remplir le fichier addon.yml ?

## Qu'est-ce que ce fichier ?

Le fichier **addon.yml** donne des informations précieuses sur votre complément à BSkyBlock quand il essaie de le charger. Ce fichier se compose d'un ensemble d'attributs, chacun défini sur une nouvelle ligne et sans indentation.

Sans ce fichier ou s'il n'est pas correctement rempli, BSkyBlock ne chargera pas votre complément et le marquera comme `INVALID_DESCRIPTION`.

## Attributs Obligatoires

### name

**Description :** Le nom de ce complément.

**Code :**
```yaml
name: "MySuperAddon"
```

**Remarques :**
1. Doit être composé de tous les caractères alphanumériques et des traits de soulignement (a-z,A-Z,0-9, \_).
2. Les espaces ne sont pas supportés et seront automatiquement convertis en traits de soulignement.
3. Il est utilisé pour identifier le complément dans l'API entière BSkyBlock.
4. Affiché quand l'utilisateur tape `/bsadmin version YourSuperAddon`.

### main

**Description :** L'adresse qui pointe vers la classe étendant `BSAddon`.

**Code :**
```yaml
main: fr.poslovitch.myaddon.MySuperAddon
```

**Remarques :**
1. Cela doit contenir l'espace de noms complet y compris le fichier de classe lui-même, comme Bukkit. Par conséquent, si votre espace de noms est `fr.poslovitch.myaddon`, et votre fichier de classe s'appelle `MySuperAddon`, cela doit être `fr.poslovitch.myaddon.MySuperAddon`.

### version

**Description :** La version de votre complément.

**Code :**
```yaml
version: 1.0.0
```

**Remarques :**
1. La version est une chaîne arbitraire, cependant le format le plus courant est MajorRelease.MinorRelease.FixRelease (par ex : 3.6.1).
2. Affiché quand l'utilisateur tape `/bsadmin version YourSuperAddon`.

## Attributs Optionnels

Mis à part les attributs obligatoires, il y a quelques autres attributs qui peuvent être utiles pour donner plus d'informations sur votre complément à BSkyBlock.

Ces attributs sont optionnels.

### authors

**Description :** Vous permet de lister tous les développeurs super gentils qui ont créé ce complément, ou juste vous.

**Code :**
```yaml
authors: ["Poslovitch", "Tastybento", "vous, peut-être ? :P"]
# N'hésitez pas à ajouter nos surnoms à la liste des auteurs de votre complément, nous apprécierions cela !
```

**Remarques :**
1. Donne du crédit au(x) développeur(s)
2. Affiché quand l'utilisateur tape `/bsadmin version YourSuperAddon`.

### description

**Description :** Description amicale-poules de la fonctionnalité que votre complément fournit.

**Code :**
```yaml
description: "Cela vous fait mourir quand vous sautez. Tellement 2017."
```

**Remarques :**
1. La description peut avoir plusieurs lignes (_parce que vous avez besoin d'un lot de place pour expliquer ce qu'il fait votre super complément !_).
2. Affiché quand l'utilisateur tape `/bsadmin version YourSuperAddon`.

### website

**Description :**  Le site web du plugin ou de l'auteur.

**Code :**
```yaml
website: "https://github.com/tastybento/bskyblock"
```

**Remarques :**
1. Si vous n'avez pas de site web dédié, un lien vers le dépôt GitHub du complément devrait faire l'affaire.
2. Affiché quand l'utilisateur tape `/bsadmin version YourSuperAddon`.
