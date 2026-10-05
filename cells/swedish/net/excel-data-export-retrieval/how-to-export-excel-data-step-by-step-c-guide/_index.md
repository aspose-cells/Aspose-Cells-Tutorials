---
category: general
date: 2026-03-29
description: Lär dig hur du exporterar Excel‑tabeller till vanlig text, skriver en
  sträng till en fil och konverterar en Excel‑tabell till CSV eller TXT med C#. Inkluderar
  fullständig kod och tips.
draft: false
keywords:
- how to export excel
- write string to file
- convert excel table
- export table as csv
- save txt file c#
language: sv
og_description: Hur man exporterar Excel‑tabeller till textfiler i C#. Få hela lösningen,
  koden och bästa praxis för att konvertera Excel‑tabeller och spara TXT‑filer.
og_title: Hur man exporterar Excel-data – Komplett C#-handledning
tags:
- C#
- Excel
- File I/O
title: Hur man exporterar Excel-data – Steg‑för‑steg C#‑guide
url: /sv/net/excel-data-export-retrieval/how-to-export-excel-data-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man exporterar Excel-data – Komplett C#-guide

Har du någonsin undrat **how to export Excel** data utan att öppna kalkylbladet manuellt? Kanske behöver du dumpa en tabell till en enkel textfil för ett äldre system, eller så vill du ha en snabb CSV‑export för data‑analys‑pipelines. I den här handledningen går vi igenom en praktisk, end‑to‑end‑lösning som **writes a string to file** och visar exakt hur du **convert Excel table** data till ett avgränsat textformat med C#.

Vi kommer att gå igenom allt från att ladda arbetsboken, välja rätt tabell, konfigurera exportalternativ och slutligen spara resultatet som en `.txt`‑fil. När du är klar kommer du att kunna **export table as CSV** (eller vilken avgränsare du än väljer) och du får även se några praktiska knep för **saving txt file C#**‑projekt. Inga externa verktyg behövs—bara några NuGet‑paket och lite kod.

---

## Vad du behöver

- **.NET 6.0+** (eller .NET Framework 4.7.2 om du föredrar klassisk)
- **Syncfusion.XlsIO** NuGet‑paket (klassen `ExportTableOptions` finns här)
- En grundläggande C#‑IDE (Visual Studio, VS Code, Rider—vilken som helst)
- En Excel‑arbetsbok som innehåller minst en tabell (vi använder `ws.Tables[0]` i exemplet)

> Pro tip: Om du ännu inte har Syncfusion‑biblioteket, kör  
> `dotnet add package Syncfusion.XlsIO.Net.Core` från kommandoraden.

---

## Steg 1 – Öppna arbetsboken och hämta den första tabellen  

Det första är att ladda Excel‑filen och få en referens till kalkylbladet som innehåller tabellen. Detta steg är avgörande eftersom **convert excel table**‑operationen arbetar på ett `ITable`‑objekt, inte på råa cellområden.

```csharp
using Syncfusion.XlsIO;
using System.IO;

class ExcelExporter
{
    static void Main()
    {
        // Load the workbook (replace with your actual file path)
        using (ExcelEngine excelEngine = new ExcelEngine())
        {
            IApplication application = excelEngine.Excel;
            application.DefaultVersion = ExcelVersion.Xlsx;

            // Open the file
            FileStream stream = new FileStream(@"C:\Data\Sample.xlsx", FileMode.Open, FileAccess.Read);
            IWorkbook workbook = application.Workbooks.Open(stream);
            IWorksheet ws = workbook.Worksheets[0];   // First worksheet
```

*Varför detta är viktigt:* Att öppna arbetsboken med `using` säkerställer att alla ohanterade resurser frigörs, vilket förhindrar fil‑lås‑problem senare när du försöker **write string to file**.

---

## Steg 2 – Konfigurera exportalternativ (vanlig text, inga rubriker, semikolon‑avgränsare)  

Nu berättar vi för Syncfusion hur vi vill att tabellen serialiseras. `ExportTableOptions` låter dig växla rubrikinkludering, välja en avgränsare och bestämma om du vill ha en sträng eller en byte‑array.

```csharp
            // Step 2: Configure export options – plain text, omit headers, ';' delimiter
            var exportOptions = new ExportTableOptions
            {
                ExportAsString = true,      // Returns a string we can write directly
                IncludeHeaders = false,     // Skip column headers if you don’t need them
                Delimiter = ";"             // Change to ',' for classic CSV
            };
```

*Varför detta är viktigt:* Att sätta `IncludeHeaders = false` matchar ofta förväntningarna hos nedströmsystem som redan känner till kolumnordningen. Att ändra avgränsaren är hur du **export table as CSV** med en anpassad separator.

---

## Steg 3 – Exportera tabellen till en sträng  

När alternativen är klara anropar vi `ExportToString`. Denna metod hämtar hela tabellen (inklusive alla rader) och returnerar en enda sträng klar för filutmatning.

```csharp
            // Step 3: Export the first table to a string using the configured options
            ITable firstTable = ws.Tables[0];               // Access the first table
            string tableText = firstTable.ExportToString(exportOptions);
```

*Varför detta är viktigt:* Anropet `ExportToString` gör det tunga arbetet med att konvertera Excel‑rutnätet till ett avgränsat format. Det respekterar den `Delimiter` du har angett, så du får ett rent **export table as csv**‑resultat utan extra bearbetning.

---

## Steg 4 – Skriv den exporterade texten till en fil  

Till sist sparar vi strängen på disk. `File.WriteAllText` är det enklaste sättet att **save txt file C#**; den skapar automatiskt filen om den inte finns och skriver över den annars.

```csharp
            // Step 4: Write the exported text to a file
            string outputPath = @"C:\Data\ExportedTable.txt";
            File.WriteAllText(outputPath, tableText);
            System.Console.WriteLine($"Table exported successfully to {outputPath}");
        }
    }
}
```

*Varför detta är viktigt:* Genom att skriva strängen direkt undviker du ett extra konverteringssteg. Filen innehåller nu rader som `Value1;Value2;Value3`, redo för vilken nedströms‑parser som helst.

---

## Fullständigt fungerande exempel (alla steg på ett ställe)  

Nedan är det kompletta, kopiera‑och‑klistra‑klara programmet som kombinerar allt vi har gått igenom. Det innehåller felhantering och kommentarer för tydlighet.

```csharp
using Syncfusion.XlsIO;
using System;
using System.IO;

class ExcelExporter
{
    static void Main()
    {
        try
        {
            // 1️⃣ Load workbook and get first worksheet
            using (ExcelEngine excelEngine = new ExcelEngine())
            {
                IApplication app = excelEngine.Excel;
                app.DefaultVersion = ExcelVersion.Xlsx;

                string sourcePath = @"C:\Data\Sample.xlsx";
                using (FileStream fs = new FileStream(sourcePath, FileMode.Open, FileAccess.Read))
                {
                    IWorkbook wb = app.Workbooks.Open(fs);
                    IWorksheet ws = wb.Worksheets[0]; // first sheet

                    // 2️⃣ Set export options (plain text, no headers, ';' delimiter)
                    var opts = new ExportTableOptions
                    {
                        ExportAsString = true,
                        IncludeHeaders = false,
                        Delimiter = ";"
                    };

                    // 3️⃣ Export the first table to a string
                    ITable table = ws.Tables[0];
                    string csvText = table.ExportToString(opts);

                    // 4️⃣ Save the string to a .txt file
                    string destPath = @"C:\Data\ExportedTable.txt";
                    File.WriteAllText(destPath, csvText);

                    Console.WriteLine($"✅ Export complete! File saved at: {destPath}");
                }
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"❌ Something went wrong: {ex.Message}");
        }
    }
}
```

**Förväntad output** (innehållet i `ExportedTable.txt`):

```
John;Doe;35
Jane;Smith;28
Bob;Brown;42
```

Varje rad motsvarar en rad från den ursprungliga Excel‑tabellen, med värden separerade av semikolon. Om du ändrar `Delimiter = ","` får du en klassisk CSV‑fil istället.

---

## Vanliga frågor & edge‑cases  

### Vad händer om min arbetsbok har flera tabeller?  
Du kan helt enkelt ändra `ws.Tables[0]` till rätt index, eller loopa igenom `ws.Tables`:

```csharp
foreach (var tbl in ws.Tables)
{
    string txt = tbl.ExportToString(opts);
    // Save each table to a separate file or concatenate as needed
}
```

### Hur inkluderar jag kolumnrubriker?  
Sätt `IncludeHeaders = true` i `ExportTableOptions`. Detta är användbart när nedströmsystemet förväntar sig en rubrikrad.

### Kan jag exportera till en annan mapp dynamiskt?  
Absolut. Använd `Path.Combine` med `Environment.GetFolderPath(Environment.SpecialFolder.Desktop)` eller någon användar‑angiven sökväg för att göra lösningen mer flexibel.

### Vad händer med stora filer?  
För enorma tabeller, överväg att strömma utdata istället för att ladda hela strängen i minnet:

```csharp
using (StreamWriter writer = new StreamWriter(outputPath))
{
    writer.Write(table.ExportToString(opts));
}
```

### Fungerar detta på .NET Core?  
Ja—Syncfusion.XlsIO stödjer .NET 5/6/7. Referera bara till rätt NuGet‑paket så är du klar.

---

## Pro‑tips för pålitliga exporter  

- **Validera filvägen** innan du skriver. En saknad katalog kastar `DirectoryNotFoundException`.  
- **Kontrollera `ExportAsString`** endast när tabellen får plats bekvämt i minnet; annars, använd `ExportToStream` för enorma dataset.  
- **Tänk på kultur**: om dina data innehåller kommatecken som decimalavgränsare, välj ett semikolon (`;`) eller tab (`\t`) som avgränsare för att undvika CSV‑tolkningsfel.  
- **Version lock**: Syncfusion ändrar ibland API‑signaturer. Lås NuGet‑versionen (`<PackageReference Include="Syncfusion.XlsIO.Net.Core" Version="21.2.0.44" />`) för att hålla din build reproducerbar.

---

## Slutsats  

I den här guiden demonstrerade vi **how to export Excel**‑tabeller till vanliga textfiler med C#. Genom att ladda arbetsboken, konfigurera `ExportTableOptions`, exportera tabellen till en sträng och slutligen **write string to file**, har du nu ett robust mönster för **convert excel table**‑data, **export table as csv** och **save txt file C#**‑uppgifter.

Känn dig fri att experimentera—byt avgränsare, inkludera rubriker eller loopa över flera tabeller. Samma tillvägagångssätt fungerar för att generera CSV‑rapporter, mata data till äldre parser eller helt enkelt arkivera kalkylbladsinnehåll som lätta textfiler.

Har du fler scenarier du vill ta itu med? Kanske behöver du **write string to file** asynkront, eller så vill du zipa utdata i farten. Kolla in våra nästa handledningar om *asynchronous file I/O in C#* och *zipping files with .NET* för att hålla momentum.

Lycka till med kodningen! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}