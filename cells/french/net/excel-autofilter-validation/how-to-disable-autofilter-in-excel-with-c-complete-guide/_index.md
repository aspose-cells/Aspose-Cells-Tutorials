---
category: general
date: 2026-10-26
description: Désactiver le filtre automatique dans Excel avec C#. Ce tutoriel montre
  comment supprimer le filtre automatique d’un tableau Excel de manière programmatique
  et inclut un exemple complet fonctionnel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- disable autofilter in excel
- remove autofilter from excel table
- Excel automation C#
- Aspose.Cells filter handling
- programmatic Excel editing
language: fr
lastmod: 2026-10-26
og_description: Désactivez rapidement le filtre automatique dans Excel. Suivez ce
  guide pour supprimer le filtre automatique d’un tableau Excel en utilisant C# et
  Aspose.Cells.
og_image_alt: Screenshot of an Excel worksheet where the autofilter has been disabled
og_title: Désactiver le filtre automatique dans Excel avec C# – guide étape par étape
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: disable autofilter in Excel using C#. This tutorial shows how to remove
    autofilter from Excel table programmatically and includes a full working example.
  headline: How to disable autofilter in Excel with C# – complete guide
  type: TechArticle
- description: disable autofilter in Excel using C#. This tutorial shows how to remove
    autofilter from Excel table programmatically and includes a full working example.
  name: How to disable autofilter in Excel with C# – complete guide
  steps:
  - name: Open the saved file (`Sample_NoFilter.xlsx`) in Microsoft Excel.
    text: Open the saved file (`Sample_NoFilter.xlsx`) in Microsoft Excel.
  - name: Click any column header – you should **not** see the drop‑down filter arrow.
    text: Click any column header – you should **not** see the drop‑down filter arrow.
  - name: 'If you still see arrows, double‑check that the table you targeted is indeed
      the one with the filter. You can list all tables with:'
    text: 'If you still see arrows, double‑check that the table you targeted is indeed
      the one with the filter. You can list all tables with:'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Comment désactiver le filtre automatique dans Excel avec C# – guide complet
url: /fr/net/excel-autofilter-validation/how-to-disable-autofilter-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment désactiver l'autofilter dans Excel avec C# – guide complet

Si vous devez **désactiver l'autofilter dans Excel**, ce guide vous montre exactement comment le faire depuis C#. Que vous nettoyiez un rapport avant publication ou que vous automatisiez un pipeline d'exportation de données, supprimer le filtre garantit que la feuille de calcul affiche chaque ligne. Vous apprendrez également comment **supprimer l'autofilter d'un tableau Excel** en un seul appel fiable.

Nous utiliserons la populaire bibliothèque **Aspose.Cells for .NET** car elle fonctionne sans nécessiter l'installation d'Excel sur le serveur. À la fin de ce tutoriel, vous disposerez d'une application console autonome qui charge un classeur, trouve le premier tableau et désactive son autofilter. La solution fonctionne avec les fichiers .xlsx créés par Excel 2007 ou une version plus récente.

## Ce dont vous avez besoin

| Prérequis | Pourquoi c'est important |
|--------------|--------------------------|
| .NET 6.0 or later | Fournit le runtime pour le code C#. |
| Aspose.Cells for .NET (NuGet package `Aspose.Cells`) | Permet l'accès programmatique aux feuilles de calcul, aux tableaux et aux autofilters. |
| A sample Excel file (`Sample.xlsx`) that contains at least one table with an autofilter applied | Un fichier Excel d'exemple (`Sample.xlsx`) contenant au moins un tableau avec un autofilter appliqué. Le code agit sur le premier tableau ; disposer d'un tableau nous permet de démontrer la désactivation du filtre. |
| Visual Studio 2022 (or any C# IDE) | Facilite la création et le débogage de l'application console. |

> **Astuce :** Si vous préférez une alternative gratuite, vous pouvez adapter le code pour utiliser **ClosedXML** ou **EPPlus** ; l'idée principale—définir la propriété `AutoFilter` du tableau à `null`—reste la même.

## Étape 1 : Créer un nouveau projet console

Ouvrez un terminal ou l'invite de commandes Visual Studio et exécutez :

```bash
dotnet new console -n ExcelFilterDemo
cd ExcelFilterDemo
dotnet add package Aspose.Cells
```

Cela crée un nouveau projet nommé `ExcelFilterDemo` et ajoute la bibliothèque Aspose.Cells.

## Étape 2 : Charger le classeur et localiser la première feuille de calcul

La première opération logique consiste à ouvrir le fichier du classeur. Aspose.Cells lit le fichier dans un objet `Workbook` qui vous donne un accès direct aux feuilles de calcul et aux tableaux.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Path to the Excel file you want to modify
        const string inputPath = "Sample.xlsx";

        // Load the workbook into memory
        Workbook wb = new Workbook(inputPath);

        // Access the first worksheet (index 0)
        Worksheet worksheet = wb.Worksheets[0];
```

> **Pourquoi cette étape ?** Charger le classeur est nécessaire avant de pouvoir manipuler des objets Excel. Utiliser la première feuille (`Worksheets[0]`) reflète le scénario typique où les données principales se trouvent sur la première feuille.

## Étape 3 : Récupérer le premier tableau défini sur la feuille de calcul

Les tableaux Excel (également appelés ListObjects) sont les conteneurs qui contiennent des données structurées. Chaque tableau peut avoir son propre autofilter. Pour supprimer le filtre, nous avons d'abord besoin d'une référence à l'objet tableau.

```csharp
        // Get the first table on the worksheet.
        // If the worksheet has no tables, this will throw an IndexOutOfRangeException.
        Table table = worksheet.Tables[0];
```

> **Cas limite :** Si le classeur peut contenir des feuilles sans tableaux, encapsulez l'accès dans une vérification `if (worksheet.Tables.Count > 0)`. Cela évite les erreurs d'exécution et rend la solution robuste.

## Étape 4 : Désactiver l'autofilter pour le tableau

La désactivation réelle se fait en une seule ligne : affectez `null` à la propriété `AutoFilter` de l'objet `Table`. Cela supprime tout critère de filtre et enlève les flèches déroulantes de la ligne d'en-tête.

```csharp
        // Disable the autofilter – this clears any applied filter.
        table.AutoFilter = null;
```

Après l'exécution de cette ligne, le tableau se comporte comme une plage ordinaire sans interface de filtre.

## Étape 5 : Enregistrer le classeur modifié

Enfin, écrivez les modifications sur le disque. Vous pouvez écraser le fichier original ou en créer un nouveau pour conserver la source intacte.

```csharp
        // Save the workbook. Use a new file name to avoid overwriting the original.
        const string outputPath = "Sample_NoFilter.xlsx";
        wb.Save(outputPath);

        System.Console.WriteLine($"Autofilter disabled. Saved to {outputPath}");
    }
}
```

### Code source complet

En assemblant tous les éléments, le programme complet ressemble à ceci :

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Path to the original Excel file
        const string inputPath = "Sample.xlsx";

        // Load the workbook
        Workbook wb = new Workbook(inputPath);

        // Access the first worksheet
        Worksheet worksheet = wb.Worksheets[0];

        // Ensure the worksheet contains at least one table
        if (worksheet.Tables.Count == 0)
        {
            System.Console.WriteLine("No tables found on the first worksheet.");
            return;
        }

        // Get the first table
        Table table = worksheet.Tables[0];

        // Disable the autofilter – clears any applied filter
        table.AutoFilter = null;

        // Save the modified workbook
        const string outputPath = "Sample_NoFilter.xlsx";
        wb.Save(outputPath);

        System.Console.WriteLine($"Autofilter disabled. Saved to {outputPath}");
    }
}
```

Exécutez le programme avec `dotnet run`. Après l'exécution, ouvrez `Sample_NoFilter.xlsx` dans Excel ; vous verrez que les flèches de filtre ont disparu et que toutes les lignes sont visibles.

## Vérifier que l'autofilter a réellement disparu

1. Ouvrez le fichier enregistré (`Sample_NoFilter.xlsx`) dans Microsoft Excel.  
2. Cliquez sur n'importe quel en-tête de colonne – vous ne devriez **pas** voir la flèche de filtre déroulante.  
3. Si vous voyez toujours des flèches, revérifiez que le tableau ciblé est bien celui avec le filtre. Vous pouvez lister tous les tableaux avec :

```csharp
foreach (var tbl in worksheet.Tables)
{
    System.Console.WriteLine($"Table name: {tbl.Name}, Has AutoFilter: {tbl.AutoFilter != null}");
}
```

La sortie de la console devrait indiquer `Has AutoFilter: False` pour le tableau que vous avez modifié.

## Pièges courants et comment les éviter

| Symptôme | Cause probable | Solution |
|----------|----------------|----------|
| `IndexOutOfRangeException` at `worksheet.Tables[0]` | La feuille de calcul ne contient aucun tableau. | Ajoutez une vérification `if (worksheet.Tables.Count == 0)` avant d'accéder. |
| Le fichier enregistré affiche toujours les filtres | Vous avez modifié la mauvaise feuille ou le mauvais tableau. | Utilisez `wb.Worksheets["SheetName"]` ou parcourez `wb.Worksheets` pour localiser le tableau correct. |
| Le programme plante sur d'anciennes versions de .NET | Aspose.Cells nécessite .NET 6.0+ pour le dernier package. | Mettez à jour le framework cible dans le fichier `.csproj`. |
| NullReferenceException lorsque `table.AutoFilter` est déjà null | Vous avez appelé le code deux fois sur le même fichier sans le recharger. | Rechargez le classeur ou vérifiez `if (table.AutoFilter != null)` avant d'affecter. |

## Étendre la solution

Maintenant que vous savez comment **désactiver l'autofilter dans Excel**, vous pourriez vouloir :

* **Supprimer l'autofilter d'un tableau Excel** uniquement lorsqu'une condition spécifique est remplie (par ex., lorsqu'un indicateur utilisateur est activé). Ajoutez une instruction `if` autour de `table.AutoFilter = null;`.
* **Appliquer un nouveau filtre** programmatique après avoir effacé l'ancien, en utilisant `table.AutoFilter.Range` et `table.AutoFilter.AddFilterColumn(...)`.
* **Traiter plusieurs tableaux** dans le même classeur en parcourant `worksheet.Tables` et en désactivant chaque filtre.

Ces extensions suivent le même modèle démontré ci‑dessus et maintiennent le code propre.

## Conclusion

Vous disposez maintenant d'une méthode concise et prête pour la production afin de **désactiver l'autofilter dans Excel** avec C#. En chargeant le classeur, en accédant au premier tableau et en définissant `table.AutoFilter = null`, vous **supprimez l'autofilter du tableau Excel** sans intervention manuelle. L'exemple complet se compile, s'exécute et produit un fichier propre prêt pour une automatisation ou une distribution supplémentaire.

N'hésitez pas à expérimenter avec d'autres tableaux, une logique conditionnelle ou des bibliothèques alternatives. Si vous rencontrez des cas particuliers, revenez à la section de dépannage ou explorez la documentation exhaustive d'Aspose.Cells pour la gestion avancée des filtres. Bon codage !

## Que devez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Comment supprimer l'autofilter des tableaux Excel avec C#](/cells/english/net/excel-autofilter-validation/how-to-remove-autofilter-from-excel-tables-using-c/)
- [Effacer l'interface du filtre dans Excel avec C# – Supprimer le bouton AutoFilter](/cells/english/net/excel-autofilter-validation/clear-filter-ui-in-excel-with-c-remove-autofilter-button/)
- [Comment utiliser AutoFilter dans l'automatisation Excel avec C# – Guide complet étape par étape](/cells/english/net/excel-autofilter-validation/how-to-use-autofilter-in-c-excel-automation-full-step-by-ste/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}