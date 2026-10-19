---
category: general
date: 2026-05-30
description: Apprenez à ajouter des couleurs de lignes alternées dans les feuilles
  de calcul C#, à définir l'arrière-plan des cellules avec un motif de remplissage
  uni, et à personnaliser le style des cellules de la feuille de calcul sans effort.
draft: false
keywords:
- alternating row colors
- set cell background
- solid fill pattern
- add background color
- worksheet cell style
language: fr
og_description: Couleurs de lignes alternées dans les feuilles de calcul C# simplifiées.
  Apprenez à définir l’arrière‑plan des cellules, à utiliser un motif de remplissage
  uni et à maîtriser le style des cellules de la feuille.
og_title: Couleurs de lignes alternées dans les feuilles de calcul C# – Guide complet
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Learn how to add alternating row colors in C# worksheets, set cell
    background with a solid fill pattern, and customize worksheet cell style effortlessly.
  headline: Alternating Row Colors in C# Worksheets – Complete Guide
  type: TechArticle
- description: Learn how to add alternating row colors in C# worksheets, set cell
    background with a solid fill pattern, and customize worksheet cell style effortlessly.
  name: Alternating Row Colors in C# Worksheets – Complete Guide
  steps:
  - name: Why Use a **Solid Fill Pattern**?
    text: The `Pattern` property tells the engine how to render the color. A `Solid`
      fill guarantees that the entire cell background is painted, eliminating any
      faint gridlines that might otherwise show through. This is the most common way
      to **set cell background** when you want a clean look.
  - name: Change the Colors
    text: 'If your brand uses different hues, just replace `Color.LightYellow` and
      `Color.LightCyan` with any `System.Drawing.Color` you prefer. For example:'
  - name: Use a Different **Background Type**
    text: While `BackgroundType.Solid` is the most common, you can experiment with
      `BackgroundType.Gray125`, `BackgroundType.Horizontal`, or any pattern that the
      library supports. This changes the visual texture while still **adding background
      color**.
  - name: Apply a **Worksheet Cell Style** to Specific Columns
    text: 'Sometimes you only want the alternating effect on data columns, leaving
      the first column (e.g., IDs) untouched. Create a separate style for that column
      and assign it after the import:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- DataTable
- Styling
title: Couleurs de lignes alternées dans les feuilles de calcul C# – Guide complet
url: /fr/net/excel-colors-and-background-settings/alternating-row-colors-in-c-worksheets-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Couleurs de ligne alternées dans les feuilles de calcul C# – Guide complet

Vous êtes‑vous déjà demandé comment rendre votre export Excel plus élégant en utilisant des **couleurs de ligne alternées** ? Vous n'êtes pas seul — les développeurs demandent constamment comment *ajouter une couleur d'arrière‑plan* aux lignes sans écrire des millions de lignes de code.  

Dans ce tutoriel, nous allons parcourir une méthode simple pour **définir l’arrière‑plan des cellules** sur chaque ligne, appliquer un **motif de remplissage solide**, et contrôler le **style de cellule de la feuille de calcul** afin que le résultat soit à la fois lisible et visuellement attrayant.

## Ce que vous allez apprendre

- Récupérer des données dans un `DataTable` (ou toute source tabulaire).  
- Construire un tableau d'objets `Style` qui alternent entre deux couleurs.  
- Importer le `DataTable` dans une feuille de calcul tout en appliquant ces styles.  
- Vérifier le résultat et ajuster les couleurs ou les motifs si nécessaire.  

Aucun outil externe n’est nécessaire au‑delà d’un environnement .NET et d’une bibliothèque de feuilles de calcul (nous utiliserons **Aspose.Cells** dans les exemples). À la fin, vous disposerez d’une méthode réutilisable que vous pourrez intégrer à n’importe quel pipeline de reporting.

---

## Étape 1 : Récupérer les données sources sous forme de `DataTable`

First things first—without data there’s nothing to style. Below is a tiny helper that builds a `DataTable` with sample rows. In a real project you’d replace this with a database call or CSV parser.

```csharp
using System;
using System.Data;

static DataTable GetData()
{
    // Create a simple table with three columns
    DataTable table = new DataTable("Report");
    table.Columns.Add("ID", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    // Populate with dummy rows
    for (int i = 1; i <= 10; i++)
    {
        table.Rows.Add(i, $"Item {i}", Math.Round(new Random().NextDouble() * 100, 2));
    }

    return table;
}
```

> **Pourquoi c’est important :** Disposer des données dans un `DataTable` permet au moteur de feuille de calcul de les *importer* en un seul appel, en préservant automatiquement les noms de colonnes et les types de données.

## Étape 2 : Créer les styles de **couleurs de ligne alternées**

Now we’ll generate an array of `Style` objects—one per row—so that even rows get a light yellow shade while odd rows receive a gentle cyan. This is the core of the **alternating row colors** technique.

```csharp
using Aspose.Cells;
using System.Drawing;

// Assume workbook and worksheet are already instantiated
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Retrieve data
DataTable dataTable = GetData();

// Prepare an array of styles – one for each row in the table
Style[] rowStyles = new Style[dataTable.Rows.Count];

for (int i = 0; i < rowStyles.Length; i++)
{
    // Create a fresh style for the current row
    rowStyles[i] = workbook.CreateStyle();

    // **Add background color**: LightYellow for even rows, LightCyan for odd rows
    rowStyles[i].ForegroundColor = (i % 2 == 0)
        ? Color.LightYellow
        : Color.LightCyan;

    // **Set cell background** using a **solid fill pattern**
    rowStyles[i].Pattern = BackgroundType.Solid;

    // Optional: you could also set font color, borders, etc., here
}
```

### Pourquoi utiliser un **motif de remplissage solide** ?

The `Pattern` property tells the engine how to render the color. A `Solid` fill guarantees that the entire cell background is painted, eliminating any faint gridlines that might otherwise show through. This is the most common way to **set cell background** when you want a clean look.

## Étape 3 : Importer le `DataTable` avec les styles préparés

With the style array ready, the import call becomes a one‑liner. Aspose.Cells will apply the corresponding style to each row automatically.

```csharp
// Import the DataTable into the worksheet, applying the prepared styles
worksheet.Cells.ImportDataTable(
    dataTable,                     // source
    true,                          // include column names
    0,                             // start row (0‑based)
    0,                             // start column (0‑based)
    rowStyles);                    // array of styles
```

> **Que se passe-t-il en coulisses ?**  
> La bibliothèque parcourt chaque ligne, copie les valeurs dans les cellules, puis applique le `Style` correspondant depuis `rowStyles`. Comme nous avons déjà défini un **motif de remplissage solide**, chaque cellule d’une ligne hérite de la même couleur d’arrière‑plan, vous offrant ainsi des **couleurs de ligne alternées** parfaites.

## Étape 4 : Enregistrer le classeur et vérifier le résultat

A quick save lets you open the file in Excel (or any compatible viewer) and see the effect.

```csharp
// Save to disk – you can change the format to .xlsx, .xls, .csv, etc.
workbook.Save("AlternatingRowsReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Workbook saved. Open 'AlternatingRowsReport.xlsx' to see the result.");
```

When you open the file, rows 1, 3, 5… will be light yellow, while rows 2, 4, 6… will be light cyan. The column headers stay white, making the data stand out.

![Feuille de calcul affichant des couleurs de ligne alternées](/images/alternating-row-colors.png "Capture d’écran d’une feuille de calcul avec des couleurs de ligne alternées")

*Texte alternatif de l’image :* **alternating row colors** capture d’écran d’une feuille de calcul où l’arrière‑plan de chaque ligne alterne entre jaune clair et cyan clair.

## Étape 5 : Personnalisation supplémentaire (facultatif)

### Modifier les couleurs

If your brand uses different hues, just replace `Color.LightYellow` and `Color.LightCyan` with any `System.Drawing.Color` you prefer. For example:

```csharp
rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.FromArgb(255, 235, 205) // Peach
                                            : Color.FromArgb(205, 235, 255); // Soft blue
```

### Utiliser un **type d’arrière‑plan** différent

While `BackgroundType.Solid` is the most common, you can experiment with `BackgroundType.Gray125`, `BackgroundType.Horizontal`, or any pattern that the library supports. This changes the visual texture while still **adding background color**.

### Appliquer un **style de cellule de feuille de calcul** à des colonnes spécifiques

Sometimes you only want the alternating effect on data columns, leaving the first column (e.g., IDs) untouched. Create a separate style for that column and assign it after the import:

```csharp
Style idStyle = workbook.CreateStyle();
idStyle.ForegroundColor = Color.White;
idStyle.Pattern = BackgroundType.Solid;

// Apply to the first column (A)
for (int row = 0; row < dataTable.Rows.Count + 1; row++) // +1 for header
{
    worksheet.Cells[row, 0].SetStyle(idStyle);
}
```

---

## Conclusion

You now have a complete, reusable solution for **alternating row colors** in C# worksheets. By building an array of `Style` objects, **setting cell background** with a **solid fill pattern**, and importing a `DataTable` in one call, you can produce professional‑looking reports with minimal code.  

From here you might:

- **Ajouter une couleur d'arrière‑plan** aux lignes d’en‑tête pour plus d’accentuation.  
- Combiner la technique avec le formatage conditionnel pour des repères visuels dynamiques.  
- Explorer d’autres propriétés du **style de cellule de feuille de calcul** comme les polices, les bordures ou les formats numériques.

Give it a try in your next export routine—your users will thank you for the cleaner, more readable spreadsheets. Happy coding!

## Que devriez‑vous apprendre ensuite ?

- [Définir la hauteur des lignes dans une feuille de calcul avec Aspose.Cells pour .NET](/cells/english/net/size-and-spacing-customization/setting-height-of-all-rows-in-worksheet/)
- [Convertir les noms de cellules Excel en indices de ligne et de colonne avec Aspose.Cells pour .NET](/cells/english/net/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-dotnet/)
- [Définir les couleurs des onglets de feuille de calcul dans Excel avec Aspose.Cells .NET – Guide complet](/cells/english/net/worksheet-management/set-worksheet-tab-colors-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}