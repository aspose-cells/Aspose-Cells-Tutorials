---
category: general
date: 2026-09-15
description: Apprenez comment copier un tableau croisé dynamique, copier une feuille
  de calcul avec un tableau croisé dynamique et enregistrer le classeur au format pptx
  en utilisant Aspose.Cells en C#. Guide complet étape par étape.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy worksheet with pivot
- save workbook as pptx
language: fr
lastmod: 2026-09-15
og_description: Comment copier un tableau croisé dynamique, copier une feuille de
  calcul contenant un tableau croisé dynamique et enregistrer le classeur au format pptx
  à l’aide d’Aspose.Cells. Suivez les exemples C# complets et exécutables.
og_image_alt: Screenshot showing how to copy pivot table in a C# code editor
og_title: Comment copier un tableau croisé dynamique et exporter des feuilles de calcul
  – guide complet C#
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to copy pivot table, copy worksheet with pivot, and save
    workbook as pptx using Aspose.Cells in C#. Complete step‑by‑step guide.
  headline: How to copy pivot table while preserving worksheets
  type: TechArticle
- description: Learn how to copy pivot table, copy worksheet with pivot, and save
    workbook as pptx using Aspose.Cells in C#. Complete step‑by‑step guide.
  name: How to copy pivot table while preserving worksheets
  steps:
  - name: – Load the source workbook that holds the pivot table
    text: '```csharp // Load the workbook that contains the pivot table you want to
      copy Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx"); ```'
  - name: – Create an empty destination workbook
    text: '```csharp // Create a new, empty workbook that will receive the copied
      data Workbook destinationWorkbook = new Workbook(); ```'
  - name: – Copy the rows that include the pivot table
    text: '```csharp // Copy rows 0‑19 (A1:G20) from the first worksheet of the source
      sourceWorkbook.Worksheets[0].Cells.CopyRows(0, 0, 20); ```'
  - name: – Copy the columns that contain the pivot table
    text: '```csharp // Copy columns 0‑6 (A‑G) from the same worksheet sourceWorkbook.Worksheets[0].Cells.CopyColumns(0,
      0, 7); ```'
  - name: – Transfer the prepared sheet into the destination workbook
    text: '```csharp // Move the fully prepared worksheet into the destination workbook
      sourceWorkbook.Worksheets[0].Copy(destinationWorkbook.Worksheets[0]); ```'
  - name: – Save the result – the pivot table remains intact
    text: '```csharp // Save the destination workbook; the pivot table works exactly
      like the original destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
      ```'
  - name: – Load the workbook that includes the textbox
    text: '```csharp // Load the Excel file that contains an editable textbox shape
      Workbook workbookWithTextbox = new Workbook("YOUR_DIRECTORY/DocWithTextbox.xlsx");
      ```'
  - name: – Configure PPTX save options
    text: '```csharp // Create PPTX save options and enable the editable textbox feature
      (available from v25.11) PptxSaveOptions pptxOptions = new PptxSaveOptions {
      ExportEditableTextBox = true }; ```'
  - name: – Save the workbook as PPTX
    text: '```csharp // Export the workbook to a PPTX file; the textbox stays editable
      in PowerPoint workbookWithTextbox.Save("YOUR_DIRECTORY/Result.pptx", pptxOptions);
      ```'
  - name: – Prepare the SmartMarkerProcessor
    text: '```csharp // Initialise the processor that will fill Smart Markers SmartMarkerProcessor
      smartMarkerProcessor = new SmartMarkerProcessor(); ```'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Comment copier un tableau croisé dynamique tout en préservant les feuilles
  de calcul
url: /fr/net/pivot-tables/how-to-copy-pivot-table-while-preserving-worksheets/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment copier un tableau croisé dynamique tout en préservant les feuilles de calcul

Si vous devez **how to copy pivot table** d'un classeur à un autre sans perdre le cache du tableau croisé dynamique sous‑jacent, ce guide fournit une solution prête à l'emploi. Vous verrez également comment **copy worksheet with pivot** et comment **save workbook as pptx** tout en conservant les zones de texte éditables intactes. Tous les exemples utilisent la dernière version d'Aspose.Cells pour .NET, vous pouvez donc insérer le code dans n'importe quel projet C# et voir les résultats immédiatement.

Travailler avec des fichiers Excel de manière programmatique implique souvent de déplacer des données entre classeurs, d'exporter vers des présentations ou d'insérer des Smart Markers complexes. Les trois extraits de code ci‑dessous couvrent ces scénarios courants et expliquent pourquoi chaque étape est importante.

## Prérequis

* .NET 6.0 ou version ultérieure installé  
* Aspose.Cells for .NET (version 25.11 ou plus récente) référencé dans votre projet  
* Un dossier nommé `YOUR_DIRECTORY` où les fichiers d'exemple seront lus et écrits  

Aucun package NuGet supplémentaire n'est requis.

---

## Comment copier un tableau croisé dynamique avec Aspose.Cells

Copier une plage contenant un tableau croisé dynamique tout en préservant le cache du tableau croisé dynamique est une exigence fréquente. Les étapes suivantes démontrent la séquence exacte dont vous avez besoin.

### Étape 1 – Charger le classeur source contenant le tableau croisé dynamique

```csharp
// Load the workbook that contains the pivot table you want to copy
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
```

*Pourquoi* : Aspose.Cells lit le classeur en mémoire, vous donnant accès aux feuilles de calcul, aux cellules et aux tableaux croisés dynamiques.

### Étape 2 – Créer un classeur de destination vide

```csharp
// Create a new, empty workbook that will receive the copied data
Workbook destinationWorkbook = new Workbook();
```

*Pourquoi* : Commencer avec un classeur vierge garantit qu'aucun style caché ou plage nommée n'interfère avec l'opération de copie.

### Étape 3 – Copier les lignes qui incluent le tableau croisé dynamique

```csharp
// Copy rows 0‑19 (A1:G20) from the first worksheet of the source
sourceWorkbook.Worksheets[0].Cells.CopyRows(0, 0, 20);
```

*Pourquoi* : `CopyRows` copie les valeurs brutes des cellules, les formats et les références du cache du tableau croisé dynamique sous‑jacent. La plage doit inclure l'intégralité de la zone du tableau croisé dynamique.

### Étape 4 – Copier les colonnes contenant le tableau croisé dynamique

```csharp
// Copy columns 0‑6 (A‑G) from the same worksheet
sourceWorkbook.Worksheets[0].Cells.CopyColumns(0, 0, 7);
```

*Pourquoi* : Les tableaux croisés dynamiques s'étendent sur les lignes et les colonnes ; copier les colonnes garantit que la mise en page complète du tableau est conservée.

### Étape 5 – Transférer la feuille préparée dans le classeur de destination

```csharp
// Move the fully prepared worksheet into the destination workbook
sourceWorkbook.Worksheets[0].Copy(destinationWorkbook.Worksheets[0]);
```

*Pourquoi* : La méthode `Copy` clone la feuille de calcul, y compris le cache du tableau croisé dynamique, de sorte que le classeur de destination affiche un tableau croisé dynamique identique.

### Étape 6 – Enregistrer le résultat – le tableau croisé dynamique reste intact

```csharp
// Save the destination workbook; the pivot table works exactly like the original
destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
```

*Pourquoi* : La persistance du classeur écrit toutes les structures internes, garantissant que le tableau croisé dynamique pourra être actualisé ultérieurement.

**Astuce** : Après la copie, vous pouvez appeler `destinationWorkbook.Worksheets[0].PivotTables[0].Refresh()` pour mettre à jour les données si les données source ont changé.

---

## Copier une feuille de calcul avec pivot – une alternative concise

Si vous avez simplement besoin de dupliquer une feuille de calcul entière contenant déjà un tableau croisé dynamique, vous pouvez ignorer les étapes de copie de lignes/colonnes et utiliser directement la méthode `Copy` au niveau de la feuille de calcul.

```csharp
// Load source workbook
Workbook src = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");

// Create destination workbook
Workbook dst = new Workbook();

// Copy the first worksheet (including its pivot table) to the destination
src.Worksheets[0].Copy(dst.Worksheets[0]);

// Save the new file
dst.Save("YOUR_DIRECTORY/WorksheetCopy.xlsx");
```

Cette approche est utile lorsque la feuille de calcul ne contient pas de données supplémentaires en dehors de la zone du tableau croisé dynamique. L'opération **copy worksheet with pivot** préserve automatiquement toute la mise en forme, les plages nommées et les caches de tableau croisé dynamique.

---

## Enregistrer le classeur au format PPTX avec des zones de texte éditables

Exporter une feuille Excel contenant une zone de texte éditable vers PowerPoint peut être nécessaire pour les tableaux de bord de reporting. Le code ci‑dessous montre **save workbook as pptx** tout en conservant la zone de texte éditable.

### Étape 1 – Charger le classeur qui inclut la zone de texte

```csharp
// Load the Excel file that contains an editable textbox shape
Workbook workbookWithTextbox = new Workbook("YOUR_DIRECTORY/DocWithTextbox.xlsx");
```

### Étape 2 – Configurer les options d'enregistrement PPTX

```csharp
// Create PPTX save options and enable the editable textbox feature (available from v25.11)
PptxSaveOptions pptxOptions = new PptxSaveOptions
{
    ExportEditableTextBox = true
};
```

*Pourquoi* : Le réglage `ExportEditableTextBox` indique à Aspose.Cells de traduire la zone de texte Excel en une forme PowerPoint qui reste éditable après l'exportation.

### Étape 3 – Enregistrer le classeur au format PPTX

```csharp
// Export the workbook to a PPTX file; the textbox stays editable in PowerPoint
workbookWithTextbox.Save("YOUR_DIRECTORY/Result.pptx", pptxOptions);
```

**Résultat attendu** : Ouvrez `Result.pptx` dans PowerPoint, sélectionnez la zone de texte et modifiez son contenu comme n'importe quelle forme native.

**Question fréquente** : *Et si je dois garder la zone de texte verrouillée ?*  
Définissez `pptxOptions.ExportEditableTextBox = false` ; la forme sera alors convertie en image statique.

---

## Exporter un Smart Marker contenant un tableau JSON en tant que valeur d'une seule cellule

Les Smart Markers vous permettent de remplir des modèles Excel avec des structures de données complexes. Ci‑dessous se trouve un exemple complet qui démontre la gestion de données de type **how to copy pivot table** tout en insérant un tableau JSON dans une seule cellule.

### Étape 1 – Préparer le SmartMarkerProcessor

```csharp
// Initialise the processor that will fill Smart Markers
SmartMarkerProcessor smartMarkerProcessor = new SmartMarkerProcessor();
```

### Étape 2 – Insérer un Smart Marker dans la cellule A1

```csharp
// The marker ${Orders:ArrayAsSingle} tells the processor to write the whole array into one cell
Workbook workbook = new Workbook();
workbook.Worksheets[0].Cells["A1"].PutValue("${Orders:ArrayAsSingle}");
```

### Étape 3 – Définir la source de données avec un tableau de style JSON

```csharp
// Anonymous object that mimics a JSON array
var dataModel = new { Orders = new[] { "A", "B", "C" } };
```

### Étape 4 – Traiter le classeur

```csharp
// Fill the Smart Marker with the array data; the array becomes a comma‑separated string
smartMarkerProcessor.Process(workbook, dataModel);
```

### Étape 5 – Enregistrer le classeur résultant

```csharp
// Persist the workbook; cell A1 now contains "A,B,C"
workbook.Save("YOUR_DIRECTORY/JsonSingleCell.xlsx");
```

**Vérification du résultat** : Ouvrez `JsonSingleCell.xlsx` et confirmez que la cellule A1 contient `A,B,C`. Cela montre comment traiter une collection comme valeur d'une seule cellule, un modèle souvent nécessaire lors de l'exportation de données vers des systèmes en aval.

---

## Exemple complet fonctionnel

Ci‑dessous se trouve un programme unique qui combine les trois scénarios. Vous pouvez copier le code dans une application console, ajuster les chemins de fichiers et l'exécuter pour voir les trois résultats.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1. How to copy pivot table (preserve pivot cache)
        // -------------------------------------------------
        Workbook srcPivot = new Workbook("YOUR_DIRECTORY/Source.xlsx");
        Workbook dstPivot = new Workbook();
        srcPivot.Worksheets[0].Cells.CopyRows(0, 0, 20);
        srcPivot.Worksheets[0].Cells.CopyColumns(0, 0, 7);
        srcPivot.Worksheets[0].Copy(dstPivot.Worksheets[0]);
        dstPivot.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");

        // -------------------------------------------------
        // 2. Save workbook as PPTX with editable textbox
        // -------------------------------------------------
        Workbook txtWorkbook = new Workbook("YOUR_DIRECTORY/DocWithTextbox.xlsx");
        PptxSaveOptions pptxOpts = new PptxSaveOptions { ExportEditableTextBox = true };
        txtWorkbook.Save("YOUR_DIRECTORY/Result.pptx", pptxOpts);

        // -------------------------------------------------
        // 3. Export Smart Marker containing a JSON array
        // -------------------------------------------------
        SmartMarkerProcessor smProcessor = new SmartMarkerProcessor();
        Workbook smWorkbook = new Workbook();
        smWorkbook.Worksheets[0].Cells["A1"].PutValue("${Orders:ArrayAsSingle}");
        var model = new { Orders = new[] { "A", "B", "C" } };
        smProcessor.Process(smWorkbook, model);
        smWorkbook.Save("YOUR_DIRECTORY/JsonSingleCell.xlsx");
    }
}
```

L'exécution de ce programme produit :

* `CopyWithPivot.xlsx` – une copie parfaite du tableau croisé dynamique original.  
* `Result.pptx` – une diapositive PowerPoint avec une zone de texte éditable.  
* `JsonSingleCell.xlsx` – une feuille où le tableau JSON apparaît dans une seule cellule.

---

## Conclusion

Vous savez maintenant comment **how to copy pivot table** en toute sécurité, comment **copy worksheet with pivot** en un seul appel, et comment **save workbook as pptx** tout en préservant les zones de texte éditables. Ces modèles couvrent les flux de travail les plus courants d'Excel vers PowerPoint et d'Excel vers JSON que vous rencontrerez dans les projets d'automatisation d'entreprise.

Ensuite, envisagez d'explorer :

* Actualiser les tableaux croisés dynamiques copiés programmatique­ment (`PivotTable.Refresh()`)  
* Exporter vers d'autres formats tels que PDF ou HTML (`PdfSaveOptions`, `HtmlSaveOptions`)  
* Utiliser des options avancées de Smart Marker comme les fonctions personnalisées ou la mise en forme conditionnelle  

N'hésitez pas à expérimenter avec différentes plages, plusieurs feuilles de calcul ou des structures JSON plus grandes. L'API Aspose.Cells vous offre un contrôle granulaire, vous permettant d'adapter ces exemples à tout scénario réel. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités supplémentaires de l'API et à explorer des approches d'implémentation alternatives dans vos propres projets.

- [Créer un nouveau classeur – Comment copier une feuille de calcul avec un tableau croisé dynamique](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Comment copier un tableau croisé dynamique en C# – Convertir Excel en PPTX, copier une plage et créer une zone de texte](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Copier des feuilles au sein d'un classeur avec Aspose.Cells pour .NET – Guide étape par étape](/cells/english/net/worksheet-management/copy-sheets-within-workbook-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}