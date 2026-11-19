---
category: general
date: 2026-11-19
description: Définir le format monétaire dans Excel avec C# – apprenez comment définir
  le format numérique et le style des colonnes Excel lors de l'importation d'une feuille
  de calcul.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set currency format
- how to set number format
- assign number format
- excel worksheet import
- style excel columns
language: fr
lastmod: 2026-11-19
og_description: Définissez le format monétaire dans Excel avec C# et découvrez comment
  définir le format des nombres, attribuer le format des nombres et styliser les colonnes
  Excel lors de l’importation d’une feuille de calcul.
og_image_alt: Screenshot showing Excel cells formatted as currency after import
og_title: Définir le format monétaire dans Excel avec C# – guide complet étape par
  étape
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Set currency format in Excel with C# – learn how to set number format
    and style excel columns during an excel worksheet import.
  headline: Set currency format while importing data into Excel using C#
  type: TechArticle
- description: Set currency format in Excel with C# – learn how to set number format
    and style excel columns during an excel worksheet import.
  name: Set currency format while importing data into Excel using C#
  steps:
  - name: Expected result
    text: 'When you open **FinancialReport.xlsx**, you’ll see:'
  - name: Assign number format to date columns
    text: '```csharp // Suppose column 2 contains dates and you want "dd-MMM-yyyy"
      columnStyles[2].Number = 14; // 14 = built‑in short date ```'
  - name: Use custom number formats for percentages
    text: '```csharp columnStyles[3].Custom = "0.00%"; // Shows 0.75 as 75.00% ```'
  - name: Styling beyond number formats
    text: 'You can also set font, background color, or alignment on the same `Style`
      object:'
  type: HowTo
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
- Formatting
title: Définir le format monétaire lors de l'importation de données dans Excel avec
  C#
url: /fr/net/excel-custom-number-date-formatting/set-currency-format-while-importing-data-into-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Définir le format monétaire lors de l'importation de données dans Excel avec C#

Si vous devez **définir le format monétaire** dans une feuille de calcul Excel, ce guide vous montre comment **définir le format numérique** et styliser les colonnes lors d’une **importation de feuille de calcul Excel**. Vous verrez un exemple complet et exécutable qui attribue le format numérique correct à chaque colonne d’un `DataTable` et importe les données avec le style souhaité.

Travailler avec Excel depuis C# nécessite souvent plus que de simplement vider des valeurs brutes — vous devez également contrôler l’apparence des nombres. Que vous génériez des factures, des rapports financiers ou des tableaux de bord, formater correctement les devises, les pourcentages ou les dates rend la sortie immédiatement lisible.

## Prérequis

* .NET 6.0 (ou version ultérieure) installé.
* Une référence à **Aspose.Cells for .NET** (ou toute bibliothèque exposant une classe `Style` avec une propriété `Number`).  
  *NuGet* : `Install-Package Aspose.Cells`.
* Familiarité de base avec `DataTable` et les collections C#.
* Un IDE tel que Visual Studio 2022 ou VS Code.

## Étape 1 : Récupérer les données à écrire dans la feuille de calcul

Commencez par obtenir un `DataTable` contenant les données brutes que vous souhaitez exporter. Dans des projets réels, cela peut provenir d’une requête de base de données, d’un appel d’API ou d’un analyseur CSV.

```csharp
using System.Data;

/// <summary>
/// Returns a sample DataTable with three columns:
/// Id (int), Amount (decimal), and Description (string).
/// </summary>
DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Amount", typeof(decimal));
    table.Columns.Add("Description", typeof(string));

    // Sample rows
    table.Rows.Add(1, 1234.56m, "Office supplies");
    table.Rows.Add(2, 98765.43m, "Consulting fees");
    table.Rows.Add(3, 0.99m, "Miscellaneous");

    return table;
}

// Retrieve the data
DataTable dataTable = GetData();
```

> **Pourquoi c’est important :** L’importation d’un `DataTable` entièrement rempli vous permet de séparer la logique de récupération des données de la logique de génération Excel, ce qui améliore la testabilité et la maintenabilité.

## Étape 2 : Créer un tableau de styles – une entrée par colonne du DataTable

Aspose.Cells attend un `Style[]` dont la longueur correspond au nombre de colonnes que vous prévoyez d’importer. Chaque élément peut contenir un format numérique spécifique.

```csharp
// Allocate a Style object for each column
Style[] columnStyles = new Style[dataTable.Columns.Count];

// Initialize each Style instance (required before assigning properties)
for (int i = 0; i < columnStyles.Length; i++)
{
    columnStyles[i] = ws.Workbook.CreateStyle();
}
```

> **Astuce :** Même si vous n’avez besoin de formatage que pour un sous‑ensemble de colonnes, vous devez tout de même créer une instance `Style` pour chaque colonne ; sinon vous obtiendrez une `NullReferenceException` lors de l’importation.

## Étape 3 : Attribuer le format numérique aux colonnes souhaitées

Les numéros de style intégrés diffèrent selon la bibliothèque. Dans Aspose.Cells :

* `0` → Général (entier)  
* `2` → Monétaire (p. ex., `$#,##0.00`)  
* `3` → Date, etc.

Ici nous **attribuons le format numérique** à deux colonnes : la première colonne (Id) reste un entier, tandis que la deuxième colonne (Amount) reçoit un format monétaire.

```csharp
// Column 0 → integer format (style number 0)
columnStyles[0].Number = 0;

// Column 1 → currency format (style number 2)
columnStyles[1].Number = 2;

// If you need a custom format, you can also use a format string:
// columnStyles[1].Custom = "$#,##0.00";
```

> **Comment définir le format numérique** : Utiliser la propriété `Number` est le moyen le plus rapide de choisir un format intégré. Pour des devises spécifiques à une locale, envisagez d’utiliser une chaîne de format personnalisée incluant le symbole monétaire approprié.

## Étape 4 : Importer le DataTable dans la feuille de calcul, en appliquant les styles de colonne

Maintenant que le tableau de styles est prêt, importez les données. La méthode `ImportDataTable` respecte les styles que vous avez fournis.

```csharp
// Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();
Worksheet ws = workbook.Worksheets[0];

// Import the DataTable, starting at cell A1 (row 0, column 0)
// The third argument (true) tells the method to write column headers.
ws.Cells.ImportDataTable(
    dataTable,
    /* includeColumnNames */ true,
    /* startRow */ 0,
    /* startColumn */ 0,
    columnStyles);

// Save the workbook
workbook.Save("FinancialReport.xlsx", SaveFormat.Xlsx);
```

### Résultat attendu

Lorsque vous ouvrez **FinancialReport.xlsx**, vous verrez :

| Id | Amount      | Description      |
|----|------------|------------------|
| 1  | $1,234.56  | Office supplies |
| 2  | $98,765.43 | Consulting fees |
| 3  | $0.99      | Miscellaneous    |

*La colonne **Amount** est affichée en utilisant le format monétaire que vous avez défini, tandis que **Id** reste un entier.*

## Comment définir le format numérique pour des scénarios supplémentaires

### Attribuer le format numérique aux colonnes de date

```csharp
// Suppose column 2 contains dates and you want "dd-MMM-yyyy"
columnStyles[2].Number = 14; // 14 = built‑in short date
```

### Utiliser des formats numériques personnalisés pour les pourcentages

```csharp
columnStyles[3].Custom = "0.00%"; // Shows 0.75 as 75.00%
```

### Styliser au-delà des formats numériques

Vous pouvez également définir la police, la couleur d’arrière‑plan ou l’alignement sur le même objet `Style` :

```csharp
columnStyles[1].Font.IsBold = true;
columnStyles[1].ForegroundColor = Color.LightYellow;
columnStyles[1].HorizontalAlignment = TextAlignmentType.Center;
```

> **Pourquoi cela fonctionne :** L’objet `Style` regroupe toutes les propriétés visuelles d’une cellule. Lorsque vous transmettez le tableau à `ImportDataTable`, chaque cellule hérite automatiquement du style défini.

## Pièges courants et comment les éviter

| Piège | Symptôme | Solution |
|-------|----------|----------|
| Oublier d’instancier chaque `Style` | `NullReferenceException` lors de l’importation | Parcourir le tableau et appeler `CreateStyle()` avant de définir les propriétés. |
| Utiliser le mauvais index de nombre intégré | Mauvais format (p. ex., les dates apparaissent comme des entiers) | Consultez la documentation de la bibliothèque pour les constantes `Number` correctes. |
| Ne pas enregistrer le classeur | Aucun fichier de sortie ou fichier vide | Appelez `workbook.Save(...)` après la fin de l’importation. |
| Incohérence de locale pour le symbole monétaire | `$` apparaît même dans les locales non‑US | Utilisez une chaîne de format personnalisée avec le symbole approprié (p. ex., `"€#,##0.00"`). |

## Exemple complet et exécutable



## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Créer un fichier Excel c# – styliser les cellules et définir le format monétaire](/cells/english/net/excel-formatting-and-styling/create-excel-file-c-style-cells-and-set-currency-format/)
- [Comment formater les colonnes Excel en C# – Guide complet](/cells/english/net/formatting-rows-and-columns-in-excel/how-to-format-excel-columns-in-c-complete-guide/)
- [Créer un classeur Excel C# – Appliquer le format monétaire et importer DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}