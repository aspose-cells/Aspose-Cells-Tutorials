---
category: general
date: 2026-10-01
description: Couleurs de colonnes alternées dans Excel avec C# – apprenez à créer
  un fichier Excel à partir d’un DataTable, définir la couleur d’arrière‑plan d’une
  cellule en C#, et importer un DataTable dans Excel avec des colonnes stylisées.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- alternating column colors excel
- set cell background color c#
- create excel file from datatable c#
- import datatable to excel
language: fr
lastmod: 2026-10-01
og_description: Couleurs de colonnes alternées dans Excel, c’est facile. Suivez ce
  guide pour créer un fichier Excel à partir d’un DataTable, définir la couleur d’arrière‑plan
  des cellules en C# et importer un DataTable vers Excel avec des colonnes stylisées.
og_image_alt: Screenshot of an Excel sheet showing alternating column colors applied
  by C# code
og_title: Ajouter des couleurs de colonnes alternées dans Excel avec C# – guide étape
  par étape
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: alternating column colors excel using C# – learn to create an Excel
    file from a DataTable, set cell background color c#, and import datatable to excel
    with styled columns.
  headline: How to add alternating column colors in Excel using C#
  type: TechArticle
tags:
- C#
- Excel automation
- Aspose.Cells
title: Comment ajouter des couleurs de colonnes alternées dans Excel avec C#
url: /fr/net/excel-colors-and-background-settings/how-to-add-alternating-column-colors-in-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment ajouter des couleurs de colonnes alternées dans Excel avec C#

Si vous avez besoin de **alternating column colors excel** dans un rapport généré par votre application, ce guide vous montre une solution complète. Vous verrez comment créer un fichier Excel à partir d’un `DataTable`, définir la couleur d’arrière‑plan des cellules en style C#, et importer le datatable vers Excel tout en appliquant un style distinct à chaque colonne.

Le tutoriel couvre tout ce dont vous avez besoin : les packages NuGet requis, un exemple de code complet et exécutable, et des explications sur l’importance de chaque étape. À la fin, vous disposerez d’un classeur stylisé qui pourra être ouvert directement dans Microsoft Excel.

## Prérequis

* .NET 6.0 (ou supérieur) SDK installé  
* Visual Studio 2022 (ou tout IDE compatible C#)  
* La bibliothèque **Aspose.Cells for .NET** – installez‑la avec  

```bash
dotnet add package Aspose.Cells
```

Aspose.Cells fournit les classes `Workbook`, `Worksheet`, `Style` et `BackgroundType` utilisées dans l’exemple.

## Étape 1 : Récupérer les données source sous forme de `DataTable`

La première tâche consiste à obtenir les données que vous souhaitez exporter. Dans des projets réels, vous pouvez remplir le `DataTable` à partir d’une requête de base de données, d’un appel d’API ou de toute collection en mémoire.

```csharp
using System;
using System.Data;
using Aspose.Cells;

static DataTable GetData()
{
    // Create a sample DataTable with three columns and five rows
    DataTable table = new DataTable("Sample");
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    for (int i = 1; i <= 5; i++)
    {
        table.Rows.Add(i, $"Student {i}", 60 + i * 5);
    }
    return table;
}
```

**Pourquoi c’est important :**  
Un `DataTable` est un conteneur universel qui se mappe proprement à une feuille de calcul Excel. Utiliser un `DataTable` vous permet de **create excel file from datatable c#** sans écrire de boucles personnalisées pour chaque colonne.

## Étape 2 : Créer un nouveau classeur et obtenir sa première feuille de calcul

```csharp
// Initialize a new workbook – this represents the Excel file
Workbook workbook = new Workbook();

// The first worksheet is created by default
Worksheet worksheet = workbook.Worksheets[0];
```

**Explication :**  
`Workbook` est l’objet racine ; `Worksheets[0]` vous donne la feuille par défaut où les données seront placées.

## Étape 3 : Préparer un style distinct pour chaque colonne (couleurs d’arrière‑plan alternées)

Pour obtenir **alternating column colors excel**, nous générons un `Style` pour chaque colonne et attribuons une couleur d’arrière‑plan claire qui alterne entre deux nuances.

```csharp
// Determine how many columns we have
int columnCount = dataTable.Columns.Count;
Style[] columnStyles = new Style[columnCount];

// Create a style for each column
for (int i = 0; i < columnCount; i++)
{
    // Create a fresh style instance
    Style style = workbook.CreateStyle();

    // Alternate between LightYellow and LightCyan
    style.ForegroundColor = (i % 2 == 0)
        ? System.Drawing.Color.LightYellow
        : System.Drawing.Color.LightCyan;

    // Use a solid fill pattern
    style.Pattern = BackgroundType.Solid;

    columnStyles[i] = style;
}
```

**Pourquoi nous utilisons une boucle :**  
La boucle garantit que **set cell background color c#** est appliquée de manière cohérente, même si le nombre de colonnes change à l’exécution. Cela rend la solution robuste pour les rapports dynamiques.

## Étape 4 : Importer le `DataTable` dans la feuille de calcul, en appliquant les styles de colonnes

Aspose.Cells peut importer directement un `DataTable`, et nous pouvons passer le tableau de styles pour colorer chaque colonne.

```csharp
// Import the DataTable starting at cell A1 (row 0, column 0)
// The second argument (true) tells the API to add column headers
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

**Ce qui se passe en coulisses :**  
`ImportDataTable` écrit la ligne d’en‑tête, puis chaque ligne de données. Comme nous avons fourni `columnStyles`, chaque cellule d’une colonne donnée reçoit le style correspondant, nous donnant les couleurs alternées souhaitées.

## Étape 5 : Enregistrer le classeur stylisé dans un fichier

```csharp
// Choose an output path – adjust as needed for your environment
string outputPath = @"C:\Temp\StyledTable.xlsx";
workbook.Save(outputPath);

Console.WriteLine($"Workbook saved to {outputPath}");
```

Lorsque vous ouvrez *StyledTable.xlsx* dans Excel, vous verrez chaque colonne ombrée alternativement, ce qui rend le tableau plus lisible.

## Exemple complet et exécutable

En assemblant toutes les pièces, voici un programme autonome que vous pouvez copier, coller et exécuter.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Get the source data
        DataTable dataTable = GetData();

        // Step 2: Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 3: Build alternating column styles
        int columnCount = dataTable.Columns.Count;
        Style[] columnStyles = new Style[columnCount];
        for (int i = 0; i < columnCount; i++)
        {
            Style style = workbook.CreateStyle();
            style.ForegroundColor = (i % 2 == 0)
                ? System.Drawing.Color.LightYellow
                : System.Drawing.Color.LightCyan;
            style.Pattern = BackgroundType.Solid;
            columnStyles[i] = style;
        }

        // Step 4: Import DataTable with styles
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // Step 5: Save the file
        string outputPath = @"C:\Temp\StyledTable.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }

    static DataTable GetData()
    {
        DataTable table = new DataTable("Students");
        table.Columns.Add("Id", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        for (int i = 1; i <= 5; i++)
        {
            table.Rows.Add(i, $"Student {i}", 60 + i * 5);
        }
        return table;
    }
}
```

### Résultat attendu

* Un fichier nommé **StyledTable.xlsx** situé à `C:\Temp\`.
* La feuille de calcul affiche trois colonnes (`Id`, `Name`, `Score`) avec des couleurs d’arrière‑plan alternées : les colonnes 1 et 3 en *LightYellow*, la colonne 2 en *LightCyan*.
* Toutes les lignes du `DataTable` apparaissent sous la ligne d’en‑tête.

## Questions fréquentes et cas particuliers

| Question | Réponse |
|----------|--------|
| *Puis-je utiliser d’autres couleurs ?* | Oui. Remplacez `System.Drawing.Color.LightYellow` et `LightCyan` par n’importe quelle valeur `System.Drawing.Color`. |
| *Et si le DataTable possède de nombreuses colonnes ?* | La boucle crée automatiquement un style pour chaque colonne, ainsi le motif s’adapte sans modification du code. |
| *Do I need to dispose of the workbook?* | Aspose.Cells implémente `IDisposable`. Si vous encapsulez le `Workbook` dans un bloc `using`, les ressources sont libérées rapidement. |
| *Comment appliquer les mêmes couleurs alternées aux lignes au lieu des colonnes ?* | Créez un `Style[]` pour les lignes et appelez `worksheet.Cells.ImportDataTable(..., rowStyles)` – les surcharges d’Aspose.Cells prennent en charge les deux. |
| *Puis-je écrire le fichier directement dans un flux (par ex., pour une API web) ?* | Oui. Utilisez `workbook.Save(stream, SaveFormat.Xlsx);` au lieu d’un chemin de fichier. |

## Astuces du terrain

* **Pro tip :** Mettez en cache les objets de style si vous générez de nombreuses feuilles de calcul en une seule exécution – créer un style est relativement peu coûteux, mais les réutiliser réduit la consommation de mémoire.  
* **Watch out for :** Lors de l’utilisation de `System.Drawing.Color` sur des plateformes non Windows, ajoutez le package NuGet `System.Drawing.Common` et assurez‑vous que le runtime prend en charge GDI+.

## Conclusion

Vous savez maintenant comment **alternating column colors excel** en créant un fichier Excel à partir d’un `DataTable` en C#, en définissant les couleurs d’arrière‑plan des cellules avec Aspose.Cells, et **import datatable to excel** avec un tableau de colonnes stylisé. Cette approche est rapide, maintenable et fonctionne avec tout jeu de données.

### Prochaines étapes

* Explorez **set cell background color c#** pour le formatage conditionnel (par ex., mettre en évidence les scores faibles).  
* Combinez cette technique avec **create excel file from datatable c#** pour générer des rapports multi‑feuilles.  
* Examinez l’API de création de graphiques d’Aspose.Cells pour ajouter des résumés visuels au même classeur.

N’hésitez pas à adapter les couleurs, le format de fichier ou la source de données pour répondre aux besoins de votre projet. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités d’API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Définir l’arrière‑plan des colonnes dans Excel avec C# – Guide complet](/cells/english/net/excel-colors-and-background-settings/set-column-background-in-excel-with-c-complete-guide/)
- [Ajouter une couleur d’arrière‑plan excel – Styles de lignes alternés en C#](/cells/english/net/excel-colors-and-background-settings/add-background-color-excel-alternating-row-styles-in-c/)
- [Créer un classeur C# – Importer DataTable vers Excel avec styles](/cells/english/net/excel-data-import-export/create-workbook-c-import-datatable-to-excel-with-styles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}