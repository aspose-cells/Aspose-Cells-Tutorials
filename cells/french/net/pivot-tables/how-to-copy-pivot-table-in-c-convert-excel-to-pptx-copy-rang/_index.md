---
category: general
date: 2026-01-14
description: Comment copier un tableau croisé dynamique avec Aspose.Cells et également
  apprendre à convertir Excel en PPTX, copier une plage vers un autre classeur, et
  rendre une zone de texte modifiable dans PPTX, le tout dans un seul tutoriel.
draft: false
keywords:
- how to copy pivot table
- convert excel to pptx
- copy range to another workbook
- make textbox editable pptx
- save workbook as pptx
language: fr
og_description: Comment copier un tableau croisé dynamique, puis convertir Excel en
  PPTX, copier une plage vers un autre classeur et rendre une zone de texte modifiable
  dans PPTX — le tout avec Aspose.Cells.
og_title: Comment copier un tableau croisé dynamique en C# – Guide complet d'Excel
  à PPTX
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
title: Comment copier un tableau croisé dynamique en C# – Convertir Excel en PPTX,
  copier une plage et rendre la zone de texte modifiable
url: /fr/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment copier un tableau croisé dynamique en C# – Guide complet Excel vers PPTX

Copier un tableau croisé dynamique d’un classeur à un autre est une question fréquente lorsque vous automatisez des rapports basés sur Excel. Dans ce tutoriel, nous parcourrons trois scénarios réels en utilisant **Aspose.Cells for .NET** : copier une plage de tableau croisé dynamique, exporter une feuille de calcul vers un fichier PPTX avec une zone de texte modifiable, et remplir une cellule unique avec un tableau JSON via Smart Markers.  

Vous verrez également comment **convertir Excel en PPTX**, **copier une plage vers un autre classeur**, et **rendre la zone de texte modifiable dans PPTX** sans altérer le formatage. À la fin, vous disposerez d’une base de code prête à l’emploi que vous pourrez intégrer à n’importe quel projet .NET.

> **Astuce :** Tous les exemples ciblent Aspose.Cells 23.12, mais les mêmes concepts s’appliquent aux versions antérieures avec de légères modifications d’API.

![Diagramme montrant comment un tableau croisé dynamique est copié, une feuille de calcul exportée en PPTX, et un tableau JSON inséré – flux de travail de copie de tableau croisé dynamique](how-to-copy-pivot-table-diagram.png)

---

## Ce dont vous avez besoin

- Visual Studio 2022 (ou tout IDE C#)
- .NET 6.0 ou version ultérieure runtime
- Package NuGet Aspose.Cells for .NET  
  ```bash
  dotnet add package Aspose.Cells
  ```
- Deux fichiers Excel d’exemple (`source.xlsx`, `chartWithTextbox.xlsx`) placés dans un dossier que vous contrôlez (remplacez `YOUR_DIRECTORY` par votre chemin réel).

Aucune bibliothèque supplémentaire n’est requise ; le même assembly `Aspose.Cells` gère Excel, PPTX et Smart Markers.

---

## Comment copier un tableau croisé dynamique et préserver ses données

Lorsque vous copiez une plage contenant un tableau croisé dynamique, le comportement par défaut est de coller uniquement les **valeurs**. Pour conserver la définition du tableau croisé dynamique intacte, vous devez activer le drapeau `CopyPivotTable`.

### Étape par étape

1. **Chargez le classeur source** qui contient le tableau croisé dynamique.  
2. **Créez un classeur de destination vide** – il recevra la plage copiée.  
3. **Utilisez `CopyRange` avec `CopyPivotTable = true`** afin que la définition du tableau croisé dynamique accompagne les données.  
4. **Enregistrez le fichier de destination** où vous le souhaitez.

#### Exemple complet de code

```csharp
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // Step 1: Load the source workbook and define the range to copy
        Workbook sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
        // Assuming the pivot table lives inside A1:G20
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

        // Step 2: Create a destination workbook (blank)
        Workbook destinationWorkbook = new Workbook();
        Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

        // Step 3: Copy the range, preserving the pivot table
        destinationSheet.Cells.CopyRange(
            sourceRange,
            "B2", // paste start cell
            new CopyOptions { CopyPivotTable = true });

        // Step 4: Save the result
        destinationWorkbook.Save(@"YOUR_DIRECTORY\copyWithPivot.xlsx");
    }
}
```

**Pourquoi cela fonctionne :**  
`CopyOptions.CopyPivotTable` indique à Aspose.Cells de cloner l’objet `PivotTable` sous‑jacent plutôt que seulement ses valeurs rendues. Le classeur de destination contient désormais un tableau croisé dynamique pleinement fonctionnel que vous pouvez actualiser ou modifier par programme.

**Cas particulier :** Si le classeur source utilise des sources de données externes, il peut être nécessaire d’intégrer les données ou d’ajuster les chaînes de connexion après la copie, sinon le tableau croisé dynamique affichera “#REF!”.

---

## Convertir Excel en PPTX et rendre la zone de texte modifiable

Exporter une feuille de calcul vers PowerPoint est pratique pour créer des présentations directement à partir des données. Par défaut, la zone de texte exportée devient une forme statique, mais le réglage `IsTextBoxEditable` inverse ce comportement.

### Étape par étape

1. **Ouvrez le classeur** qui contient le graphique et la zone de texte que vous souhaitez exporter.  
2. **Configurez `ImageOrPrintOptions`** avec `SaveFormat = SaveFormat.Pptx`.  
3. **Définissez une zone d’impression** qui inclut la zone de texte.  
4. **Activez `IsTextBoxEditable`** afin que le texte puisse être modifié après l’ouverture du PPTX.  
5. **Enregistrez le fichier PPTX**.

#### Exemple complet de code

```csharp
using Aspose.Cells;

class ExcelToPptxDemo
{
    static void Main()
    {
        // Step 1: Load the workbook with chart and textbox
        Workbook chartWorkbook = new Workbook(@"YOUR_DIRECTORY\chartWithTextbox.xlsx");

        // Step 2: Set export options for PPTX
        ImageOrPrintOptions pptxOptions = new ImageOrPrintOptions
        {
            SaveFormat = SaveFormat.Pptx
        };

        // Step 3: Define the print area that captures the textbox (A1:D20)
        chartWorkbook.Worksheets[0].PageSetup.PrintArea = "A1:D20";

        // Step 4: Make the textbox editable in the exported PPTX
        chartWorkbook.Worksheets[0].PageSetup.IsTextBoxEditable = true;

        // Step 5: Export the worksheet to a PPTX file
        chartWorkbook.Save(@"YOUR_DIRECTORY\result.pptx", pptxOptions);
    }
}
```

**Résultat :** Ouvrez `result.pptx` dans PowerPoint – la zone de texte que vous avez placée dans Excel sera désormais une zone de texte ordinaire dans laquelle vous pouvez taper. Aucun besoin de la recréer manuellement.

**Erreur fréquente :** Si la feuille de calcul contient des cellules fusionnées qui intersectent la zone d’impression, la diapositive résultante peut être décalée. Ajustez la zone d’impression ou dés‑fusionnez les cellules avant l’exportation.

---

## Copier une plage vers un autre classeur avec Smart Markers (JSON → Cellule unique)

Parfois, vous devez intégrer un tableau JSON dans une seule cellule Excel, par exemple lors du passage de données à des systèmes en aval qui attendent une chaîne JSON. Les Smart Markers d’Aspose.Cells peuvent sérialiser un tableau en une seule cellule lorsque vous définissez `ArrayAsSingle = true`.

### Étape par étape

1. **Chargez un classeur modèle** qui contient un espace réservé Smart Marker (par ex., `&=Items.Name`).  
2. **Préparez l’objet de données** – un type anonyme avec un tableau `Items`.  
3. **Créez un `SmartMarkerProcessor`** et appliquez les données avec `ArrayAsSingle`.  
4. **Enregistrez le classeur rempli**.

#### Exemple complet de code

```csharp
using Aspose.Cells;
using System;

class SmartMarkerDemo
{
    static void Main()
    {
        // Step 1: Load the template workbook containing a smart marker like "&=Items.Name"
        Workbook templateWorkbook = new Workbook(@"YOUR_DIRECTORY\SmartMarkerTemplate.xlsx");

        // Step 2: Prepare the data object with an array of items
        var data = new
        {
            Items = new[]
            {
                new { Name = "A" },
                new { Name = "B" }
            }
        };

        // Step 3: Apply the SmartMarkerProcessor with ArrayAsSingle option
        SmartMarkerProcessor processor = new SmartMarkerProcessor(templateWorkbook);
        processor.Apply(data, new SmartMarkerOptions { ArrayAsSingle = true });

        // Step 4: Save the result – the JSON array will appear in a single cell
        templateWorkbook.Save(@"YOUR_DIRECTORY\jsonSingleCell.xlsx");
    }
}
```

**Explication :**  
Lorsque `ArrayAsSingle` est vrai, Aspose.Cells concatène chaque élément de `Items.Name` en une chaîne de style JSON (`["A","B"]`) et l’écrit dans la cellule qui contenait le smart marker. Cela évite de créer une ligne distincte pour chaque élément du tableau.

**Quand l’utiliser :** Idéal pour exporter des tables de configuration, des charges utiles d’API, ou tout scénario où le consommateur attend une chaîne JSON compacte plutôt qu’une mise en page tabulaire.

---

## Conseils supplémentaires & gestion des cas particuliers

| Scénario | À surveiller | Solution suggérée |
|----------|--------------|-------------------|
| **Grandes tables de pivot** | L’utilisation de la mémoire augmente fortement lors de la copie de caches de tableau croisé dynamique volumineux. | Utilisez `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference` avant le chargement. |
| **Exportation vers PPTX avec images** | Les images peuvent être rasterisées à faible DPI. | Définissez `pptxOptions.ImageResolution = 300` pour des diapositives plus nettes. |
| **Mise en forme JSON avec Smart Marker** | Les caractères spéciaux (`"` , `\`) cassent le JSON. | Échappez‑les manuellement ou utilisez `JsonSerializer` pour pré‑sérialiser avant d’alimenter les Smart Markers. |
| **Copier une plage entre différentes versions d’Excel** | Les anciens fichiers `.xls` peuvent perdre le formatage. | Enregistrez la destination au format `.xlsx` pour préserver les fonctionnalités modernes. |

---

## Récapitulatif – Comment copier un tableau croisé dynamique et bien plus

Nous avons commencé par répondre à **comment copier un tableau croisé dynamique** tout en préservant sa fonctionnalité, puis nous vous avons montré comment **convertir Excel en PPTX**, **rendre la zone de texte modifiable dans PPTX**, et enfin comment **copier une plage vers un autre classeur** en utilisant les Smart Markers pour intégrer un tableau JSON dans une cellule unique.  

Les trois extraits sont autonomes ; vous pouvez les coller dans une nouvelle application console, ajuster les chemins de fichiers, et les exécuter dès aujourd’hui.

## Et après ?

- **Explorez d’autres formats d’exportation** – Aspose.Cells prend également en charge PDF, XPS et HTML.  
- **Actualisez les tableaux croisés dynamiques par programme** en utilisant `PivotTable.RefreshData()` après la copie.  
- **Combinez les Smart Markers avec des graphiques** pour générer des tableaux de bord dynamiques qui se mettent à jour automatiquement.  

Si vous êtes intéressé par **l’enregistrement d’un classeur au format PPTX** avec des mises en page de diapositive personnalisées, consultez la documentation Aspose.Cells sur `SlideOptions`.  

N’hésitez pas à expérimenter — changez la zone d’impression, essayez différents `CopyOptions`, ou fournissez une charge JSON plus complexe. L’API est suffisamment flexible pour la plupart des pipelines de reporting.

### Questions fréquemment posées

**Q : `CopyPivotTable` copie‑t‑il également les segments ?**  
R : Pas directement. Les segments sont des objets séparés ; après la copie, vous devrez les recréer ou les copier via la collection `Worksheet.Shapes`.

**Q : Puis‑je exporter plusieurs feuilles de calcul dans un seul diaporama PPTX ?**  
R : Oui. Parcourez chaque feuille, appelez `Save` avec les mêmes `ImageOrPrintOptions` et définissez `pptxOptions.StartSlideNumber` pour poursuivre la numérotation.

**Q : Que faire si mon tableau JSON contient des objets imbriqués ?**  
R : Définissez `ArrayAsSingle = false` et utilisez un modèle personnalisé qui itère sur

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}