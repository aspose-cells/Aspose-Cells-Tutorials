---
category: general
date: 2026-03-30
description: Créer un classeur Excel en C# avec Aspose.Cells. Apprenez à appliquer
  la fonction LAMBDA d’Excel, la fonction SEQUENCE d’Excel, la fonction EXPAND d’Excel,
  et à enregistrer le classeur au format xlsx.
draft: false
keywords:
- create excel workbook c#
- lambda function excel
- save workbook as xlsx
- sequence function excel
- expand array excel
language: fr
og_description: Créez rapidement un classeur Excel en C#. Ce guide montre comment
  utiliser la fonction lambda Excel, la fonction séquence Excel, la fonction d'expansion
  de tableau Excel, et enregistrer le classeur au format xlsx.
og_title: Créer un classeur Excel en C# – Guide Lambda, SEQUENCE et EXPAND
tags:
- Aspose.Cells
- C#
- Excel automation
title: Créer un classeur Excel en C# – Guide Lambda, SEQUENCE et EXPAND
url: /fr/net/formulas-functions/create-excel-workbook-c-lambda-sequence-expand-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un classeur Excel C# – Guide Lambda, SEQUENCE & EXPAND

Vous avez déjà eu besoin de **créer un classeur Excel C#** pour un rapport automatisé, mais vous ne saviez pas quelles appels d’API utiliser ? Vous n’êtes pas seul — de nombreux développeurs rencontrent le même obstacle lorsqu’ils s’initient à la génération programmatique d’Excel. Dans ce guide, vous verrez un exemple complet et exécutable qui couvre tout, de la nouvelle **fonction SEQUENCE Excel** à la puissante **fonction LAMBDA Excel**, en passant par la façon d’**étendre les résultats de tableau Excel**.  

Nous vous montrerons également les étapes exactes pour **enregistrer le classeur au format xlsx** afin que vous puissiez remettre le fichier à quiconque utilise Excel. À la fin de ce tutoriel, vous disposerez d’un extrait de code solide, prêt pour la production, que vous pourrez intégrer à n’importe quel projet .NET. Pas de liens vagues « voir la documentation » — juste du code qui fonctionne dès aujourd’hui.

## Ce dont vous avez besoin

- **.NET 6.0 ou version ultérieure** – l’exemple cible .NET 6, mais toute version récente fonctionne.  
- **Aspose.Cells for .NET** – installez via NuGet (`Install-Package Aspose.Cells`).  
- Une compréhension de base de la syntaxe C# (variables, objets et expressions lambda).  
- Un IDE avec lequel vous êtes à l’aise (Visual Studio, Rider ou VS Code).  

C’est tout. Aucun interop COM supplémentaire, aucun Office installé sur le serveur — Aspose.Cells gère tout en mémoire.

## Créer un classeur Excel C# – Implémentation pas à pas

Ci‑dessous, nous découpons le processus en étapes faciles à digérer. Chaque étape possède un titre clair, un court extrait de code et une explication du **pourquoi**. N’hésitez pas à copier le bloc complet à la fin et à l’exécuter comme application console.

### Étape 1 – Initialiser un nouveau classeur

Tout d’abord : nous avons besoin d’un objet classeur vierge qui représente le fichier Excel en mémoire.

```csharp
using Aspose.Cells;

// Step 1: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // empty workbook
Worksheet sheet = workbook.Worksheets[0];         // default first sheet
```

*Pourquoi c’est important :* `Workbook` est le point d’entrée pour toutes les opérations Aspose.Cells. En récupérant le premier `Worksheet`, nous obtenons une toile où nous pouvons écrire des formules, des valeurs ou appliquer du formatage.  

> **Astuce :** Si vous avez besoin de plusieurs feuilles, appelez simplement `workbook.Worksheets.Add()` et conservez une référence à chacune.

### Étape 2 – Utiliser la fonction SEQUENCE Excel pour générer des données

La **fonction SEQUENCE Excel** crée un tableau dynamique de nombres sans aucun VBA. Nous la placerons dans la cellule `A1` et laisserons Excel l’étendre automatiquement.

```csharp
// Step 2: Generate a 5‑row, 1‑column array from a SEQUENCE
sheet["A1"].Formula = "EXPAND(SEQUENCE(3),5,1)"; // 1..3 padded with blanks
```

*Pourquoi c’est important :* `SEQUENCE(3)` renvoie `[1,2,3]`. L’envelopper avec `EXPAND` force le résultat dans une plage de 5 lignes, remplissant les lignes supplémentaires avec des cellules vides. Cela montre à la fois la **fonction SEQUENCE Excel** et **l’expansion de tableau Excel** en une seule fois.

### Étape 3 – Agréger les nombres avec la fonction LAMBDA Excel

Passons maintenant à la capacité de la **fonction LAMBDA Excel**. Nous additionnerons les nombres 1‑5 en utilisant la nouvelle fonction `REDUCE`, qui s’appuie en interne sur une lambda.

```csharp
// Step 3: Aggregate a sequence (sum 1..5) using REDUCE/LAMBDA
sheet["B1"].Formula = "REDUCE(0, SEQUENCE(5), LAMBDA(a,b, a+b))"; // result = 15
```

*Pourquoi c’est important :* `REDUCE` parcourt le tableau produit par `SEQUENCE(5)`, en transmettant chaque élément (`b`) à la lambda avec l’accumulateur (`a`). La lambda `a+b` les additionne, laissant `15` dans `B1`. C’est une façon propre, uniquement avec des formules, d’effectuer des réductions sans boucle en C#.

### Étape 4 – Appliquer des fonctions trigonométriques directement dans les cellules

Les fonctions mathématiques intégrées d’Excel sont pratiques pour des calculs rapides. Nous placerons une cotangente et une cotangente hyperbolique dans des cellules adjacentes.

```csharp
// Step 4: Trigonometric functions directly in Excel cells
sheet["C1"].Formula = "COT(PI()/4)";   // evaluates to 1
sheet["D1"].Formula = "COTH(1)";      // hyperbolic cotangent of 1
```

*Pourquoi c’est important :* Cela montre que vous pouvez mélanger les fonctions mathématiques classiques avec les nouvelles formules à tableau dynamique. Aucun besoin de calculer ces valeurs en C# sauf si vous avez une raison de performance précise.

### Étape 5 – Calculer toutes les formules

Aspose.Cells n’évalue pas automatiquement les formules lorsqu’on les définit. Vous devez lui demander de les calculer.

```csharp
// Step 5: Force calculation so that cells store the results
workbook.CalculateFormula();
```

*Pourquoi c’est important :* Après cet appel, la propriété `Value` de chaque cellule contient le résultat évalué, prêt à être enregistré ou relu.

### Étape 6 – Enregistrer le classeur au format Xlsx

Enfin, nous persistons le classeur sur le disque en utilisant le modèle **enregistrer le classeur au format xlsx**.

```csharp
// Step 6: Save the workbook to an Excel file (XLSX format)
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "NewFunctions.xlsx");

workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to: {outputPath}");
```

*Pourquoi c’est important :* La méthode `Save` détecte automatiquement l’extension du fichier. En utilisant « .xlsx », nous nous assurons que le fichier est compatible avec les versions modernes d’Excel. Le chemin pointe vers le bureau pour un accès facile lors des tests.

### Exemple complet fonctionnel

Voici le programme complet que vous pouvez coller dans un nouveau projet console. Il inclut toutes les étapes ci‑dessus, ainsi qu’un petit bloc de vérification qui affiche les valeurs calculées dans la console.

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Initialize workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // SEQUENCE + EXPAND
        sheet["A1"].Formula = "EXPAND(SEQUENCE(3),5,1)";

        // REDUCE with LAMBDA
        sheet["B1"].Formula = "REDUCE(0, SEQUENCE(5), LAMBDA(a,b, a+b))";

        // Trig functions
        sheet["C1"].Formula = "COT(PI()/4)";
        sheet["D1"].Formula = "COTH(1)";

        // Calculate formulas
        workbook.CalculateFormula();

        // Verify results (optional)
        Console.WriteLine("A1‑A5 (expanded SEQUENCE):");
        for (int i = 0; i < 5; i++)
        {
            Console.WriteLine($"  Row {i + 1}: {sheet.Cells[i, 0].Value ?? "blank"}");
        }
        Console.WriteLine($"B1 (sum 1‑5): {sheet["B1"].Value}");
        Console.WriteLine($"C1 (cot(π/4)): {sheet["C1"].Value}");
        Console.WriteLine($"D1 (coth(1)): {sheet["D1"].Value}");

        // Save workbook
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "NewFunctions.xlsx");
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to: {outputPath}");
    }
}
```

**Sortie attendue dans la console**

```
A1‑A5 (expanded SEQUENCE):
  Row 1: 1
  Row 2: 2
  Row 3: 3
  Row 4: blank
  Row 5: blank
B1 (sum 1‑5): 15
C1 (cot(π/4)): 1
D1 (coth(1)): 1.31303528549933
Workbook saved to: C:\Users\YourName\Desktop\NewFunctions.xlsx
```

Et lorsque vous ouvrez *NewFunctions.xlsx*, vous verrez les mêmes nombres disposés dans les quatre premières colonnes.

![créer classeur excel c# capture d’écran du tableau résultant](/images/create-excel-workbook-csharp.png)

## Cas limites, astuces et questions fréquentes

- **Et si j’ai besoin de plus d’une feuille ?**  
  Appelez simplement `workbook.Worksheets.Add()` et répétez les affectations de formules sur chaque nouvel objet `Worksheet`.  

- **Puis‑je utiliser des versions plus anciennes d’Excel ?**  
  Les fonctions à tableau dynamique (`SEQUENCE`, `EXPAND`, `REDUCE`) nécessitent Excel 365 ou Excel 2021+. Si vous ciblez des versions plus anciennes, utilisez les formules classiques ou calculez les valeurs en C# avant de les écrire.  

- **Problèmes de performance ?**  
  Pour des milliers de lignes, définir des formules sur une plage puis appeler `CalculateFormula` est généralement plus rapide que de boucler et d’assigner les valeurs une par une.  

- **Enregistrer dans un flux au lieu d’un fichier ?**  
  `work

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}