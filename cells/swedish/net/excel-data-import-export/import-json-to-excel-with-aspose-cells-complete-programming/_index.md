---
category: general
date: 2026-06-21
description: Importera JSON till Excel snabbt och lär dig hur du konverterar JSON
  till XLSX, genererar Excel från JSON och exporterar JSON till kalkylblad på några
  enkla steg.
draft: false
keywords:
- import json to excel
- convert json to xlsx
- generate excel from json
- save json as excel
- export json to spreadsheet
language: sv
og_description: Importera JSON till Excel utan ansträngning. Den här guiden visar
  hur du konverterar JSON till XLSX, genererar Excel från JSON och exporterar JSON
  till kalkylblad med C#.
og_title: Importera JSON till Excel med Aspose.Cells – Fullständig guide
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Import JSON to Excel quickly and learn how to convert JSON to XLSX,
    generate Excel from JSON, and export JSON to spreadsheet in a few easy steps.
  headline: Import JSON to Excel with Aspose.Cells – Complete Programming Guide
  type: TechArticle
- description: Import JSON to Excel quickly and learn how to convert JSON to XLSX,
    generate Excel from JSON, and export JSON to spreadsheet in a few easy steps.
  name: Import JSON to Excel with Aspose.Cells – Complete Programming Guide
  steps:
  - name: Expected Output
    text: 'Running the program prints:'
  - name: 1. Import Multiple JSON Arrays into Different Sheets
    text: 'If you have several arrays—say `"Employees"` and `"Departments"`—you can
      import each into its own worksheet:'
  - name: 2. Styling the Generated Table
    text: 'You can apply a style after the data expands:'
  - name: 3. Using a JSON File Instead of a String
    text: 'If your JSON lives on disk, just read it first:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- JSON
- Excel automation
title: Importera JSON till Excel med Aspose.Cells – Komplett programmeringsguide
url: /sv/net/excel-data-import-export/import-json-to-excel-with-aspose-cells-complete-programming/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Importera JSON till Excel – Komplett programmeringsguide

Har du någonsin undrat **hur man importerar JSON till Excel** utan att skriva en egen parser? Du är inte ensam. Många utvecklare stöter på problem när de behöver omvandla en JSON‑payload till ett prydligt kalkylblad för rapportering eller data‑analys. Den goda nyheten? Med Aspose.Cells kan du **konvertera JSON till XLSX** med bara några få rader kod, och hela processen är både snabb och typ‑säker.

I den här handledningen går vi igenom varje steg som krävs för att **generera Excel från JSON**, spara resultatet som en `.xlsx`‑fil, och även utforska några praktiska varianter — som att exportera JSON till ett kalkylblad som uppdateras automatiskt när du ändrar källdata. I slutet har du ett återanvändbart kodsnutt som du kan klistra in i vilket .NET‑projekt som helst.

## Förutsättningar

Innan vi dyker ner, se till att du har:

- .NET 6.0 eller senare (koden fungerar även på .NET Framework)
- En giltig Aspose.Cells för .NET‑licens eller en tillfällig utvärderingsnyckel
- Visual Studio 2022 (eller någon C#‑IDE du föredrar)
- Grundläggande kunskap om JSON‑strukturer och C#‑syntax

Inga extra NuGet‑paket utöver **Aspose.Cells** behövs, vilket gör installationen lättviktig.

## Steg 1: Installera Aspose.Cells och konfigurera projektet

Först och främst, lägg till Aspose.Cells‑biblioteket i ditt projekt. Öppna Package Manager Console och kör:

```powershell
Install-Package Aspose.Cells
```

Om du använder .NET‑CLI är motsvarande:

```bash
dotnet add package Aspose.Cells
```

> **Pro tip:** Efter installationen, lägg till din licensfil (`Aspose.Cells.lic`) i projektets rot och ladda den vid start:

```csharp
// Load the Aspose.Cells license (optional but removes evaluation watermark)
var license = new Aspose.Cells.License();
license.SetLicense("Aspose.Cells.lic");
```

Nu är du redo att börja **importera JSON till Excel**.

## Steg 2: Förbered JSON‑payloaden

För demonstration använder vi en enkel array av person‑objekt. I ett verkligt scenario kan du läsa denna sträng från en fil, ett API‑svar eller en databas.

```csharp
// Step 2: Define the JSON data to be imported
string json = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":28}]";
```

Observera hur JSON‑en är en platt array — exakt den struktur som fungerar bäst med Aspose.Cells smart markers.

## Steg 3: Konfigurera alternativ för JSON‑laddning

Aspose.Cells låter dig behandla hela JSON‑arrayen som en *enda* datakälla. Detta är avgörande när du vill att raderna ska expandera automatiskt i kalkylbladet.

```csharp
// Step 3: Configure JSON loading options to treat the whole array as a single data source
var loadOptions = new Aspose.Cells.JsonLoadOptions
{
    // When true, the whole array becomes one data source (e.g., "People")
    ArrayAsSingle = true
};
```

Genom att sätta `ArrayAsSingle = true` instruerar du biblioteket **att generera en smart marker som upprepas för varje element** i arrayen, vilket är kärnan i arbetsflödet för **konvertera JSON till XLSX**.

## Steg 4: Skapa arbetsboken och importera JSON

Nu skapar vi en ny `Workbook`‑instans och importerar JSON‑en med en smart marker som heter `"People"`.

```csharp
// Step 4: Create a new workbook and import the JSON using a smart marker named "People"
var workbook = new Aspose.Cells.Workbook();
workbook.ImportJson(json, loadOptions, new Aspose.Cells.SmartMarkerOptions
{
    DataSourceName = "People"
});
```

Bakom kulisserna parsar Aspose.Cells JSON‑en, mappar varje egenskap (`Name`, `Age`) till en kolumn och förbereder en platshållare som senare expanderas till rader.

## Steg 5: Placera smart marker i kalkylbladet

En smart marker ser ut som `{{People}}`. När arbetsboken sparas ersätter Aspose.Cells denna marker med en tabell som innehåller all data från JSON‑arrayen.

```csharp
// Step 5: Put the smart marker in cell A1 so the data expands when saved
workbook.Worksheets[0].Cells["A1"].PutValue("{{People}}");
```

Du kan flytta markern var som helst — övre‑vänstra hörnet är ett vanligt val eftersom det ger tabellen utrymme att växa nedåt och åt höger.

## Steg 6: Spara arbetsboken som en XLSX‑fil

Slutligen skriver vi arbetsboken till disk. Här **sparar vi JSON som Excel** och får en riktig `.xlsx`‑fil som du kan öppna i Excel, Google Sheets eller någon annan kalkylbladsapp.

```csharp
// Step 6: Save the workbook to a file (convert JSON to XLSX)
string outputPath = Path.Combine(Environment.CurrentDirectory, "JsonSingleCell.xlsx");
workbook.Save(outputPath, Aspose.Cells.SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}");
```

När du öppnar `JsonSingleCell.xlsx` kommer du att se något liknande:

| Name | Age |
|------|-----|
| John | 30  |
| Anna | 28  |

Det är resultatet av **generera Excel från JSON** i praktiken.

## Fullt fungerande exempel

Sätter vi ihop allt, så är här det kompletta, körklara programmet:

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load license (optional)
        // var license = new License();
        // license.SetLicense("Aspose.Cells.lic");

        // Step 1: Define JSON data
        string json = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":28}]";

        // Step 2: Configure loading options
        var loadOptions = new JsonLoadOptions { ArrayAsSingle = true };

        // Step 3: Create workbook and import JSON
        var workbook = new Workbook();
        workbook.ImportJson(json, loadOptions, new SmartMarkerOptions { DataSourceName = "People" });

        // Step 4: Insert smart marker
        workbook.Worksheets[0].Cells["A1"].PutValue("{{People}}");

        // Step 5: Save as XLSX (export JSON to spreadsheet)
        string outputPath = Path.Combine(Environment.CurrentDirectory, "JsonSingleCell.xlsx");
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Excel file generated successfully at: {outputPath}");
    }
}
```

### Förväntad utdata

När programmet körs skrivs följande ut:

```
Excel file generated successfully at: C:\YourProject\JsonSingleCell.xlsx
```

Att öppna filen visar en två‑radig tabell med rubrikerna **Name** och **Age**, exakt som den ursprungliga JSON‑arrayen.

## Avancerade varianter

### 1. Importera flera JSON‑arrayer till olika blad

Om du har flera arrayer — exempelvis `"Employees"` och `"Departments"` — kan du importera varje till ett eget kalkylblad:

```csharp
// Load a more complex JSON with two arrays
string complexJson = @"
{
  ""Employees"": [{""Name"":""John"",""Age"":30}],
  ""Departments"": [{""Dept"":""HR"",""Count"":5}]
}";
var options = new JsonLoadOptions { ArrayAsSingle = false };
var wb = new Workbook();
wb.ImportJson(complexJson, options, new SmartMarkerOptions());

// Place markers
wb.Worksheets[0].Cells["A1"].PutValue("{{Employees}}");
wb.Worksheets.Add();
wb.Worksheets[1].Cells["A1"].PutValue("{{Departments}}");
wb.Save("MultipleSheets.xlsx");
```

Nu har du **exporterat JSON till kalkylblad** med flera flikar, där varje flik speglar ett separat dataset.

### 2. Formatera den genererade tabellen

Du kan applicera en stil efter att datan har expanderat:

```csharp
var table = workbook.Worksheets[0].Cells["A1"].GetSmartMarkerTable();
var style = workbook.CreateStyle();
style.Font.IsBold = true;
style.ForegroundColor = System.Drawing.Color.LightBlue;
style.Pattern = BackgroundType.Solid;
table.ApplyStyle(style);
```

Denna lilla justering får rubrikraden att sticka ut, vilket är praktiskt för rapporterings‑dashboards.

### 3. Använda en JSON‑fil istället för en sträng

Om din JSON finns på disk, läs den först:

```csharp
string jsonFromFile = File.ReadAllText(@"C:\Data\people.json");
workbook.ImportJson(jsonFromFile, loadOptions, new SmartMarkerOptions { DataSourceName = "People" });
```

Resten av stegen förblir exakt desamma, så du kan **spara JSON som Excel** från vilken källa som helst.

## Vanliga fallgropar & hur du undviker dem

- **Saknad `ArrayAsSingle`** – Att glömma detta flagga gör att varje objekt behandlas som en separat datakälla, vilket resulterar i tomma celler. Sätt alltid den när din JSON är en top‑level array.
- **Fel smart marker‑namn** – Markern (`{{People}}`) måste matcha `DataSourceName` du angav (`"People"`). Ett stavfel lämnar platshållaren orörd.
- **Licens ej laddad** – I utvärderingsläge innehåller den genererade filen ett vattenmärke. Ladda din licens tidigt för att hålla arbetsboken ren.
- **Fil‑sökvägsbehörigheter** – Att försöka spara till en skyddad mapp kastar ett undantag. Använd `Environment.CurrentDirectory` eller en sökväg som är skrivbar för användaren.

## Testa resultatet programatiskt

Om du vill verifiera att exporten lyckades utan att öppna Excel kan du läsa tillbaka den första cellen:

```csharp
var wbCheck = new Workbook("JsonSingleCell.xlsx");
string firstName = wbCheck.Worksheets[0].Cells["A2"].StringValue; // Should be "John"
Console.WriteLine($"First imported name: {firstName}");
```

En snabb konsollkontroll som denna bekräftar att **konvertera JSON till XLSX** fungerade som förväntat.

## Slutsats

Vi har precis gått igenom allt du behöver för att **importera JSON till Excel** med Aspose.Cells: från att installera biblioteket, förbereda JSON‑en, konfigurera smart markers, till att slutligen **spara JSON som Excel**. Oavsett om du behöver **konvertera JSON till XLSX**, **generera Excel från JSON**, eller **exportera JSON till kalkylblad** för analys, är mönstret detsamma — smart markers sköter det tunga arbetet.

Känn dig fri att experimentera med formatering, flera blad eller till och med dynamiska uppdateringar genom att åter‑importera JSON vid körning. Nästa logiska steg är att integrera denna kod i ett web‑API som levererar Excel‑rapporter på begäran — byt bara ut raden som sparar filen mot en ström som returneras till klienten.

Har du frågor om kantfall, som nästlade JSON‑objekt eller stora dataset? Lämna en kommentar nedan, och lycka till med kodandet!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Effektiv import av JSON till Excel med Aspose.Cells för Java: En omfattande guide](/cells/english/java/import-export/import-json-to-excel-aspose-cells-java/)
- [Importera JSON‑data till Excel med Aspose.Cells Java: En omfattande guide](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [Importera JSON till Excel utan ansträngning med Aspose.Cells för .NET](/cells/english/net/import-export/import-json-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}