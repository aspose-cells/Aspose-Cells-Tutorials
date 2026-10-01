---
category: general
date: 2026-10-01
description: Créez rapidement un classeur Excel en C# et apprenez un exemple de formule
  de tableau dynamique pour écrire une formule Excel en C# avec Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook c#
- dynamic array formula example
- write excel formula c#
language: fr
lastmod: 2026-10-01
og_description: Créez rapidement un classeur Excel en C# et découvrez un exemple de
  formule de tableau dynamique montrant comment écrire une formule Excel en C# avec
  Aspose.Cells. Suivez le guide étape par étape pour générer, calculer et enregistrer
  le fichier.
og_image_alt: Screenshot of C# code creating an Excel workbook and applying a SORT
  dynamic array formula
og_title: Créer un classeur Excel C# avec une formule de tableau dynamique
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Create Excel workbook C# quickly and learn a dynamic array formula
    example to write Excel formula C# in Aspose.Cells.
  headline: How to create Excel workbook C# with a dynamic array formula
  type: TechArticle
- description: Create Excel workbook C# quickly and learn a dynamic array formula
    example to write Excel formula C# in Aspose.Cells.
  name: How to create Excel workbook C# with a dynamic array formula
  steps:
  - name: Verifying the result (expected output)
    text: 'You can print the spilled values to the console to confirm the calculation
      succeeded:'
  - name: What if I need to use a different dynamic array function?
    text: 'Replace the formula string with any other dynamic array function, such
      as `=FILTER(A2:A10, B2:B10>10)` or `=UNIQUE(A2:A10)`. The same **write Excel
      formula C#** pattern applies:'
  - name: How do I handle formulas that reference other worksheets?
    text: 'Reference another sheet by its name:'
  - name: Can I suppress automatic calculation and calculate later?
    text: 'Yes. Set the workbook’s calculation mode to manual:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Comment créer un classeur Excel en C# avec une formule de tableau dynamique
url: /fr/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-c-with-a-dynamic-array-formula/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment créer un classeur Excel C# avec une formule de tableau dynamique

Si vous devez **créer un classeur Excel C#** de façon programmatique, ce guide vous montre exactement comment le faire en utilisant Aspose.Cells. Vous obtiendrez également un **exemple de formule de tableau dynamique** qui illustre la meilleure façon de **écrire une formule Excel C#** pour les fonctions modernes d’Excel comme `SORT`.

Créer un fichier Excel depuis C# nécessitait auparavant l’interop COM ou la génération manuelle de XML, deux approches fragiles et difficiles à maintenir. À la fin de ce tutoriel, vous disposerez d’un classeur pleinement fonctionnel qui calcule automatiquement un tableau dynamique, et vous comprendrez pourquoi cette méthode est fiable pour une automatisation de niveau production.

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

- .NET 6.0 ou une version ultérieure installée (le code fonctionne également avec .NET Core et .NET Framework)
- Une licence valide Aspose.Cells ou une clé d’évaluation gratuite
- Visual Studio 2022 (ou tout IDE supportant C#)
- Une connaissance de base de la syntaxe C# et des formules Excel

Aucun package NuGet supplémentaire n’est requis au‑delà de `Aspose.Cells`, que vous pouvez ajouter avec :

```bash
dotnet add package Aspose.Cells
```

## Étape 1 : Configurer le projet C# et référencer Aspose.Cells

Créez une nouvelle application console et ajoutez la référence Aspose.Cells. Cette étape est essentielle car la bibliothèque fournit les objets `Workbook`, `Worksheet` et le moteur de calcul dont vous avez besoin pour **écrire une formule Excel C#**.

```csharp
// Program.cs
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // The rest of the tutorial code lives inside this method.
    }
}
```

> **Pourquoi c’est important :** Aspose.Cells masque les détails bas‑niveau d’OpenXML, vous permettant de vous concentrer sur la logique métier plutôt que sur les particularités du format de fichier.

## Étape 2 : Créer le classeur Excel et obtenir la première feuille

Nous **créons maintenant le classeur Excel C#** en instanciant un objet `Workbook`. Le classeur par défaut contient une seule feuille, que nous récupérons pour les opérations suivantes.

```csharp
// Step 2: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // creates a blank .xlsx file in memory
Worksheet worksheet = workbook.Worksheets[0];    // first (and only) sheet by default
```

> **Astuce :** Si vous avez besoin de plusieurs feuilles, appelez `workbook.Worksheets.Add()` avant d’y accéder.

## Étape 3 : Remplir les données sources pour le tableau dynamique

Les fonctions de tableau dynamique comme `SORT` nécessitent une plage source. Remplissons les cellules *A2:A10* avec des nombres non triés afin que la formule `SORT` puisse démontrer son comportement.

```csharp
// Step 3: Fill A2:A10 with sample data
int[] numbers = { 42, 7, 19, 33, 5, 27, 14, 8, 21 };
for (int i = 0; i < numbers.Length; i++)
{
    worksheet.Cells[i + 1, 0].PutValue(numbers[i]); // Row i+2, Column A (0‑based index)
}
```

> **Pourquoi faisons‑nous cela :** Fournir des données concrètes vous permet de voir l’**exemple de formule de tableau dynamique** en action sans avoir besoin de fichiers d’entrée externes.

## Étape 4 : Inscrire la formule de tableau dynamique dans la cellule A1

Voici le cœur de la partie **écrire une formule Excel C#**. Nous assignons une formule `SORT` à la cellule *A1*. Comme `SORT` est une fonction de tableau dynamique, Excel déversera automatiquement les résultats triés dans les cellules en dessous.

```csharp
// Step 4: Insert a dynamic array formula (SORT) into cell A1
worksheet.Cells[0, 0].Formula = "=SORT(A2:A10)";
```

> **Explication :**  
> - `worksheet.Cells[0, 0]` cible la cellule **A1** (ligne 0, colonne 0).  
> - La chaîne `=SORT(A2:A10)` est une formule Excel standard. Aspose.Cells la parse de la même façon qu’Excel, offrant un support complet des fonctions de tableau dynamique modernes.

## Étape 5 : Recalculer le classeur afin que la formule se remplisse automatiquement

Aspose.Cells ne recalcule pas les formules automatiquement à l’écriture. Vous devez déclencher explicitement le calcul pour voir les résultats déversés.

```csharp
// Step 5: Recalculate the workbook so the formula evaluates
workbook.Calculate();   // runs the calculation engine once
```

Après cet appel, les cellules **A1:A9** contiendront la liste triée : 5, 7, 8, 14, 19, 21, 27, 33, 42.

### Vérification du résultat (sortie attendue)

Vous pouvez afficher les valeurs déversées dans la console pour confirmer que le calcul a réussi :

```csharp
Console.WriteLine("Sorted values from A1 down:");
for (int row = 0; row < 9; row++)
{
    Console.WriteLine(worksheet.Cells[row, 0].StringValue);
}
```

**Sortie console attendue**

```
Sorted values from A1 down:
5
7
8
14
19
21
27
33
42
```

> **Note de cas limite :** Si la plage source contient des données non numériques, `SORT` les triera lexicographiquement. Validez toujours les types de données avant d’appliquer des fonctions réservées aux nombres.

## Étape 6 : Enregistrer le classeur sur le disque (optionnel)

Sauvegarder le fichier vous permet de l’ouvrir dans Excel et de voir le tableau dynamique visuellement. Cette étape n’est pas requise pour le calcul lui‑même, mais elle est utile pour le débogage et la distribution.

```csharp
// Step 6: Save the workbook as an .xlsx file
string outputPath = "SortedNumbers.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Lorsque vous ouvrirez *SortedNumbers.xlsx* dans Excel 365 ou une version ultérieure, vous verrez la liste triée se déverser automatiquement à partir de **A1** vers le bas—exactement ce que l’**exemple de formule de tableau dynamique** a produit depuis C#.

## Exemple complet fonctionnel

En réunissant tous les éléments, voici le programme complet et exécutable :

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1. Create workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2. Fill source data (A2:A10)
        int[] numbers = { 42, 7, 19, 33, 5, 27, 14, 8, 21 };
        for (int i = 0; i < numbers.Length; i++)
        {
            worksheet.Cells[i + 1, 0].PutValue(numbers[i]); // A2:A10
        }

        // 3. Write dynamic array formula (SORT) into A1
        worksheet.Cells[0, 0].Formula = "=SORT(A2:A10)";

        // 4. Force calculation so the array spills
        workbook.Calculate();

        // 5. Display the spilled values in the console
        Console.WriteLine("Sorted values from A1 down:");
        for (int row = 0; row < 9; row++)
        {
            Console.WriteLine(worksheet.Cells[row, 0].StringValue);
        }

        // 6. Save the workbook (optional)
        string outputPath = "SortedNumbers.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Exécutez le programme (`dotnet run`) et vous verrez les nombres triés affichés, suivis d’une confirmation que le fichier a été enregistré.

## Questions fréquentes et variantes

### Et si je dois utiliser une fonction de tableau dynamique différente ?

Remplacez la chaîne de formule par n’importe quelle autre fonction de tableau dynamique, comme `=FILTER(A2:A10, B2:B10>10)` ou `=UNIQUE(A2:A10)`. Le même modèle **écrire une formule Excel C#** s’applique :

```csharp
worksheet.Cells[0, 0].Formula = "=UNIQUE(A2:A10)";
```

### Comment gérer les formules qui font référence à d’autres feuilles ?

Référez‑vous à une autre feuille par son nom :

```csharp
worksheet.Cells[0, 0].Formula = "=SORT('Sheet2'!A2:A10)";
```

Aspose.Cells résout automatiquement les références inter‑feuilles lors de `workbook.Calculate()`.

### Puis‑je désactiver le calcul automatique et le lancer plus tard ?

Oui. Définissez le mode de calcul du classeur sur manuel :

```csharp
workbook.Settings.CalcMode = CalcMode.Manual;
// ... make many changes ...
workbook.Calculate(); // call once when ready
```

Cela améliore les performances lorsque vous mettez à jour des milliers de cellules avant un calcul final.

## Conclusion

Vous savez maintenant comment **créer un classeur Excel C#** avec Aspose.Cells, insérer un **exemple de formule de tableau dynamique**, et **écrire une formule Excel C#** qui déverse automatiquement les résultats. La solution complète couvre la configuration du projet, la préparation des données, l’insertion de la formule, le calcul forcé, la vérification et l’enregistrement optionnel du fichier.

À partir d’ici, vous pouvez explorer des scénarios plus avancés : chaîner plusieurs fonctions de tableau dynamique, appliquer des formats numériques personnalisés, ou intégrer la génération de classeur dans une API web. N’oubliez pas de toujours valider les données d’entrée avant d’appliquer des formules, et profitez du moteur de calcul riche d’Aspose.Cells pour un traitement Excel côté serveur fiable. Bon codage !

## Que devez‑vous apprendre ensuite ?


Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Créer un nouveau classeur en C# – Ajouter une formule et enregistrer le fichier Excel](/cells/english/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/)
- [Automatisation Excel avec Aspose.Cells .NET : Maîtriser les classeurs et le calcul des formules](/cells/english/net/formulas-functions/excel-automation-aspose-cells-net-workbook-formulas/)
- [Créer un classeur Excel C# – Guide complet avec Aspose.Cells](/cells/english/net/excel-workbook/create-excel-workbook-c-complete-guide-with-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}