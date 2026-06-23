---
category: general
date: 2026-02-26
description: hur man exporterar Excel till en tab‑avgränsad txt‑fil med C#. Lär dig
  exportera Excel som tab, konvertera Excel till txt och exportera Excel med avgränsare
  i tre enkla steg.
draft: false
keywords:
- how to export excel
- export excel as tab
- convert excel to txt
- export excel with delimiter
- export excel range
language: sv
og_description: hur man exporterar Excel till en flikavgränsad txt‑fil med C#. Denna
  handledning visar hur man exporterar Excel som flik, konverterar Excel till txt
  och exporterar Excel med avgränsare.
og_title: hur man exporterar Excel – guide för tab‑separerad text
tags:
- csharp
- excel
- file-conversion
title: Hur man exporterar Excel – Guide för tabbavgränsad text
url: /sv/net/converting-excel-files-to-other-formats/how-to-export-excel-tab-delimited-text-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# hur man exporterar excel – Komplett C#‑handledning

Har du någonsin funderat **hur man exporterar excel**‑data till en ren‑textfil utan att förlora formatering? Kanske behöver du snabbt en TSV (tab‑separerade värden) för en datapipeline, eller så matar du ett äldre system som bara läser `.txt`. Oavsett är du inte ensam – utvecklare stöter ständigt på detta hinder när de ska föra ut data från kalkylblad.

Den goda nyheten? På bara tre enkla steg kan du **exportera excel som tab**‑avgränsad text, **konvertera excel till txt**, och till och med välja ett eget avgränsningstecken om du ändrar dig senare. Nedan ser du ett fullt körbart C#‑exempel, varför varje rad är viktig, och några tips för att undvika vanliga fallgropar.

> **Pro tip:** Detta tillvägagångssätt fungerar med det populära Aspose.Cells‑biblioteket, men koncepten kan överföras till vilket .NET Excel‑API som helst som erbjuder en `ExportTable`‑liknande metod.

## Vad du behöver

- **.NET 6+** (eller .NET Framework 4.6+). Koden kompileras på alla moderna runtime‑miljöer.
- **Aspose.Cells for .NET** (gratis prov eller licens). Installera via NuGet: `dotnet add package Aspose.Cells`.
- En inmatningsarbetsbok med namnet `input.xlsx` placerad i en mapp du kontrollerar.
- En liten dos nyfikenhet – inga djupa Excel‑interna kunskaper krävs.

Om du redan har detta, låt oss hoppa rakt in i lösningen.

## Steg 1 – Ladda arbetsboken du vill exportera

Först skapar vi ett `Workbook`‑objekt som pekar på källfilen. Detta objekt representerar hela Excel‑filen, inklusive alla kalkylblad, namngivna områden och formatering.

```csharp
using Aspose.Cells;

// Step 1: Load the workbook that contains the data to export
Workbook workbook = new Workbook(@"C:\Data\input.xlsx");
```

*Varför detta är viktigt:*  
Att ladda arbetsboken ger dig åtkomst till kalkylblads‑samlingen (`workbook.Worksheets`). Utan detta objekt kan du inte adressera celler, områden eller exportinställningar.  

> **Obs:** Om din fil ligger på en nätverksdel, lägg till `\\` eller använd en UNC‑sökväg – Aspose.Cells hanterar det utan problem.

## Steg 2 – Konfigurera exportalternativ (Strängvärden & Tab‑avgränsare)

Nu talar vi om för biblioteket hur vi vill att datan ska skrivas ut. Genom att sätta `ExportAsString = true` tvingar vi varje cell att behandlas som en ren sträng, vilket eliminerar Excels lokalanpassade talformat. `Delimiter = "\t"`‑delen är kärnan i **exportera excel som tab**.

```csharp
// Step 2: Configure the export options – export values as strings and use a tab delimiter
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,   // ensures numbers become plain text, not scientific notation
    Delimiter = "\t"         // tab character – perfect for TSV files
};
```

*Varför detta är viktigt:*  
Om du hoppar över `ExportAsString` kan en cell som innehåller `12345` bli `12,345` i vissa språkinställningar, vilket förstör efterföljande parsers. Avgränsaren kan bytas ut mot kommatecken, pipe‑tecken eller vilket tecken som helst om du senare bestämmer dig för **exportera excel med avgränsare** annat än en tab.

## Steg 3 – Exportera ett specifikt område till en textfil

Slutligen väljer vi det område vi är intresserade av (`A1:D10` i detta exempel) och skriver det till `out.txt`. Metoden `ExportTable` gör allt tungt arbete: den läser cellerna, tillämpar alternativen och strömmar resultatet till disk.

```csharp
// Step 3: Export the range A1:D10 from the first worksheet to a text file
Worksheet sheet = workbook.Worksheets[0]; // first worksheet (index 0)
sheet.Cells.ExportTable("A1", "D10", @"C:\Data\out.txt", exportOptions);
```

Efter att detta har körts hittar du `out.txt` med innehåll som ser ut så här:

```
Name    Age    City    Score
Alice   30     NY      85
Bob     25     LA      90
...
```

Varje kolumn separeras av en **tab**, vilket gör den klar för `awk`, `PowerShell` eller vilket CSV‑kompatibelt verktyg som helst som respekterar tabbar.

### Snabb verifiering

Öppna den genererade filen i en ren‑textredigerare (Notepad, VS Code) och bekräfta:

1. Kolumnerna ligger i linje när du aktiverar “Visa blanksteg”.
2. Inga extra citattecken eller kommatecken visas.
3. Alla numeriska celler visas exakt som de gjorde i Excel (tack vare `ExportAsString`).

Om något ser felaktigt ut, dubbelkolla att källarbetsboken inte döljer rader/kolumner, och säkerställ att du refererat rätt kalkylblads‑index.

## Vanliga variationer & kantfall

### Exportera ett helt kalkylblad

Om du vill **exportera excel‑område** som täcker hela bladet kan du använda `sheet.Cells.MaxDisplayRange`:

```csharp
var maxRange = sheet.Cells.MaxDisplayRange;
sheet.Cells.ExportTable(maxRange.FirstRow, maxRange.FirstColumn,
                       maxRange.RowCount, maxRange.ColumnCount,
                       @"C:\Data\fullSheet.txt", exportOptions);
```

### Använda en annan avgränsare

Att byta från tab till pipe (`|`) är lika enkelt som att ändra en rad:

```csharp
exportOptions.Delimiter = "|"; // now we have a pipe‑delimited file
```

Det uppfyller scenariot **exportera excel med avgränsare** utan att behöva skriva om någon annan kod.

### Hantera stora filer (> 100 MB)

För enorma arbetsböcker, strömma exporten för att undvika att ladda in allt i minnet:

```csharp
using (FileStream fs = new FileStream(@"C:\Data\largeOut.txt", FileMode.Create, FileAccess.Write))
{
    sheet.Cells.ExportTable("A1", "Z5000", fs, exportOptions);
}
```

### Konvertera flera blad i ett svep

Om du behöver **konvertera excel till txt** för flera blad, loopa över dem:

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    string outPath = $@"C:\Data\Sheet{i + 1}.txt";
    workbook.Worksheets[i].Cells.ExportTable("A1", "D10", outPath, exportOptions);
}
```

Varje blad får sin egen TSV‑fil – praktiskt för batch‑jobb.

## Fullt fungerande exempel (Kopiera‑klistra‑redo)

Nedan är hela programmet, redo att kompileras. Byt bara ut filsökvägarna mot dina egna.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToTxtDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook
            string inputPath = @"C:\Data\input.xlsx";
            Workbook workbook = new Workbook(inputPath);

            // 2️⃣ Set export options – strings + tab delimiter
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                Delimiter = "\t"
            };

            // 3️⃣ Export range A1:D10 from the first worksheet
            Worksheet sheet = workbook.Worksheets[0];
            string outputPath = @"C:\Data\out.txt";
            sheet.Cells.ExportTable("A1", "D10", outputPath, exportOptions);

            Console.WriteLine($"Export complete! Check {outputPath}");
        }
    }
}
```

**Förväntat resultat:** En fil med namnet `out.txt` där varje kolumn separeras av ett tab‑tecken, och varje cellvärde visas exakt som i Excel.

## Vanliga frågor

- **Fungerar detta med .xls‑filer?**  
  Ja. Aspose.Cells upptäcker automatiskt formatet, så du kan peka `Workbook` på en äldre `.xls` och samma kod gäller.

- **Vad händer om min data innehåller tabbar?**  
  Tabbar inuti en cell bevaras, vilket kan bryta TSV‑parsrar. I så fall överväg att byta till en pipe (`|`)‑avgränsare genom att uppdatera `exportOptions.Delimiter`.

- **Kan jag exportera formler istället för värden?**  
  Sätt `exportOptions.ExportAsString = false` och använd `ExportTableOptions`‑överladdningen som inkluderar `ExportFormula = true`. Utdata kommer då att innehålla den råa formeltexten.

- **Finns det ett sätt att hoppa över dolda rader?**  
  Ja. Sätt `exportOptions.ExportHiddenRows = false` (standard är `true`). Dolda rader utelämnas från den slutliga textfilen.

## Slutsats

Du har nu ett robust, produktionsklart recept för **hur man exporterar excel**‑data som en tab‑avgränsad textfil, hur man **exporterar excel som tab**, och hur man **konverterar excel till txt** med full kontroll över avgränsare och områdeval. Genom att utnyttja Aspose.Cells `ExportTable`‑metod undviker du manuell CSV‑konstruktion, bevarar dataintegriteten och håller din kodbas ren.

Redo för nästa utmaning? Prova:

- Exportera direkt till en `MemoryStream` för webb‑API:er.  
- Lägg till en rubrikrad dynamiskt baserat på innehållet i den första raden.  
- Integrera denna rutin i en Azure Function som övervakar en lagringsbucket för nya Excel‑uppladdningar.

Ge det ett försök, justera avgränsaren, och låt datan flöda dit du behöver den. Lycka till med kodningen!  

<img src="export-excel.png" alt="exempel på hur man exporterar excel" style="max-width:100%; height:auto;" />

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}