---
category: general
date: 2026-03-22
description: Anpassad talformat‑Excel‑handledning som visar hur man importerar en
  datatabell till Excel, sätter kolumnens bakgrundsfärg, formaterar kolumnen som valuta
  och sparar arbetsboken som xlsx.
draft: false
keywords:
- custom number format excel
- import datatable to excel
- set column background color
- format column as currency
- save workbook as xlsx
language: sv
og_description: Anpassad talformat i Excel-handledning som guidar dig genom att importera
  en DataTable, sätta kolumnens bakgrundsfärg, formatera en kolumn som valuta och
  spara arbetsboken som xlsx.
og_title: Anpassat talformat i Excel med C# – Steg‑för‑steg‑guide
tags:
- C#
- Excel automation
- Aspose.Cells
- Data export
title: Anpassade talformat i Excel med C# – Komplett guide
url: /sv/net/excel-custom-number-date-formatting/custom-number-format-excel-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Anpassat talformat Excel – Full‑Stack C#‑handledning

Har du någonsin undrat hur man applicerar ett **custom number format excel**‑stil direkt från C#? Kanske har du försökt dumpa en DataTable i ett kalkylblad bara för att se rena siffror, inga färger och ingen valutformatering. Det är ett vanligt problem—särskilt när du behöver en polerad rapport för intressenter.

I den här guiden kommer vi att lösa det problemet tillsammans: du kommer att lära dig hur man **import datatable to excel**, **set column background color**, **format column as currency**, och slutligen **save workbook as xlsx** med ett anpassat talformat som får dina siffror att sticka ut. Inga vaga referenser, bara en komplett, körbar lösning som du kan kopiera‑klistra in i ditt projekt.

---

## Vad du kommer att bygga

I slutet av den här handledningen kommer du att ha en självständig C#‑konsolapp som:

1. Hämtar en `DataTable` (du kan ersätta stubben med din egen fråga).  
2. Skapar en ny Excel-arbetsbok med Aspose.Cells (eller vilket kompatibelt bibliotek som helst).  
3. Applicerar ett blått, fetstilat teckensnitt på den första kolumnen, en ljus‑gul bakgrund på den andra, och ett valutformat (`$#,##0.00`) på den tredje.  
4. Sparar filen som `DataTableWithStyleArray.xlsx` i en mapp du väljer.

Du kommer att se exakt hur varje rad bidrar till den slutgiltiga Excel-filen, och vi kommer att diskutera varför dessa val är viktiga för underhållbarhet och prestanda.

---

## Förutsättningar

- .NET 6.0 eller senare (koden fungerar även med .NET Framework 4.7+).  
- Aspose.Cells för .NET (gratis provversion eller licensierad version). Installera via NuGet:

```bash
dotnet add package Aspose.Cells
```

- Grundläggande kunskap om `DataTable` och C#‑konsolapplikationer.

---

## Steg 1: Hämta källdata som en DataTable

Först behöver vi lite data att exportera. I ett verkligt scenario skulle du förmodligen anropa ett repository eller köra en SQL‑fråga. För illustration skapar vi en enkel tabell i minnet.

```csharp
using System;
using System.Data;
using Aspose.Cells;

static DataTable GetSampleData()
{
    var table = new DataTable("Sales");
    table.Columns.Add("Product", typeof(string));
    table.Columns.Add("Quantity", typeof(int));
    table.Columns.Add("Revenue", typeof(decimal));

    table.Rows.Add("Widget A", 120, 3450.75m);
    table.Rows.Add("Widget B", 85, 2190.00m);
    table.Rows.Add("Widget C", 60, 1580.40m);

    return table;
}
```

> **Varför detta är viktigt:** Att använda en `DataTable` ger dig en tabellbaserad, schema‑medveten källa som mappar rent på Excel‑rader och -kolumner. Det låter dig också återanvända samma exportlogik för vilken dataset som helst utan att skriva om koden.

---

## Steg 2: Skapa en ny arbetsbok och hämta det första kalkylbladet

Nu skapar vi en Excel‑arbetsbok. Klassen `Workbook` representerar hela filen; dess `Worksheets[0]` är standardbladet där vi placerar våra data.

```csharp
// Initialize a fresh workbook
Workbook workbook = new Workbook();

// Grab the first (and only) worksheet
Worksheet worksheet = workbook.Worksheets[0];
```

> **Proffstips:** Om du behöver flera blad, anropa bara `workbook.Worksheets.Add("SheetName")` och upprepa stilstegen för varje.

---

## Steg 3: Definiera kolumnstilar – teckensnitt, bakgrund och talformat

Stil i Aspose.Cells görs via `Style`‑objekt. Vi kommer att bygga en array där varje element motsvarar en kolumn i DataTable.

```csharp
// Prepare an array to hold three distinct styles
Style[] columnStyles = new Style[3];

// 1️⃣ First column – blue, bold font
columnStyles[0] = workbook.CreateStyle();
columnStyles[0].Font.Color = System.Drawing.Color.Blue;
columnStyles[0].Font.IsBold = true;

// 2️⃣ Second column – light‑yellow background
columnStyles[1] = workbook.CreateStyle();
columnStyles[1].ForegroundColor = System.Drawing.Color.LightYellow;
columnStyles[1].Pattern = BackgroundType.Solid;

// 3️⃣ Third column – custom currency format (custom number format excel)
columnStyles[2] = workbook.CreateStyle();
columnStyles[2].Custom = "$#,##0.00";
```

> **Varför en stilarray?** Att skicka en array till `ImportDataTable` låter dig applicera en distinkt stil på varje kolumn i ett enda anrop, vilket är både koncist och prestandaeffektivt. Det garanterar också att formateringen hålls i synk med datasekvensen.

---

## Steg 4: Importera DataTable samtidigt som du applicerar stilarna

Här är kärnan i operationen: vi matar in `DataTable` i kalkylbladet, instruerar Aspose att inkludera rubrikraden, och överlämnar vår `columnStyles`‑array.

```csharp
// Import data starting at cell A1 (row 0, column 0)
worksheet.Cells.ImportDataTable(
    GetSampleData(),   // source DataTable
    true,              // include column names as header
    0, 0,              // start row, start column
    columnStyles);     // apply the style array
```

> **Vad händer under huven?** Aspose itererar genom varje kolumn, skriver rubriken och sedan varje radvärde. Under tiden applicerar den motsvarande `Style` från arrayen, så du får en blå rubrik för “Product”, en gul‑tonad “Quantity” och en snyggt formaterad “Revenue”-kolumn.

---

## Steg 5: Spara arbetsboken som en XLSX‑fil

Till sist sparar vi arbetsboken till disk. Metoden `Save` väljer automatiskt XLSX‑formatet baserat på filändelsen.

```csharp
// Choose a folder that exists on your machine
string outputPath = @"C:\Temp\DataTableWithStyleArray.xlsx";

// Ensure the directory exists (optional safety check)
System.IO.Directory.CreateDirectory(System.IO.Path.GetDirectoryName(outputPath)!);

// Save the workbook
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

> **Tips:** Om du behöver strömma filen (t.ex. för ett web‑API), använd `workbook.Save(stream, SaveFormat.Xlsx)` istället för en filsökväg.

---

## Fullständigt fungerande exempel

Nedan är det kompletta programmet som du kan klistra in i ett nytt konsolprojekt. Det kompileras och körs som det är, och producerar en stylad Excel‑fil.

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1 – Get data
            DataTable dataTable = GetSampleData();

            // Step 2 – Create workbook & worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // Step 3 – Prepare column styles
            Style[] columnStyles = new Style[3];

            // Font style for first column (blue, bold)
            columnStyles[0] = workbook.CreateStyle();
            columnStyles[0].Font.Color = System.Drawing.Color.Blue;
            columnStyles[0].Font.IsBold = true;

            // Background style for second column (light yellow)
            columnStyles[1] = workbook.CreateStyle();
            columnStyles[1].ForegroundColor = System.Drawing.Color.LightYellow;
            columnStyles[1].Pattern = BackgroundType.Solid;

            // Currency format for third column (custom number format excel)
            columnStyles[2] = workbook.CreateStyle();
            columnStyles[2].Custom = "$#,##0.00";

            // Step 4 – Import data with styles
            worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

            // Step 5 – Save as XLSX
            string outputPath = @"C:\Temp\DataTableWithStyleArray.xlsx";
            System.IO.Directory.CreateDirectory(System.IO.Path.GetDirectoryName(outputPath)!);
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }

        // Helper method to build a demo DataTable
        static DataTable GetSampleData()
        {
            var table = new DataTable("Sales");
            table.Columns.Add("Product", typeof(string));
            table.Columns.Add("Quantity", typeof(int));
            table.Columns.Add("Revenue", typeof(decimal));

            table.Rows.Add("Widget A", 120, 3450.75m);
            table.Rows.Add("Widget B", 85, 2190.00m);
            table.Rows.Add("Widget C", 60, 1580.40m);

            return table;
        }
    }
}
```

### Förväntat resultat

När du öppnar `DataTableWithStyleArray.xlsx` kommer du att se:

| **Product** (blue, bold) | **Quantity** (light‑yellow) | **Revenue** (currency) |
|--------------------------|-----------------------------|------------------------|
| Widget A                 | 120                         | $3,450.75              |
| Widget B                 | 85                          | $2,190.00              |
| Widget C                 | 60                          | $1,580.40              |

Det **custom number format excel** du specificerade (`$#,##0.00`) säkerställer att varje intäktscell visar ett dollartecken, tusentalsavgränsare och två decimaler—precis vad finansavdelningar förväntar sig.

---

## Vanliga frågor & specialfall

### Kan jag använda detta med ett annat Excel‑bibliotek?

Absolut. Konceptet—att skapa en stil per kolumn och applicera den under import—översätts till EPPlus, ClosedXML eller NPOI. API‑anropen skiljer sig, men mönstret förblir detsamma.

### Vad händer om min DataTable har fler kolumner än stilar?

Aspose kommer att applicera standardstilen på varje kolumn utan motsvarande post i `columnStyles`‑arrayen. För att undvika överraskningar, antingen storleksanpassa arrayen till `dataTable.Columns.Count` eller generera stilar dynamiskt i en loop.

### Hur sätter jag ett anpassat talformat för datum?

Ställ bara in `style.Custom = "dd‑mm‑yyyy"` (eller någon giltig Excel‑formatsträng). Samma array‑baserade metod fungerar för datum, procenttal eller vetenskaplig notation.

### Finns det ett sätt att automatiskt anpassa kolumnbredder efter import?

Ja—anropa `worksheet.AutoFitColumns();` efter importen. Det kör en snabb breddberäkning baserad på cellinnehållet.

### Vad händer med stora dataset (100 000+ rader)?

`ImportDataTable` är optimerad för bulkoperationer, men du kan stöta på minnesgränser. I så fall, överväg att strömma rader manuellt med `Cells[i, j].PutValue(...)` och återanvända ett enda `Style`‑objekt för att minska overhead.

---

## Proffstips & vanliga fallgropar

- **Undvik att hårdkoda sökvägar** i produktionskod; använd `Environment.GetFolderPath` eller konfigurationsinställningar.  
- **Disposera arbetsboken** om du kör i en långlivad tjänst—omslut den i ett `using`‑block för att frigöra inhemska resurser.  
- **Var uppmärksam på kulturspecifika avgränsare**. Det anpassade formatet `$#,##0.00` tvingar en punkt som decimalavgränsare oavsett OS‑lokal, vilket vanligtvis är önskvärt för finansiella rapporter.  
- **Kom ihåg att referera System.Drawing** (eller `System.Drawing.Common` på .NET Core) för färgstrukturerna som används i styling.  
- **Testa utdata i olika Excel‑versioner**; äldre versioner kan tolka vissa anpassade format lite annorlunda.

---

## Slutsats

Vi har gått igenom allt du behöver för att **custom number format excel**‑filer från C#: hämta data från en `DataTable`, **import datatable to excel**, applicera en **set column background color**, använda **format column as currency**, och slutligen **save workbook as x

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}