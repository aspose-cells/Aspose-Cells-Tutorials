---
category: general
date: 2026-10-20
description: Copier le tableau croisé dynamique dans un nouveau classeur à l'aide
  d'Aspose.Cells et apprendre comment exporter une forme éditable vers PowerPoint
  dans un guide unique.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table to new workbook
- copy rows between worksheets
- Aspose.Cells copy rows
- export shape to PowerPoint
- editable textbox in PowerPoint
language: fr
lastmod: 2026-10-20
og_description: Copier un tableau croisé dynamique vers un nouveau classeur avec Aspose.Cells
  et exporter une forme modifiable vers PowerPoint — code étape par étape que vous
  pouvez exécuter dès aujourd’hui.
og_image_alt: Screenshot showing copy pivot table to new workbook using Aspose.Cells
og_title: Copier le tableau croisé dynamique dans un nouveau classeur, exporter la
  forme vers PowerPoint
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Copy pivot table to new workbook using Aspose.Cells and learn how to
    export an editable shape to PowerPoint in a single guide.
  headline: Copy pivot table to new workbook, export shape to PowerPoint
  type: TechArticle
- description: Copy pivot table to new workbook using Aspose.Cells and learn how to
    export an editable shape to PowerPoint in a single guide.
  name: Copy pivot table to new workbook, export shape to PowerPoint
  steps:
  - name: – Load the source workbook and select the first worksheet
    text: '```csharp // Load the workbook that already contains the pivot table Workbook
      srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");'
  - name: – Define the cell area that includes the pivot table
    text: '```csharp // CellArea(startRow, startColumn, endRow, endColumn) // Here
      we copy rows 0‑20 and columns 0‑10, which covers the whole pivot table CellArea
      sourceArea = new CellArea(0, 0, 20, 10); ```'
  - name: – Create the destination workbook and get its first worksheet
    text: '```csharp // Create an empty workbook that will receive the copied range
      Workbook destWorkbook = new Workbook();'
  - name: – Copy the rows from the source area to the destination sheet
    text: '```csharp // CopyRows(startRow, endRow, destinationCells, destinationStartRow)
      srcWorksheet.Cells.CopyRows( sourceArea.StartRow, sourceArea.EndRow, destWorksheet.Cells,
      0); // start at row 0 in the destination sheet ```'
  - name: – Save the new workbook
    text: '```csharp destWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx"); ```'
  - name: – Create a new workbook and access its first worksheet
    text: '```csharp Workbook workbook = new Workbook(); // Empty workbook Worksheet
      worksheet = workbook.Worksheets[0]; // First (and only) sheet ```'
  - name: – Add a textbox shape to the worksheet
    text: '```csharp // AddTextBox(startRow, startColumn, width, height, text) int
      shapeIndex = worksheet.Shapes.AddTextBox(10, 10, 200, 50, "Editable text");
      ```'
  - name: – Retrieve the shape and modify its text
    text: '```csharp Shape textShape = worksheet.Shapes[shapeIndex]; textShape.Text
      = "Change me in PowerPoint"; ```'
  - name: – Save the workbook as a PowerPoint presentation
    text: '```csharp workbook.Save("YOUR_DIRECTORY/Presentation.pptx", SaveFormat.Pptx);
      ```'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Pivot Table
- PowerPoint Export
title: Copier le tableau croisé dynamique dans un nouveau classeur, exporter la forme
  vers PowerPoint
url: /fr/net/pivot-tables/copy-pivot-table-to-new-workbook-export-shape-to-powerpoint/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copier un tableau croisé dynamique vers un nouveau classeur, exporter une forme vers PowerPoint

Si vous devez **copier un tableau croisé dynamique vers un nouveau classeur** tout en conservant sa fonctionnalité, ce guide vous montre exactement comment le faire avec Aspose.Cells. Vous découvrirez également la façon la plus rapide d'**exporter une forme éditable vers PowerPoint**, afin que la zone de texte reste modifiable après la conversion.

De nombreux développeurs supposent que copier une plage contenant un tableau croisé dynamique entraînera la perte de la logique du tableau, ou que les formes deviennent des images statiques lorsqu'elles sont enregistrées au format PPTX. Ce tutoriel démystifie ces idées reçues et vous fournit une solution fiable, prête pour la production.

Dans les sections suivantes, vous allez :

* Charger un classeur source et copier une plage qui inclut un tableau croisé dynamique.
* Créer un classeur de destination contenant le même tableau croisé dynamique.
* Ajouter une forme de zone de texte, modifier son texte, puis enregistrer le classeur sous forme de présentation PowerPoint où la zone de texte reste éditable.
* Comprendre pourquoi chaque appel d’API est nécessaire et comment éviter les pièges courants.

**Prerequisites**

* .NET 6.0 ou version ultérieure (le code fonctionne également avec .NET Framework 4.7+).
* Aspose.Cells for .NET installé (`Install-Package Aspose.Cells`).
* Connaissances de base en C# et Visual Studio (ou tout autre IDE de votre choix).

---

## Copier un tableau croisé dynamique vers un nouveau classeur

Cette section pas à pas montre comment copier une plage contenant un tableau croisé dynamique et conserver la définition du tableau dans le nouveau fichier.

### Step 1 – Load the source workbook and select the first worksheet

```csharp
// Load the workbook that already contains the pivot table
Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

// The first worksheet (index 0) holds the pivot table we want to copy
Worksheet srcWorksheet = srcWorkbook.Worksheets[0];
```

*Why?*  
`Workbook` est le point d’entrée pour toute manipulation Excel dans Aspose.Cells. Sélectionner la bonne feuille garantit que nous travaillons sur l’emplacement exact du tableau croisé dynamique.

### Step 2 – Define the cell area that includes the pivot table

```csharp
// CellArea(startRow, startColumn, endRow, endColumn)
// Here we copy rows 0‑20 and columns 0‑10, which covers the whole pivot table
CellArea sourceArea = new CellArea(0, 0, 20, 10);
```

*Why?*  
Le tableau croisé dynamique vit à l’intérieur d’un bloc de cellules spécifique. En spécifiant un `CellArea` qui englobe complètement le tableau, Aspose.Cells sait copier également le cache de pivot sous‑jacent.

### Step 3 – Create the destination workbook and get its first worksheet

```csharp
// Create an empty workbook that will receive the copied range
Workbook destWorkbook = new Workbook();

// Destination worksheet (also index 0)
Worksheet destWorksheet = destWorkbook.Worksheets[0];
```

*Why?*  
Un classeur vierge assure l’absence de plages nommées conflictuelles ou de pivots existants, rendant l’opération de copie propre.

### Step 4 – Copy the rows from the source area to the destination sheet

```csharp
// CopyRows(startRow, endRow, destinationCells, destinationStartRow)
srcWorksheet.Cells.CopyRows(
    sourceArea.StartRow,
    sourceArea.EndRow,
    destWorksheet.Cells,
    0); // start at row 0 in the destination sheet
```

*Why?*  
`CopyRows` fait partie de l’**API Aspose.Cells copy rows**. Elle copie à la fois les valeurs des cellules et le cache de pivot caché, de sorte que le tableau croisé dynamique reste fonctionnel après le déplacement.

### Step 5 – Save the new workbook

```csharp
destWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
```

*Result*  
Ouvrez `CopyWithPivot.xlsx` dans Excel. Le tableau croisé dynamique apparaît exactement comme dans le fichier source, et vous pouvez le rafraîchir ou le modifier normalement.

---

## Exporter une forme éditable vers PowerPoint

Nous allons maintenant ajouter une forme de zone de texte, modifier son contenu, puis enregistrer le classeur au format PPTX. La forme restera entièrement éditable lorsqu’elle sera ouverte dans PowerPoint.

### Step 1 – Create a new workbook and access its first worksheet

```csharp
Workbook workbook = new Workbook();          // Empty workbook
Worksheet worksheet = workbook.Worksheets[0]; // First (and only) sheet
```

### Step 2 – Add a textbox shape to the worksheet

```csharp
// AddTextBox(startRow, startColumn, width, height, text)
int shapeIndex = worksheet.Shapes.AddTextBox(10, 10, 200, 50, "Editable text");
```

*Why?*  
`AddTextBox` crée une **zone de texte éditable compatible PowerPoint**. Les coordonnées sont exprimées en points ; ajustez‑les selon votre mise en page.

### Step 3 – Retrieve the shape and modify its text

```csharp
Shape textShape = worksheet.Shapes[shapeIndex];
textShape.Text = "Change me in PowerPoint";
```

*Why?*  
Accéder directement à l’objet `Shape` vous permet de modifier des propriétés telles que `Text`, `Font` ou `Fill`. Cette étape montre comment définir programmétiquement le contenu initial.

### Step 4 – Save the workbook as a PowerPoint presentation

```csharp
workbook.Save("YOUR_DIRECTORY/Presentation.pptx", SaveFormat.Pptx);
```

*Result*  
Ouvrez `Presentation.pptx` dans Microsoft PowerPoint. La zone de texte apparaît sur la première diapositive, et vous pouvez double‑cliquer dessus pour modifier le texte comme toute forme native de PowerPoint.

---

## Expected output

| File | What you’ll see |
|------|-----------------|
| `CopyWithPivot.xlsx` | A worksheet containing the original pivot table, fully functional (refresh works). |
| `Presentation.pptx` | A single slide with an editable textbox that reads “Change me in PowerPoint”. |

---

## Common pitfalls and best‑practice tips

* **Pivot cache loss** – Si vous ne copiez que les valeurs des cellules (par ex. en utilisant `CopyRows` avec le drapeau `PasteOptions` réglé sur `PasteValues`), le cache de pivot est omis et le tableau devient statique. Utilisez toujours la surcharge par défaut de `CopyRows` comme indiqué.
* **Shape positioning** – `AddTextBox` utilise des unités en points, pas des indices de cellules Excel. Testez les coordonnées sur un fichier d’exemple pour éviter un placement hors diapositive.
* **File format mismatch** – Enregistrer un classeur au format PPTX avec `SaveFormat.Pptx` convertit automatiquement toutes les formes prises en charge. Tenter d’enregistrer en `Pdf` rasterisera la forme, la rendant non‑éditable.

---

## Conclusion

Vous savez maintenant comment **copier un tableau croisé dynamique vers un nouveau classeur** et comment **exporter une forme éditable vers PowerPoint** en utilisant Aspose.Cells pour .NET. Les exemples de code complets et exécutables couvrent chaque appel d’API requis, expliquent pourquoi chaque étape est importante et montrent les résultats attendus.

Ensuite, vous pourriez explorer :

* **Working with charts** – copy charts together with pivot tables (`Aspose.Cells copy rows between worksheets`).
* **

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités de l’API et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [Create New Workbook – How to Copy a Worksheet with a Pivot Table](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Copy pivot table and export Excel to PPTX with Aspose.Cells](/cells/english/net/converting-excel-files-to-other-formats/copy-pivot-table-and-export-excel-to-pptx-with-aspose-cells/)
- [Create New Workbook in C# – Copy Pivot Table](/cells/english/net/pivot-tables/create-new-workbook-in-c-copy-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}