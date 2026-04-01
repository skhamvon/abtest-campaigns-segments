# abtest-campaigns-segments

Ce dépôt contient les **données fonctionnelles** de l’A/B testing :

- la définition des **campagnes** (ciblage, variantes, configuration),
- la définition des **segments** d’utilisateurs,
- les fichiers **JS/CSS/HTML** associés aux variantes front (par exemple pour des démos).

Il est pensé comme un dépôt **d’assets et de configuration**, versionné indépendamment du code de la solution (`abtest-solution`).

## Structure

L’arborescence peut évoluer, mais on retrouve typiquement :

- `Campaigns/` : une sous-arborescence par campagne.
  - ex. `Campaigns/DemoFrontendCampaign/config.json`
  - ex. `Campaigns/DemoFrontendCampaign/variant-a/…`
- `Segments/` : les segments d’utilisateurs (règles de ciblage, critères).
  - ex. `Segments/AllUsers/config.json`

Chaque campagne ou segment est généralement décrit par un fichier `config.json`, éventuellement accompagné de ressources front (`script.js`, `style.css`, etc.).

## Utilisation comme submodule

Ce dépôt est généralement consommé comme **submodule Git** dans `abtest-solution` :

```bash
cd abtest-solution
git submodule update --init abtest-campaigns-segments
```

Lorsqu’il est mis à jour (nouvelle campagne, nouveau segment, correction de config), il faut :

1. **committer ici** les changements,
2. **mettre à jour le pointeur** dans `abtest-solution`.

## Installation / développement local

Il n’y a pas de dépendances Node ni de build ici : il s’agit uniquement de fichiers de configuration et de front statique.

Pour travailler dessus :

```bash
git clone git@github.com:skhamvon/abtest-campaigns-segments.git
cd abtest-campaigns-segments
```

Tu peux ensuite :

- ajouter/modifier des campagnes dans `Campaigns/`,
- ajouter/modifier des segments dans `Segments/`,
- versionner le tout via les commandes Git habituelles :

```bash
git status
git add .
git commit -m "add or update campaigns/segments"
git push
```

Les changements seront automatiquement pris en compte par la solution d’A/B testing (`abtest-solution`) une fois le submodule mis à jour côté `abtest-solution`.
