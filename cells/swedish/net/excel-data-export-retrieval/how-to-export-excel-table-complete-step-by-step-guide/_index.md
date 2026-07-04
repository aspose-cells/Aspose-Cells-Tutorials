---
category: general
date: 2026-07-03
description: Lär dig hur du exporterar en Excel‑tabell till en .txt‑fil och sparar
  en Excel‑tabell till .txt‑fil med C#. Exportera Excel‑data som vanlig text med ett
  komplett kodexempel.
draft: false
keywords:
- how to export excel table
- save excel table to .txt file
- export excel data as plain text
- Aspose.Cells export table
- C# Excel to text
language: sv
og_description: Hur man exporterar Excel‑tabell som ren text. Den här guiden visar
  hur du exporterar Excel‑data som ren text och sparar Excel‑tabellen i en .txt‑fil
  med Aspose.Cells.
og_title: Hur man exporterar en Excel‑tabell – Fullständig C#‑handledning
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Learn how to export Excel table to a .txt file and save Excel table
    to .txt file using C#. Export Excel data as plain text with full code example.
  headline: How to Export Excel Table – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- C#
- Excel
- Aspose.Cells
- File I/O
title: Hur man exporterar Excel‑tabell – Komplett steg‑för‑steg‑guide
url: /sv/net/excel-data-export-retrieval/how-to-export-excel-table-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Så exporterar du Excel‑tabell – Komplett steg‑för‑steg‑guide

Har du någonsin undrat **how to export Excel table** utan att ladda hela arbetsboken i minnet? Du är inte ensam. I många automatiseringsjobb accepterar det nedströms systemet bara en enkel `.txt`‑fil, så du behöver **save Excel table to .txt file** snabbt och pålitligt.  

I den här handledningen går vi igenom en ren C#‑lösning som **exports Excel data as plain text** med Aspose.Cells. I slutet har du ett färdigt program, förstår varför varje rad är viktig och ser hur du kan finjustera exporten för dina egna edge cases.

## Vad du behöver

- **Aspose.Cells for .NET** (any recent version, e.g., 23.12).  
- .NET 6 SDK eller senare – koden kompileras även med .NET Core.  
- En exempel‑fil `input.xlsx` som innehåller minst en Excel‑tabell.  
- En textredigerare eller IDE (Visual Studio, VS Code, Rider… du väljer).

Inga extra NuGet‑paket utöver Aspose.Cells behövs, och hela processen körs på Windows, Linux eller macOS.

## Steg 1: Ställ in projektet och importerna

Först, skapa en konsolapp och importera de nödvändiga namnutrymmena.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelTableExport
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll place the export logic here.
        }
    }
}
```

> **Pro tip:** Om du använder .NET‑CLI, kör `dotnet new console -n ExcelTableExport` och sedan `dotnet add package Aspose.Cells` innan du klistrar in koden ovan.

## Steg 2: Läs in arbetsboken och hämta det första kalkylbladet

Workbook‑objektet representerar hela Excel‑filen. Att läsa in den en gång håller minnesanvändningen låg.

```csharp
// Step 2: Load the workbook and get the first worksheet
Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");
Worksheet ws = wb.Worksheets[0];
```

Varför väljer vi det första kalkylbladet? I många genererade rapporter finns data på det första bladet, men du kan ändra indexet eller använda `wb.Worksheets["SheetName"]` för ett namngivet blad.

## Steg 3: Hämta den första tabellen som definierats på kalkylbladet

Excel‑tabeller (ListObjects) ger oss strukturerad data, vilket gör exporten förutsägbar.

```csharp
// Step 3: Retrieve the first table defined on the worksheet
Table tbl = ws.Tables[0];
```

Om din arbetsbok innehåller flera tabeller, iterera helt enkelt `ws.Tables` eller välj med `tbl.Name`.

## Steg 4: Konfigurera exportalternativ – Exportera varje cell som en sträng

Aspose.Cells låter dig kontrollera formatet för varje cell under export. Att sätta `ExportAsString` säkerställer att tal, datum och formler blir ren text.

```csharp
// Step 4: Set up export options – export every cell as a string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true
};
```

### Lägg till en anpassad exportåtgärd för att trimma blanksteg

Ofta innehåller källdata inledande eller avslutande mellanslag. Att trimma dem gör den slutgiltiga `.txt`‑filen renare.

```csharp
// Define a custom export action to trim cell values before writing
exportOptions.CustomExport = (cell, writer) =>
{
    writer.Write(cell.StringValue.Trim());
};
```

Lambda‑funktionen får `Cell`‑objektet och en `TextWriter`. Du kan också lägga till villkorlig logik här—t.ex. ersätta kommatecken med semikolon för CSV‑liknande output.

## Steg 5: Exportera tabellen med start i cell A1 till en textfil

Nu skriver vi faktiskt tabellen till disk. Metoden `ExportTable` går igenom tabellen rad för rad och tillämpar de alternativ vi just definierade.

```csharp
// Step 5: Export the table starting at cell A1 to a text file
using (StreamWriter writer = new StreamWriter("YOUR_DIRECTORY/Table.txt"))
{
    ws.Cells.ExportTable(tbl, "A1", exportOptions, writer);
}
```

**Vad du kommer att se:** Varje rad i Excel‑tabellen blir en rad i `Table.txt`. Kolumner separeras som standard med ett tab‑tecken (`\t`)—perfekt för nedströms parsning.

### Exempel på förväntad output

Om vi antar att `input.xlsx` innehåller en tabell med tre kolumner (`ID`, `Name`, `Score`) och två datarader, så kommer `Table.txt` att se ut så här:

```
1    Alice    85
2    Bob      92
```

Observera att mellanslagen har trimmats och allt är ren text—precis vad kravet **export excel data as plain text** efterfrågar.

## Hantera vanliga edge cases

| Situation | Vad du gör | Varför |
|-----------|------------|--------|
| **Table has empty cells** | Lambda‑funktionen skriver `cell.StringValue.Trim()` vilket returnerar en tom sträng för tomma celler. | Behåller kolumnjusteringen utan att lägga till oönskade tecken. |
| **You need a custom delimiter** | Ersätt `writer.Write(cell.StringValue.Trim());` med `writer.Write($"{cell.StringValue.Trim()},");` och trimma den avslutande avgränsaren efter varje rad. | Vissa system föredrar kommatecken eller rörtecken istället för tabbar. |
| **Large worksheets ( > 100 k rows )** | Använd `ExportTableOptions` med `ExportAsString = true` och strömma filen som visat; Aspose.Cells bearbetar rader i ett strömningsläge, vilket undviker OOM‑fel. | Säkerställer skalbarhet. |
| **Multiple tables in one sheet** | Loopa över `ws.Tables` och anropa `ExportTable` för varje, eventuellt lägg till en separationsrad mellan exporterna. | Gör att du kan **save Excel table to .txt file** för varje tabell. |

## Fullständigt fungerande exempel

Nedan är det kompletta programmet som du kan kopiera‑klistra in i `Program.cs`. Ersätt `YOUR_DIRECTORY` med en absolut eller relativ sökväg som finns på din maskin.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelTableExport
{
    class Program
    {
        static void Main(string[] args)
        {
            // Load workbook
            Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");
            Worksheet ws = wb.Worksheets[0];

            // Get first table
            if (ws.Tables.Count == 0)
            {
                Console.WriteLine("No tables found on the first worksheet.");
                return;
            }
            Table tbl = ws.Tables[0];

            // Configure export options
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                CustomExport = (cell, writer) =>
                {
                    // Trim whitespace and write value
                    writer.Write(cell.StringValue.Trim());
                }
            };

            // Export to text file
            string outputPath = "YOUR_DIRECTORY/Table.txt";
            using (StreamWriter writer = new StreamWriter(outputPath))
            {
                ws.Cells.ExportTable(tbl, "A1", exportOptions, writer);
            }

            Console.WriteLine($"Table exported successfully to {outputPath}");
        }
    }
}
```

Kör programmet med `dotnet run`. Om allt är korrekt konfigurerat kommer du att se bekräftelsemeddelandet och en nygenererad `Table.txt` som innehåller **export excel data as plain text**.

## Bonus: Visuell bekräftelse (valfritt)

Om du vill se en snabb skärmdump av den resulterande filen kan du öppna den i någon textredigerare. Nedan är en platshållarbild som visar den förväntade layouten.

![how to export excel table screenshot](https://example.com/images/export-excel-table.png "how to export excel table")

*Alt text:* **how to export excel table** – visar ren‑text‑output av en exporterad Excel‑tabell.

## Sammanfattning & nästa steg

Vi har gått igenom allt du behöver veta **how to export Excel table** med Aspose.Cells, från att läsa in arbetsboken till att trimma cellvärden och slutligen skriva en ren `.txt`‑fil.  

- Du förstår nu **save Excel table to .txt file** med anpassad logik.  
- Du kan anpassa lambda‑funktionen för att hantera datum, tal eller egna avgränsare.  
- För större projekt, överväg att paketera logiken i en återanvändbar metod eller klass.

**Vad blir nästa?** Prova att exportera flera tabeller, eller byt utdataformatet till CSV genom att ändra avgränsaren. Du kan också utforska **export excel data as plain text** direkt till en nätverksström för real‑tids‑integrationer.

Har du frågor eller stöter på problem? Lämna en kommentar, och lycka till med kodandet!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [How to Export Excel Files in .NET Using Aspose.Cells: A Comprehensive Guide](/cells/english/net/workbook-operations/export-excel-files-net-aspose-cells-guide/)
- [How to Export Visible Excel Rows Using Aspose.Cells for .NET: A Step-by-Step Guide](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)
- [How to Combine Excel Sheets into a Single Text File Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/combine-excel-sheets-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}