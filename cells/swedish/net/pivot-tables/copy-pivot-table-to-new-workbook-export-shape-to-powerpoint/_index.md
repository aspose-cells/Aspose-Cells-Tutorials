---
category: general
date: 2026-10-20
description: Kopiera pivottabell till ny arbetsbok med Aspose.Cells och lär dig hur
  du exporterar en redigerbar form till PowerPoint i en enda guide.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table to new workbook
- copy rows between worksheets
- Aspose.Cells copy rows
- export shape to PowerPoint
- editable textbox in PowerPoint
language: sv
lastmod: 2026-10-20
og_description: Kopiera pivottabell till ny arbetsbok med Aspose.Cells och exportera
  en redigerbar form till PowerPoint – steg‑för‑steg‑kod du kan köra idag.
og_image_alt: Screenshot showing copy pivot table to new workbook using Aspose.Cells
og_title: Kopiera pivottabell till ny arbetsbok, exportera form till PowerPoint
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
title: Kopiera pivottabell till ny arbetsbok, exportera form till PowerPoint
url: /sv/net/pivot-tables/copy-pivot-table-to-new-workbook-export-shape-to-powerpoint/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kopiera pivottabell till ny arbetsbok, exportera form till PowerPoint

Om du behöver **copy pivot table to new workbook** medan du bevarar dess funktionalitet, visar den här guiden exakt hur du gör det med Aspose.Cells. Du får också se det snabbaste sättet att **export an editable shape to PowerPoint**, så att textrutan förblir redigerbar efter konverteringen.

Många utvecklare antar att kopiering av ett område som innehåller en pivottabell kommer att förlora pivottlogiken, eller att former blir statiska bilder när de sparas som PPTX. Denna handledning motbevisar dessa myter och ger dig en pålitlig, produktionsklar lösning.

I de följande avsnitten kommer du att:

* Ladda en källarbetsbok och kopiera ett område som inkluderar en pivottabell.
* Skapa en destinationsarbetsbok som innehåller samma pivottabell.
* Lägg till en textruteform, ändra dess text och spara arbetsboken som en PowerPoint‑presentation där textrutan förblir redigerbar.
* Förstå varför varje API‑anrop krävs och hur du undviker vanliga fallgropar.

**Förutsättningar**

* .NET 6.0 eller senare (koden fungerar även med .NET Framework 4.7+).
* Aspose.Cells för .NET installerat (`Install-Package Aspose.Cells`).
* Grundläggande kunskaper i C# och Visual Studio (eller någon annan IDE du föredrar).

---

## Kopiera pivottabell till ny arbetsbok

Detta steg‑för‑steg‑avsnitt demonstrerar hur du kopierar ett område som innehåller en pivottabell och behåller pivottdefinitionen i den nya filen.

### Steg 1 – Ladda källarbetsboken och välj det första kalkylbladet

```csharp
// Load the workbook that already contains the pivot table
Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

// The first worksheet (index 0) holds the pivot table we want to copy
Worksheet srcWorksheet = srcWorkbook.Worksheets[0];
```

*Varför?*  
`Workbook` är ingångspunkten för all Excel‑manipulation i Aspose.Cells. Att välja rätt kalkylblad säkerställer att vi arbetar med den exakta pivottabellens plats.

### Steg 2 – Definiera cellområdet som inkluderar pivottabellen

```csharp
// CellArea(startRow, startColumn, endRow, endColumn)
// Here we copy rows 0‑20 and columns 0‑10, which covers the whole pivot table
CellArea sourceArea = new CellArea(0, 0, 20, 10);
```

*Varför?*  
Pivottabellen finns inom ett specifikt block av celler. Genom att ange ett `CellArea` som helt omsluter pivottabellen vet Aspose.Cells att kopiera den underliggande pivottcachen också.

### Steg 3 – Skapa destinationsarbetsboken och hämta dess första kalkylblad

```csharp
// Create an empty workbook that will receive the copied range
Workbook destWorkbook = new Workbook();

// Destination worksheet (also index 0)
Worksheet destWorksheet = destWorkbook.Worksheets[0];
```

*Varför?*  
En ny arbetsbok garanterar att inga konflikterande namngivna områden eller befintliga pivoter finns, vilket gör kopieringsoperationen ren.

### Steg 4 – Kopiera raderna från källområdet till destinationsbladet

```csharp
// CopyRows(startRow, endRow, destinationCells, destinationStartRow)
srcWorksheet.Cells.CopyRows(
    sourceArea.StartRow,
    sourceArea.EndRow,
    destWorksheet.Cells,
    0); // start at row 0 in the destination sheet
```

*Varför?*  
`CopyRows` är en del av **Aspose.Cells copy rows**‑API:t. Det kopierar både cellvärden och den dolda pivottcachen, så pivottabellen förblir funktionell efter flytten.

### Steg 5 – Spara den nya arbetsboken

```csharp
destWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
```

*Resultat*  
Öppna `CopyWithPivot.xlsx` i Excel. Pivottabellen visas exakt som i källfilen, och du kan uppdatera eller ändra den som vanligt.

---

## Exportera redigerbar form till PowerPoint

Nu lägger vi till en textruteform, ändrar dess innehåll och sparar arbetsboken som en PPTX‑fil. Formen förblir fullt redigerbar när den öppnas i PowerPoint.

### Steg 1 – Skapa en ny arbetsbok och gå till dess första kalkylblad

```csharp
Workbook workbook = new Workbook();          // Empty workbook
Worksheet worksheet = workbook.Worksheets[0]; // First (and only) sheet
```

### Steg 2 – Lägg till en textruteform i kalkylbladet

```csharp
// AddTextBox(startRow, startColumn, width, height, text)
int shapeIndex = worksheet.Shapes.AddTextBox(10, 10, 200, 50, "Editable text");
```

*Varför?*  
`AddTextBox` skapar en **editable textbox in PowerPoint**‑kompatibel form. Koordinaterna är i punkter; justera dem för att passa din layout.

### Steg 3 – Hämta formen och ändra dess text

```csharp
Shape textShape = worksheet.Shapes[shapeIndex];
textShape.Text = "Change me in PowerPoint";
```

*Varför?*  
Genom att direkt komma åt `Shape`‑objektet kan du ändra egenskaper som `Text`, `Font` eller `Fill`. Detta steg visar hur du programatiskt sätter det initiala innehållet.

### Steg 4 – Spara arbetsboken som en PowerPoint‑presentation

```csharp
workbook.Save("YOUR_DIRECTORY/Presentation.pptx", SaveFormat.Pptx);
```

*Resultat*  
Öppna `Presentation.pptx` i Microsoft PowerPoint. Textrutan visas på den första bilden, och du kan dubbelklicka den för att redigera texten precis som någon inbyggd PowerPoint‑form.

---

## Förväntat resultat

| Fil | Vad du kommer att se |
|------|-----------------|
| `CopyWithPivot.xlsx` | Ett kalkylblad som innehåller den ursprungliga pivottabellen, fullt funktionell (uppdatering fungerar). |
| `Presentation.pptx` | En enda bild med en redigerbar textruta som visar “Change me in PowerPoint”. |

---

## Vanliga fallgropar och bästa praxis‑tips

* **Pivot cache loss** – Om du bara kopierar cellvärden (t.ex. med `CopyRows` och `PasteOptions`‑flaggan satt till `PasteValues`), utelämnas pivottcachen och tabellen blir statisk. Använd alltid standard‑overloaden för `CopyRows` som visas.
* **Shape positioning** – `AddTextBox` använder enheter i punkter, inte Excel‑cellindex. Testa koordinaterna i en exempel‑fil för att undvika felaktig placering utanför bilden.
* **File format mismatch** – Att spara en arbetsbok som PPTX med `SaveFormat.Pptx` konverterar automatiskt alla stödda former. Att försöka spara som `Pdf` rasteriserar formen, vilket gör den icke‑redigerbar.

---

## Slutsats

Du vet nu hur du **copy pivot table to new workbook** och hur du **export an editable shape to PowerPoint** med Aspose.Cells för .NET. De kompletta, körbara kodexemplen täcker varje nödvändigt API‑anrop, förklarar varför varje steg är viktigt och visar de förväntade resultaten.

Nästa steg kan vara att utforska:

* **Working with charts** – kopiera diagram tillsammans med pivottabeller (`Aspose.Cells copy rows between worksheets`).

## Vad bör du lära dig härnäst?

De följande handledningarna täcker närbesläktade ämnen som bygger vidare på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Skapa ny arbetsbok – Hur man kopierar ett kalkylblad med en pivottabell](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Kopiera pivottabell och exportera Excel till PPTX med Aspose.Cells](/cells/english/net/converting-excel-files-to-other-formats/copy-pivot-table-and-export-excel-to-pptx-with-aspose-cells/)
- [Skapa ny arbetsbok i C# – Kopiera pivottabell](/cells/english/net/pivot-tables/create-new-workbook-in-c-copy-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}