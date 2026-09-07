---
category: general
date: 2026-02-15
description: Comment utiliser WRAPCOLS pour créer une mise en page à deux colonnes,
  ajouter une formule et générer un tableau de séquence dans les feuilles de calcul
  C# – guide étape par étape.
draft: false
keywords:
- how to use wrapcols
- create two column layout
- how to add formula
- how to create columns
- generate sequence array
language: fr
og_description: Comment utiliser WRAPCOLS pour créer une mise en page à deux colonnes,
  ajouter des formules et générer un tableau de séquence dans une feuille de calcul
  C# – guide complet.
og_title: 'Comment utiliser WRAPCOLS : mise en page à deux colonnes en C#'
tags:
- CSharp
- ExcelAutomation
- WorksheetFormula
title: 'Comment utiliser WRAPCOLS : créer une mise en page à deux colonnes en C#'
url: /fr/net/row-and-column-management/how-to-use-wrapcols-create-a-two-column-layout-in-c/
---

lines.

Let's produce final output.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment utiliser WRAPCOLS : créer une mise en page à deux colonnes en C#

Vous vous êtes déjà demandé **comment utiliser WRAPCOLS** lorsque vous avez besoin d’une vue à deux colonnes rapide dans une feuille de calcul de type Excel ? Vous n’êtes pas seul. De nombreux développeurs se heurtent à un mur lorsqu’ils essaient de diviser une liste générée en colonnes nettes sans écrire une boucle pour chaque cellule. La bonne nouvelle ? Avec la fonction `WRAPCOLS` vous pouvez déposer une seule formule dans `A1` et laisser Excel (ou un moteur compatible) faire le travail lourd.

Dans ce tutoriel, nous allons parcourir **comment ajouter une formule** qui crée une **mise en page à deux colonnes**, vous montrer **comment créer des colonnes** dynamiquement, et même **générer des valeurs de tableau séquence** à la volée. À la fin, vous disposerez d’un extrait C# entièrement exécutable que vous pourrez coller dans votre projet, exécuter et voir immédiatement apparaître un bloc à deux colonnes bien ordonné.

## Ce que vous allez apprendre

- Le but de `WRAPCOLS` et pourquoi c’est une meilleure alternative à la boucle manuelle.  
- Comment **ajouter une formule** à une cellule de feuille de calcul en C#.  
- Comment générer un tableau séquence avec `SEQUENCE` et le transmettre à `WRAPCOLS`.  
- Astuces pour recalculer la feuille afin que la formule se résolve immédiatement.  
- Gestion des cas limites (par ex., feuilles vides, nombre de colonnes personnalisé).

Aucune bibliothèque externe au-delà d’un package de traitement Excel standard n’est requise – nous utiliserons **ClosedXML** pour son API simple, mais les concepts s’appliquent également à EPPlus, SpreadsheetGear, ou même Google Sheets via son API.

---

## Prérequis

- .NET 6.0 ou supérieur (le code se compile sur .NET Core et .NET Framework).  
- Une référence à **ClosedXML** (`dotnet add package ClosedXML`).  
- Connaissances de base en C# – vous devez être à l’aise avec les instructions `using` et l’initialisation d’objets.  

Si vous avez déjà un classeur ouvert, vous pouvez ignorer la partie création de fichier et passer directement à la section formule.

---

## Étape 1 : Configurer la feuille de calcul (Comment créer des colonnes)

Tout d’abord, nous avons besoin d’un objet `Worksheet` avec lequel travailler. Dans ClosedXML, vous l’obtenez à partir d’un `XLWorkbook`. L’extrait ci‑dessous crée un nouveau classeur, ajoute une feuille nommée *Demo*, et récupère une référence nommée `worksheet` pour plus de clarté.

```csharp
using ClosedXML.Excel;

namespace WrapColsDemo
{
    class Program
    {
        static void Main()
        {
            // Create a fresh workbook and add a worksheet named "Demo"
            using var workbook = new XLWorkbook();
            var ws = workbook.Worksheets.Add("Demo");

            // Rename for clarity – this is the worksheet we’ll manipulate
            var worksheet = ws;   // <-- same object, just a clearer name

            // --------------------------------------------------------------
            // Next step: write the WRAPCOLS formula
            // --------------------------------------------------------------
```

> **Pourquoi renommer ?**  
> Garder le nom de variable court (`worksheet`) rend le code ultérieur plus lisible, surtout lorsque vous enchaînez plusieurs opérations. Cela reflète également le style de nommage que l’on retrouve dans la plupart de la documentation, réduisant la charge cognitive.

---

## Étape 2 : Écrire la formule (Comment ajouter une formule + générer un tableau séquence)

Voici maintenant la ligne magique. Nous placerons une formule dans la cellule **A1** qui fait deux choses :

1. **Générer un tableau séquence** de six nombres (`SEQUENCE(6)` → 1,2,3,4,5,6).  
2. **Envelopper ces nombres en deux colonnes** (`WRAPCOLS(..., 2)`).

```csharp
            // Write the WRAPCOLS formula into A1
            worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(6), 2)";

            // --------------------------------------------------------------
            // Finally, force the engine to evaluate the formula
            // --------------------------------------------------------------
```

> **Que se passe‑t‑il ?**  
> `SEQUENCE(6)` crée un tableau vertical `{1;2;3;4;5;6}`. `WRAPCOLS` prend alors ce tableau et le « enveloppe » dans le nombre de colonnes spécifié — dans ce cas **2**. Le résultat est un bloc de 3 lignes × 2 colonnes qui ressemble à :

| A | B |
|---|---|
| 1 | 4 |
| 2 | 5 |
| 3 | 6 |

Si vous changez le deuxième argument en **3**, vous obtiendrez une mise en page à trois colonnes. C’est le cœur de **comment créer des colonnes** à la volée sans boucles manuelles.

---

## Étape 3 : Recalculer la feuille (Assurer l’évaluation de la formule)

ClosedXML n’évalue pas automatiquement les formules lorsqu’on les écrit. Vous devez appeler `Calculate()` sur le classeur (ou sur la feuille spécifique) pour forcer l’évaluation.

```csharp
            // Recalculate so the formula is evaluated immediately
            worksheet.Calculate();

            // Optional: save the workbook to inspect the result
            workbook.SaveAs("WrapColsDemo.xlsx");
        }
    }
}
```

> **Astuce pro :** Si vous travaillez avec de gros classeurs, appelez `Calculate()` uniquement sur les feuilles qui ont réellement changé. Cela économise de la mémoire et accélère le traitement.

Lorsque vous ouvrez `WrapColsDemo.xlsx`, vous verrez la mise en page à deux colonnes correctement remplie dans **A1:B3**. Aucun code supplémentaire n’a été nécessaire pour boucler sur les lignes ou les colonnes – `WRAPCOLS` a tout géré.

---

## Étape 4 : Vérifier le résultat (Ce à quoi s’attendre)

Après l’exécution du programme, ouvrez le fichier généré. Vous devriez voir :

| A | B |
|---|---|
| 1 | 4 |
| 2 | 5 |
| 3 | 6 |

Si les nombres apparaissent verticalement (c’est‑à‑dire tous dans la colonne A), revérifiez que vous avez appelé `worksheet.Calculate()` **après** avoir défini la formule. Certains moteurs nécessitent également `workbook.Calculate()` ; l’extrait ci‑dessus fonctionne avec l’évaluateur intégré de ClosedXML.

---

## Variations courantes & cas limites

### Modifier le nombre de colonnes

Pour **créer une mise en page à deux colonnes** avec un nombre de lignes différent, ajustez simplement la taille de `SEQUENCE` ou le deuxième argument de `WRAPCOLS` :

```csharp
worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(12), 3)";
```

Cela produit un bloc de 4 lignes × 3 colonnes (12 nombres répartis sur trois colonnes).

### Utiliser un nombre de colonnes dynamique

Si le nombre de colonnes provient d’une variable, intégrez‑le avec l’interpolation de chaîne :

```csharp
int colCount = 4;
worksheet.Cell("A1").FormulaA1 = $"=WRAPCOLS(SEQUENCE(8), {colCount})";
```

Vous avez maintenant **comment ajouter une formule** qui s’adapte à l’exécution.

### Feuilles vides

Si la feuille est vide, `Calculate()` fonctionne toujours – la formule remplira les cellules à partir de A1. Cependant, si vous supprimez plus tard des lignes/colonnes qui intersectent la plage de sortie, vous pourriez voir des erreurs `#REF!`. Pour éviter cela, videz d’abord la plage cible :

```csharp
worksheet.Range("A1:Z100").Clear(); // wipes any leftovers
```

### Compatibilité

`WRAPCOLS` et `SEQUENCE` font partie des fonctions **Dynamic Array** d’Excel, introduites dans Office 365. Si vous ciblez des versions plus anciennes d’Excel, ces fonctions n’existent pas et vous devrez recourir à une boucle manuelle. L’évaluateur de ClosedXML reproduit le comportement le plus récent d’Excel, il est donc sûr pour les environnements modernes.

---

## Exemple complet (Prêt à copier‑coller)

```csharp
using ClosedXML.Excel;

namespace WrapColsDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create workbook & worksheet
            using var workbook = new XLWorkbook();
            var ws = workbook.Worksheets.Add("Demo");
            var worksheet = ws;   // clearer name

            // 2️⃣ Write WRAPCOLS formula that generates a sequence array
            worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(6), 2)";

            // 3️⃣ Force calculation so the formula resolves immediately
            worksheet.Calculate();

            // 4️⃣ Save the file (optional, but handy for verification)
            workbook.SaveAs("WrapColsDemo.xlsx");
        }
    }
}
```

**Résultat attendu :** L’ouverture de *WrapColsDemo.xlsx* montre une mise en page à deux colonnes bien ordonnée avec les nombres 1‑6 disposés comme décrit précédemment.

---

## Conclusion

Nous avons couvert **comment utiliser WRAPCOLS** pour **créer une mise en page à deux colonnes**, démontré **comment ajouter une formule** programmatique, et vu comment `SEQUENCE` vous permet de **générer des valeurs de tableau séquence** sans boucle. En exploitant les fonctions de tableau dynamique d’Excel depuis C#, vous pouvez garder votre code concis, lisible et maintenable.

Ensuite, vous pourriez explorer :

- **Créer des comptes de lignes dynamiques** avec `ROWS` ou `COUNTA`.  
- **Styler la sortie** (bordures, formats numériques) à l’aide de l’API de style de ClosedXML.  
- **Exporter en CSV** après la construction de la mise en page, pour un traitement en aval.

Essayez, modifiez le nombre de colonnes, et voyez à quel point il est rapide de prototyper des feuilles de calcul complexes. Bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}