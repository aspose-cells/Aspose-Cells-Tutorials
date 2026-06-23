---
category: general
date: 2026-03-27
description: Skapa Excel-arbetsbok i C# med Aspose.Cells, tillämpa villkorsstyrd formatering,
  importera en datatabell till Excel och spara arbetsboken som xlsx – allt i en handledning.
draft: false
keywords:
- create excel workbook c#
- apply conditional formatting
- import datatable to excel
- save workbook as xlsx
- create excel file programmatically
language: sv
og_description: Skapa en Excel-arbetsbok i C# med Aspose.Cells, tillämpa villkorsstyrd
  formatering, importera en datatabell till Excel och spara arbetsboken som xlsx på
  några minuter.
og_title: Skapa Excel-arbetsbok C# – Komplett guide med villkorsstyrd formatering
tags:
- Aspose.Cells
- C#
- Excel automation
title: Skapa Excel‑arbetsbok i C# – Steg‑för‑steg‑guide med villkorsstyrd formatering
url: /sv/net/excel-conditional-formatting/create-excel-workbook-c-step-by-step-guide-with-conditional/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa Excel Workbook C# – Komplett programmeringshandledning

Har du någonsin behövt **create excel workbook c#** i farten men varit osäker på var du ska börja? Du är inte ensam—många utvecklare stöter på den muren när de först automatiserar rapporter. I den här guiden visar vi exakt hur du **create excel workbook c#** med Aspose.Cells, applicerar villkorsstyrd formatering, importerar datatabell till Excel och slutligen sparar arbetsboken som xlsx.  

Vad du får ut av den här handledningen är en färdig‑att‑köra konsolapp som skapar en färgstark Excel‑fil, plus en tydlig förklaring av varje rad så att du kan anpassa den till dina egna projekt. Inga externa dokument behövs; bara kopiera, klistra in och kör.  

### Prerequisites

- .NET 6+ (eller .NET Framework 4.7.2+) installerat  
- Visual Studio 2022 eller någon C#‑redigerare du föredrar  
- Aspose.Cells för .NET (du kan hämta ett gratis prov‑NuGet‑paket)  

Om du har dem, låt oss dyka ner i.

## Skapa Excel Workbook C# – Initiera arbetsboken

Det första du måste göra är att **create excel workbook c#** genom att instansiera `Workbook`‑klassen. Detta objekt representerar hela Excel‑filen i minnet.

```csharp
using Aspose.Cells;
using Aspose.Cells.Tables;
using System.Data;
using System.Drawing;

class SmartMarkerConditionalDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();                // <-- creates the workbook
        Worksheet worksheet = workbook.Worksheets[0];      // first sheet (Sheet1)
```

> **Varför detta är viktigt:** `Workbook`‑klassen abstraherar filformatet, så du slipper hantera låg‑nivå XML eller COM‑interop. Den ger dig också tillgång till stilar, tabeller och smarta markörer direkt ur lådan.

## Applicera villkorsstyrd formatering

Nu när arbetsboken finns, låt oss **apply conditional formatting** för att markera rader där kvantiteten överstiger 100. Villkorsstyrd formatering finns på kalkylbladet, inte i cellen, vilket gör den återanvändbar.

```csharp
        // Step 4: Apply conditional formatting to highlight quantities > 100
        int cfIndex = worksheet.ConditionalFormattings.Add();               // add a new CF collection
        var conditionalFormatting = worksheet.ConditionalFormattings[cfIndex];
        var condition = conditionalFormatting.AddCondition(
            FormatConditionType.CellValue, OperatorType.Greater, "100");   // > 100

        // Define the style that will be applied when the condition is true
        condition.Style = workbook.CreateStyle();
        condition.Style.Font.Color = Color.Red;               // red font
        condition.Style.Pattern = BackgroundType.Solid;       // solid background
        condition.Style.ForegroundColor = Color.Yellow;      // yellow fill
```

> **Proffstips:** Om du behöver mer komplexa regler (t.ex. mellan två värden), anropa bara `AddCondition` igen med `OperatorType.Between`.

## Skriv rubriker och smarta markörer

Innan vi **import datatable to excel** behöver vi platshållarceller—smarta markörer—som biblioteket kommer att ersätta med faktiska data. Tänk på dem som malltaggar.

```csharp
        // Step 2: Write the header row
        worksheet.Cells["A1"].PutValue("Product");
        worksheet.Cells["B1"].PutValue("Quantity");
        worksheet.Cells["C1"].PutValue("Status");

        // Step 3: Define smart markers that will be replaced by data
        worksheet.Cells["A2"].PutValue("&=Products.ProductName");
        worksheet.Cells["B2"].PutValue("&=Products.Quantity");
        worksheet.Cells["C2"].PutValue("&=Products.Quantity > 100 ? \"High\" : \"Low\"");
```

> **Varför smarta markörer?** De låter dig hålla ditt Excel‑layout separat från koden. Du designar bladet en gång, och matar sedan in en `DataTable` så sköter biblioteket resten.

## Importera DataTable till Excel

Här är kärnan i **import datatable to excel**. Vi bygger en `DataTable` som speglar de smarta markörfälten och överlämnar den till `ImportDataTable`.

```csharp
        // Step 5: Build a simple DataTable that matches the smart marker fields
        DataTable products = new DataTable();
        products.Columns.Add("ProductName");
        products.Columns.Add("Quantity", typeof(int));
        products.Rows.Add("Apple", 120);
        products.Rows.Add("Banana", 80);
        products.Rows.Add("Cherry", 150);

        // Step 6: Populate the worksheet with the DataTable via smart markers
        worksheet.Cells.ImportDataTable(products, true, "A2");
```

> **Edge case:** Om din tabell har fler kolumner än du behöver, utelämna bara de extra kolumnerna från de smarta markörerna; de kommer att ignoreras.

## Spara arbetsboken som XLSX

Till sist **save workbook as xlsx** till disk. `Save`‑metoden bestämmer automatiskt formatet från filändelsen.

```csharp
        // Step 7: Save the result to an Excel file
        workbook.Save("SmartMarkersConditional.xlsx");   // <-- saves as .xlsx
    }
}
```

Det är hela programmet. När du kör det kommer du att se en fil med namnet `SmartMarkersConditional.xlsx` i utdata‑mappen.

### Förväntad output

| Product | Quantity | Status |
|---------|----------|--------|
| Apple   | 120      | High   |
| Banana  | 80       | Low    |
| Cherry  | 150      | High   |

Raderna med **Quantity > 100** (Apple och Cherry) kommer att ha röd text på gul bakgrund tack vare den villkorsstyrda formatering vi lade till tidigare.

## Skapa Excel File Programmatically – Fullständig källkodslista

Nedan är den kompletta, färdig‑att‑kopiera källkoden. Den innehåller varje del vi diskuterade, plus några extra kommentarer för tydlighet.

```csharp
using Aspose.Cells;
using Aspose.Cells.Tables;
using System.Data;
using System.Drawing;

class SmartMarkerConditionalDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Write header cells
        worksheet.Cells["A1"].PutValue("Product");
        worksheet.Cells["B1"].PutValue("Quantity");
        worksheet.Cells["C1"].PutValue("Status");

        // 3️⃣ Insert smart markers – placeholders for our data
        worksheet.Cells["A2"].PutValue("&=Products.ProductName");
        worksheet.Cells["B2"].PutValue("&=Products.Quantity");
        worksheet.Cells["C2"].PutValue("&=Products.Quantity > 100 ? \"High\" : \"Low\"");

        // 4️⃣ Apply conditional formatting (highlight >100)
        int cfIdx = worksheet.ConditionalFormattings.Add();
        var cf = worksheet.ConditionalFormattings[cfIdx];
        var cond = cf.AddCondition(FormatConditionType.CellValue, OperatorType.Greater, "100");
        cond.Style = workbook.CreateStyle();
        cond.Style.Font.Color = Color.Red;
        cond.Style.Pattern = BackgroundType.Solid;
        cond.Style.ForegroundColor = Color.Yellow;

        // 5️⃣ Build a DataTable that matches the markers
        DataTable products = new DataTable();
        products.Columns.Add("ProductName");
        products.Columns.Add("Quantity", typeof(int));
        products.Rows.Add("Apple", 120);
        products.Rows.Add("Banana", 80);
        products.Rows.Add("Cherry", 150);

        // 6️⃣ Import the DataTable – this replaces the smart markers
        worksheet.Cells.ImportDataTable(products, true, "A2");

        // 7️⃣ Save the workbook – this will create an .xlsx file
        workbook.Save("SmartMarkersConditional.xlsx");
    }
}
```

> **Tips:** Om du behöver generera flera blad, upprepa bara steg 2‑6 på en ny `Worksheet`‑instans som erhålls via `workbook.Worksheets.Add()`.

## Varför använda Aspose.Cells för C# Excel‑automatisering?

- **Performance:** Fungerar helt i minnet, ingen COM‑interop, så det är snabbt även med stora datamängder.  
- **Feature‑rich:** Stöder smarta markörer, villkorsstyrd formatering, diagram, pivottabeller och mer.  
- **Cross‑platform:** Fungerar på Windows, Linux och macOS med .NET Core/5/6+.  

Om du fastnar på en specifik funktion—t.ex. att lägga till ett diagram eller skydda ett blad—sök bara efter “asp​ose.cells add chart c#” så hittar du ett liknande mönster.

## Nästa steg & relaterade ämnen

- **Export to PDF:** Efter att du har **create excel workbook c#**, kan du omedelbart exportera till PDF med `workbook.Save("output.pdf")`.  
- **Read existing Excel files:** Använd `new Workbook("ExistingFile.xlsx")` för att modifiera en mall.  
- **Bulk import:** För massiva data, överväg `ImportArray` eller `ImportDataTable` med `ImportOptions` för att förbättra hastigheten.  

Känn dig fri att experimentera med olika villkorsregler, färger eller till och med lägga till en totalsumma‑rad med formler. Himlen är gränsen när du **create excel file programmatically**.

---

*Redo att prova själv? Hämta koden, kör den och öppna den genererade `SmartMarkersConditional.xlsx`. Om du stöter på problem, lämna en kommentar nedan—lycklig kodning!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}