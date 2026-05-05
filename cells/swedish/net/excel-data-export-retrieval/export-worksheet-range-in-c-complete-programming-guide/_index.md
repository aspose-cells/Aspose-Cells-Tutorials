---
category: general
date: 2026-05-04
description: Exportera arbetsbladsområde med C# och anpassad formatering. Lär dig
  hur du exporterar ett Excel‑område och hur du anpassar cellexport i några enkla
  steg.
draft: false
keywords:
- export worksheet range
- how to export excel range
- how to customize cell export
- C# Excel export
- worksheet export options
language: sv
og_description: Exportera arbetsbladområde med C#. Den här guiden visar hur du exporterar
  ett Excel‑område och anpassar cellexport snabbt och pålitligt.
og_title: Exportera arbetsbladsområde i C# – Komplett programmeringsguide
tags:
- C#
- Excel
- Data Export
title: Exportera arbetsbladsområde i C# – Komplett programmeringsguide
url: /sv/net/excel-data-export-retrieval/export-worksheet-range-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exportera kalkylbladsintervall i C# – Komplett programmeringsguide

Har du någonsin behövt **exportera kalkylbladsintervall** men standardutdata var inte vad du ville ha? Du är inte ensam – många utvecklare stöter på samma hinder när de försöker dra ett block med celler till en CSV‑ eller JSON‑fil. Den goda nyheten? Med några få rader C# kan du inte bara **exportera excel‑intervall** utan också **anpassa cellexport** så att den matchar vilket efterföljande format som helst.

I den här handledningen går vi igenom ett verkligt scenario: att ta cellerna *A1:D10* från en Excel‑arbetsbok, omvandla varje värde till en sträng i hakparenteser och skriva resultatet till en fil. När du är klar vet du exakt **hur du exporterar kalkylbladsintervall** med full kontroll över varje cells representation, samt ett antal tips för kantfall du kan stöta på senare.

## Vad du behöver

- .NET 6 eller senare (koden fungerar även med .NET Framework 4.7+)  
- NuGet‑paketet **GemBox.Spreadsheet** (eller vilket bibliotek som helst som erbjuder `ExportTableOptions`; API‑exemplet är från GemBox)  
- Grundläggande förståelse för C#‑syntax – inget avancerat, bara vanliga `using`‑satser och objekt‑instansering  

Om du har detta är du redo att dyka in.

## Steg 1: Ställ in exportalternativen – primär kontrollpunkt  

Det första du gör är att skapa en `ExportTableOptions`‑instans och tala om för den att behandla varje cell som en sträng. Detta är grunden för **hur du exporterar excel‑intervall** samtidigt som datatypen hålls konsekvent.

```csharp
using GemBox.Spreadsheet;

public class WorksheetExporter
{
    public void ExportRange(string sourcePath, string destinationPath)
    {
        // Load the workbook.
        var workbook = ExcelFile.Load(sourcePath);
        var worksheet = workbook.Worksheets[0]; // assume first sheet

        // Step 1: Create export options and enable string export.
        var exportOptions = new ExportTableOptions
        {
            ExportAsString = true // forces every cell to be exported as text
        };
```

*Varför tvinga sträng‑export?*  
När du senare anpassar varje cell kommer du att injicera hakparenteser och eventuellt andra symboler. Att hålla allt som en sträng förhindrar överraskningar vid typkonvertering (t.ex. datum som blir till serienummer).

## Steg 2: Haka in i CellExport‑händelsen – anpassa varje cell  

Nu kommer den roliga delen: **hur du anpassar cellexport**. GemBox utlöser en `CellExport`‑händelse för varje cell som är på väg att skrivas. Genom att hantera den kan du omsluta värdet i hakparenteser, lägga till ett prefix eller till och med hoppa över en cell helt.

```csharp
        // Step 2: Customize each cell's exported value.
        exportOptions.CellExport += (sender, e) =>
        {
            // e.Value holds the original cell content.
            // We'll wrap it in square brackets.
            e.Value = $"[{e.Value}]";
        };
```

*Pro‑tips:* Om du bara vill modifiera numeriska celler, kontrollera `e.Value.GetType()` innan du applicerar hakparenteserna. Det lilla skyddet kan rädda dig från att oavsiktligt förstöra rubriktext.

## Steg 3: Exportera det önskade intervallet – kärnhandlingen  

Med alternativen klara anropar du `ExportTable`. Metoden tar den arbetsbok du laddat, adressen på intervallet du vill ha och de alternativ du just konfigurerat.

```csharp
        // Step 3: Export the range A1:D10 using the configured options.
        worksheet.ExportTable(workbook, "A1:D10", exportOptions, destinationPath);
    }
}
```

Överlagringen vi använde skriver direkt till en fil (CSV som standard). Om du föredrar en sträng i minnet, byt ut det sista argumentet mot en `StringWriter` och läs resultatet efteråt.

### Fullt fungerande exempel

Nedan är en fristående konsolapp som du kan klistra in i ett nytt projekt och köra direkt (byt bara ut filsökvägarna).

```csharp
using System;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // License key (free version works with limited rows/columns).
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        var exporter = new WorksheetExporter();
        exporter.ExportRange(
            sourcePath: @"C:\Temp\Sample.xlsx",
            destinationPath: @"C:\Temp\ExportedRange.csv");

        Console.WriteLine("Export completed. Check C:\\Temp\\ExportedRange.csv");
    }
}
```

**Förväntad output (CSV‑snippet):**

```
[Header1],[Header2],[Header3],[Header4]
[123],[456],[789],[012]
[ABC],[DEF],[GHI],[JKL]
...
```

Varje cell från *A1* till *D10* är nu omsluten av hakparenteser, exakt som vi definierade i `CellExport`‑hanteraren.

## Hantera vanliga kantfall  

### 1. Tomma celler  
Om en cell är tom blir `e.Value` `null`. Att försöka formatera den med stränginterpolering kastar ett undantag. Skydda mot detta:

```csharp
exportOptions.CellExport += (s, e) =>
{
    var raw = e.Value?.ToString() ?? string.Empty;
    e.Value = $"[{raw}]";
};
```

### 2. Stora intervall  
Att exportera miljontals rader kan nå minnesgränser. I sådant scenario bör du strömma utdata istället för att ladda hela arbetsboken i minnet:

```csharp
using (var writer = new StreamWriter(destinationPath))
{
    worksheet.ExportTable(workbook, "A1:D1000000", exportOptions, writer);
}
```

### 3. Olika avgränsare  
CSV är inte det enda format du kan behöva. Ändra avgränsaren genom att justera `ExportTableOptions.CsvSeparator`:

```csharp
exportOptions.CsvSeparator = '\t'; // Tab‑delimited
```

## Vanliga frågor  

**Q: Fungerar detta med .xlsx‑filer skapade av Excel 365?**  
Absolut. GemBox läser det moderna OpenXML‑formatet utan extra konfiguration.

**Q: Kan jag exportera flera icke‑sammanhängande intervall på en gång?**  
Inte direkt via ett enda `ExportTable`‑anrop. Loopa över varje intervallsträng (`"A1:D10"`, `"F1:H5"` osv.) och slå ihop resultaten själv.

**Q: Vad händer om jag behöver applicera olika formatering per kolumn?**  
I `CellExport`‑hanteraren har du tillgång till `e.ColumnIndex`. Använd en `switch`‑sats för att tillämpa kolumnspecifik logik.

## Avslutning  

Vi har gått igenom **hur du exporterar kalkylbladsintervall** med full kontroll över varje cells utseende, demonstrerat **hur du exporterar excel‑intervall** med `ExportTableOptions` och visat **hur du anpassar cellexport** via `CellExport`‑händelsen. Den kompletta lösningen ryms i några dussin rader C#, men är ändå flexibel nog för produktionsscenarier.

Nästa steg? Prova att byta ut hakparentes‑omslaget mot ett JSON‑vänligt format, eller experimentera med villkorlig logik som hoppar över dolda rader. Du kan också utforska export direkt till en `MemoryStream` för webb‑API‑svar – utan temporära filer.

Om du har följt med har du nu ett robust, återanvändbart mönster för att exportera vilket kalkylbladsintervall som helst exakt på det sätt du behöver. Lycka till med kodandet, och lämna gärna en kommentar om du stöter på problem!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}