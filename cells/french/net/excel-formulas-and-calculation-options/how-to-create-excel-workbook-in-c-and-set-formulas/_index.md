---
category: general
date: 2026-10-01
description: Créez rapidement un classeur Excel en C#, apprenez à définir une formule,
  à calculer la cotangente et à utiliser la fonction PI dans Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook c#
- how to calculate cot
- set formula in cell
- write formula to cell
- how to use pi function
language: fr
lastmod: 2026-10-01
og_description: Créer un classeur Excel en C# avec Aspose.Cells. Apprenez à définir
  une formule, à utiliser la fonction PI et à calculer la cotangente en quelques étapes.
og_image_alt: Diagram showing an Excel workbook created in C# with a formula in cell
  A1
og_title: Créer un classeur Excel en C# – définir des formules et calculer le cot
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Create Excel workbook in C# quickly, learn how to set a formula, calculate
    cotangent, and use the PI function in Aspose.Cells.
  headline: How to create Excel workbook in C# and set formulas
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Comment créer un classeur Excel en C# et définir des formules
url: /fr/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-in-c-and-set-formulas/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment créer un classeur Excel en C# et définir des formules

Si vous avez besoin de **créer un classeur Excel en C#** qui écrit une formule dans une cellule, ce guide vous montre exactement comment. Vous verrez comment définir une formule dans une feuille de calcul, utiliser la fonction intégrée PI, et calculer la cotangente d’un angle — le tout avec Aspose.Cells.

Le tutoriel couvre tout, de l'initialisation du classeur à la récupération du résultat calculé, afin que vous puissiez copier l'exemple complet dans votre propre projet sans aucune pièce manquante.

## Prérequis

* .NET 6.0 ou version ultérieure installé  
* Une licence valide Aspose.Cells (ou une clé d'évaluation temporaire)  
* Visual Studio 2022 ou tout IDE C# de votre choix  

Aucun package NuGet supplémentaire n'est requis au-delà de `Aspose.Cells`.

## Créer un classeur Excel en C#

La première étape consiste à instancier un nouvel objet `Workbook`. Cet objet représente l'intégralité du fichier Excel en mémoire et vous donne accès à ses feuilles de calcul.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        var workbook = new Workbook();                 // creates an empty .xlsx file
        var worksheet = workbook.Worksheets[0];        // the default first sheet

        // Continue with the rest of the steps...
```

Créer le classeur de cette façon garantit que le fichier est prêt pour toute manipulation ultérieure, comme l'ajout de données, le style des cellules ou l'écriture de formules.

## Définir une formule dans une cellule en utilisant la fonction PI

Vous allez maintenant **écrire une formule dans la cellule** A1. La formule utilise la fonction `PI()` pour fournir la constante π et la fonction `COT` pour calculer sa cotangente.

```csharp
        // Step 2: Set a formula in cell A1 (row 0, column 0)
        // The formula calculates the cotangent of π/4, which equals 1
        worksheet.Cells[0, 0].Formula = "=COT(PI()/4)";

        // Continue with calculation...
```

*Pourquoi c'est important* : `PI()` est une fonction Excel intégrée qui renvoie la valeur de π. En la divisant par 4, vous obtenez 45°, et `COT` renvoie la cotangente de cet angle. Cela démontre **comment utiliser la fonction pi** dans une formule Excel depuis C#.

## Comment calculer la cotangente avec Aspose.Cells

Si vous vous demandez **comment calculer la cotangente** sans convertir manuellement les angles, la fonction `COT` fait le travail lourd. Elle accepte un angle en radians, vous pouvez donc la combiner avec `PI()` pour des angles courants.

```csharp
        // Step 3: Recalculate the workbook so the formula is evaluated
        workbook.Calculate();

        // Step 4: Retrieve and display the calculated result
        double result = worksheet.Cells[0, 0].DoubleValue;
        Console.WriteLine($"Cotangent of PI/4 = {result}");
    }
}
```

L'exécution du programme affiche :

```
Cotangent of PI/4 = 1
```

Parce que `COT(π/4)` vaut 1, la sortie confirme que la formule a été correctement **définie dans la cellule** et évaluée.

## Écrire une formule dans une cellule – conseils supplémentaires

* **Formules multiples** : Vous pouvez assigner une formule à n'importe quelle cellule en utilisant la même propriété `Formula`, par ex., `worksheet.Cells["B2"].Formula = "=SIN(PI()/2)";`.
* **Paramètres internationaux** : Aspose.Cells respecte la locale du classeur, de sorte que les noms de fonctions restent en anglais (`PI`, `COT`) quel que soit le paramètre régional de l'utilisateur.
* **Performance** : Si vous devez définir des milliers de formules, regroupez‑les et appelez `workbook.Calculate()` une fois à la fin pour éviter des recalculs répétés.

## Exemple complet exécutable

Voici le programme complet que vous pouvez copier‑coller dans un projet console. Il inclut toutes les instructions `using` requises et montre le flux de travail complet, de la création du classeur à la sortie du résultat.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook and obtain the first worksheet
        var workbook = new Workbook();
        var worksheet = workbook.Worksheets[0];

        // Write a formula that uses the PI function and calculates cotangent
        worksheet.Cells[0, 0].Formula = "=COT(PI()/4)";

        // Force calculation so the formula value is materialized
        workbook.Calculate();

        // Read the calculated value and display it
        double cotValue = worksheet.Cells[0, 0].DoubleValue;
        Console.WriteLine($"Cotangent of PI/4 = {cotValue}");

        // Optional: save the workbook to verify the formula visually
        workbook.Save("CotExample.xlsx");
    }
}
```

**Sortie attendue** lors de l'exécution du programme :

```
Cotangent of PI/4 = 1
```

Le fichier généré `CotExample.xlsx` contient la formule dans la cellule A1, vous permettant de l'ouvrir dans Excel et de voir le même résultat.

## Conclusion

Vous savez maintenant comment **créer un classeur Excel en C#** du code qui écrit une formule, utilise la fonction `PI`, et **calcule la cotangente** avec Aspose.Cells. L'exemple couvre tout le cycle de vie : création du classeur, **définir une formule dans la cellule**, recalcul, et récupération du résultat.

Les prochaines étapes que vous pourriez explorer :

* Appliquer **écrire une formule dans la cellule** pour des calculs plus complexes comme des modèles financiers.  
* Utiliser **définir une formule dans la cellule** avec le formatage conditionnel pour mettre en évidence les résultats.  
* Combiner **comment utiliser la fonction pi** avec des graphiques trigonométriques pour les rapports scientifiques.

N'hésitez pas à expérimenter avec différents angles, fonctions et mises en page de feuilles de calcul. Maîtriser la gestion des formules en C# ouvre la porte à des pipelines de reporting Excel entièrement automatisés. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Comment calculer la cotangente dans Excel avec C# – Créer un classeur, utiliser EXPAND](/cells/english/net/formulas-functions/how-to-calculate-cotangent-in-excel-with-c-create-workbook-u/)
- [Comment utiliser WRAPCOLS en C# – Créer un classeur Excel avec des fonctions d'enveloppe](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [Comment créer des plages nommées à portée du classeur dans Excel en utilisant Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}