---
category: general
date: 2026-10-20
description: Spara arbetsboken som CSV med exakta decimaler, citerade värden och japanskt
  eradatumsformat med Aspose.Cells för .NET.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save workbook as csv
- set excel number format
- export excel to csv
- quote csv values
language: sv
lastmod: 2026-10-20
og_description: Spara arbetsboken som CSV med full kontroll över decimaler, citattecken
  och japanska era‑datum. Följ den här steg‑för‑steg C#‑handledningen med Aspose.Cells.
og_image_alt: Screenshot illustrating how to save workbook as CSV with custom options
  in C#
og_title: Spara arbetsbok som CSV – komplett guide för C#‑utvecklare
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Save workbook as CSV with precise decimal digits, quoted values and
    Japanese era date format using Aspose.Cells for .NET.
  headline: How to save workbook as CSV with custom formatting in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- CSV export
- Excel formatting
title: Hur man sparar arbetsbok som CSV med anpassad formatering i C#
url: /sv/net/csv-file-handling/how-to-save-workbook-as-csv-with-custom-formatting-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man sparar arbetsbok som CSV med anpassad formatering i C#

Om du behöver **spara arbetsbok som CSV** samtidigt som du styr decimalprecision, citerar värden och hanterar japanska era‑datum, visar den här handledningen hur du gör det med Aspose.Cells för .NET. Du kommer att lära dig att **exportera Excel till CSV**, **ange Excel-nummerformat** och **cita CSV‑värden** så att resultatet matchar vanliga datautbyteskrav.

Guiden förutsätter att du har en .NET‑utvecklingsmiljö (Visual Studio 2022 eller senare) och en giltig Aspose.Cells‑licens. Inga ytterligare NuGet‑paket krävs förutom `Aspose.Cells`.

## Förutsättningar

- .NET 6.0 SDK eller senare  
- Aspose.Cells för .NET (installerad via NuGet: `Install-Package Aspose.Cells`)  
- En exempel‑Excel‑fil (`Data.xlsx`) placerad i en mapp som du kan referera till från kod  

## Steg 1: Läs in källarbetsboken – grunden för att spara arbetsbok som CSV

Först skapar du en `Workbook`‑instans som pekar på den Excel‑fil du vill konvertera.

```csharp
using Aspose.Cells;
using System;

// Load the source workbook
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\Data.xlsx");
```

*Varför detta steg är viktigt*: `Workbook`‑objektet innehåller alla kalkylblad, stilar och formler. Alla efterföljande CSV‑operationer arbetar på denna minnesrepresentation.

## Steg 2: Begränsa decimalprecision när du sparar arbetsbok som CSV

När du behöver exakt fyra siffror efter decimaltecknet, konfigurera `CsvSaveOptions`.

```csharp
// Configure CSV saving options
CsvSaveOptions csvOptions = new CsvSaveOptions
{
    // Keep 4 digits after the decimal point
    SignificantDigits = 4
};

// Save the workbook as CSV with the defined precision
workbook.Save(@"YOUR_DIRECTORY\Data_Sig4.csv", csvOptions);
```

*Viktigt*: `SignificantDigits` avrundar varje numerisk cell till det angivna antalet decimaler innan CSV‑filen skrivs. Detta förhindrar flyttalsbrus i nedströmsystem.

## Steg 3: Exportera Excel till CSV med citerade värden

Vissa nedströms‑parser kräver att varje fält omsluts av dubbla citattecken, särskilt när värden innehåller kommatecken eller radbrytningar. Klassen `ExportTableOptions` låter dig behandla varje cell som en sträng och tillämpa anpassad citering.

```csharp
// Prepare export options that treat every cell as a string
ExportTableOptions tableOptions = new ExportTableOptions
{
    ExportAsString = true, // Force string export for all cells
    // Custom delegate to wrap each value in double quotes
    CustomExport = (cell, writer) =>
    {
        writer.Write('"' + cell.StringValue + '"');
    }
};

// Export the first worksheet as a CSV file with quoted values
workbook.Save(@"YOUR_DIRECTORY\TableExport.csv", tableOptions);
```

*Varför du bör citera värden*: Citering skyddar kommatecken, radbrytningar samt inledande/slutande mellanslag från att tolkas som avgränsare, vilket är avgörande för pålitlig dataimport.

## Steg 4: Ange Excel‑nummerformat för japanska era‑datum

Excel kan lagra datum med era‑specifika kalendrar. För att demonstrera, infoga en japansk era‑datumsträng och tillämpa lämpligt nummerformat.

```csharp
// Create a new workbook for the era‑date example
Workbook eraWorkbook = new Workbook();
Worksheet sheet = eraWorkbook.Worksheets[0];

// Insert a Japanese‑era date string (Reiwa 3‑04‑01)
sheet.Cells["A1"].PutValue("R3-04-01");

// Apply the Japanese locale number format
sheet.Cells["A1"].SetNumberFormat("[$-ja-JP]yyyy-mm-dd");

// Retrieve the parsed DateTime value
DateTime parsedDate = sheet.Cells["A1"].GetDateTime();
Console.WriteLine(parsedDate); // Outputs: 2021-04-01
```

*Förklaring*: Anropet `SetNumberFormat` instruerar Aspose.Cells att tolka strängen med den japanska kalendern. När du anropar `GetDateTime()` konverterar biblioteket automatiskt era‑notationen till det gregorianska datumet.

## Steg 5: Verifiera de genererade CSV‑filerna

Efter att ha kört koden bör du se tre filer i `YOUR_DIRECTORY`:

| Filnamn               | Höjdpunkter |
|----------------------|------------|
| `Data_Sig4.csv`      | Tal avrundade till 4 decimaler |
| `TableExport.csv`    | Varje cell omsluten av dubbla citattecken |
| `Data.xlsx` (unchanged) | Demonstrerar hantering av japanska era‑datum (visas i Excel) |

Öppna `Data_Sig4.csv` i en vanlig textredigerare för att bekräfta precisionen, och öppna `TableExport.csv` för att se de citerade värdena, t.ex.:

```
"Name","Score","Comment"
"Alice","95.1234","Excellent"
"Bob","88.0000","Good"
```

Konsolutdata för era‑datumet blir:

```
2021-04-01 00:00:00
```

## Vanliga fallgropar och hur du undviker dem

- **Lokalt beroende decimalseparatorer**: `CsvSaveOptions` respekterar aktuell kultur. Om du behöver en punkt (`.`) som separator oavsett kultur, sätt `csvOptions.Separator = ',';`.
- **Stora kalkylblad**: Export av en arbetsbok med miljontals rader kan förbruka mycket minne. Använd `ExportTableOptions.StartRow` och `EndRow` för att begränsa exportintervallet.
- **Specialtecken i strängar**: Den anpassade skribenten i Steg 3 lägger bara till omgivande citattecken. Om en cell redan innehåller ett citattecken, dubbla det (`""`) för att behålla CSV‑validiteten.

## Proffstips: Kombinera alternativ för maximal kontroll

Du kan kedja `CsvSaveOptions` och `ExportTableOptions` genom att först konvertera arbetsboken till en `MemoryStream` med ett uppsättning alternativ, och sedan skriva strömmen till disk med ett annat. Detta tillvägagångssätt låter dig till exempel tillämpa både decimalavrundning **och** citering i ett enda steg:

```csharp
using (MemoryStream ms = new MemoryStream())
{
    // Apply rounding
    workbook.Save(ms, csvOptions);
    ms.Position = 0; // Reset stream

    // Load the intermediate CSV into a new workbook for quoting
    Workbook temp = new Workbook(ms, new LoadOptions(LoadFormat.Csv));
    temp.Save(@"YOUR_DIRECTORY\RoundedAndQuoted.csv", tableOptions);
}
```

## Slutsats

Du vet nu hur du **sparar arbetsbok som CSV** med exakt decimalhantering, citerade värden och anpassad datumformatering. Den kompletta lösningen täcker inläsning av en arbetsbok, konfiguration av `CsvSaveOptions`, användning av `ExportTableOptions` för att **cita CSV‑värden**, och tillämpning av ett **Excel‑nummerformat** för japanska era‑datum. Härifrån kan du utforska ytterligare alternativ såsom anpassade separatorer, olika kodningar eller selektiv export av kalkylblad.

---

*Nästa steg*  
- Utforska `CsvSaveOptions.Encoding` för att skriva UTF‑8 BOM‑ eller UTF‑16‑filer.  
- Använd `ExportTableOptions.StartColumn` / `EndColumn` för att exportera endast ett delmängd av kolumner.  
- Kombinera dessa tekniker med Aspose.Cells’ `DataFormatter` för kultur‑medveten numerisk formatering.  

Lycka till med kodningen!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Spara arbetsbok som CSV – Komplett guide för att exportera Excel till CSV med kontrollerad](/cells/english/net/csv-file-handling/save-workbook-as-csv-complete-guide-to-export-excel-to-csv-w/)
- [Spara arbetsbok som CSV i C# – Exportera Excel till CSV](/cells/english/net/csv-file-handling/save-workbook-as-csv-in-c-export-excel-to-csv/)
- [Skapa och spara Excel‑arbetsbok som PDF i ASP.NET med Aspose.Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}