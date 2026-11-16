---
category: general
date: 2026-11-16
description: Comment copier un tableau croisé dynamique d’un fichier Excel vers un
  nouveau classeur en utilisant C#. Apprenez à charger le classeur, copier la plage
  et préserver les tableaux croisés dynamiques.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy range to new workbook
- load excel workbook c#
- Aspose.Cells copy pivot
- preserve pivot table C#
- Excel automation C#
language: fr
lastmod: 2026-11-16
og_description: Comment copier un tableau croisé dynamique d’un classeur existant
  vers un nouveau classeur en utilisant C#. Suivez ce guide complet pour charger le
  classeur Excel, copier la plage et conserver le tableau croisé dynamique intact.
og_image_alt: how to copy pivot table example in C#
og_title: Comment copier un tableau croisé dynamique dans un nouveau classeur en C#
  – guide étape par étape
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: How to copy pivot table from one Excel file to a new workbook using
    C#. Learn to load workbook, copy range, and preserve pivot tables.
  headline: How to copy a pivot table to a new workbook in C#
  type: TechArticle
- description: How to copy pivot table from one Excel file to a new workbook using
    C#. Learn to load workbook, copy range, and preserve pivot tables.
  name: How to copy a pivot table to a new workbook in C#
  steps:
  - name: Expected output
    text: 'Running the program produces `CopyWithPivot.xlsx`. Opening the file in
      Excel shows:'
  - name: Copying multiple pivot tables
    text: If your source sheet contains several pivots, expand the `CellArea` to cover
      the union of all ranges, or repeat the copy step for each distinct area.
  - name: Preserving styles and conditional formatting
    text: '`CopyRows` copies cell styles automatically. If you need to preserve workbook‑wide
      named styles or custom number formats, call `destWorkbook.Worksheets[0].CopyStyle`
      before saving.'
  - name: Working with large workbooks
    text: For files larger than 100 MB, consider using `Workbook.LoadOptions` with
      the `MemorySetting` set to `MemorySetting.MemoryPreference` to reduce memory
      pressure.
  - name: Next steps
    text: '* Explore **Aspose.Cells** features such as refreshing pivots programmatically.
      * Combine this approach with **ExcelPackage** (EPPlus) if you need an open‑source
      alternative. * Automate copying across multiple sheets by looping through `srcWorkbook.Worksheets`.'
  type: HowTo
- questions:
  - answer: Aspose.Cells can read macro‑enabled files (`.xlsm`), but the macro code
      isn’t copied. The pivot table itself is preserved because it’s part of the worksheet
      XML.
    question: Does this work with macros or VBA‑enabled workbooks?
  - answer: The copy operation includes the cached data only. If the destination workbook
      needs to refresh from the original source, you’ll have to re‑configure the data
      connection manually.
    question: What if the pivot uses an external data source?
  - answer: 'No. A pivot table needs its cache. The most reliable way is to copy the
      rows that contain the cache, as demonstrated. You can later hide those rows
      if you don’t want them visible. ## Conclusion You now know **how to copy pivot
      table** from one Excel file to another using C#. The tutorial covered **l'
    question: Can I copy the pivot without the underlying data rows?
  type: FAQPage
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: Comment copier un tableau croisé dynamique dans un nouveau classeur en C#
url: /fr/net/pivot-tables/how-to-copy-a-pivot-table-to-a-new-workbook-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment copier un tableau croisé dynamique vers un nouveau classeur en C#

Si vous avez besoin de **how to copy pivot table** d'un fichier Excel vers un nouveau classeur, ce guide vous montre les étapes exactes. Vous apprendrez comment **load excel workbook c#**, définir la plage source, et **copy range to new workbook** tout en conservant le tableau croisé dynamique intact.

Copier un tableau croisé dynamique est une exigence courante lorsque vous souhaitez réutiliser un modèle de rapport, migrer des données entre projets, ou générer un fichier léger pour la distribution. L'exemple de code ci‑dessous utilise Aspose.Cells, une bibliothèque .NET entièrement gérée qui fonctionne sans Microsoft Office installé. À la fin de ce tutoriel, vous disposerez d'un programme exécutable qui crée un nouveau classeur contenant le tableau croisé dynamique original, prêt pour un traitement supplémentaire ou un partage.

## Prérequis

* .NET 6.0 SDK ou version ultérieure (l'exemple fonctionne avec .NET Core et .NET Framework)
* Visual Studio 2022 ou tout éditeur C# de votre choix
* Une licence Aspose.Cells pour .NET (l'essai gratuit fonctionne pour l'évaluation)
* Un fichier Excel source (`Source.xlsx`) contenant au moins un tableau croisé dynamique

> **Astuce :** Si vous utilisez l'essai gratuit, définissez la licence dans le code pour éviter les filigranes d'évaluation.

## Étape 1 : Charger le classeur source (load excel workbook c#)

La première action consiste à ouvrir le classeur qui contient le tableau croisé dynamique. Aspose.Cells lit le fichier en mémoire, vous donnant un accès complet aux feuilles de calcul, aux cellules et aux objets de tableau croisé dynamique.

```csharp
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // Load the source workbook that contains the pivot table
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY\Source.xlsx");
```

*Pourquoi c’est important* : Charger le classeur est la base de toute automatisation Excel. Sans un objet `Workbook` valide, vous ne pouvez pas inspecter le tableau croisé dynamique ni copier ses données.

## Étape 2 : Définir la zone de cellules qui englobe le tableau croisé dynamique (copy range to new workbook)

Un tableau croisé dynamique se trouve à l'intérieur d'un bloc rectangulaire de cellules. Vous devez spécifier ce bloc afin que l'opération de copie sache quoi déplacer. Le constructeur `CellArea` utilise des index à base zéro : `StartRow, StartColumn, EndRow, EndColumn`.

```csharp
        // Define the cell range that encloses the pivot table, e.g., A1:K21
        // Row and column indexes start at 0, so A1 = (0,0)
        CellArea sourceRange = new CellArea(0, 0, 20, 10); // A1:K21
```

*Pourquoi c’est important* : En définissant explicitement la plage, vous évitez de copier des données non liées et vous vous assurez que le cache du tableau croisé dynamique est inclus. La plage peut être calculée dynamiquement si vous devez gérer des tailles de tableau variables.

## Étape 3 : Créer un nouveau classeur et obtenir sa première feuille de calcul

Créez maintenant le classeur de destination qui recevra les lignes copiées. Aspose.Cells ajoute automatiquement une feuille de calcul par défaut, que nous utiliserons comme cible.

```csharp
        // Create a new workbook that will receive the copied range
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];
```

*Pourquoi c’est important* : Commencer avec un classeur vierge garantit que seul le tableau croisé dynamique (et ses lignes de support) se retrouvent dans le fichier, ce qui maintient la sortie légère.

## Étape 4 : Copier les lignes de la plage source vers la feuille de destination (how to copy pivot table)

La méthode `CopyRows` copie des lignes entières, en préservant les formules, le formatage et—crucialement—les tableaux croisés dynamiques. Les paramètres de la méthode sont : ligne de début, ligne de fin, collection de cellules cibles, et l'index de ligne dans la cible où la copie commence (ici `0` pour commencer à la première ligne).

```csharp
        // Copy the rows that contain the pivot table.
        // Pivot tables inside the range are preserved automatically.
        destWorksheet.Cells.CopyRows(
            sourceRange.StartRow,
            sourceRange.EndRow,
            destWorksheet.Cells,
            0);
```

*Pourquoi c’est important* : Utiliser `CopyRows` au lieu de copier des cellules individuelles garantit que le cache du tableau reste lié aux données copiées. Aspose.Cells gère les structures XML sous‑jacentes, vous n’avez donc pas besoin de reconstruire le tableau manuellement.

## Étape 5 : Enregistrer le classeur résultant (copy range to new workbook)

Enfin, écrivez le nouveau fichier sur le disque. Le classeur de destination contient maintenant un tableau croisé dynamique identique qui fonctionne indépendamment du fichier source.

```csharp
        // Save the new workbook with the copied pivot table
        destWorkbook.Save(@"YOUR_DIRECTORY\CopyWithPivot.xlsx");

        // Optional: inform the user
        System.Console.WriteLine("Pivot table copied successfully!");
    }
}
```

### Résultat attendu

L'exécution du programme produit `CopyWithPivot.xlsx`. L'ouverture du fichier dans Excel montre :

* La même mise en page du tableau croisé dynamique que dans `Source.xlsx`
* Toutes les lignes de données source qui faisaient partie du cache du tableau
* Aucune référence au classeur original (le tableau fonctionne hors ligne)

## Gestion des variations courantes

### Copier plusieurs tableaux croisés dynamiques

Si votre feuille source contient plusieurs tableaux, élargissez le `CellArea` pour couvrir l'union de toutes les plages, ou répétez l'étape de copie pour chaque zone distincte.

```csharp
// Example: copy two separate ranges
CellArea firstPivot = new CellArea(0, 0, 20, 10);
CellArea secondPivot = new CellArea(25, 0, 45, 10);

destWorksheet.Cells.CopyRows(firstPivot.StartRow, firstPivot.EndRow, destWorksheet.Cells, 0);
destWorksheet.Cells.CopyRows(secondPivot.StartRow, secondPivot.EndRow, destWorksheet.Cells, 21); // start after first block
```

### Conserver les styles et le formatage conditionnel

`CopyRows` copie automatiquement les styles de cellules. Si vous devez conserver les styles nommés à l'échelle du classeur ou les formats numériques personnalisés, appelez `destWorkbook.Worksheets[0].CopyStyle` avant d'enregistrer.

### Travailler avec de gros classeurs

Pour des fichiers supérieurs à 100 Mo, envisagez d'utiliser `Workbook.LoadOptions` avec le `MemorySetting` défini sur `MemorySetting.MemoryPreference` afin de réduire la pression mémoire.

```csharp
LoadOptions loadOptions = new LoadOptions(LoadFormat.Xlsx)
{
    MemorySetting = MemorySetting.MemoryPreference
};
Workbook largeSrc = new Workbook(@"bigfile.xlsx", loadOptions);
```

## Code source complet (prêt à l'exécution)

Ci‑dessous se trouve le programme complet, incluant les directives `using` et les commentaires. Copiez‑le dans un nouveau projet console et remplacez `YOUR_DIRECTORY` par le chemin réel du dossier.

```csharp
using System;
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the source workbook (load excel workbook c#)
        // -------------------------------------------------
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY\Source.xlsx");

        // -------------------------------------------------
        // Step 2: Define the area that contains the pivot table
        // -------------------------------------------------
        // Adjust the indices if your pivot occupies a different range.
        CellArea sourceRange = new CellArea(0, 0, 20, 10); // A1:K21

        // -------------------------------------------------
        // Step 3: Create the destination workbook
        // -------------------------------------------------
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];

        // -------------------------------------------------
        // Step 4: Copy rows (how to copy pivot table)
        // -------------------------------------------------
        destWorksheet.Cells.CopyRows(
            sourceRange.StartRow,
            sourceRange.EndRow,
            destWorksheet.Cells,
            0);

        // -------------------------------------------------
        // Step 5: Save the new file (copy range to new workbook)
        // -------------------------------------------------
        destWorkbook.Save(@"YOUR_DIRECTORY\CopyWithPivot.xlsx");

        Console.WriteLine("Pivot table copied successfully!");
    }
}
```

Exécutez le programme (`dotnet run` ou `Ctrl+F5` dans Visual Studio). Après l'exécution, ouvrez `CopyWithPivot.xlsx` pour vérifier que le tableau croisé dynamique se comporte exactement comme l'original.

## Questions fréquentes

**Q : Cette méthode fonctionne‑t‑elle avec des classeurs contenant des macros ou activés VBA ?**  
R : Aspose.Cells peut lire les fichiers activés macro (`.xlsm`), mais le code macro n’est pas copié. Le tableau croisé dynamique lui‑même est conservé car il fait partie du XML de la feuille de calcul.

**Q : Et si le tableau utilise une source de données externe ?**  
R : L'opération de copie n'inclut que les données mises en cache. Si le classeur de destination doit se rafraîchir à partir de la source originale, vous devrez reconfigurer manuellement la connexion de données.

**Q : Puis‑je copier le tableau sans les lignes de données sous‑jacentes ?**  
R : Non. Un tableau croisé dynamique a besoin de son cache. La façon la plus fiable est de copier les lignes contenant le cache, comme démontré. Vous pouvez ensuite masquer ces lignes si vous ne souhaitez pas qu'elles soient visibles.

## Conclusion

Vous savez maintenant **how to copy pivot table** d'un fichier Excel à un autre en utilisant C#. Le tutoriel a couvert **load excel workbook c#**, a défini le **copy range to new workbook**, et a utilisé la méthode `CopyRows` d’Aspose.Cells pour conserver le tableau croisé dynamique intact. Avec l'exemple complet et exécutable, vous pouvez intégrer ce modèle dans des pipelines de reporting, des outils d'exportation automatisés, ou tout scénario où un tableau doit être transféré entre classeurs.

### Prochaines étapes

* Explorez les fonctionnalités d’**Aspose.Cells** telles que le rafraîchissement des tableaux croisés dynamiques par programmation.  
* Combinez cette approche avec **ExcelPackage** (EPPlus) si vous avez besoin d’une alternative open‑source.  
* Automatisez la copie sur plusieurs feuilles en parcourant `srcWorkbook.Worksheets`.  

N’hésitez pas à expérimenter avec différentes plages, ajouter du style personnalisé, ou intégrer la logique dans un service de traitement de données plus vaste. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code fonctionnels complets avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités d’API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Create New Workbook in C# – Copy Pivot Table](/cells/english/net/pivot-tables/create-new-workbook-in-c-copy-pivot-table/)
- [How to copy pivot table in Excel with C# and Aspose.Cells](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-excel-with-c-and-aspose-cells/)
- [Copy pivot table to new workbook, export shape to PowerPoint](/cells/english/net/pivot-tables/copy-pivot-table-to-new-workbook-export-shape-to-powerpoint/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}