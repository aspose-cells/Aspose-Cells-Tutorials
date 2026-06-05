---
category: general
date: 2026-06-05
description: Créer rapidement un classeur Excel en C# et apprendre à définir le format
  numérique des cellules, à exporter une cellule Excel et à convertir la valeur d’une
  cellule en chaîne avec une précision de deux décimales.
draft: false
keywords:
- create excel workbook
- set cell number format
- format number with two decimals
- how to export excel cell
- convert cell value to string
language: fr
og_description: Créer un classeur Excel en C# et maîtriser le réglage du format numérique
  des cellules, l'exportation d'une cellule Excel en chaîne, ainsi que le formatage
  des nombres avec deux décimales.
og_title: Créer un classeur Excel en C# – Guide complet étape par étape
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: Create Excel workbook in C# quickly and learn how to set cell number
    format, export Excel cell, and convert cell value to string with two‑decimal precision.
  headline: Create Excel Workbook in C# – Complete Programming Guide
  type: TechArticle
- description: Create Excel workbook in C# quickly and learn how to set cell number
    format, export Excel cell, and convert cell value to string with two‑decimal precision.
  name: Create Excel Workbook in C# – Complete Programming Guide
  steps:
  - name: What if the cell already has a style?
    text: The `GetStyle` method returns a copy of the existing style, so any previous
      formatting (font, color, etc.) is retained. You only overwrite the `Custom`
      property, leaving everything else untouched.
  - name: How does culture affect the decimal separator?
    text: 'Aspose.Cells respects the thread’s `CultureInfo`. If you need a comma instead
      of a dot, set:'
  - name: Can I export a range of cells at once?
    text: Yes—use `Worksheet.ExportDataTable` or `Worksheet.ExportString` with a range
      address. The `ExportTableOptions` you defined for a single cell can be reused
      for the whole range.
  - name: What if I don’t want the value rounded but truncated?
    text: 'Change the custom format to `"0.00"` with a rounding mode, or manually
      truncate before putting the value:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
title: Créer un classeur Excel en C# – Guide complet de programmation
url: /fr/net/excel-workbook/create-excel-workbook-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un classeur Excel en C# – Guide complet de programmation

Vous vous êtes déjà demandé comment **créer un classeur Excel** en C# sans vous battre avec l’interop COM ou des astuces CSV désordonnées ? Vous n’êtes pas seul. De nombreux développeurs recherchent une méthode native .NET propre pour générer un fichier .xlsx, y placer un nombre dans une cellule, puis exporter cette valeur sous forme de chaîne correctement formatée.  

Dans ce tutoriel, nous allons parcourir exactement cela : partir d’un classeur vide, définir le format numérique de la cellule, formater le nombre avec deux décimales, et enfin apprendre **comment exporter les données d’une cellule Excel** sous forme de chaîne. À la fin, vous verrez aussi comment **convertir la valeur d’une cellule en chaîne** sans perdre de précision.

> **Astuce :** L’approche ci‑dessous utilise la bibliothèque **Aspose.Cells for .NET**, une API commerciale éprouvée. Si vous cherchez une alternative gratuite, EPPlus ou ClosedXML fonctionnent de façon similaire, mais les extraits de code différeront légèrement.

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

- .NET 6.0 SDK (ou toute version .NET récente) installé.
- Visual Studio 2022 ou VS Code avec l’extension C#.
- Le package NuGet **Aspose.Cells** (`Install-Package Aspose.Cells`).

Aucune autre dépendance n’est requise — tout le reste se trouve dans la bibliothèque.

## Étape 1 : Installer Aspose.Cells et configurer le projet

Ouvrez votre terminal (ou la console du Gestionnaire de packages) et exécutez :

```powershell
dotnet new console -n ExcelDemo
cd ExcelDemo
dotnet add package Aspose.Cells
```

Cela crée une nouvelle application console nommée `ExcelDemo` et ajoute l’assembly `Aspose.Cells`.  

Pourquoi cette étape est importante : sans la bibliothèque, vous ne pouvez pas **créer un classeur Excel** ni manipuler les cellules de façon typée.

## Étape 2 : Créer le classeur et récupérer la première feuille

Ouvrez maintenant `Program.cs` et remplacez le code par défaut par l’extrait ci‑dessous. Il montre la toute première chose à faire lorsque vous **créez un classeur Excel** : instancier la classe `Workbook` et obtenir une référence à la feuille par défaut.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 2: Create a workbook and get the first worksheet
        Workbook workbook = new Workbook();               // creates a new .xlsx in memory
        Worksheet ws = workbook.Worksheets[0];           // first (default) sheet

        // The rest of the steps will follow here...
```

> **Pourquoi ?** L’objet `Workbook` représente en mémoire un fichier Excel. Par défaut il contient une feuille de calcul, que nous accédons via l’indice zéro.

## Étape 3 : Insérer une valeur numérique dans une cellule précise

Visons la ligne 5, colonne 2 (indices zéro‑based) et insérons un nombre décimal. Cela servira plus tard à **formater le nombre avec deux décimales**.

```csharp
        // Step 3: Access the cell at row 5, column 2 (zero‑based) and insert a number
        Cell cell = ws.Cells[5, 2];          // corresponds to cell C6 in Excel UI
        cell.PutValue(12345.6789);          // raw value with many decimal places
```

La méthode `PutValue` stocke le double brut. À ce stade, Excel afficherait la pleine précision sauf si nous appliquons un format.

## Étape 4 : Définir le format numérique de la cellule (deux décimales)

Voici où nous **définissons le format numérique de la cellule**. Nous utilisons l’objet `Style` pour spécifier un format numérique personnalisé `"0.00"` — exactement deux décimales.

```csharp
        // Step 4: Apply a number format to show only two decimal places
        Style style = cell.GetStyle();               // clone existing style
        style.Custom = "0.00";                       // forces two digits after the dot
        cell.SetStyle(style);                        // apply the style back to the cell
```

Pourquoi utiliser un style plutôt qu’une conversion en chaîne ? Conserver la cellule sous forme numérique préserve sa nature calculable (vous pouvez toujours sommer, faire la moyenne, etc.) tout en affichant exactement ce dont vous avez besoin.

## Étape 5 : Exporter la valeur de la cellule sous forme de chaîne formatée

Parfois, vous avez besoin de **comment exporter la valeur d’une cellule Excel** en texte brut — par exemple pour l’écrire dans un fichier journal ou l’envoyer via une API web. Aspose.Cells vous permet d’attacher des options d’exportation à une cellule, indiquant à la bibliothèque de rendre la valeur sous forme de chaîne en utilisant le même format numérique.

```csharp
        // Step 5: Configure export options to get the formatted string
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,          // forces string output
            NumberFormat = "0.00"           // matches the style we set earlier
        };
        cell.ExportOptions = exportOptions; // attach options to the cell
```

Désormais, lorsque nous lisons la valeur de la cellule via l’API d’exportation, nous recevrons une chaîne qui respecte déjà la règle des deux décimales.

## Étape 6 : Récupérer la chaîne formatée (Convertir la valeur d’une cellule en chaîne)

Effectuons réellement l’exportation et voyons le résultat. La méthode `ExportString` renvoie le contenu de la cellule sous forme de chaîne, en appliquant les `ExportTableOptions` que nous avons attachées.

```csharp
        // Step 6: Export the cell as a formatted string
        string formattedValue = cell.ExportString();
        Console.WriteLine($"Formatted cell value: {formattedValue}");
```

Lorsque vous exécutez le programme, la console affiche :

```
Formatted cell value: 12345.68
```

Remarquez l’arrondi de `12345.6789` à `12345.68` — c’est l’effet de **formater le nombre avec deux décimales**.

## Étape 7 : (Optionnel) Enregistrer le classeur sur le disque

Si vous voulez également voir le résultat dans un vrai fichier `.xlsx`, il suffit d’appeler `Save` :

```csharp
        // Optional: write the workbook to a file so you can open it in Excel
        workbook.Save("DemoWorkbook.xlsx");
    }
}
```

L’ouverture de `DemoWorkbook.xlsx` montre le même nombre dans la cellule **C6**, formaté avec deux décimales.

## Cas limites et questions fréquentes

### Et si la cellule possède déjà un style ?

La méthode `GetStyle` renvoie une copie du style existant, de sorte que tout formatage antérieur (police, couleur, etc.) est conservé. Vous ne remplacez que la propriété `Custom`, laissant le reste intact.

### Comment la culture affecte‑t‑elle le séparateur décimal ?

Aspose.Cells respecte le `CultureInfo` du thread. Si vous avez besoin d’une virgule au lieu d’un point, définissez :

```csharp
System.Threading.Thread.CurrentThread.CurrentCulture = new System.Globalization.CultureInfo("fr-FR");
```

Le même format `"0.00"` affichera désormais `12 345,68`.

### Puis‑je exporter une plage de cellules en une fois ?

Oui — utilisez `Worksheet.ExportDataTable` ou `Worksheet.ExportString` avec une adresse de plage. Les `ExportTableOptions` définies pour une cellule unique peuvent être réutilisées pour toute la plage.

### Et si je ne veux pas que la valeur soit arrondie mais tronquée ?

Modifiez le format personnalisé pour inclure un mode d’arrondi, ou tronquez manuellement avant d’insérer la valeur :

```csharp
double raw = Math.Truncate(12345.6789 * 100) / 100; // yields 12345.67
cell.PutValue(raw);
```

## Exemple complet fonctionnel (prêt à copier‑coller)

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 2: Create a workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // Step 3: Access the cell at row 5, column 2 (zero‑based) and insert a number
        Cell cell = ws.Cells[5, 2];
        cell.PutValue(12345.6789);

        // Step 4: Apply a number format to show only two decimal places
        Style style = cell.GetStyle();
        style.Custom = "0.00";
        cell.SetStyle(style);

        // Step 5: Configure export options to get the formatted string
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "0.00"
        };
        cell.ExportOptions = exportOptions;

        // Step 6: Export the cell as a formatted string
        string formattedValue = cell.ExportString();
        Console.WriteLine($"Formatted cell value: {formattedValue}");

        // Optional: save the workbook for visual verification
        workbook.Save("DemoWorkbook.xlsx");
    }
}
```

**Sortie console attendue**

```
Formatted cell value: 12345.68
```

Ouvrez `DemoWorkbook.xlsx` → allez à la cellule **C6** → vous verrez le même nombre avec deux décimales.

## Conclusion

Nous venons de couvrir tout ce dont vous avez besoin pour **créer un classeur Excel** en C#, **définir le format numérique d’une cellule**, **formater le nombre avec deux décimales**, comprendre **comment exporter les données d’une cellule Excel**, et **convertir la valeur d’une cellule en chaîne** pour un traitement en aval.  

Les points clés sont :

1. Utilisez `Workbook` et `Worksheet` pour créer un fichier Excel en mémoire.  
2. Appliquez un style personnalisé (`"0.00"`) pour imposer l’affichage à deux décimales.  
3. Attachez `ExportTableOptions` à une cellule lorsque vous avez besoin d’une représentation chaîne qui respecte le même format.  

À partir d’ici, vous pouvez expérimenter — ajouter d’autres cellules, appliquer un format conditionnel, voire générer des graphiques. Si vous êtes curieux concernant le style des polices ou l’ajout de formules, consultez la documentation Aspose.Cells sur **cell styling** et **formula evaluation**.

Vous avez d’autres questions sur l’automatisation d’Excel en C# ? Laissez un commentaire, et bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Master Workbook Operations in Aspose.Cells .NET&#58; Load Excel Files and Trace Cell Precedents Effectively](/cells/english/net/workbook-operations/aspose-cells-net-master-workbook-operations/)
- [Master Excel Cell Formatting and Workbook Management with Aspose.Cells for .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Master Aspose.Cells for .NET&#58; Advanced Excel Workbook and Cell Management](/cells/english/net/advanced-features/excel-aspose-cells-net-create-manage/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}