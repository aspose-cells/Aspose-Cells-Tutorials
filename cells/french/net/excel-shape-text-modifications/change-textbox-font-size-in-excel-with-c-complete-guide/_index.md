---
category: general
date: 2026-05-30
description: Modifiez la taille de police d’une zone de texte dans Excel avec C#.
  Apprenez à modifier rapidement la police d’une zone de texte Excel grâce à un code
  étape par étape.
draft: false
keywords:
- change textbox font size
- modify excel textbox font
language: fr
og_description: Modifier la taille de police d’une zone de texte dans Excel avec C#.
  Ce guide montre comment modifier la police d’une zone de texte Excel de manière
  sûre et efficace.
og_title: Modifier la taille de police d’une zone de texte dans Excel avec C# – Tutoriel
  complet
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Change textbox font size in Excel using C#. Learn how to modify excel
    textbox font quickly with step‑by‑step code.
  headline: Change Textbox Font Size in Excel with C# – Complete Guide
  type: TechArticle
- description: Change textbox font size in Excel using C#. Learn how to modify excel
    textbox font quickly with step‑by‑step code.
  name: Change Textbox Font Size in Excel with C# – Complete Guide
  steps:
  - name: Why this matters
    text: Opening the workbook via COM gives us a live object model—meaning any change
      we make reflects instantly in the file. Setting `Visible = false` speeds things
      up and avoids popping windows during automation.
  - name: Why we use `TextFrame2`
    text: '`TextFrame2` is the newer object model introduced with Office 2007. It
      supports advanced typographic features and is generally more reliable than the
      older `TextFrame`. Using it ensures our **change textbox font size** operation
      works across modern Excel versions.'
  - name: 1. Change *all* textboxes on a sheet
    text: '```csharp foreach (Excel.Shape s in xlWorksheet.Shapes) { if (s.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
      { var tr = s.TextFrame2.TextRange; tr.Font.Name = fontName; tr.Font.Size = newSize;
      } } ```'
  - name: 2. Identify a textbox by its **Name** instead of index
    text: 'If you gave your textbox a meaningful name (e.g., “TitleBox”), you can
      fetch it directly:'
  type: HowTo
tags:
- Excel Interop
- C#
- Office Automation
title: Modifier la taille de police d’une zone de texte dans Excel avec C# – Guide
  complet
url: /fr/net/excel-shape-text-modifications/change-textbox-font-size-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Modifier la taille de police d’une zone de texte dans Excel avec C# – Guide complet

Vous devez **modifier la taille de police d’une zone de texte** dans une feuille Excel depuis C# ? Vous êtes au bon endroit. Que vous génériez des rapports, construisiez un tableau de bord ou simplement ajustiez un modèle, modifier l’apparence d’une zone de texte peut rendre votre classeur beaucoup plus professionnel.

Dans ce tutoriel, nous allons également **modifier la police d’une zone de texte Excel** au‑delà de la taille — famille de police, gras, et même la gestion de plusieurs formes. À la fin, vous disposerez d’un extrait prêt à l’emploi qui couvre chaque étape du processus, de l’ouverture du classeur au nettoyage des objets COM. Pas de blabla, juste du code pratique que vous pouvez intégrer dès aujourd’hui.

## Prérequis — Ce dont vous avez besoin

Avant de commencer, assurez‑vous que les éléments suivants sont installés sur votre machine :

| Exigence | Pourquoi c’est important |
|----------|---------------------------|
| **.NET 6+** (ou .NET Framework 4.7.2+) | Fournit le compilateur et le runtime C#. |
| **Microsoft.Office.Interop.Excel** package NuGet | Nous donne les types d’interop COM nécessaires pour communiquer avec Excel. |
| **Excel installé** (toute version récente) | La couche Interop ne fonctionne que si l’application Office est présente. |
| **Connaissances de base en C#** | Vous suivrez facilement, mais nous expliquerons chaque ligne. |

Si l’un de ces éléments manque, faites une pause et installez‑le ; le reste du guide part du principe qu’ils sont présents.

## Étape 1 : Configurer le projet et importer les espaces de noms

Première chose à faire — créez une nouvelle application console (ou intégrez‑la à un projet existant) et importez l’espace de noms d’interop.

```csharp
using System;
using Excel = Microsoft.Office.Interop.Excel;

namespace ExcelTextboxDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll call the helper method that does the heavy lifting.
            ChangeTextboxFontSize(@"C:\Temp\Sample.xlsx", "Sheet1", 0, 14, "Calibri");
        }
    }
}
```

> **Astuce :** Si vous ciblez .NET 6+, ajoutez le package `Microsoft.Office.Interop.Excel` via `dotnet add package Microsoft.Office.Interop.Excel`. Cela garantit que l’alias `Excel` se résout correctement.

## Étape 2 : Ouvrir le classeur et récupérer la feuille cible

Nous devons maintenant lancer Excel, ouvrir le fichier et pointer vers la feuille qui contient la zone de texte. Envelopper cela dans un bloc `try/finally` assure que les objets COM sont libérés même en cas d’erreur.

```csharp
static void ChangeTextboxFontSize(string workbookPath,
                                  string sheetName,
                                  int textboxIndex,
                                  double newSize,
                                  string fontName)
{
    Excel.Application xlApp = null;
    Excel.Workbook xlWorkbook = null;
    Excel.Worksheet xlWorksheet = null;

    try
    {
        xlApp = new Excel.Application
        {
            // Keep Excel hidden; set to true if you want to watch the changes.
            Visible = false,
            DisplayAlerts = false
        };

        xlWorkbook = xlApp.Workbooks.Open(workbookPath);
        xlWorksheet = xlWorkbook.Worksheets[sheetName] as Excel.Worksheet;
        if (xlWorksheet == null)
            throw new ArgumentException($"Worksheet '{sheetName}' not found.");
```

### Pourquoi c’est important

Ouvrir le classeur via COM nous donne un modèle d’objet vivant — tout changement se reflète immédiatement dans le fichier. Définir `Visible = false` accélère le processus et évite l’apparition de fenêtres pendant l’automatisation.

## Étape 3 : Récupérer la forme de la zone de texte

Excel traite les zones de texte comme des objets `Shape` dans la collection `Shapes`, pas comme une collection dédiée `TextBox`. C’est pourquoi le code ci‑dessous diffère légèrement de l’exemple que vous avez pu voir en ligne.

```csharp
        // Excel stores all drawing objects (including textboxes) in the Shapes collection.
        Excel.Shapes shapes = xlWorksheet.Shapes;

        // Guard against an out‑of‑range index.
        if (textboxIndex < 0 || textboxIndex >= shapes.Count)
            throw new IndexOutOfRangeException("Textbox index is out of range.");

        // Grab the specific shape; we assume it’s a textbox.
        Excel.Shape textboxShape = shapes.Item(textboxIndex + 1); // COM collections are 1‑based.
        if (!textboxShape.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
            throw new InvalidOperationException("Selected shape is not a textbox.");
```

> **Attention :** La collection `Shapes` est indexée à partir de 1, donc nous ajoutons `+1` à l’index zéro‑based `textboxIndex` que vous transmettez. Oublier cela entraîne des erreurs « index out of range » frustrantes à déboguer.

## Étape 4 : Modifier la taille de police de la zone de texte (et le nom)

C’est ici que nous **modifions la taille de police de la zone de texte**. La propriété `TextFrame2` nous donne accès aux options de mise en forme riche, dont `Font.Name` et `Font.Size`.

```csharp
        // Access the text range inside the textbox.
        Excel.TextRange2 textRange = textboxShape.TextFrame2.TextRange;

        // Change the font name – this also “modifies excel textbox font”.
        textRange.Font.Name = fontName;

        // Change the font size – the core of our tutorial.
        textRange.Font.Size = newSize;

        // Optional: make the text bold for extra emphasis.
        // textRange.Font.Bold = Microsoft.Office.Core.MsoTriState.msoTrue;
```

### Pourquoi nous utilisons `TextFrame2`

`TextFrame2` est le modèle d’objet plus récent introduit avec Office 2007. Il prend en charge des fonctionnalités typographiques avancées et est généralement plus fiable que l’ancien `TextFrame`. L’utiliser garantit que notre **modification de la taille de police de la zone de texte** fonctionne sur les versions modernes d’Excel.

## Étape 5 : Enregistrer, nettoyer et vérifier

Après avoir ajusté la police, nous devons persister les modifications et libérer chaque référence COM. Négliger le nettoyage peut laisser des processus Excel orphelins en arrière‑plan.

```csharp
        // Save the workbook – you can also use SaveAs to create a copy.
        xlWorkbook.Save();

        Console.WriteLine($"Successfully changed textbox font size to {newSize} pt and font to '{fontName}'.");
    }
    catch (Exception ex)
    {
        Console.Error.WriteLine($"Error: {ex.Message}");
    }
    finally
    {
        // Release COM objects in reverse order of creation.
        if (xlWorksheet != null) System.Runtime.InteropServices.Marshal.ReleaseComObject(xlWorksheet);
        if (xlWorkbook != null)
        {
            xlWorkbook.Close(false);
            System.Runtime.InteropServices.Marshal.ReleaseComObject(xlWorkbook);
        }
        if (xlApp != null)
        {
            xlApp.Quit();
            System.Runtime.InteropServices.Marshal.ReleaseComObject(xlApp);
        }

        // Force garbage collection to clean up any remaining RCWs.
        GC.Collect();
        GC.WaitForPendingFinalizers();
    }
}
```

> **Astuce :** Si vous devez **modifier la police d’une zone de texte Excel** sur de nombreuses feuilles, encapsulez la logique interne dans une boucle qui itère sur `Workbook.Worksheets`. N’oubliez pas de réinitialiser `textboxIndex` pour chaque feuille.

## Gestion des cas particuliers — Plusieurs zones de texte et formes manquantes

Les classeurs réels contiennent rarement une seule zone de texte. Voici deux stratégies rapides que vous pouvez adopter sans réécrire toute la méthode.

### 1. Modifier *toutes* les zones de texte d’une feuille

```csharp
foreach (Excel.Shape s in xlWorksheet.Shapes)
{
    if (s.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
    {
        var tr = s.TextFrame2.TextRange;
        tr.Font.Name = fontName;
        tr.Font.Size = newSize;
    }
}
```

### 2. Identifier une zone de texte par son **Nom** plutôt que par son index

Si vous avez donné à votre zone de texte un nom significatif (par ex. : “TitleBox”), vous pouvez la récupérer directement :

```csharp
Excel.Shape namedBox = xlWorksheet.Shapes.Item("TitleBox");
namedBox.TextFrame2.TextRange.Font.Size = newSize;
```

Les deux approches vous permettent de **modifier la police d’une zone de texte Excel** avec précision, quel que soit le découpage du classeur.

## Aperçu visuel (Optionnel)

Si vous préférez un indice visuel rapide, imaginez le diagramme suivant :

![Screenshot showing Excel worksheet with a highlighted textbox – demonstrates how to change textbox font size](change-textbox-font-size.png)

*Texte alternatif :* *modifier la taille de police d’une zone de texte dans Excel – zone de texte mise en évidence prête pour la modification de la police.*

## Exemple complet fonctionnel

En rassemblant tous les morceaux, voici un fichier unique que vous pouvez copier‑coller dans un projet console et exécuter immédiatement (n’oubliez pas de mettre à jour le chemin du fichier et le nom de la feuille).

```csharp
using System;
using Excel = Microsoft.Office.Interop.Excel;

namespace ExcelTextboxDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Ajustez ces paramètres pour votre environnement.
            string workbookPath = @"C:\Temp\Sample.xlsx";
            string sheetName = "Sheet1";
            int textboxIndex = 0;          // Première zone de texte sur la feuille.
            double newFontSize = 14;       // Taille de police souhaitée.
            string newFontName = "Calibri";

            ChangeTextboxFontSize(workbookPath, sheetName, textboxIndex, newFontSize, newFontName);
        }

        static void ChangeTextboxFontSize(string workbookPath,
                                          string sheetName,
                                          int textboxIndex,
                                          double newSize,
                                          string fontName)
        {
            Excel.Application xlApp = null;
            Excel.Workbook xlWorkbook = null;
            Excel.Worksheet xlWorksheet = null;

            try
            {
                xlApp = new Excel.Application { Visible = false, DisplayAlerts = false };
                xlWorkbook = xlApp.Workbooks.Open(workbookPath);
                xlWorksheet = xlWorkbook.Worksheets[sheetName] as Excel.Worksheet;

                if (xlWorksheet == null)


## Que devez‑vous apprendre ensuite ?

- [Changing Font Size in Excel](/cells/english/net/working-with-fonts-in-excel/changing-font-size/)
- [How to Customize Font Size in Excel Cells Using Aspose.Cells .NET | Complete Guide](/cells/english/net/formatting/customize-font-size-excel-aspose-cells-dotnet/)
- [How to Set Font Styles in Excel Using Aspose.Cells for .NET (Step‑by‑Step Guide)](/cells/english/net/formatting/aspose-cells-dotnet-set-font-styles-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}