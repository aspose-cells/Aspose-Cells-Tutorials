---
category: general
date: 2026-03-22
description: Hur man exporterar Excel med formatering och bevarar talformat. Lär dig
  att konvertera Excel‑område, hämta formelresultat och exportera Excel med formatering
  med hjälp av Aspose.Cells.
draft: false
keywords:
- how to export excel
- preserve number format
- convert excel range
- get formula result
- export excel with formatting
language: sv
og_description: Hur man exporterar Excel med formatering och bevarar talformat. Steg‑för‑steg‑guide
  för att konvertera Excel‑område, hämta formelresultat och exportera Excel med formatering
  i C#.
og_title: Hur man exporterar Excel med formatering – Bevara talformat
tags:
- C#
- Aspose.Cells
- Excel automation
title: Hur man exporterar Excel med formatering – bevara talformat
url: /sv/net/number-and-display-formats-in-excel/how-to-export-excel-with-formatting-preserve-number-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man exporterar Excel med formatering – bevara talformat

Har du någonsin funderat **hur man exporterar Excel**‑data samtidigt som varje cells utseende behålls exakt som du ser det i arbetsboken? Kanske behöver du skicka en rapport till en kund, fylla ett rutnät‑kontroll eller bara lagra värdena i en databas. Smärtan är oftast att talformatet går förlorat eller att formler blir till rena strängar.  

I den här handledningen går vi igenom ett komplett, färdigt C#‑exempel som **bevarar talformat**, **konverterar ett Excel‑område** till en `DataTable`, **hämtar formelresultatet**, och slutligen **exporterar Excel med formatering** med Aspose.Cells. I slutet har du en enda metod som du kan klistra in i vilket projekt som helst och anropa med en arbetsbladsreferens.

> **Snabb förhandsgranskning:** koden skapar en arbetsbok, skriver ett värde och en formel, säger åt Aspose.Cells att exportera cellerna som formaterade strängar, och skriver ut `123.456 | 246.912` – exakt vad du förväntar dig att se i Excel.

---

## Vad du behöver

- **Aspose.Cells for .NET** (gratis provversion räcker för inlärning)
- .NET 6.0 eller senare (API‑et är detsamma på .NET Framework)
- En grundläggande C#‑utvecklingsmiljö (Visual Studio, VS Code, Rider… du bestämmer)

Inga extra NuGet‑paket utöver Aspose.Cells krävs. Om du inte har installerat det ännu, kör:

```bash
dotnet add package Aspose.Cells
```

---

## Steg 1 – Skapa en arbetsbok och skriv värden (inklusive en formel)

Först startar vi en ny arbetsbok och lägger in ett numeriskt värde i **A1**. Sedan lägger vi till en enkel formel i **B1** som multiplicerar den första cellen med två. Detta förbereder demonstrationen av **get formula result** senare.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExportExcelDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and get its first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write a numeric value and a formula that uses it
        worksheet.Cells["A1"].PutValue(123.456);
        worksheet.Cells["B1"].PutFormula("=A1*2");

        // Continue with export options...
        ExportRangeAsDataTable(worksheet);
    }
}
```

**Varför detta är viktigt:**  
- `PutValue` lagrar det råa talet, medan `PutFormula` lagrar beräkningen.  
- Aspose.Cells håller formeln **levande**, så när vi senare frågar efter cellens värde får vi faktiskt `246.912`, inte strängen `"=A1*2"`.

---

## Steg 2 – Berätta för Aspose.Cells att exportera värden som formaterade strängar

Om du bara anropar `ExportDataTable` med standardinställningar returneras numeriska celler som deras underliggande `double`‑värden. Det tar bort tusentalsavgränsare, valutasymboler eller anpassade decimalplatser du eventuellt har ställt in. Klassen `ExportTableOptions` låter oss **bevara talformat** och **exportera som sträng**.

```csharp
static void ExportRangeAsDataTable(Worksheet worksheet)
{
    // Step 2: Set export options to retrieve values as formatted strings
    ExportTableOptions exportOptions = new ExportTableOptions
    {
        ExportAsString = true,          // Return values as strings
        ExportNumberFormat = true      // Preserve the cell's number format
    };

    // Step 3: Export the range A1:B1 to a DataTable
    DataTable dataTable = worksheet.Cells.ExportDataTable(
        firstRow: 0,
        firstColumn: 0,
        totalRows: 1,
        totalColumns: 2,
        includeColumnNames: true,
        options: exportOptions);

    PrintDataTable(dataTable);
}
```

**Viktig punkt:** `ExportNumberFormat = true` är flaggan som får **preserve number format** att fungera. Utan den ser du `"123.456"` och `"246.912"` som råa tal, vilket kan se okej ut i kod men inte när du klistrar in data i ett UI som förväntar sig samma formatering som i Excel.

---

## Steg 3 – Skriv ut den exporterade datan (verifiering)

Nu när vi har en `DataTable` full av formaterade strängar, låt oss dumpa innehållet till konsolen. Detta visar också att vi framgångsrikt **get formula result** utan att själva utvärdera formeln.

```csharp
static void PrintDataTable(DataTable table)
{
    // Step 4: Print the exported values (already formatted)
    foreach (DataRow row in table.Rows)
    {
        // The output will look like: 123.456 | 246.912
        Console.WriteLine($"{row[0]} | {row[1]}");
    }
}
```

När programmet körs skrivs ut:

```
123.456 | 246.912
```

Lägg märke till hur den andra kolumnen visar **formelresultatet**, inte formeltexten. Det är exakt vad du behöver när du **exporterar Excel med formatering** för vidare bearbetning.

---

## Steg 4 – Konvertera större Excel‑områden (valfritt)

Exemplet ovan hanterar en liten `A1:B1`‑slice, men i verkligheten krävs ofta export av hela tabeller. Samma metod fungerar för vilket rektangulärt block som helst – justera bara argumenten `firstRow`, `firstColumn`, `totalRows` och `totalColumns`.

```csharp
// Example: Export a 10‑row by 5‑column block starting at C3
DataTable bigTable = worksheet.Cells.ExportDataTable(
    firstRow: 2,          // Zero‑based index (C3 = row 2, column 2)
    firstColumn: 2,
    totalRows: 10,
    totalColumns: 5,
    includeColumnNames: true,
    options: exportOptions);
```

**Proffstips:** Om ditt blad redan har en rubrikrad, sätt `includeColumnNames` till `true`. Aspose.Cells använder då den första raden i området som kolumnnamn, vilket är praktiskt när du senare binder `DataTable` till ett UI‑rutnät.

---

## Steg 5 – Vanliga fallgropar & hur du undviker dem

| Problem | Varför det händer | Lösning |
|---------|-------------------|---------|
| **Tal förlorar kommatecken eller valutasymboler** | `ExportAsString` är `false` eller `ExportNumberFormat` saknas | Sätt både `ExportAsString = true` **och** `ExportNumberFormat = true`. |
| **Formelceller returnerar formeltexten** | Du anropade inte `CalculateFormula` före export (endast behövs om arbetsboken inte är satt till auto‑calculate) | Aktivera auto‑calculate (`workbook.CalculateFormula()`) eller förlita dig på `ExportAsString` som tvingar utvärdering. |
| **Rubriker visas som datarader** | `includeColumnNames` är `false` medan ditt område innehåller en rubrikrad | Sätt `includeColumnNames = true` för att behandla den första raden som kolumnnamn. |
| **Stora områden ger minnespress** | Export av hela bladet på en gång laddar allt i minnet | Exportera i delar (t.ex. 500 rader åt gången) och slå ihop `DataTable`s vid behov. |

---

## Steg 6 – Fullt fungerande exempel (Kopiera‑klistra‑klart)

Nedan är hela programmet, från `using`‑satser till `Main`. Klistra in det i en konsolapp och tryck **F5** – du ser den formaterade utskriften omedelbart.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExportExcelDemo
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate cells
        worksheet.Cells["A1"].PutValue(123.456);
        worksheet.Cells["B1"].PutFormula("=A1*2");

        // Export options: keep formatting and return strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            ExportNumberFormat = true
        };

        // Export A1:B1 as a DataTable
        DataTable dataTable = worksheet.Cells.ExportDataTable(
            firstRow: 0,
            firstColumn: 0,
            totalRows: 1,
            totalColumns: 2,
            includeColumnNames: true,
            options: exportOptions);

        // Print results
        foreach (DataRow row in dataTable.Rows)
        {
            Console.WriteLine($"{row[0]} | {row[1]}"); // Expected: "123.456 | 246.912"
        }

        // Keep console window open
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

**Förväntad utskrift**

```
123.456 | 246.912

Press any key to exit...
```

Det är hela **hur man exporterar Excel**‑arbetsflödet, med formatering intakt, formelresultat utvärderade och en ren `DataTable` klar för vilken .NET‑konsument som helst.

---

## Slutsats

Vi har gått igenom allt du behöver veta om **hur man exporterar Excel**‑data samtidigt som du **bevarar talformat**, **konverterar ett Excel‑område** till en `DataTable`, och **hämtar formelresultat** utan extra parsning. Nyckeln är konfigurationen av `ExportTableOptions` – när du sätter `ExportAsString` och `ExportNumberFormat` till `true` sköter Aspose.Cells det tunga lyftet åt dig.

Från här kan du:

- Koppla `DataTable` till ett WPF `DataGrid` eller en ASP.NET MVC‑vy.  
- Skriva tabellen till en CSV‑fil medan du behåller den exakta visuella representationen.  
- Utöka metoden till flera blad eller dynamiska områden.

Känn dig fri att experimentera med olika format (valuta, procent) och större datamängder. Om du stöter på några konstigheter, gå tillbaka till tabellen **vanliga fallgropar** – den täcker de mest frekventa hindren när du **exporterar Excel med formatering**.

Lycka till med kodandet, och må dina exporterade kalkylblad alltid se lika polerade ut som originalen!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}