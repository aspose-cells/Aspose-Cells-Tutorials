---
category: general
date: 2026-05-30
description: Comment utiliser AutoFilter en automatisation Excel avec C#. Apprenez
  à créer un classeur Excel, filtrer les lignes par valeur et rationaliser vos tâches
  de feuille de calcul.
draft: false
keywords:
- how to use autofilter
- create excel workbook
- filter rows by value
- filter column b
- excel automation c#
language: fr
og_description: Comment utiliser AutoFilter dans l'automatisation Excel en C#. Maîtrisez
  la création de classeur Excel, le filtrage des lignes par valeur et l'automatisation
  des feuilles de calcul avec facilité.
og_title: Comment utiliser AutoFilter dans l'automatisation Excel en C# – Guide complet
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: How to use AutoFilter in C# Excel automation. Learn how to create Excel
    workbook, filter rows by value, and streamline your spreadsheet tasks.
  headline: How to Use AutoFilter in C# Excel Automation – Full Step‑by‑Step Guide
  type: TechArticle
- description: How to use AutoFilter in C# Excel automation. Learn how to create Excel
    workbook, filter rows by value, and streamline your spreadsheet tasks.
  name: How to Use AutoFilter in C# Excel Automation – Full Step‑by‑Step Guide
  steps:
  - name: '**Creating the workbook** – `new Workbook()` gives you a clean file; `Worksheets[0]`
      grabs the default sheet.'
    text: '**Creating the workbook** – `new Workbook()` gives you a clean file; `Worksheets[0]`
      grabs the default sheet.'
  - name: '**Filling sample data** – We write a tiny dataset so you can see the filter
      in action.'
    text: '**Filling sample data** – We write a tiny dataset so you can see the filter
      in action.'
  - name: '**Adding a table** – `ListObjects.Add` converts the range into an Excel
      table, which automatically supports filtering and styling.'
    text: '**Adding a table** – `ListObjects.Add` converts the range into an Excel
      table, which automatically supports filtering and styling.'
  - name: '**Applying AutoFilter** – `table.AutoFilter.Filter(1, "Apple")` tells the
      engine: “Show only rows where the second column (B) equals *Apple*.”'
    text: '**Applying AutoFilter** – `table.AutoFilter.Filter(1, "Apple")` tells the
      engine: “Show only rows where the second column (B) equals *Apple*.”'
  - name: '**Saving files** – Two files are written: one filtered, one with the filter
      removed, proving that `RemoveAutoFilter()` works as expected.'
    text: '**Saving files** – Two files are written: one filtered, one with the filter
      removed, proving that `RemoveAutoFilter()` works as expected.'
  type: HowTo
- questions:
  - answer: Yes. Aspose.Cells can save to both `.xlsx` and `.xls` by changing the
      file extension or using `SaveOptions`.
    question: Does this work with older .xls files?
  - answer: Load the file with `new Workbook("path.xlsx")`, apply the filter, then
      `Save` again.
    question: What if I need to filter *after* the workbook is already saved?
  - answer: 'Absolutely. Use `worksheet.AutoFilter.Range = "A1:C5";` and then `worksheet.AutoFilter.ApplyFilter();`.
      However, tables give you built‑in styling and easier column referencing. ---
      ## Image – Visual Confirmation ![Screenshot showing AutoFilter applied to column
      B in an Excel workbook created with C#'
    question: Can I apply a filter to a *range* that isn’t a table?
  type: FAQPage
tags:
- C#
- Excel
- Automation
title: Comment utiliser AutoFilter dans l’automatisation Excel en C# – Guide complet
  étape par étape
url: /fr/net/excel-autofilter-validation/how-to-use-autofilter-in-c-excel-automation-full-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment utiliser AutoFilter en automatisation Excel avec C# – Guide complet

Vous vous êtes déjà demandé **comment utiliser AutoFilter** lorsque vous générez des fichiers Excel à partir de code C# ? Vous n'êtes pas seul — de nombreux développeurs rencontrent ce problème lorsqu'ils doivent masquer les lignes qui ne correspondent pas à un certain critère.  

Dans ce tutoriel, nous parcourrons un exemple concret et exécutable qui **crée un classeur Excel**, ajoute un tableau, puis **filtre les lignes par valeur** dans la colonne B. À la fin, vous disposerez d’un extrait propre et réutilisable que vous pourrez intégrer à n’importe quel projet C# nécessitant une automatisation Excel.

## Ce que vous allez apprendre

- Configurer un projet C# avec la bibliothèque Aspose.Cells (ou Microsoft.Office.Interop).  
- **Créer un classeur Excel** par programme et ajouter un tableau stylisé.  
- Appliquer **AutoFilter** pour n’afficher que les lignes où **la colonne B** est égale à une chaîne spécifique.  
- Supprimer complètement le filtre, rétablissant l’ensemble complet des données.  
- Astuces pour gérer les cas limites comme les colonnes manquantes ou plusieurs critères de filtrage.

Aucune expérience préalable en Excel‑VBA n’est requise ; il suffit d’une compréhension de base du C# et des packages NuGet.

---

## Prérequis

| Prérequis | Pourquoi c’est important |
|-------------|----------------|
| .NET 6.0 ou ultérieur (ou .NET Framework 4.7+) | Les runtimes modernes offrent de meilleures performances et une gestion de paquets plus simple. |
| Aspose.Cells for .NET (ou Microsoft.Office.Interop.Excel) installé via NuGet | Cette bibliothèque nous fournit les objets `Workbook`, `Worksheet` et `Table` utilisés dans le code. |
| Un éditeur de code (Visual Studio, VS Code, Rider, etc.) | Vous aurez besoin de compiler et d’exécuter l’exemple. |
| Connaissances de base en C# | Le tutoriel explique *pourquoi* chaque ligne existe, pas seulement *ce que* elle fait. |

Vous pouvez installer Aspose.Cells avec :

```bash
dotnet add package Aspose.Cells
```

---

## Comment utiliser AutoFilter avec Aspose.Cells en C#

Voici le programme complet et autonome. Enregistrez‑le sous le nom `Program.cs` dans un projet console et exécutez‑le — vous obtiendrez `FilteredWorkbook.xlsx` dans le dossier de sortie.

```csharp
using System;
using Aspose.Cells;

namespace ExcelAutoFilterDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Create an Excel workbook and grab the first worksheet
            // -------------------------------------------------
            Workbook workbook = new Workbook();               // creates a new, empty workbook
            Worksheet sheet = workbook.Worksheets[0];         // the default sheet is named "Sheet1"

            // Populate the sheet with sample data (A‑C columns, 5 rows)
            sheet.Cells["A1"].PutValue("ID");
            sheet.Cells["B1"].PutValue("Fruit");
            sheet.Cells["C1"].PutValue("Quantity");

            sheet.Cells["A2"].PutValue(1);
            sheet.Cells["B2"].PutValue("Apple");
            sheet.Cells["C2"].PutValue(10);

            sheet.Cells["A3"].PutValue(2);
            sheet.Cells["B3"].PutValue("Banana");
            sheet.Cells["C3"].PutValue(15);

            sheet.Cells["A4"].PutValue(3);
            sheet.Cells["B4"].PutValue("Apple");
            sheet.Cells["C4"].PutValue(7);

            sheet.Cells["A5"].PutValue(4);
            sheet.Cells["B5"].PutValue("Cherry");
            sheet.Cells["C5"].PutValue(20);

            // -------------------------------------------------
            // Step 2: Convert the range into a ListObject (Excel table)
            // -------------------------------------------------
            // Parameters: firstRow, firstColumn, totalRows, totalColumns, hasHeaders
            int tableIdx = sheet.ListObjects.Add(0, 0, 5, 3, true);
            ListObject table = sheet.ListObjects[tableIdx];
            table.TableStyleType = TableStyleType.TableStyleMedium2; // nice built‑in styling

            // -------------------------------------------------
            // Step 3: Apply an AutoFilter to show only rows where column B = "Apple"
            // -------------------------------------------------
            // The AutoFilter is attached to the table’s range automatically.
            // We target column B (index 1) and set the criteria.
            table.AutoFilter.Filter(1, "Apple"); // 1 = zero‑based column index for B

            // -------------------------------------------------
            // Step 4: Save the filtered workbook to disk
            // -------------------------------------------------
            workbook.Save("FilteredWorkbook.xlsx");

            // -------------------------------------------------
            // Step 5: (Optional) Remove the AutoFilter completely
            // -------------------------------------------------
            // This demonstrates that you can revert to the full dataset without re‑loading.
            table.RemoveAutoFilter();   // clears the filter
            workbook.Save("UnfilteredWorkbook.xlsx");

            Console.WriteLine("Workbook created and filtered successfully.");
        }
    }
}
```

### Comment le code fonctionne

1. **Création du classeur** – `new Workbook()` vous fournit un fichier vierge ; `Worksheets[0]` récupère la feuille par défaut.  
2. **Remplissage de données d’exemple** – Nous écrivons un petit jeu de données afin que vous puissiez voir le filtre en action.  
3. **Ajout d’un tableau** – `ListObjects.Add` convertit la plage en un tableau Excel, qui prend automatiquement en charge le filtrage et le style.  
4. **Application d’AutoFilter** – `table.AutoFilter.Filter(1, "Apple")` indique au moteur : « Afficher uniquement les lignes où la deuxième colonne (B) est égale à *Apple* ».  
5. **Enregistrement des fichiers** – Deux fichiers sont écrits : un filtré, un autre avec le filtre supprimé, prouvant que `RemoveAutoFilter()` fonctionne comme prévu.

> **Astuce :** Si vous devez filtrer selon plusieurs critères (par ex., « Apple » *ou* « Banana »), utilisez la surcharge `Filter(int columnIndex, string criteria1, string criteria2)` ou passez un tableau de chaînes.

---

## Filtrer les lignes par valeur – Variations courantes

Bien que l’exemple ci‑dessus se concentre sur **le filtrage de la colonne B**, vous pourriez vouloir filtrer d’autres colonnes ou utiliser des critères numériques. Voici une petite feuille de triche :

| Filtre souhaité | Extrait de code |
|----------------|-----------------|
| Correspondance de texte dans la colonne C | `table.AutoFilter.Filter(2, "Cherry");` |
| Nombres supérieurs à 10 dans la colonne C | `table.AutoFilter.CustomFilter(2, "10", OperatorType.GreaterThan);` |
| Valeurs multiples dans la colonne B | `table.AutoFilter.Filter(1, new[] { "Apple", "Banana" });` |

**Cas limite :** Si l’en‑tête de colonne est mal orthographié ou que l’indice de colonne est hors limites, Aspose.Cells lève une `ArgumentException`. Protégez‑vous en vérifiant `table.ListColumns.Count` avant d’appliquer le filtre.

---

## Suppression d’AutoFilter – Quand réinitialiser

Parfois, vous devez à nouveau présenter l’ensemble complet des données (par ex., après qu’un utilisateur ait vidé une zone de recherche). Appeler `table.RemoveAutoFilter()` résout le problème en une seule ligne. Si vous utilisez Microsoft.Office.Interop à la place, vous appelleriez `worksheet.AutoFilterMode = false;`.

---

## Récapitulatif de l’exemple complet fonctionnel

Voici le programme *entier* à nouveau, dépouillé des commentaires pour ceux qui préfèrent une vue concise :

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        ws.Cells["A1"].PutValue("ID");
        ws.Cells["B1"].PutValue("Fruit");
        ws.Cells["C1"].PutValue("Quantity");

        ws.Cells["A2"].PutValue(1); ws.Cells["B2"].PutValue("Apple");  ws.Cells["C2"].PutValue(10);
        ws.Cells["A3"].PutValue(2); ws.Cells["B3"].PutValue("Banana"); ws.Cells["C3"].PutValue(15);
        ws.Cells["A4"].PutValue(3); ws.Cells["B4"].PutValue("Apple");  ws.Cells["C4"].PutValue(7);
        ws.Cells["A5"].PutValue(4); ws.Cells["B5"].PutValue("Cherry"); ws.Cells["C5"].PutValue(20);

        int idx = ws.ListObjects.Add(0, 0, 5, 3, true);
        ListObject tbl = ws.ListObjects[idx];
        tbl.TableStyleType = TableStyleType.TableStyleMedium2;

        tbl.AutoFilter.Filter(1, "Apple");
        wb.Save("FilteredWorkbook.xlsx");

        tbl.RemoveAutoFilter();
        wb.Save("UnfilteredWorkbook.xlsx");
    }
}
```

L’exécution de ce programme génère deux fichiers :

- **FilteredWorkbook.xlsx** – seules les lignes contenant *Apple* sont visibles.  
- **UnfilteredWorkbook.xlsx** – les données originales restaurées.

---

## Questions fréquentes

**Q : Cela fonctionne-t-il avec les anciens fichiers .xls ?**  
R : Oui. Aspose.Cells peut enregistrer à la fois en `.xlsx` et en `.xls` en modifiant l’extension du fichier ou en utilisant `SaveOptions`.

**Q : Et si je dois filtrer *après* que le classeur ait déjà été enregistré ?**  
R : Chargez le fichier avec `new Workbook("path.xlsx")`, appliquez le filtre, puis `Save` à nouveau.

**Q : Puis‑je appliquer un filtre à une *plage* qui n’est pas un tableau ?**  
R : Absolument. Utilisez `worksheet.AutoFilter.Range = "A1:C5";` puis `worksheet.AutoFilter.ApplyFilter();`. Cependant, les tableaux offrent un style intégré et une référence de colonne plus simple.

---

## Image – Confirmation visuelle

![Capture d’écran montrant AutoFilter appliqué à la colonne B dans un classeur Excel créé avec C#](/images/autofilter-column-b.png "AutoFilter sur la colonne B")

*(L’image illustre la vue filtrée où seules les lignes contenant « Apple » restent.)*

---

## Conclusion

Nous venons de couvrir **comment utiliser AutoFilter** dans un scénario d’automatisation Excel piloté par C#, depuis **la création d’un classeur Excel** jusqu’à **le filtrage des lignes par valeur** dans **la colonne B**, et enfin **la suppression du filtre** lorsqu’il n’est plus nécessaire. Les étapes essentielles—initialiser, ajouter un tableau, appliquer le filtre et nettoyer—sont réutilisables dans tout projet nécessitant **excel automation c#**.

Prêt pour le prochain défi ? Essayez :

- Ajouter une mise en forme conditionnelle pour mettre en évidence les lignes filtrées.  
- Exporter les données filtrées vers un CSV pour le traitement en aval.  
- Combiner plusieurs filtres (par ex., « Apple » *et* quantité > 8).

Expérimentez, cassez des choses, puis réparez‑les—

## Que devriez‑vous apprendre ensuite ?

- [Comment implémenter AutoFilter dans Excel avec Aspose.Cells pour .NET (Guide d’analyse de données)](/cells/english/net/data-analysis/implement-autofilter-excel-aspose-cells-dotnet/)
- [Comment utiliser Autofilter Not Contains dans Aspose.Cells .NET pour l’analyse de données Excel](/cells/english/net/data-analysis/master-autofilter-not-contains-aspose-cells-net/)
- [Comment implémenter Excel Autofilter 'EndsWith' en utilisant Aspose.Cells pour .NET](/cells/english/net/data-analysis/implement-autofilter-endswith-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}