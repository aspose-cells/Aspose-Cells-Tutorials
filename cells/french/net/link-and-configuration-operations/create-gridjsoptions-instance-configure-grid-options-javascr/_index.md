---
category: general
date: 2026-05-30
description: Apprenez à créer une instance de GridJsOptions et à configurer les options
  de grille JavaScript pour les tableaux dynamiques. Guide étape par étape avec le
  code complet.
draft: false
keywords:
- create gridjsoptions instance
- configure grid options javascript
- gridjs initialization
- javascript data grid settings
- dynamic table configuration
language: fr
og_description: Créez une instance GridJsOptions et configurez les options de la grille
  JavaScript en quelques minutes. Exemple complet, explications et conseils de bonnes
  pratiques.
og_title: Créer une instance GridJsOptions – Configurer les options de la grille JavaScript
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Learn how to create GridJsOptions instance and configure grid options
    JavaScript for dynamic tables. Step‑by‑step guide with full code.
  headline: Create GridJsOptions Instance – Configure Grid Options JavaScript
  type: TechArticle
- description: Learn how to create GridJsOptions instance and configure grid options
    JavaScript for dynamic tables. Step‑by‑step guide with full code.
  name: Create GridJsOptions Instance – Configure Grid Options JavaScript
  steps:
  - name: Prerequisites
    text: '- A modern browser (Chrome, Edge, Firefox) – no build tools required. -
      Basic familiarity with JavaScript (variables, objects, DOM). - The Grid.js library
      (we’ll pull it from a CDN).'
  - name: Why this matters
    text: Loading the library from a CDN ensures you always get the latest stable
      version without a local install. The `<div id="grid-wrapper">` is the placeholder
      that the Grid.js constructor will target once we **configure grid options JavaScript**.
  - name: What you’re configuring
    text: '- **NumberFormatAlignment** – aligns numeric strings automatically. - **Pagination**
      – controls page size and navigation. - **Sorting** – toggles column sorting.
      - **Columns** – defines headers, data types, and custom renderers.'
  - name: Edge‑case note
    text: If you later supply a custom data source that already returns paginated
      results, you’ll want to disable Grid.js’s built‑in pagination to avoid double‑paging.
      Simply set `gridOptions.Pagination.enabled = false;`.
  - name: Expected Output
    text: 'When you open the HTML file in a browser you should see:'
  type: HowTo
tags:
- gridjs
- javascript
- data‑grid
title: Créer une instance GridJsOptions – Configurer les options de la grille en JavaScript
url: /fr/net/link-and-configuration-operations/create-gridjsoptions-instance-configure-grid-options-javascr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer une instance GridJsOptions – Configurer les options de grille JavaScript

Vous vous êtes déjà demandé comment **créer une instance GridJsOptions** sans fouiller dans des docs éparses ? Vous n'êtes pas le seul. Lorsque vous avez besoin d'un tableau élégant et triable sur une page web, maîtriser la façon de **configurer les options de grille JavaScript** est la première étape vers une interface soignée.

Dans ce tutoriel, nous passerons en revue le code exact dont vous avez besoin, expliquerons pourquoi chaque paramètre est important, et vous montrerons un exemple complet et exécutable. À la fin, vous serez à l'aise pour créer une instance GridJsOptions, ajuster l'alignement, la pagination, et même les rendus de cellules personnalisés — le tout avec du JavaScript pur.

## Ce que vous apprendrez

- Comment **créer une instance GridJsOptions** à partir de zéro.
- Les propriétés clés qui vous permettent de **configurer les options de grille JavaScript** (tri, pagination, formatage des nombres, etc.).
- Les pièges courants (par ex., mélange de chaînes et de types numériques) et comment les éviter.
- Une page HTML complète que vous pouvez copier‑coller dans n'importe quel projet et voir les résultats instantanément.

### Prérequis

- Un navigateur moderne (Chrome, Edge, Firefox) – aucun outil de construction requis.
- Une familiarité de base avec JavaScript (variables, objets, DOM).
- La bibliothèque Grid.js (nous la récupérerons depuis un CDN).

Si l'un de ces points vous semble inconnu, ne paniquez pas — chaque étape inclut un rappel rapide.

---

## Étape 1 : Charger Grid.js et préparer le squelette HTML

Avant de pouvoir **créer une instance GridJsOptions**, nous avons besoin de la bibliothèque elle-même. Le moyen le plus simple est d'utiliser le CDN officiel. Ci-dessous se trouve un squelette HTML minimal qui réserve également un `<div>` où la grille sera rendue.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Grid.js Demo – Configuring Options</title>
  <!-- Grid.js CSS -->
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
</head>
<body>
  <h2>Simple Data Grid</h2>
  <div id="grid-wrapper"></div>

  <!-- Grid.js JS -->
  <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
  <!-- Our custom script will go here -->
  <script src="grid-config.js"></script>
</body>
</html>
```

> **Astuce :** Placez le lien CSS avant vos propres styles afin que le thème par défaut de la grille se charge correctement.

### Pourquoi c'est important

Charger la bibliothèque depuis un CDN garantit que vous obtenez toujours la dernière version stable sans installation locale. Le `<div id="grid-wrapper">` est le placeholder que le constructeur Grid.js ciblera une fois que nous aurons **configuré les options de grille JavaScript**.

## Étape 2 : Créer une nouvelle instance GridJsOptions

Voici le cœur du tutoriel : la ligne qui **crée réellement une instance GridJsOptions**. Dans un fichier séparé nommé `grid-config.js` (référencé dans le HTML ci‑dessus), nous écrirons :

```javascript
// grid-config.js

// Step 2: Create a new GridJsOptions instance to configure grid behavior
const gridOptions = new GridJsOptions();
```

Cette ligne unique vous fournit un objet propre que vous pouvez commencer à remplir avec des paramètres. Pensez à `gridOptions` comme le panneau de contrôle de chaque fonctionnalité que vous activerez plus tard.

### Ce que vous configurez

- **NumberFormatAlignment** – aligne automatiquement les chaînes numériques.
- **Pagination** – contrôle la taille des pages et la navigation.
- **Sorting** – active/désactive le tri des colonnes.
- **Columns** – définit les en‑têtes, les types de données et les rendus personnalisés.

Vous pouvez ajouter n'importe laquelle de ces propriétés avant d'instancier finalement la grille elle-même.

## Étape 3 : Activer l'alignement des nombres (une exigence courante)

La plupart des tableaux contiennent un mélange de texte et de nombres. Par défaut, Grid.js aligne tout à gauche, ce qui paraît étrange pour les valeurs monétaires. Pour **configurer les options de grille JavaScript** afin d'obtenir un alignement correct, définissez le drapeau `NumberFormatAlignment` :

```javascript
// Enable left/right alignment for numeric strings
gridOptions.NumberFormatAlignment = true;
```

Pourquoi activer cela ? Lorsque le drapeau est vrai, Grid.js inspecte chaque cellule ; si elle ressemble à un nombre (par ex., « 1234 », « 12,34 % »), il l’aligne automatiquement à droite. Cette petite modification rend les rapports beaucoup plus lisibles.

## Étape 4 : Ajouter la pagination et le tri

Une grille du monde réel tient rarement sur un seul écran. Activons la pagination (10 lignes par page) et permettons aux utilisateurs de trier n'importe quelle colonne.

```javascript
gridOptions.Pagination = {
  limit: 10,          // rows per page
  enabled: true
};

gridOptions.Sort = true;   // enables click‑to‑sort on all columns
```

### Note de cas limite

Si vous fournissez plus tard une source de données personnalisée qui renvoie déjà des résultats paginés, vous voudrez désactiver la pagination intégrée de Grid.js pour éviter une double pagination. Il suffit de définir `gridOptions.Pagination.enabled = false;`.

## Étape 5 : Définir les colonnes et les données d'exemple

Nous allons maintenant fournir à la grille des données factices et indiquer ce que chaque colonne représente. C’est ici que le modèle **créer une instance gridjsoptions** brille vraiment — tout réside dans un seul objet bien ordonné.

```javascript
// Sample data array of objects
const sampleData = [
  { id: 1, name: "Alice", salary: "54000", department: "Engineering" },
  { id: 2, name: "Bob",   salary: "47000", department: "Marketing" },
  { id: 3, name: "Cara",  salary: "62000", department: "Design" },
  // ...more rows as needed
];

// Column definitions
gridOptions.Columns = [
  { id: "id",   name: "ID",          width: "5%" },
  { id: "name", name: "Employee",    width: "35%" },
  { id: "salary", name: "Salary ($)", width: "20%" },
  { id: "department", name: "Dept.",  width: "40%" }
];

// Attach data source
gridOptions.Data = sampleData;
```

Remarquez que nous conservons les valeurs `id` des colonnes identiques aux clés de chaque objet de données. Cette convention permet à Grid.js de faire correspondre les valeurs automatiquement, vous évitant d'écrire un formateur personnalisé pour chaque colonne.

## Étape 6 : Instancier la grille avec nos options

Nous **configurons enfin les options de grille JavaScript** en passant l'objet `gridOptions` au constructeur Grid. La grille sera rendue à l'intérieur du `<div id="grid-wrapper">` que nous avons préparé précédemment.

```javascript
// Create the Grid instance using the previously built options
const grid = new Grid(gridOptions);

// Render the grid into the page
grid.render(document.getElementById("grid-wrapper"));
```

C’est tout. Le processus complet — de **créer une instance gridjsoptions** au rendu — prend moins d'une minute de codage.

### Résultat attendu

Lorsque vous ouvrez le fichier HTML dans un navigateur vous devriez voir :

- Une ligne d’en‑tête avec « ID », « Employee », « Salary ($) », « Dept. ».
- Des nombres de salaire alignés à droite (grâce à `NumberFormatAlignment`).
- Des contrôles de pagination en bas (si vous avez ajouté plus de dix lignes).
- Des en‑têtes de colonne cliquables qui trient ascendant/descendant.

Si quelque chose semble incorrect, ouvrez la console du navigateur (F12) et recherchez les messages d’erreur — la plupart des bugs proviennent d’identifiants de colonnes non correspondants ou de scripts de bibliothèque manquants.

## Étape 7 : Ajustements avancés (optionnel)

Voici quelques idées rapides que vous pouvez expérimenter une fois que la grille de base fonctionne.

| Fonctionnalité | Comment activer | Pourquoi c’est utile |
|----------------|-----------------|----------------------|
| **Rendu de cellule personnalisé** | `gridOptions.Columns[2].formatter = (cell) => \`<b>$${cell}</b>\`;` | Met en évidence les salaires en gras. |
| **Barre de recherche** | `gridOptions.Search = true;` | Permet aux utilisateurs de filtrer les lignes instantanément. |
| **Données côté serveur** | Set `gridOptions.Server = { url: "/api/employees", then: data => data.items };` | S’adapte à des milliers de lignes. |
| **Changement de thème** | Add `gridOptions.ClassName = "gridjs-theme-dark";` | Correspond aux conceptions en mode sombre. |

N'hésitez pas à combiner — Grid.js est délibérément flexible. Gardez simplement à l'esprit de conserver la ligne originale **créer une instance gridjsoptions** en haut ; tous les ajustements ultérieurs reposent sur cet unique objet.

## Conclusion

Nous venons de parcourir un flux de travail complet pour **créer une instance GridJsOptions** et **configurer les options de grille JavaScript** afin d’obtenir un tableau de données fonctionnel, triable et paginé. En partant d’une page HTML simple, nous avons chargé la bibliothèque, construit un objet d’options, activé l’alignement numérique, ajouté la pagination, défini les colonnes, et enfin rendu la grille.

Vous pouvez maintenant :

- Remplacer les `sampleData` statiques par un appel AJAX.
- Ajouter des formateurs personnalisés pour les dates, les devises ou les icônes.
- Intégrer la grille dans un framework comme React ou Vue (le même objet `gridOptions` fonctionne également).

Les possibilités sont pratiquement infinies, et le modèle que nous avons utilisé — centraliser tous les paramètres dans une seule instance `GridJsOptions` — maintient votre code propre et maintenable.

Vous avez un cas d’utilisation qui vous pose problème ? Laissez un commentaire, et nous l’explorerons ensemble. Bon codage, et amusez‑vous à créer des tableaux dynamiques avec Grid.js !

## Que devriez‑vous apprendre ensuite ?

- [Comment créer et configurer des classeurs Excel avec Aspose.Cells .NET : guide étape par étape](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Comment créer et styliser des tableaux Excel avec Aspose.Cells pour .NET | guide étape par étape](/cells/english/net/tables-structured-references/aspose-cells-net-excel-tables-styling/)
- [Comment créer et formater des cellules Excel avec Aspose.Cells pour Java : guide étape par étape](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}