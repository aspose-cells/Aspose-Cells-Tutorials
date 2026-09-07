---
category: general
date: 2026-02-21
description: Créez rapidement un style de cellule en C#. Apprenez comment appliquer
  un style à une cellule, centrer le texte dans la cellule, définir l'alignement de
  la cellule et maîtriser le formatage des cellules.
draft: false
keywords:
- create cell style
- apply style to cell
- center text in cell
- set cell alignment
- how to center text
language: fr
og_description: Créez un style de cellule en C# et apprenez comment appliquer le style
  à une cellule, centrer le texte dans la cellule et définir l'alignement de la cellule
  grâce à un guide clair, étape par étape.
og_title: Créer un style de cellule en C# – Appliquer le style à une cellule et centrer
  le texte
tags:
- C#
- Aspose.Cells
- Excel automation
title: Créer un style de cellule en C# – Comment appliquer un style à une cellule
  et centrer le texte
url: /fr/net/excel-formatting-and-styling/create-cell-style-in-c-how-to-apply-style-to-a-cell-and-cent/
---

with shortcodes unchanged.

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un style de cellule en C# – Guide complet pour appliquer des styles et centrer le texte

Vous avez déjà eu besoin de **créer un style de cellule** dans une feuille Excel sans savoir par où commencer ? Vous n'êtes pas seul. Dans de nombreux projets d’automatisation, la capacité à **appliquer un style à une cellule** fait la différence entre une feuille banale et un rapport soigné.  

Dans ce tutoriel, nous parcourrons un exemple complet et exécutable qui vous montre **comment centrer le texte** à l’intérieur d’une cellule, définir l’alignement et ajouter une bordure fine — le tout en quelques lignes de C#. À la fin, vous saurez exactement pourquoi chaque élément est important et comment l’ajuster à vos propres scénarios.

## Ce que vous allez retenir

- Une compréhension claire du flux **create cell style** avec Aspose.Cells (ou toute bibliothèque similaire).
- Le code exact que vous pouvez copier‑coller dans une application console pour **apply style to cell**.
- Des informations sur **center text in cell**, **set cell alignment**, et la gestion des cas particuliers comme les cellules fusionnées ou les formats numériques personnalisés.
- Des astuces pour étendre le style : polices différentes, couleurs d’arrière‑plan ou mise en forme conditionnelle.

> **Prérequis :** Visual Studio 2022 (ou tout IDE C#) et le package NuGet Aspose.Cells for .NET. Aucune autre dépendance n’est requise.

---

## Étape 1 : Configurez votre projet et importez les espaces de noms

Avant de pouvoir **create cell style**, il nous faut un projet qui référence la bibliothèque Excel.

```csharp
// Program.cs – entry point
using System;
using Aspose.Cells;   // Make sure the Aspose.Cells NuGet package is installed

class Program
{
    static void Main()
    {
        // We'll fill in the rest of the steps here.
    }
}
```

*Pourquoi c’est important :* L’import de `Aspose.Cells` nous donne accès aux classes `Workbook`, `Worksheet`, `Style` et `Border`. Si vous utilisez une autre bibliothèque (par ex., EPPlus), les noms de classe changent mais le concept reste le même.

---

## Étape 2 : Créez un classeur et récupérez la première cellule

Nous **create cell style** en obtenant d’abord une référence à la cellule que nous voulons formater.

```csharp
// Inside Main()
Workbook workbook = new Workbook();           // New, empty workbook
Worksheet ws = workbook.Worksheets[0];        // First worksheet (index 0)

// Step 1: Get a reference to the first cell (row 0, column 0) in the worksheet
Cell firstCell = ws.Cells[0, 0];               // A1 in Excel terms
firstCell.PutValue("Hello, styled world!");
```

Remarquez que nous utilisons `Cell` au lieu du générique `var` — la typisation explicite rend le code plus clair pour les débutants. L’appel à `PutValue` écrit une chaîne afin que nous puissions voir l’effet du style plus tard.

---

## Étape 3 : Définissez le style – centrer le texte, ajouter une bordure fine

Voici le cœur de l’opération **create cell style**. Nous allons définir l’alignement horizontal, une bordure fine, et quelques options supplémentaires.

```csharp
// Step 2: Define a style that centers the text and adds a thin border
Style cellStyle = workbook.CreateStyle();          // Create a fresh Style object
cellStyle.HorizontalAlignment = TextAlignmentType.Center; // Center text horizontally
cellStyle.VerticalAlignment = TextAlignmentType.Center;   // Center vertically – often forgotten
cellStyle.Borders[BorderType.TopBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.BottomBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.LeftBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.RightBorder].LineStyle = CellBorderType.Thin;

// Optional: set a light gray background to make the border pop
cellStyle.ForegroundColor = System.Drawing.Color.LightGray;
cellStyle.Pattern = BackgroundType.Solid;
```

*Pourquoi faisons‑nous cela :*  
- **HorizontalAlignment** et **VerticalAlignment** répondent ensemble à la question « **how to center text** in a cell ? ».  
- Ajouter les quatre bordures assure que la cellule ressemble à une étiquette encadrée, utile pour les en‑têtes.  
- La couleur d’arrière‑plan n’est pas obligatoire, mais elle montre comment vous pouvez étendre le style ultérieurement.

---

## Étape 4 : Appliquez le style défini à la cellule sélectionnée

Maintenant que le style existe, nous **apply style to cell** avec un seul appel de méthode.

```csharp
// Step 3: Apply the defined style to the selected cell
firstCell.SetStyle(cellStyle);
```

C’est tout — Aspose.Cells se charge de copier le style dans la collection interne de styles de la cellule. Si vous avez besoin du même formatage sur une plage, vous pouvez utiliser `ws.Cells.CreateRange("A1:D1").ApplyStyle(cellStyle, new StyleFlag { All = true });`.

---

## Étape 5 : Enregistrez le classeur et vérifiez le résultat

Un enregistrement rapide vous permet d’ouvrir le fichier dans Excel et de confirmer que le texte est bien centré et que la bordure apparaît.

```csharp
// Save the workbook to disk
string outputPath = "StyledCell.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the styled cell.");
```

*Résultat attendu :* En ouvrant **StyledCell.xlsx**, la cellule **A1** contient « Hello, styled world! » centré horizontalement et verticalement, entouré d’une bordure grise fine, et posé sur un arrière‑plan gris clair.

---

## Variations courantes & cas limites

### 1. Centrer le texte dans une région fusionnée

Si vous fusionnez les cellules **A1:C1** et que vous voulez toujours que le texte soit centré, vous devez appliquer le style à la cellule en haut‑à‑gauche **après** la fusion :

```csharp
ws.Cells.Merge(0, 0, 1, 3); // Merge A1:C1
firstCell.SetStyle(cellStyle); // Style still works because it’s applied to the anchor cell
```

### 2. Utiliser un format numérique

Parfois vous devez **set cell alignment** *et* afficher des nombres avec un format spécifique :

```csharp
cellStyle.Custom = "#,##0.00"; // Two decimal places
firstCell.PutValue(12345.678);
firstCell.SetStyle(cellStyle);
```

L’alignement reste centré tandis que le nombre apparaît sous la forme `12,345.68`.

### 3. Réutiliser les styles de façon efficace

Créer un nouveau `Style` pour chaque cellule peut nuire aux performances. À la place, créez un objet style unique et réutilisez‑le sur de nombreuses cellules ou plages. La classe `StyleFlag` vous permet d’appliquer uniquement les parties qui vous intéressent, économisant ainsi de la mémoire.

```csharp
StyleFlag flag = new StyleFlag { HorizontalAlignment = true, Borders = true };
ws.Cells.CreateRange("B2:B10").ApplyStyle(cellStyle, flag);
```

---

## Astuces pro & pièges à éviter

- **N’oubliez pas l’alignement vertical** — centrer uniquement horizontalement donne souvent un rendu déséquilibré, surtout avec des lignes hautes.
- **Types de bordure** : `CellBorderType.Thin` convient à la plupart des rapports, mais vous pouvez passer à `Medium` ou `Dashed` pour créer une hiérarchie visuelle.
- **Gestion des couleurs** : sous .NET Core, utilisez `System.Drawing.Color` du package `System.Drawing.Common` ; sinon vous rencontrerez une erreur d’exécution.
- **Format d’enregistrement** : si vous avez besoin de compatibilité avec d’anciennes versions d’Excel, changez `SaveFormat.Xlsx` en `SaveFormat.Xls`.

---

![Create cell style example](https://example.com/images/create-cell-style.png "Créer un style de cellule en C#")

*Texte alternatif : capture d’écran montrant une cellule avec texte centré et bordure fine créée par le tutoriel create cell style.*

---

## Exemple complet fonctionnel (prêt à copier‑coller)

```csharp
using System;
using Aspose.Cells;
using System.Drawing; // For Color

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // 2️⃣ Grab the first cell and put a sample value
        Cell firstCell = ws.Cells[0, 0];
        firstCell.PutValue("Hello, styled world!");

        // 3️⃣ Create the style: center text, thin border, light gray background
        Style cellStyle = workbook.CreateStyle();
        cellStyle.HorizontalAlignment = TextAlignmentType.Center;
        cellStyle.VerticalAlignment   = TextAlignmentType.Center;
        cellStyle.Borders[BorderType.TopBorder].LineStyle    = CellBorderType.Thin;
        cellStyle.Borders[BorderType.BottomBorder].LineStyle = CellBorderType.Thin;
        cellStyle.Borders[BorderType.LeftBorder].LineStyle   = CellBorderType.Thin;
        cellStyle.Borders[BorderType.RightBorder].LineStyle  = CellBorderType.Thin;
        cellStyle.ForegroundColor = Color.LightGray;
        cellStyle.Pattern = BackgroundType.Solid;

        // 4️⃣ Apply the style to the cell
        firstCell.SetStyle(cellStyle);

        // 5️⃣ Save the result
        string outputPath = "StyledCell.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);
        Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the styled cell.");
    }
}
```

Exécutez ce programme, ouvrez **StyledCell.xlsx**, et vous verrez exactement le résultat décrit précédemment. N’hésitez pas à modifier le texte, le style de bordure ou la couleur d’arrière‑plan pour l’adapter à votre charte graphique.

---

## Conclusion

Nous venons de **create cell style** à partir de zéro, **apply style to cell**, et de démontrer **how to center text** à la fois horizontalement et verticalement. En maîtrisant ces blocs de construction, vous pouvez maintenant formater des en‑têtes, mettre en évidence des totaux ou créer des modèles de rapports complets sans quitter C#.  

Si vous êtes curieux des étapes suivantes, essayez :

- **Appliquer le même style à toute une ligne** (`ws.Cells.CreateRange("A2:E2").ApplyStyle(cellStyle, new StyleFlag { All = true });`).
- **Ajouter une mise en forme conditionnelle** pour changer l’arrière‑plan selon les valeurs des cellules.
- **Exporter en PDF** tout en conservant le style.

Rappelez‑vous, le style concerne autant la lisibilité que l’esthétique. Expérimentez, itérez, et vos feuilles de calcul seront bientôt aussi professionnelles que votre code.

*Bon codage !*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}