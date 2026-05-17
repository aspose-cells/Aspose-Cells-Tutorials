---
category: general
date: 2026-03-22
description: Comment utiliser lambda en C# pour travailler avec les formules Excel.
  Apprenez à écrire une formule dans une cellule, convertir une plage en tableau,
  afficher le tableau dans la console et calculer la cotangente dans Excel.
draft: false
keywords:
- how to use lambda
- display array in console
- convert range to array
- write formula to cell
- calculate cotangent in excel
language: fr
og_description: Comment utiliser les lambda en C# pour manipuler les formules Excel,
  convertir une plage en tableau, écrire une formule dans une cellule, afficher le
  tableau dans la console et calculer la cotangente dans Excel.
og_title: Comment utiliser les lambda en C# avec les formules Excel – Étape par étape
tags:
- C#
- Aspose.Cells
- Excel Automation
- Lambda Expressions
title: Comment utiliser les lambda en C# avec les formules Excel – Guide complet
url: /fr/net/formulas-functions/how-to-use-lambda-in-c-with-excel-formulas-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment utiliser Lambda en C# avec les formules Excel – Guide complet

Vous vous êtes déjà demandé **comment utiliser lambda** lorsque vous automatisez Excel depuis C# ? Vous n'êtes pas seul. De nombreux développeurs se heurtent à un mur lorsqu'ils doivent combiner la puissance des nouvelles fonctions de tableau dynamique d'Excel avec la capacité `LAMBDA` de C#. Bonne nouvelle ? C’est en fait assez simple une fois que vous voyez comment les pièces s’emboîtent.

Dans ce tutoriel, nous passerons en revue **l’écriture d’une formule dans une cellule**, **la conversion d’une plage en tableau**, **l’affichage de ce tableau dans la console**, et même **le calcul de la cotangente dans Excel** — tout en vous montrant **comment utiliser lambda** à l’intérieur d’un appel `REDUCE`. À la fin, vous disposerez d’un extrait exécutable que vous pourrez intégrer à n’importe quel projet .NET faisant référence à Aspose.Cells (ou à une bibliothèque similaire).

---

## Ce que vous apprendrez

- Comment **écrire une formule dans une cellule** en utilisant C#.
- Comment **convertir une plage en tableau** avec la fonction `EXPAND`.
- Comment **afficher le tableau dans la console** après le calcul.
- Comment **calculer la cotangente dans Excel** en utilisant `COT` et `COTH`.
- La syntaxe exacte pour **comment utiliser lambda** à l’intérieur de la fonction `REDUCE` d’Excel depuis C#.

> **Prérequis :** Vous avez besoin d’une version récente de .NET (Core 6+ ou .NET Framework 4.7+) et de la bibliothèque Aspose.Cells pour .NET installée via NuGet.

---

## Étape 1 : Configurer le classeur et écrire la formule dans la cellule

La première chose que nous faisons est de créer un nouveau classeur et de récupérer la première feuille de calcul. Ensuite, nous **écrivons une formule dans une cellule** – dans ce cas, `A1` contiendra le résultat d’un appel `EXPAND`.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write formula to A1 – we’ll expand B1:C2 into a 4‑by‑5 array later
        worksheet.Cells["A1"].Formula = "=EXPAND(B1:C2, 4, 5)";
```

**Pourquoi c’est important :** Écrire la formule directement depuis le code vous permet de générer des feuilles de calcul complexes à la volée sans jamais ouvrir Excel. Cela prépare également l’étape suivante où nous **convertissons une plage en tableau**.

---

## Étape 2 : Convertir une plage en tableau avec EXPAND

`EXPAND` est la façon dont Excel transforme une petite plage en une matrice plus grande. En plaçant la formule dans `A1`, Excel déversera un bloc de 4 × 5 cellules à partir de cette cellule. Depuis C#, nous n’avons pas besoin de copier manuellement les valeurs – la bibliothèque se charge du travail lourd lorsque nous appelons `Calculate`.

```csharp
        // The EXPAND formula will spill into A1:E4 (4 rows × 5 columns)
        // No extra code needed – the workbook will handle the spill.
```

**Comment utiliser lambda :** Pas encore, mais restez à l’écoute. D’abord nous avons besoin des données dans la feuille, puis nous les réduirons avec un lambda.

---

## Étape 3 : Utiliser LAMBDA à l’intérieur de REDUCE – Le cœur de « Comment utiliser Lambda »

Excel 365 a introduit `REDUCE`, qui accepte une **valeur initiale**, une **plage**, et un **LAMBDA** qui indique comment combiner chaque élément. Depuis C#, nous assignons simplement la chaîne de formule ; le lambda vit à l’intérieur de la formule Excel, pas dans le code C#.

```csharp
        // Reduce the spilled array by summing all its values.
        // This demonstrates how to use lambda inside REDUCE.
        worksheet.Cells["E1"].Formula = "=REDUCE(0, A1:D4, LAMBDA(acc, x, acc + x))";
```

**Explication :**  
- `0` est l’accumulateur de départ (`acc`).  
- `A1:D4` est la plage que nous voulons traiter (les quatre premières colonnes du débordement).  
- `LAMBDA(acc, x, acc + x)` indique à Excel d’ajouter chaque cellule (`x`) à l’accumulateur.

C’est l’essence de **comment utiliser lambda** pour l’agrégation dans le contexte d’une feuille de calcul.

---

## Étape 4 : Calculer la cotangente dans Excel – Des degrés à l’hyperbolique

Si vous avez besoin de résultats trigonométriques, les fonctions `COT` et `COTH` d’Excel sont un jeu d’enfant. Nous les placerons respectivement dans `G1` et `G2`.

```csharp
        // Demonstrate trigonometric functions – cotangent and hyperbolic cotangent
        worksheet.Cells["G1"].Formula = "=COT(PI()/4)";   // Expected result: 1
        worksheet.Cells["G2"].Formula = "=COTH(1)";      // Hyperbolic cotangent of 1
```

**Pourquoi c’est pratique :** Savoir **calculer la cotangente dans Excel** peut vous éviter d’écrire du code mathématique personnalisé, surtout lorsque le classeur sera partagé avec des non‑développeurs.

---

## Étape 5 : Forcer le calcul et récupérer le tableau étendu

Nous demandons maintenant au classeur d’évaluer chaque formule, puis d’extraire le tableau déversé de `A1`. C’est ici que nous **affichons le tableau dans la console**.

```csharp
        // Force calculation of all formulas
        workbook.Calculate();

        // Retrieve the spilled array from A1 as a 2‑D object
        var expanded = worksheet.Cells["A1"].Value;

        // Pretty‑print the 2‑D array to the console
        Console.WriteLine("Expanded array from A1 (4×5):");
        if (expanded is object[,] matrix)
        {
            for (int r = 0; r < matrix.GetLength(0); r++)
            {
                for (int c = 0; c < matrix.GetLength(1); c++)
                {
                    Console.Write($"{matrix[r, c]}\t");
                }
                Console.WriteLine();
            }
        }
        else
        {
            Console.WriteLine("Unexpected data type.");
        }

        // Show the result of the REDUCE lambda
        Console.WriteLine($"\nSum of A1:D4 (via REDUCE lambda): {worksheet.Cells["E1"].Value}");

        // Show cotangent results
        Console.WriteLine($"Cotangent of π/4: {worksheet.Cells["G1"].Value}");
        Console.WriteLine($"Hyperbolic cotangent of 1: {worksheet.Cells["G2"].Value}");
    }
}
```

**Ce que vous verrez :**  
- Une matrice 4 × 5 joliment formatée imprimée ligne par ligne.  
- La somme calculée par le lambda `REDUCE`.  
- Les deux valeurs de cotangente.

Cela complète le flux depuis **écrire une formule dans une cellule** jusqu’à **afficher le tableau dans la console**.

---

## Exemple complet (prêt à copier‑coller)

Ci-dessous se trouve le programme complet que vous pouvez insérer dans une application console. N’oubliez pas d’ajouter d’abord le package NuGet `Aspose.Cells` (`dotnet add package Aspose.Cells`).

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 2: Write EXPAND formula (convert range to array)
        worksheet.Cells["A1"].Formula = "=EXPAND(B1:C2, 4, 5)";

        // Step 3: Use REDUCE with LAMBDA (how to use lambda)
        worksheet.Cells["E1"].Formula = "=REDUCE(0, A1:D4, LAMBDA(acc, x, acc + x))";

        // Step 4: Calculate cotangent values (calculate cotangent in excel)
        worksheet.Cells["G1"].Formula = "=COT(PI()/4)";   // Expected: 1
        worksheet.Cells["G2"].Formula = "=COTH(1)";

        // Step 5: Force calculation
        workbook.Calculate();

        // Step 6: Retrieve and display the expanded array (display array in console)
        var expanded = worksheet.Cells["A1"].Value;
        Console.WriteLine("Expanded array from A1 (4×5):");
        if (expanded is object[,] matrix)
        {
            for (int r = 0; r < matrix.GetLength(0); r++)
            {
                for (int c = 0; c < matrix.GetLength(1); c++)
                {
                    Console.Write($"{matrix[r, c]}\t");
                }
                Console.WriteLine();
            }
        }
        else
        {
            Console.WriteLine("Unexpected data type.");
        }

        // Show REDUCE result
        Console.WriteLine($"\nSum of A1:D4 (via REDUCE lambda): {worksheet.Cells["E1"].Value}");

        // Show cotangent results
        Console.WriteLine($"Cotangent of π/4: {worksheet.Cells["G1"].Value}");
        Console.WriteLine($"Hyperbolic cotangent of 1: {worksheet.Cells["G2"].Value}");
    }
}
```

**Sortie console attendue (les valeurs varieront en fonction du contenu par défaut de B1:C2, qui est 0 par défaut) :**

```
Expanded array from A1 (4×5):
0   0   0   0   0
0   0   0   0   0
0   0   0   0   0
0   0   0   0   0

Sum of A1:D4 (via REDUCE lambda): 0
Cotangent of π/4: 1
Hyperbolic cotangent of 1: 1.31303528549933
```

N’hésitez pas à remplir `B1:C2` avec vos propres nombres avant d’exécuter – la matrice reflétera ces valeurs.

---

## Astuces pro & pièges courants

- **Astuce pro :** Si vous avez besoin que la plage déversée commence ailleurs, il suffit de changer la cellule cible (`A1`). La fonction `EXPAND` respecte l’ancre.
- **Attention à :** Les cellules vides dans la plage source deviennent `0` dans le tableau déversé, ce qui peut affecter la somme `REDUCE`.
- **Cas limite :** Lorsque le classeur contient des formules dépendant de fonctions volatiles (par ex., `NOW()`), appelez `workbook.Calculate()` après avoir défini toutes les formules pour garantir que tout est à jour.
- **Note de performance :** Pour de très grands débordements, envisagez de limiter la taille dans l’appel `EXPAND` ; sinon vous pourriez allouer plus de mémoire que nécessaire.
- **Compatibility:** The `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}