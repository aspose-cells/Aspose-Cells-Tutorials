---
category: general
date: 2026-03-18
description: Hur man exporterar Excel-data till en DataTable i C# med kod som hanterar
  specifika celler, konverterar Excel till DataTable och formaterar tal. Lär dig att
  exportera specifika celler och mer.
draft: false
keywords:
- how to export excel
- convert excel to datatable
- export specific cells
- excel to datatable c#
- excel range to datatable
language: sv
og_description: Hur man exporterar Excel-data till en DataTable i C#. Denna handledning
  visar hur man exporterar specifika celler, konverterar Excel till DataTable och
  formaterar siffror enkelt.
og_title: Hur man exporterar Excel till en DataTable i C# – Komplett guide
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
title: Hur man exporterar Excel till en DataTable i C# – Steg‑för‑steg‑guide
url: /sv/net/excel-data-import-export/how-to-export-excel-to-a-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man exporterar Excel till en DataTable i C# – Steg‑för‑steg‑guide

Har du någonsin undrat **hur man exporterar Excel**-data till en `DataTable` utan att förlora formatering? Du är inte ensam—utvecklare behöver ständigt hämta en del av ett kalkylblad till minnet för rapportering, validering eller bulk‑insert‑operationer. Den goda nyheten? Med några rader C# kan du exportera ett exakt område (t.ex. *A1:F11*), tvinga varje cell att behandlas som en sträng och till och med tillämpa ett anpassat talformat.

I den här handledningen går vi igenom allt du behöver veta: från att ladda arbetsboken, konfigurera **exportera specifika celler**, konvertera området till en `DataTable` och hantera kantfall som tomma rader eller lokalanpassade tal. I slutet har du en återanvändbar metod som fungerar med **excel to datatable c#**-scenarier i produktionskod.

> **Förutsättningar** – Du behöver Aspose.Cells for .NET‑biblioteket (eller något liknande API som erbjuder `ExportDataTable`). Exemplet förutsätter .NET 6+, men koncepten gäller även för tidigare versioner.

---

## Vad du kommer att lära dig

- Hur man **konverterar Excel till DataTable** med Aspose.Cells.
- Exportera ett anpassat område (`excel range to datatable`) medan alla värden behandlas som strängar.
- Tillämpa ett talformat med två decimaler (`#,#00.00`) vid export.
- Vanliga fallgropar (null‑rader, dolda kolumner) och hur man undviker dem.
- Ett färdigt att kopiera, fullt körbart kodexempel.

## Förutsättningar och installation

Innan vi dyker ner i koden, se till att du har:

1. **Aspose.Cells for .NET** installerat via NuGet:

   ```bash
   dotnet add package Aspose.Cells
   ```

2. En Excel‑fil (`input.xlsx`) placerad i en mapp du kan referera till, t.ex. `YOUR_DIRECTORY/input.xlsx`.
3. Ett projekt som riktar sig mot .NET 6 eller senare (`using`‑satserna nedan fungerar direkt).

> **Proffstips:** Om du använder ett annat bibliotek (t.ex. EPPlus eller ClosedXML) är konceptet detsamma—ladda arbetsboken, välj ett område och anropa en metod som returnerar en `DataTable`.

## Steg 1: Ladda arbetsboken och hämta det första kalkylbladet

Det första du behöver är ett `Workbook`‑objekt som representerar din Excel‑fil. När du har det kan du komma åt vilket kalkylblad som helst via index eller namn.

```csharp
using Aspose.Cells;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // Load the workbook from disk
            Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

            // Grab the first worksheet (index 0)
            Worksheet worksheet = workbook.Worksheets[0];

            // Continue with export options...
        }
    }
}
```

**Varför detta är viktigt:** Att ladda arbetsboken tidigt låter dig inspektera dess struktur (dolda blad, skydd) innan du bestämmer vilka celler som ska exporteras. Om filen är stor, överväg att använda `LoadOptions` för att strömma endast de delar som behövs.

## Steg 2: Konfigurera exportalternativ – Behandla alla värden som strängar

När du exporterar data för efterföljande bearbetning (t.ex. bulk‑insert i SQL) vill du ofta ha en **konsekvent strängrepresentation**. Detta undviker typ‑mismatch‑fel senare.

```csharp
// Configure export behavior
ExportTableOptions exportOptions = new ExportTableOptions
{
    // Force every cell to be returned as a string, regardless of its original type
    ExportAsString = true,

    // Apply a two‑decimal‑place format to numeric cells
    NumberFormat = "#,##0.00"
};
```

**Förklaring:**  
- `ExportAsString = true` instruerar Aspose.Cells att ignorera den inbyggda celltypen och returnera den formaterade texten.  
- `NumberFormat = "#,##0.00"` säkerställer att tal som `1234.5` blir `"1,234.50"`—användbart för finansiella rapporter.

Om du behöver de ursprungliga datatyperna, sätt helt enkelt `ExportAsString` till `false` och hantera konverteringen själv.

## Steg 3: Exportera ett specifikt område (A1:F11) till en DataTable

Nu kommer kärnan i **exportera specifika celler**. Metoden `ExportDataTable` tar start-/slutrad‑/kolumnindex (noll‑baserade) plus en flagga för inkludering av rubrik.

```csharp
// Export cells A1:F11 (rows 0‑10, columns 0‑5) including the header row
DataTable table = worksheet.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    endRow: 10,
    endColumn: 5,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

**Vad du får:** En `DataTable` med 11 rader (inklusive rubriken) och 6 kolumner (`A`‑`F`). Alla värden är strängar formaterade enligt `exportOptions`.

## Steg 4: Verifiera resultatet – Skriv ut till konsolen

Det är alltid en bra idé att göra en snabbkontroll av resultatet innan du överlämnar tabellen till en annan komponent.

```csharp
// Simple console dump
foreach (DataRow row in table.Rows)
{
    foreach (var item in row.ItemArray)
    {
        Console.Write($"{item}\t");
    }
    Console.WriteLine();
}
```

Du bör se något liknande:

```
Id      Name        Qty     Price   Total   Date
1       Widget A    10      2.50    25.00   2026-01-01
2       Widget B    5       3.75    18.75   2026-01-02
...
```

Lägg märke till hur de numeriska kolumnerna visar två decimaler, exakt som vi specificerade.

## Fullt fungerande exempel (klara att kopiera‑klistra in)

Nedan är det kompletta programmet som binder ihop allt. Klistra in det i ett nytt konsolprojekt, justera filvägen och kör—ingen extra konfiguration behövs.

```csharp
using Aspose.Cells;
using System;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // 1️⃣ Load workbook and select worksheet
            // -------------------------------------------------
            string filePath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(filePath);
            Worksheet worksheet = workbook.Worksheets[0];

            // -------------------------------------------------
            // 2️⃣ Set export options – strings + number format
            // -------------------------------------------------
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                NumberFormat = "#,##0.00"
            };

            // -------------------------------------------------
            // 3️⃣ Export range A1:F11 (rows 0‑10, cols 0‑5)
            // -------------------------------------------------
            DataTable table = worksheet.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                endRow: 10,
                endColumn: 5,
                includeColumnNames: true,
                exportOptions: exportOptions);

            // -------------------------------------------------
            // 4️⃣ Output to console for verification
            // -------------------------------------------------
            Console.WriteLine("=== Exported DataTable ===");
            foreach (DataRow row in table.Rows)
            {
                foreach (var cell in row.ItemArray)
                {
                    Console.Write($"{cell}\t");
                }
                Console.WriteLine();
            }

            // Keep console window open
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Viktiga insikter från koden:**  
- Objektet `ExportTableOptions` är återanvändbart; du kan skicka det till flera `ExportDataTable`‑anrop om du behöver exportera flera områden.  
- Indexering börjar på **0**, så `A1` motsvarar `(0,0)`.  
- Genom att sätta `includeColumnNames` till `true` används automatiskt den första raden som kolumnrubriker—perfekt för efterföljande `DataTable`‑operationer.

## Hantera kantfall & vanliga frågor

### Vad händer om kalkylbladet har dolda rader eller kolumner?

Aspose.Cells respekterar synlighet som standard. Om du behöver exportera dold data, sätt `exportOptions.ExportHiddenRows = true` och `ExportHiddenColumns = true`.

### Min Excel‑fil innehåller formler—får jag de beräknade värdena?

Ja. Som standard returnerar `ExportDataTable` det **visade värdet** (formelns resultat). Om du vill ha den råa formeltexten, sätt `exportOptions.ExportFormulas = true`.

### Hur hoppar jag över helt tomma rader?

Efter exporten kan du rensa `DataTable`:

```csharp
foreach (DataRow row in table.Rows.Cast<DataRow>()
                                   .Where(r => r.ItemArray.All(c => c == DBNull.Value || string.IsNullOrWhiteSpace(c.ToString()))).ToList())
{
    table.Rows.Remove(row);
}
```

### Kan jag exportera ett icke‑sammanhängande område (t.ex. A1:B5 och D1:E5)?

Aspose.Cells stödjer inte disjunkta områden i ett enda anrop. Exportera istället varje block separat och slå sedan ihop de resulterande `DataTable`‑erna manuellt.

## Prestandatips

- **Återanvänd `ExportTableOptions`** för flera exporteringar; att skapa en ny instans varje gång ger försumbar overhead men rör till koden.
- **Strömma stora filer** med `LoadOptions` för att undvika att ladda hela arbetsboken i minnet.
- **Undvik `DataTable`** om du bara behöver en snabb CSV‑export—`ExportDataTable` är bekvämt men inte det mest minnes‑effektiva för enorma blad.

## Slutsats

Vi har gått igenom **hur man exporterar Excel**‑data till en `DataTable` samtidigt som vi styr formatering, hanterar specifika cellområden och säkerställer att varje värde kommer som en sträng. Det kompletta exemplet visar ett rent, produktionsklart tillvägagångssätt som du kan anpassa för **convert excel to datatable**, **export specific cells**, eller vilket **excel range to datatable**‑scenario du än stöter på.

Var inte rädd för att experimentera: ändra området, växla `ExportAsString`, eller skicka `DataTable` direkt till Entity Framework för bulk‑insert. Himlen är gränsen när du har detta solida fundament.

### Nästa steg & relaterade ämnen

- **Importera DataTable tillbaka till Excel** – lär dig den omvända operationen med `ImportDataTable`.
- **Bulk‑insert av en DataTable i SQL Server** – använd `SqlBulkCopy` för blixtsnabba laddningar.
- **Arbeta med EPPlus eller ClosedXML** – se hur samma uppgift ser ut med alternativa bibliotek.
- **Formatera celler vid export** – utforska `ExportTableOptions` ytterligare för datumformat, anpassade kultursättningar och mer.

Har du frågor eller ett annat användningsfall? Lämna en kommentar, så fortsätter vi samtalet. Lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}