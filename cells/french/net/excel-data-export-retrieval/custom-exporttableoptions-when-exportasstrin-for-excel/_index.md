---
category: general
date: 2026-10-26
description: Les options personnalisées ExportTableOptions lors de ExportAsString
  vous permettent d’exporter les données Excel sous forme de chaînes en C#. Suivez
  le guide étape par étape pour configurer et lancer l’exportation.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- Custom ExportTableOptions when ExportAsStrin
- how to export excel as string
- ExportTableOptions C#
- Excel to DataTable string conversion
- Aspose.Cells export as string
language: fr
lastmod: 2026-10-26
og_description: Options d'ExportTable personnalisées lorsque ExportAsStrin active
  l'exportation Excel uniquement sous forme de chaîne. Apprenez les étapes exactes
  pour configurer et exécuter l'exportation en C#.
og_image_alt: Code snippet showing ExportTableOptions configuration for string export
og_title: Options ExportTableOptions personnalisées lors d'ExportAsString – exporter
  Excel en chaîne en C#
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Custom ExportTableOptions when ExportAsStrin lets you export Excel
    data as strings in C#. Follow the step‑by‑step guide to configure and run the
    export.
  headline: Custom ExportTableOptions when ExportAsStrin for Excel
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: Options ExportTable personnalisées lors de ExportAsStrin pour Excel
url: /fr/net/excel-data-export-retrieval/custom-exporttableoptions-when-exportasstrin-for-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Options d'ExportTableOptions personnalisées lorsqu'ExportAsStrin – exporter Excel en tant que chaîne en C#

Si vous avez besoin de **Custom ExportTableOptions when ExportAsStrin** pour obtenir chaque valeur de cellule sous forme de chaîne simple, ce guide vous montre exactement comment le faire. Que vous construisiez un pipeline d'importation de données ou que vous ayez besoin d'un dump prêt pour CSV, vous verrez pourquoi configurer les options de cette manière évite les surprises de conversion de type.

Dans ce tutoriel, vous apprendrez **comment exporter excel as string** en utilisant la bibliothèque Aspose.Cells, vous verrez le code complet et exécutable, et vous comprendrez la logique derrière chaque paramètre. Aucune documentation externe n'est requise – tout ce dont vous avez besoin se trouve ici.

## Prérequis

Avant de commencer, assurez‑vous d'avoir :

* le SDK .NET 6.0 ou une version ultérieure installé  
* Visual Studio 2022 (ou tout IDE supportant .NET)  
* le package Aspose.Cells for .NET (installer via NuGet : `Install-Package Aspose.Cells`)  
* un classeur Excel (`sample.xlsx`) placé dans le répertoire racine du projet  

Ces éléments sont les seules dépendances ; le code fonctionne sous Windows, Linux ou macOS sans bibliothèques supplémentaires.

## Étape 1 : Charger le classeur que vous souhaitez exporter

La première chose à faire lorsque vous utilisez **Custom ExportTableOptions when ExportAsStrin** est d'obtenir un objet `Worksheet` à partir d'un classeur chargé. Cet objet vous donne accès aux lignes, colonnes et à l'API d'exportation.

```csharp
using Aspose.Cells;
using System.Data;

// Load the workbook from disk
Workbook workbook = new Workbook("sample.xlsx");

// Get the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];
```

*Pourquoi c’est important :*  
`Workbook` lit le fichier une fois et conserve toutes les informations de formatage en mémoire. En sélectionnant un `Worksheet` spécifique, vous limitez la portée de l'exportation et évitez le traitement inutile de feuilles masquées.

## Étape 2 : Configurer ExportTableOptions avec ExportAsString = true

Le cœur de **Custom ExportTableOptions when ExportAsStrin** est l'objet `ExportTableOptions`. Définir `ExportAsString` force l'exportateur à traiter chaque cellule comme une chaîne, quel que soit son type de données d'origine (date, nombre, booléen, etc.). Activer `PreserveFormatting` conserve le style visuel (par ex., les symboles monétaires) dans la chaîne résultante.

```csharp
// Create and configure the export options
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Export every cell value as a string
    PreserveFormatting = true      // Keep the original cell formatting
};
```

*Pourquoi c’est important :*  
Lorsque vous appelez ensuite `ExportDataTable`, la bibliothèque tente normalement d'inférer le type .NET de chaque colonne. Avec `ExportAsString = true`, cette étape d'inférence est sautée, évitant les conversions inattendues en `DateTime` ou `double` qui pourraient casser les analyseurs CSV en aval.

## Étape 3 : Exporter une plage vers un DataTable en utilisant les options personnalisées

Vous pouvez maintenant exporter une plage rectangulaire (lignes 0‑9, colonnes 0‑4) depuis la feuille de calcul. La méthode renvoie un `DataTable` où chaque champ est une `string`.

```csharp
// Export rows 0‑9 and columns 0‑4 (5 columns total) as a DataTable
DataTable dataTable = worksheet.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: 10,
    totalColumns: 5,
    options: exportOptions);
```

*Pourquoi c’est important :*  
`ExportDataTable` est le moyen le plus pratique de transférer des données Excel vers une structure relationnelle que de nombreuses API .NET comprennent déjà (par ex., Entity Framework, Dapper). En passant les **Custom ExportTableOptions when ExportAsStrin**, vous garantissez que chaque `DataColumn.DataType` sera `typeof(string)`.

## Étape 4 : Vérifier le résultat – toutes les valeurs sont des chaînes

Il est recommandé de confirmer que l'exportation s'est déroulée comme prévu. La boucle suivante affiche chaque cellule et son type d'exécution.

```csharp
Console.WriteLine("Exported DataTable (all values as strings):");
foreach (DataRow row in dataTable.Rows)
{
    for (int i = 0; i < dataTable.Columns.Count; i++)
    {
        object value = row[i];
        Console.Write($"{value} ({value.GetType().Name})\t");
    }
    Console.WriteLine();
}
```

**Sortie attendue**

```
123 (String)    2023‑01‑15 (String)    $45.67 (String)    TRUE (String)    Sample text (String)
...
```

Chaque cellule indique `String` comme type, confirmant que **Custom ExportTableOptions when ExportAsStrin** a fonctionné correctement.

## Étape 5 : Optionnel – écrire le DataTable en CSV

Si votre objectif final est un fichier texte simple, vous pouvez facilement sérialiser le `DataTable` en CSV :



## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets et fonctionnels avec des explications pas à pas pour vous aider à maîtriser d'autres fonctionnalités de l'API et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Export HTML Strings from Excel to DataTable using Aspose.Cells for .NET: A Step‑by‑Step Guide](/cells/english/net/import-export/export-html-strings-excel-datatable-aspose-cells-net/)
- [Export Custom Properties Excel Pdf Aspose Cells Net](/cells/hongkong/net/workbook-operations/export-custom-properties-excel-pdf-aspose-cells-net/)
- [Aspose Cells Java Custom Load Filters Excel Export](/cells/hongkong/java/import-export/aspose-cells-java-custom-load-filters-excel-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}