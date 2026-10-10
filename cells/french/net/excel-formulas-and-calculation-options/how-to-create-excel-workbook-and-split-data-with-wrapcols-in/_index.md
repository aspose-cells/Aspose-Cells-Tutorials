---
category: general
date: 2026-10-10
description: Créer un classeur Excel en C# et utiliser la fonction WRAPCOLS pour répartir
  les données d’un tableau en colonnes. Suivez un guide complet étape par étape avec
  du code exécutable.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- excel formula split data
- use wrapcols function
- how to use wrapcols
- split array columns
language: fr
lastmod: 2026-10-10
og_description: Créez un classeur Excel en C# et appliquez la fonction WRAPCOLS pour
  répartir les données d’un tableau en colonnes. Ce guide présente le code complet
  et explique chaque étape.
og_image_alt: Screenshot of an Excel sheet showing three columns filled by the WRAPCOLS
  formula
og_title: Créer un classeur Excel et séparer les données avec WRAPCOLS en C#
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Create Excel workbook in C# and use the WRAPCOLS function to split
    array data into columns. Follow a complete step‑by‑step guide with runnable code.
  headline: How to create Excel workbook and split data with WRAPCOLS in C#
  type: TechArticle
- description: Create Excel workbook in C# and use the WRAPCOLS function to split
    array data into columns. Follow a complete step‑by‑step guide with runnable code.
  name: How to create Excel workbook and split data with WRAPCOLS in C#
  steps:
  - name: Using the function with different data types
    text: 'The `WRAPCOLS` function is not limited to numbers. You can split text values,
      dates, or mixed types:'
  - name: Variable column count at runtime
    text: 'Often the number of columns you need depends on user input. You can build
      the formula string dynamically:'
  - name: Large arrays and performance
    text: '`WRAPCOLS` can handle thousands of elements, but evaluating extremely large
      arrays in a single cell may increase calculation time. If you notice slowdown:'
  - name: Handling empty cells
    text: If the source array contains empty strings (`""`) or `NULL` values, `WRAPCOLS`
      inserts blank cells, preserving the column layout. This behavior is useful when
      you need placeholder columns for later data entry.
  - name: Using named ranges instead of literals
    text: 'For maintainability, define a named range that holds the source data, then
      reference it:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Comment créer un classeur Excel et diviser les données avec WRAPCOLS en C#
url: /fr/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-and-split-data-with-wrapcols-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment créer un classeur Excel et scinder des données avec WRAPCOLS en C#

Si vous devez **créer un classeur Excel** de façon programmatique, ce guide vous montre exactement comment le faire et comment **scinder les données d’un tableau** sur plusieurs colonnes à l’aide de la fonction `WRAPCOLS`. Vous obtiendrez un exemple complet et exécutable qui génère un fichier `.xlsx` avec les données réparties sur trois colonnes.

Le tutoriel couvre tout ce dont vous avez besoin : les packages NuGet requis, chaque ligne de code, le fonctionnement de la formule `WRAPCOLS`, et comment adapter la solution à différentes tailles de tableau ou nombres de colonnes. À la fin, vous pourrez intégrer la technique **use wrapcols function** dans n’importe quel projet C# qui génère des fichiers Excel.

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

* .NET 6.0 SDK ou une version ultérieure installée  
* Un IDE C# (Visual Studio, VS Code, Rider, etc.)  
* Le package NuGet **Aspose.Cells for .NET** – la bibliothèque qui fournit la classe `Workbook` utilisée dans les exemples  

Vous n’avez pas besoin d’une installation d’Office ; Aspose.Cells écrit le fichier `.xlsx` directement.

## Étape 1 – créer un classeur Excel

La première tâche consiste à instancier un nouvel objet classeur et à obtenir une référence à la première feuille de calcul. Cette étape constitue la base de toute manipulation ultérieure.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();                // creates an empty Excel file in memory
        Worksheet ws = wb.Worksheets[0];             // the default worksheet is at index 0
```

`Workbook` représente le fichier complet, tandis que `Worksheet` représente une feuille unique. En créant le classeur en mémoire, vous évitez les accès disque jusqu’à ce que vous l’enregistriez explicitement.

## Étape 2 – appliquer WRAPCOLS pour scinder les colonnes d’un tableau

Vous allez maintenant placer une formule dans la cellule **A1** qui utilise `WRAPCOLS`. La fonction reçoit deux arguments : le tableau source et le nombre de colonnes dans lesquelles vous souhaitez que le tableau soit réparti.

```csharp
        // Step 2: Apply the WRAPCOLS formula to split the array into 3 columns
        // The array {1,2,3,4,5,6} will be distributed as:
        // 1 2 3
        // 4 5 6
        ws.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";
```

**Pourquoi cela fonctionne :** `WRAPCOLS` prend le tableau plat `{1,2,3,4,5,6}` et le remplit ligne par ligne, créant trois colonnes par ligne. Le premier argument peut être n’importe quel littéral de tableau Excel, une plage nommée ou une formule de tableau dynamique. Le second argument (`3`) indique à Excel combien de colonnes générer avant de passer à la ligne suivante.

### Utilisation de la fonction avec différents types de données

La fonction `WRAPCOLS` n’est pas limitée aux nombres. Vous pouvez scinder des valeurs texte, des dates ou des types mixtes :

```csharp
        // Example with mixed data: strings and numbers
        ws.Cells[2, 0].Formula = "=WRAPCOLS({\"Jan\",\"Feb\",\"Mar\",100,200,300},3)";
```

Lorsque le tableau source contient des chaînes, Excel traite automatiquement le résultat comme des cellules texte. Cette flexibilité vous permet de **excel formula split data** pour le reporting, les tableaux de bord ou les tâches de migration de données.

## Étape 3 – calculer les formules pour que la feuille soit remplie

Les formules sont stockées sous forme de chaînes jusqu’à ce que vous demandiez au classeur de les évaluer. L’appel à `CalculateFormula` force l’évaluation et écrit les résultats dans les cellules.

```csharp
        // Step 3: Calculate formulas so the worksheet is populated
        wb.CalculateFormula();   // evaluates all formulas in the workbook
```

Sans cet appel, le fichier enregistré ne contiendrait que le texte de la formule, pas les valeurs calculées. La méthode s’applique à l’ensemble du classeur, de sorte que vous pouvez placer d’autres formules ailleurs et elles seront toutes résolues en un seul appel.

## Étape 4 – enregistrer le classeur pour voir le résultat

Enfin, écrivez le classeur sur le disque. Choisissez un dossier où vous avez les droits d’écriture et donnez un nom clair au fichier.

```csharp
        // Step 4: Save the workbook to see the result
        string outputPath = @"output.xlsx";
        wb.Save(outputPath);      // creates output.xlsx in the application directory
    }
}
```

Lorsque vous ouvrez `output.xlsx` dans Excel (ou tout visualiseur compatible), vous verrez :

| A | B | C |
|---|---|---|
| 1 | 2 | 3 |
| 4 | 5 | 6 |

Si vous avez utilisé l’exemple à types mixtes, les lignes 3‑4 contiendraient le texte et les nombres en conséquence.

## Variantes avancées et gestion des cas limites

### Nombre de colonnes variable à l'exécution

Souvent, le nombre de colonnes dont vous avez besoin dépend d’une entrée utilisateur. Vous pouvez construire la chaîne de formule dynamiquement :

```csharp
int columns = 4; // could come from UI, config, etc.
string arrayLiteral = "{10,20,30,40,50,60,70,80}";
ws.Cells[5, 0].Formula = $"=WRAPCOLS({arrayLiteral},{columns})";
```

### Grands tableaux et performances

`WRAPCOLS` peut gérer des milliers d’éléments, mais l’évaluation de tableaux extrêmement grands dans une seule cellule peut augmenter le temps de calcul. Si vous constatez un ralentissement :

* Divisez le tableau source en morceaux plus petits et écrivez chaque morceau dans une cellule de départ distincte.  
* Utilisez `WorkbookSettings` pour activer le calcul multithread :

```csharp
wb.Settings.CalcMode = CalculationModeType.Automatic;
wb.Settings.EnableMultiThreadedCalc = true;
```

### Gestion des cellules vides

Si le tableau source contient des chaînes vides (`""`) ou des valeurs `NULL`, `WRAPCOLS` insère des cellules vides, préservant la disposition des colonnes. Ce comportement est utile lorsque vous avez besoin de colonnes factices pour une saisie de données ultérieure.

### Utilisation de plages nommées au lieu de littéraux

Pour plus de maintenabilité, définissez une plage nommée qui contient les données sources, puis référez‑vous à celle‑ci :

```csharp
ws.Cells["D1:D6"].PutValue(new object[] { 11, 12, 13, 14, 15, 16 });
ws.Cells["E1"].Formula = "=WRAPCOLS(D1:D6,3)";
```

La formule lit désormais les données directement depuis la feuille de calcul, permettant **how to use wrapcols** dans des scénarios de reporting dynamique.

## Pièges courants et astuces professionnelles

* **Ne pas omettre le deuxième argument.** `WRAPCOLS(array)` sans nombre de colonnes renvoie une seule colonne, ce qui annule l’objectif de scission des données.  
* **Éviter de mélanger les dimensions du tableau.** Le tableau source doit être unidimensionnel ; fournir un tableau à deux dimensions (par ex., `{ {1,2},{3,4} }`) déclenche une erreur `#VALUE!`.  
* **Enregistrer après le calcul.** Si vous appelez `wb.Save` avant `CalculateFormula`, le fichier ne contiendra que le texte de la formule.  
* **Vérifier les permissions de fichier.** Lors de l’exécution dans des environnements restreints (par ex., ASP.NET), assurez‑vous que l’identité du processus peut écrire dans le dossier cible.  

## Exemple complet fonctionnel

Voici le programme complet que vous pouvez copier, coller et exécuter. Il comprend tous les imports, la gestion des erreurs et les commentaires.

```csharp
using System;
using Aspose.Cells;

class ExcelWrapColsDemo
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Split a numeric array into 3 columns
        ws.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";

        // Split a mixed array (text + numbers) into 3 columns, starting at row 3
        ws.Cells[2, 0].Formula = "=WRAPCOLS({\"Jan\",\"Feb\",\"Mar\",100,200,300},3)";

        // Dynamically build a formula with a variable column count
        int columnCount = 4;
        string sourceArray = "{10,20,30,40,50,60,70,80}";
        ws.Cells[5, 0].Formula = $"=WRAPCOLS({sourceArray},{columnCount})";

        // Evaluate all formulas
        wb.CalculateFormula();

        // Save the workbook
        string outputPath = "output.xlsx";
        wb.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

L’exécution du programme produit `output.xlsx` avec trois zones distinctes démontrant **excel formula split data** à l’aide de la fonction `WRAPCOLS`.

## Conclusion

Vous savez maintenant comment **créer des fichiers classeur Excel** en C# et comment **utiliser la fonction wrapcols** pour **scinder les colonnes d’un tableau** de façon efficace. Les étapes principales — instanciation de `Workbook`, insertion de la formule `WRAPCOLS`, calcul et enregistrement — forment un modèle réutilisable pour toute tâche d’automatisation nécessitant la distribution de données sur plusieurs colonnes.

À partir d’ici, vous pouvez :

* Combiner `WRAPCOLS` avec d’autres fonctions de tableau dynamique comme `FILTER` ou `SORT`.  
* Exporter de grands ensembles de données depuis des bases de données et laisser Excel gérer automatiquement la mise en page.  
* Construire des rapports pilotés par l’utilisateur où le nombre de colonnes est sélectionné via un contrôle d’interface.

Expérimentez avec différentes sources de tableau, différents nombres de colonnes et des formules additionnelles pour enrichir cette base. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques présentées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités de l’API et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [How to Use WRAPCOLS in C# – Create Excel Workbook with Wrap Functions](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [Create Excel Workbook – Convert Array to Matrix with WRAPCOLS](/cells/english/net/calculation-engine/create-excel-workbook-convert-array-to-matrix-with-wrapcols/)
- [Create Excel Workbook C# – Step‑by‑Step Guide](/cells/english/net/excel-workbook/create-excel-workbook-c-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}