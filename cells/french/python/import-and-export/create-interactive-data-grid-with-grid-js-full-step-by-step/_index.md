---
category: general
date: 2026-06-21
description: Créez une grille de données interactive avec Grid.js et apprenez à afficher
  un tableau de données JSON avec tri, pagination et recherche. Parfait pour les tableaux
  de bord web.
draft: false
keywords:
- create interactive data grid
- display json data table
- how to use gridjs
language: fr
og_description: Créez une grille de données interactive en quelques minutes. Apprenez
  à utiliser Grid.js pour afficher un tableau de données JSON avec pagination, tri
  et recherche.
og_title: Créer une grille de données interactive avec Grid.js – Tutoriel complet
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create interactive data grid using Grid.js and learn how to display
    JSON data table with sorting, pagination, and search. Perfect for web dashboards.
  headline: Create Interactive Data Grid with Grid.js – Full Step‑by‑Step Guide
  type: TechArticle
- description: Create interactive data grid using Grid.js and learn how to display
    JSON data table with sorting, pagination, and search. Perfect for web dashboards.
  name: Create Interactive Data Grid with Grid.js – Full Step‑by‑Step Guide
  steps:
  - name: A modern browser (Chrome, Edge, or Firefox) – Grid.js relies on ES6 features.
    text: A modern browser (Chrome, Edge, or Firefox) – Grid.js relies on ES6 features.
  - name: A local or remote folder containing a `grid_data.json` file (we’ll show
      the format).
    text: A local or remote folder containing a `grid_data.json` file (we’ll show
      the format).
  - name: Basic familiarity with HTML and JavaScript – nothing fancy, just the ability
      to open a `.html` file in a browser.
    text: Basic familiarity with HTML and JavaScript – nothing fancy, just the ability
      to open a `.html` file in a browser.
  type: HowTo
tags:
- JavaScript
- Grid.js
- Data Visualization
title: Créer une grille de données interactive avec Grid.js – Guide complet étape
  par étape
url: /fr/python/import-and-export/create-interactive-data-grid-with-grid-js-full-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créez une grille de données interactive avec Grid.js – Guide complet étape par étape

Vous êtes-vous déjà demandé comment **créer une grille de données interactive** qui permet aux utilisateurs de trier, rechercher et paginer les lignes sans écrire de backend ? Vous n'êtes pas seul. Dans de nombreux tableaux de bord, le principal problème est de transformer un dump JSON statique en un tableau élégant et recherchable—quelque chose d’aussi fluide qu’une feuille de calcul mais qui fonctionne entièrement dans le navigateur.

Dans ce tutoriel, nous allons parcourir **comment utiliser Grid.js** pour **afficher un tableau de données JSON** sur une page HTML simple. À la fin, vous disposerez d’un exemple fonctionnel que vous pourrez intégrer dans n’importe quel projet, ainsi que de conseils pour personnaliser la barre d’outils, gérer de grands ensembles de données et éviter les pièges courants.

## Ce que vous allez apprendre

- Comment récupérer un fichier JSON qui définit les colonnes et les lignes.
- Comment initialiser **Grid.js** avec pagination, tri, recherche et une barre d’outils personnalisée.
- Comment rendre la grille dans un conteneur cible.
- Ajustements optionnels : formatage de cellules personnalisé, changement de thème et gestion des erreurs.
- Un exemple complet, prêt à copier‑coller.

### Prérequis

Avant de commencer, assurez‑vous d’avoir :

1. Un navigateur moderne (Chrome, Edge ou Firefox) – Grid.js repose sur les fonctionnalités ES6.  
2. Un dossier local ou distant contenant un fichier `grid_data.json` (nous montrerons le format).  
3. Une connaissance de base du HTML et du JavaScript – rien de sophistiqué, juste la capacité d’ouvrir un fichier `.html` dans un navigateur.

Aucun outil de construction, aucune installation npm, aucun code côté serveur. C’est la beauté de **créer une grille de données interactive** avec Grid.js : cela fonctionne directement depuis un CDN.

---

## Étape 1 : Préparer le JSON qui définit votre tableau

La première chose dont vous avez besoin est une charge JSON qui indique à Grid.js quelles colonnes existent et quelles lignes afficher. Considérez‑le comme le plan de votre **affichage du tableau de données JSON**. Voici un exemple minimal que vous pouvez enregistrer sous le nom `grid_data.json` dans le même répertoire que votre fichier HTML :

```json
{
  "columns": ["ID", "Name", "Email", "Country"],
  "rows": [
    [1, "Alice Johnson", "alice@example.com", "USA"],
    [2, "Bob Smith", "bob@example.com", "Canada"],
    [3, "Carlos Ruiz", "carlos@example.com", "Mexico"],
    [4, "Diana Lee", "diana@example.com", "UK"]
  ]
}
```

*Pourquoi ce format ?* Grid.js attend que `columns` soit un tableau de chaînes (ou d’objets pour une configuration avancée) et que `rows` soit un tableau de tableaux où chaque tableau interne correspond à l’ordre des colonnes. Vous pouvez bien sûr ajouter d’autres colonnes ou des objets imbriqués — Grid.js les rendra tant que les formes correspondent.

> **Astuce :** Si vous récupérez les données depuis une API, remplacez simplement le `fetch('grid_data.json')` statique par l’URL de votre endpoint. Le reste du code reste identique.

---

## Étape 2 : Initialiser Grid.js – Le cœur de **how to use gridjs**

Maintenant que la source de données est prête, nous devons charger Grid.js sur la page et lui indiquer comment se comporter. C’est ici que nous implémentons réellement la fonctionnalité **créez une grille de données interactive** : pagination, tri et bouton de barre d’outils pratique.

```html
<!-- Load Grid.js from the CDN -->
<script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
<link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
```

Le CDN vous fournit la dernière version stable, et le thème Mermaid ajoute un rendu propre et moderne dès le départ. Vous pouvez le remplacer par `gridjs.min.css` si vous préférez le style par défaut.

Ensuite, dans une balise `<script>`, récupérez le JSON et initialisez la grille :

```javascript
// Step 2: Initialise Grid.js with pagination, sorting, searching, and a toolbar
fetch('grid_data.json')
  .then(response => response.json())
  .then(data => {
    const grid = new gridjs.Grid({
      columns: data.columns,      // Pull column headers from JSON
      data: data.rows,            // Pull row data from JSON
      pagination: { enabled: true, limit: 10 }, // Show 10 rows per page
      sort: true,                 // Enable column sorting
      search: true,               // Add a search box above the grid
      toolbar: {
        enabled: true,
        items: [
          {
            type: 'button',
            text: 'Help',
            onClick: () => alert('Use the search box to filter rows or click column headers to sort.')
          }
        ]
      },
      // Optional: custom cell formatter for the Email column
      // This demonstrates a deeper dive into how to use Grid.js
      // and shows you can embed HTML inside cells.
      columns: data.columns.map(col => {
        if (col === 'Email') {
          return {
            name: col,
            formatter: cell => gridjs.html(`<a href="mailto:${cell}">${cell}</a>`)
          };
        }
        return col; // Simple string for other columns
      })
    });

    // Step 3: Render the grid into the target container
    grid.render(document.getElementById('grid-container'));
  })
  .catch(err => console.error('Failed to load grid data:', err));
```

### Décortication des options

| Option | Ce que ça fait | Pourquoi c’est important |
|--------|----------------|---------------------------|
| `pagination` | Divise les lignes en pages (10 par défaut) | Garde les tables volumineuses utilisables sans surcharger l’interface. |
| `sort` | Les en‑têtes de colonnes cliquables basculent entre ordre croissant et décroissant | Les utilisateurs trouvent rapidement les lignes aux valeurs les plus élevées. |
| `search` | Ajoute un champ texte qui filtre les lignes en temps réel | Idéal pour des recherches ad‑hoc sans recharger les données. |
| `toolbar` | Ajoute des boutons ou listes déroulantes au-dessus de la grille | Parfait pour les actions « Aide », « Export » ou « Rafraîchir ». |
| `formatter` | Vous permet de renvoyer du HTML brut pour une cellule | Ici nous transformons les adresses e‑mail en liens cliquables `mailto`. |

> **Pourquoi cette approche ?** En gardant la configuration de la grille déclarative, vous pouvez ajuster le comportement facilement sans toucher à la logique de rendu principale. C’est la méthode recommandée pour **how to use Grid.js** dans la plupart des projets.

---

## Étape 3 : Rendre la grille dans votre page

La dernière ligne du script—`grid.render(document.getElementById('grid-container'))`—injecte le tableau entièrement fonctionnel dans un `<div>` que vous avez placé quelque part dans le corps de votre HTML :

```html
<div id="grid-container"></div>
```

C’est tout. Lorsque la page se charge, le navigateur récupère le JSON, construit l’instance Grid.js et dessine le tableau interactif à l’écran. Aucun rafraîchissement, aucun appel serveur après le chargement initial.

---

## Optionnel : Ajustements de style et de thème

Si le thème Mermaid par défaut n’est pas à votre goût, vous pouvez le remplacer par n’importe quel thème intégré (`gridjs.min.css`) ou écrire votre propre CSS. Par exemple, pour donner à l’en‑tête un fond gris doux :

```css
.gridjs-th {
  background-color: #f5f5f5;
}
```

Ajoutez le fragment dans une balise `<style>` ou une feuille de style externe. Grid.js respecte les sélecteurs CSS standards, vous avez donc un contrôle total sur les polices, les couleurs et les espacements.

---

## Pièges courants & comment les éviter

| Piège | Symptom | Solution |
|-------|---------|----------|
| **Erreurs CORS** lors du fetch du JSON depuis un autre domaine | La console du navigateur affiche « Blocked by CORS policy » | Hébergez le JSON sur la même origine ou activez CORS sur le serveur. |
| **Ensembles de données volumineux provoquant des lenteurs** | Le défilement devient saccadé, la pagination lente | Utilisez la pagination côté serveur (`pagination: { server: { url: (prev, page, limit) => … } }`) ou le chargement paresseux des lignes. |
| **Le bouton de la barre d’outils n’apparaît pas** | Aucun bouton visible malgré `toolbar.enabled: true` | Vérifiez que vous utilisez Grid.js version 2.0+ ; les versions antérieures avaient une API de barre d’outils différente. |
| **Les liens e‑mail ne sont pas cliquables** | Le formatter renvoie du texte brut | Retournez `gridjs.html(...)` au lieu d’une chaîne simple, comme montré dans l’exemple. |

Résoudre ces problèmes dès le départ vous fera gagner des heures de débogage plus tard.

---

## Exemple complet fonctionnel (prêt à copier‑coller)

Voici le fichier HTML complet que vous pouvez enregistrer sous le nom `index.html`. Ouvrez‑le dans un navigateur et vous verrez une démonstration pleinement fonctionnelle de **créez une grille de données interactive** affichant un **tableau de données JSON** avec tri, recherche et bouton d’aide.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Create Interactive Data Grid with Grid.js</title>
  <!-- Grid.js core library -->
  <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
  <!-- Optional theme – Meri­maid -->
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
  <style>
    /* Simple custom styling */
    body { font-family: Arial, sans-serif; margin: 20px; }
    .gridjs-container { max-width: 900px; margin: auto; }
    .gridjs-th { background-color: #f0f8ff; }
  </style>
</head>
<body>
  <h1>Create Interactive Data Grid with Grid.js</h1>
  <p>This page demonstrates how to <strong>display JSON data table</strong> using Grid.js. Feel free to edit <code>grid_data.json</code> and refresh.</p>

  <!-- Grid will be rendered here -->
  <div id="grid-container"></div>

  <script>
    // Load JSON data and initialise Grid.js
    fetch('grid_data.json')
      .then(r => r.json())
      .then(data => {
        const grid = new gridjs.Grid({
          columns: data.columns.map(col => {
            // Custom formatter for Email column
            if (col === 'Email') {
              return {
                name: col,
                formatter: cell => gridjs.html(`<a href="mailto:${cell}">${cell}</a>`)
              };
            }
            return col;
          }),
          data: data.rows,
          pagination: { enabled: true, limit: 5 },
          sort: true,
          search: true,
          toolbar: {
            enabled: true,
            items: [
              {
                type: 'button',
                text: 'Formula Help',
                onClick: () => alert('Hover over a cell to see its formula description.')
              }
            ]
          }
        });

        // Render the grid
        grid.render(document.getElementById('grid-container'));
      })
      .catch(err => console.error('Error loading grid data:', err));
  </script>
</body>
</html


## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités d’API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [How to Create an Excel Data Validation List with Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/data-validation/excel-data-validation-aspose-cells-java/)
- [How to Create Checkboxes in Excel using Aspose.Cells for .NET | Data Validation Tutorial](/cells/english/net/data-validation/create-checkboxes-net-excel-aspose-cells/)
- [Create & Import XML Data into Excel Using Aspose.Cells for Java](/cells/english/java/import-export/create-import-xml-data-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}