---
category: general
date: 2026-10-04
description: Apprenez à créer un classeur Excel en C# et à utiliser EXPAND, à forcer
  le calcul des formules, et à enregistrer le classeur au format XLSX tout en remplissant
  une colonne de nombres.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- how to use expand
- force formula calculation
- save workbook as xlsx
- populate column with numbers
language: fr
lastmod: 2026-10-04
og_description: Créer un classeur Excel en C# avec Aspose.Cells. Ce tutoriel montre
  comment utiliser EXPAND, forcer le calcul des formules et enregistrer le classeur
  au format XLSX tout en remplissant une colonne de nombres.
og_image_alt: Screenshot of a C# program that creates an Excel workbook and applies
  the EXPAND function
og_title: Créer un classeur Excel en C# – guide complet avec EXPAND et sauvegarde
  XLSX
schemas:
- author: Aspose
  dateModified: '2026-10-04'
  description: Learn how to create Excel workbook in C# and use EXPAND, force formula
    calculation, and save workbook as XLSX while populating a column with numbers.
  headline: How to create Excel workbook in C# with the EXPAND function
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- Automation
title: Comment créer un classeur Excel en C# avec la fonction EXPAND
url: /fr/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-in-c-with-the-expand-function/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment créer un classeur Excel en C# avec la fonction EXPAND

Si vous devez **créer un classeur Excel** de façon programmatique, ce guide vous montre une solution complète, prête à l’emploi. Vous verrez comment **remplir une colonne avec des nombres**, appliquer la fonction **EXPAND** pour déverser les données horizontalement, **forcer le calcul des formules**, et enfin **enregistrer le classeur au format XLSX**.  

Ce tutoriel couvre chaque étape nécessaire, depuis l’initialisation du classeur jusqu’à la vérification du résultat. Aucun document externe n’est requis — copiez simplement le code, exécutez‑le, et vous obtiendrez un fichier Excel pleinement fonctionnel.

## Prérequis

- .NET 6.0 ou supérieur (le code fonctionne également avec .NET Framework 4.6+)
- Package NuGet Aspose.Cells for .NET (`Install-Package Aspose.Cells`)
- Familiarité de base avec la syntaxe C#
- Un IDE tel que Visual Studio ou VS Code

## Étape 1 : Créer le classeur Excel et accéder à la première feuille

La première action consiste à **créer un classeur Excel** et à obtenir une référence à sa feuille par défaut. Aspose.Cells ajoute automatiquement une feuille à l’index 0, vous pouvez donc travailler avec immédiatement.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();          // create Excel workbook
        Worksheet sheet = workbook.Worksheets[0];   // first (default) worksheet
```

*Pourquoi c’est important :* L’instanciation de `Workbook` alloue la structure interne du fichier, et la récupération de `Worksheets[0]` vous fournit un objet `Worksheet` concret pour manipuler les lignes, colonnes et cellules.

## Étape 2 : Remplir une colonne avec des nombres

Ensuite, remplissez une liste verticale dans la colonne A. Cela montre comment **remplir une colonne avec des nombres** et fournit la plage source pour la fonction EXPAND.

```csharp
        // Step 2: Fill a vertical list of values in column A
        sheet.Cells["A1"].PutValue(1);
        sheet.Cells["A2"].PutValue(2);
        sheet.Cells["A3"].PutValue(3);
```

*Astuce :* Utilisez `PutValue` pour les nombres bruts, chaînes, dates ou tout primitive .NET. La méthode détermine automatiquement le type de cellule.

## Étape 3 : Comment utiliser EXPAND – déverser la liste horizontalement

La partie **comment utiliser expand** est le cœur de ce tutoriel. La fonction `EXPAND` développe une plage source dans une nouvelle forme. Ici nous développons la plage verticale `A1:A3` en une seule ligne qui s’étend sur trois colonnes, à partir de `B1`.

```csharp
        // Step 3: Apply the EXPAND function to spill the list horizontally starting at B1
        // The formula expands the range A1:A3 into 1 row and 3 columns (B1:D1)
        sheet.Cells["B1"].Formula = "=EXPAND(A1:A3, 1, 3)";
```

*Explication :*  
- Le premier argument (`A1:A3`) est la plage source.  
- Le deuxième argument (`1`) force le résultat à avoir **1** ligne.  
- Le troisième argument (`3`) force le résultat à avoir **3** colonnes.  

Lorsque le classeur se recalculera, les cellules `B1`, `C1` et `D1` contiendront respectivement `1`, `2` et `3`.

## Étape 4 : Forcer le calcul des formules

Aspose.Cells n’évalue pas automatiquement les formules après les avoir définies, vous devez donc **forcer le calcul des formules** avant l’enregistrement. Cela garantit que le résultat d’EXPAND est matérialisé dans le fichier.

```csharp
        // Step 4: Force calculation of all formulas in the workbook
        workbook.CalculateFormula();   // triggers calculation engine
```

*Pourquoi c’est nécessaire :* Sans appeler `CalculateFormula`, le fichier enregistré contiendrait la chaîne de formule brute, et Excel ne recalculerait que lors de l’ouverture du fichier. Pour les pipelines automatisés, on veut généralement que les valeurs soient écrites immédiatement.

## Étape 5 : Enregistrer le classeur au format XLSX

Maintenant que le classeur est entièrement préparé, **enregistrez le classeur au format XLSX** à l’emplacement de votre choix. L’extension du fichier détermine le format de sortie ; `.xlsx` crée un classeur Office Open XML.

```csharp
        // Step 5: Save the workbook to a file
        string outputPath = @"C:\Temp\ExpandFunction.xlsx";
        workbook.Save(outputPath);   // save workbook as XLSX
        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

*Conseil :* Si vous avez besoin d’un autre format (CSV, PDF, etc.), changez simplement l’extension du fichier ou utilisez `workbook.Save(outputPath, SaveFormat.Xls)` pour les versions Excel plus anciennes.

## Exemple complet, exécutable

Assembler toutes les pièces vous donne un programme autonome qui **crée un classeur Excel**, remplit une colonne, utilise **EXPAND**, force le calcul, et **enregistre le classeur au format XLSX**.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1. Create Excel workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 2. Populate column with numbers
        sheet.Cells["A1"].PutValue(1);
        sheet.Cells["A2"].PutValue(2);
        sheet.Cells["A3"].PutValue(3);

        // 3. How to use EXPAND – spill horizontally
        sheet.Cells["B1"].Formula = "=EXPAND(A1:A3, 1, 3)";

        // 4. Force formula calculation
        workbook.CalculateFormula();

        // 5. Save workbook as XLSX
        string path = @"C:\Temp\ExpandFunction.xlsx";
        workbook.Save(path);
        System.Console.WriteLine($"Workbook saved to {path}");
    }
}
```

### Résultat attendu

Après l’exécution du programme, ouvrez `ExpandFunction.xlsx` dans Excel. Vous devriez voir :

| A | B | C | D |
|---|---|---|---|
| 1 | 1 | 2 | 3 |
| 2 |   |   |   |
| 3 |   |   |   |

Les valeurs `1`, `2`, `3` dans les cellules `B1:D1` confirment que la fonction **EXPAND** a fonctionné et que l’étape **forcer le calcul des formules** a correctement matérialisé les résultats.

## Variations courantes et cas limites

| Scénario | Ajustement |
|----------|------------|
| **Plage source dynamique** | Utilisez `=EXPAND(A1:INDEX(A:A, COUNTA(A:A)), 1, 0)` pour développer autant de lignes que nécessaire. |
| **Dimensions de sortie différentes** | Modifiez les deuxième et troisième arguments de `EXPAND` pour contrôler les lignes et colonnes. |
| **Multiples feuilles** | Parcourez `workbook.Worksheets` et appliquez la même logique à chaque feuille. |
| **Jeux de données volumineux** | Appelez `workbook.CalculateFormula()` une seule fois après avoir défini toutes les formules afin d’éviter des recalculs répétés. |
| **Enregistrement dans un flux mémoire** | Remplacez `workbook.Save(path)` par `workbook.Save(stream, SaveFormat.Xlsx)` lorsque vous avez besoin du fichier dans la réponse d’une API web. |

## Liste de vérification de dépannage

- **Formule qui ne se développe pas :** Vérifiez que `CalculateFormula()` est appelé *après* la définition de la formule.  
- **Fichier introuvable lors de l’enregistrement :** Assurez‑vous que le répertoire cible existe et que le processus possède les droits d’écriture.  
- **Type de données incorrect :** Utilisez `PutValue` pour les nombres ; pour les dates, utilisez `PutValue(DateTime.Now)` ou `PutDateTime`.  
- **Incompatibilité de version :** La fonction EXPAND nécessite un moteur de calcul compatible Excel 365 ; Aspose.Cells 23.9+ la prend en charge.

## Conclusion

Vous savez maintenant comment **créer un classeur Excel** en C#, **remplir une colonne avec des nombres**, appliquer la fonction **EXPAND**, **forcer le calcul des formules**, et **enregistrer le classeur au format XLSX**. Cet exemple de bout en bout peut être adapté pour des rapports, des transformations de données ou tout scénario d’automatisation nécessitant une sortie Excel dynamique.

### Prochaines étapes

- Explorez d’autres fonctions de tableau dynamique telles que `FILTER`, `SORT` et `UNIQUE`.  
- Intégrez la génération du classeur dans une API ASP.NET Core pour délivrer des fichiers Excel à la demande.  
- Remplacez les nombres codés en dur par des données lues depuis une base de données ou un fichier CSV pour des rapports réels.

N’hésitez pas à expérimenter avec différentes plages, noms de feuilles et formats de sortie. Bon codage !


## Que devriez‑vous apprendre ensuite ?


Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets et fonctionnels avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités de l’API et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [How to Calculate Cotangent in Excel with C# – Create Workbook, Use EXPAND,](/cells/english/net/formulas-functions/how-to-calculate-cotangent-in-excel-with-c-create-workbook-u/)
- [How to Use WRAPCOLS in C# – Create Excel Workbook with Wrap Functions](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}