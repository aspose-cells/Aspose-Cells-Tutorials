---
category: general
date: 2026-11-25
description: Lär dig hur du skapar flera blad i en Excel-fil med C#. Denna guide täcker
  att spara arbetsboken som XLSX och hantera duplicerade bladnamn.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create multiple sheets
- create excel file c#
- duplicate sheet names
- save workbook xlsx
language: sv
lastmod: 2026-11-25
og_description: Skapa flera blad i en Excel-fil med C#. Följ den här kompletta handledningen
  för att spara arbetsboken som XLSX och hantera dubbla bladnamn.
og_image_alt: Code editor showing C# sample that generates an Excel workbook with
  several detail sheets
og_title: Skapa flera blad i en Excel‑fil med C# – steg‑för‑steg‑guide
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Learn how to create multiple sheets in an Excel file using C#. This
    guide covers saving the workbook as XLSX and handling duplicate sheet names.
  headline: How to create multiple sheets in an Excel file using C#
  type: TechArticle
- description: Learn how to create multiple sheets in an Excel file using C#. This
    guide covers saving the workbook as XLSX and handling duplicate sheet names.
  name: How to create multiple sheets in an Excel file using C#
  steps:
  - name: '**Create a new workbook** and name the first worksheet *Master*.'
    text: '**Create a new workbook** and name the first worksheet *Master*.'
  - name: '**Insert a smart marker** that tells Aspose.Cells how to name the detail
      worksheets.'
    text: '**Insert a smart marker** that tells Aspose.Cells how to name the detail
      worksheets.'
  - name: '**Process the smart marker** with a data source that may contain duplicate
      names.'
    text: '**Process the smart marker** with a data source that may contain duplicate
      names.'
  - name: '**Save the workbook** as an XLSX file.'
    text: '**Save the workbook** as an XLSX file.'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: Hur man skapar flera blad i en Excel‑fil med C#
url: /sv/net/worksheet-management/how-to-create-multiple-sheets-in-an-excel-file-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man skapar flera blad i en Excel-fil med C#

Om du behöver **create multiple sheets** i en Excel-arbetsbok från C#, ger den här handledningen dig en färdig‑att‑köra lösning. I slutet av guiden har du ett program som genererar ett master‑blad, skapar detaljblad via smart markers, och sparar resultatet som en **XLSX**‑fil—med säker hantering av **duplicate sheet names**.

Du får också se hur du **create excel file c#** projekt med Aspose.Cells‑biblioteket, ett populärt val för server‑sidig kalkylblads‑automatisering.

## Förutsättningar

* .NET 6.0 SDK eller senare installerat  
* Visual Studio 2022 (eller någon IDE som stödjer .NET)  
* **Aspose.Cells for .NET** NuGet‑paketet (`Aspose.Cells`) – det tillhandahåller klasserna `Workbook`, `Worksheet` och `SmartMarkersFactory` som används i koden.  

Du kan lägga till paketet med följande CLI‑kommando:

```bash
dotnet add package Aspose.Cells
```

> **Pro tip:** Använd ett privat NuGet‑flöde eller den kostnadsfria community‑editionen om du bara behöver grundläggande funktioner.

## Översikt av lösningen

Tillvägagångssättet består av fyra logiska steg:

1. **Create a new workbook** och namnge det första kalkylbladet *Master*.  
2. **Insert a smart marker** som talar om för Aspose.Cells hur detaljbladens namn ska sättas.  
3. **Process the smart marker** med en datakälla som kan innehålla dubblettnamn.  
4. **Save the workbook** som en XLSX‑fil.  

Varje steg förklaras i detalj nedan, och den kompletta källfilen finns i slutet av artikeln.

## Steg 1: Skapa en ny arbetsbok och lägg till ett master‑blad

`Workbook`‑klassen representerar en hel Excel‑fil. När du instansierar den utan parametrar skapar Aspose.Cells en standardarbetsbok som redan innehåller ett kalkylblad. Att byta namn på det bladet till *Master* gör bladets syfte tydligt.

```csharp
using Aspose.Cells;
using System;
using System.Data;   // For DataTable used as a data source

// 1️⃣ Create a new workbook
Workbook workbook = new Workbook();

// 1️⃣ Retrieve the first worksheet (index 0) and give it a friendly name
Worksheet masterSheet = workbook.Worksheets[0];
masterSheet.Name = "Master";
```

**Varför detta är viktigt:**  
Att börja med en ren arbetsbok undviker kvarvarande formatering eller dolda blad från tidigare körningar. Att namnge bladet *Master* hjälper dig att hitta smart‑markören senare och gör filen läsbar för icke‑tekniska användare.

## Steg 2: Infoga en smart marker som definierar namn på detaljblad

Smart markers är platshållare som Aspose.Cells ersätter med data vid körning. Syntaxen `&=DetailSheetNewName=Detail` instruerar motorn att skapa ett nytt kalkylblad för varje rad i datakällan, med värdet i kolumnen `Detail` som bladnamn.

```csharp
// 2️⃣ Place a smart marker in cell A1 of the master sheet
masterSheet.Cells["A1"].PutValue("&=DetailSheetNewName=Detail");
```

**Varför detta är viktigt:**  
Smart‑markören eliminerar behovet av att skriva en loop som manuellt lägger till kalkylblad. Den kopierar också automatiskt master‑bladets layout till varje nygenererat blad, vilket säkerställer enhetlig styling.

## Steg 3: Processa smart‑markören med en datakälla som kan innehålla dubbletter

Nedan bygger vi en `DataTable` som simulerar en datakälla. Observera att *Detail*-kolumnen innehåller dubblettvärden (`"Report"` förekommer två gånger). Metoden `SmartMarkersFactory.Process` respekterar inställningen `AllowDuplicateSheetNames`, som är **true** som standard i detta exempel.

```csharp
// 3️⃣ Build a sample data source (DataTable) with duplicate sheet names
DataTable dataSource = new DataTable();
dataSource.Columns.Add("Detail", typeof(string));
dataSource.Columns.Add("Value", typeof(double));

// Add rows – "Report" appears twice to demonstrate duplicate handling
dataSource.Rows.Add("Report", 123.45);
dataSource.Rows.Add("Summary", 67.89);
dataSource.Rows.Add("Report", 101.12);   // Duplicate sheet name

// Register the data source in the workbook's data collection
workbook.Worksheets[0].SmartMarkersFactory.Process(new[] { "dataSource" });
```

> **Important:** Om du behöver garantera unika bladnamn, sätt `workbook.Settings.CheckDuplicateSheetNames = true;` innan du processar. Standardbeteendet skapar blad med samma namn, vilket Excel tillåter men kan vara förvirrande vid navigering i filen.

## Steg 4: Spara arbetsboken som en XLSX‑fil

Till sist sparas den genererade arbetsboken till disk. Metoden `Save` väljer automatiskt rätt skrivar‑implementation baserat på filändelsen.

```csharp
// 4️⃣ Save the workbook – the file will contain the master sheet and two "Report" sheets plus a "Summary" sheet
string outputPath = @"C:\Temp\duplicate_detail_sheets.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);

Console.WriteLine($"Workbook saved to {outputPath}");
```

**Förväntat resultat**

När du öppnar `duplicate_detail_sheets.xlsx` kommer du att se:

| Bladnamn | Innehåll (första raden) |
|----------|--------------------------|
| Master   | Smart marker‑platshållare (ingen data) |
| Report   | Datarad 1 (`123.45`) |
| Summary  | Datarad 2 (`67.89`) |
| Report (2) | Datarad 3 (`101.12`) |

Det andra *Report*-bladet byts automatiskt till *Report (2)* av Aspose.Cells för att undvika ett hårt fel samtidigt som det fortfarande speglar den ursprungliga dubblettavsikten.

## Fullständig källkod

Kopiera följande fil till ett konsolprojekt (`dotnet new console`) och kör det. Programmet demonstrerar hela arbetsflödet för **create multiple sheets** och **save workbook xlsx** samtidigt som det hanterar **duplicate sheet names**.

```csharp
// Program.cs
using Aspose.Cells;
using System;
using System.Data;

namespace ExcelMultipleSheetsDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook and name the first sheet "Master"
            Workbook workbook = new Workbook();
            Worksheet masterSheet = workbook.Worksheets[0];
            masterSheet.Name = "Master";

            // Step 2: Add a smart marker that will generate detail sheets
            masterSheet.Cells["A1"].PutValue("&=DetailSheetNewName=Detail");

            // Step 3: Prepare a data source with duplicate sheet names
            DataTable dataSource = new DataTable();
            dataSource.Columns.Add("Detail", typeof(string));
            dataSource.Columns.Add("Value", typeof(double));

            dataSource.Rows.Add("Report", 123.45);
            dataSource.Rows.Add("Summary", 67.89);
            dataSource.Rows.Add("Report", 101.12); // duplicate name

            // Bind the data source to the workbook
            workbook.Worksheets[0].SmartMarkersFactory.Process(new[] { "dataSource" });

            // Step 4: Save the workbook as an XLSX file
            string outputPath = @"C:\Temp\duplicate_detail_sheets.xlsx";
            workbook.Save(outputPath, SaveFormat.Xlsx);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

Kör `dotnet run` från projektmappen. Efter körning, öppna den genererade filen för att verifiera att tre detaljblad skapades, varav två delar basnamnet **Report**.

## Hantera kantfall och bästa praxis

| Situation | Rekommenderad metod |
|-----------|----------------------|
| **Mycket stora datamängder** ( > 10 000 rader) | Använd `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference;` för att minska minnesbelastningen. |
| **Anpassade regler för bladnamn** | Förprocessa `Detail`‑kolumnen för att ersätta otillåtna tecken (`/ \ ? * [ ] :`) innan du anropar `Process`. |
| **Behov av verkligen unika namn** | Sätt `workbook.Settings.CheckDuplicateSheetNames = true;` och tillhandahåll ett reservnamnschema (t.ex. lägg till ett GUID). |
| **Generera PDF istället för XLSX** | Efter sparning, anropa `workbook.Save("output.pdf", SaveFormat.Pdf);` – Aspose.Cells kan exportera direkt till PDF. |
| **Kör i en webbtjänst** | Skriv arbetsboken till en `MemoryStream` och returnera den som en filnedladdning för att undvika disk‑I/O. |

### Pro tip: återanvänd samma `Workbook`‑instans för flera exporteringar

Om din applikation skapar flera rapporter per begäran, behåll ett enda `Workbook`‑objekt i minnet, rensa dess kalkylblad (`workbook.Worksheets.Clear();`) och upprepa stegen. Detta undviker overheaden av att upprepade gånger ladda Aspose.Cells‑runtime.

## Slutsats

Du vet nu hur du **create multiple sheets** i en Excel‑arbetsbok med C#, hur du **create excel file c#** med Aspose.Cells, hur du hanterar **duplicate sheet names**, och hur du **save workbook xlsx** på ett pålitligt sätt. Det kompletta exemplet visar ett rent, underhållbart mönster som skalar från snabba skript till produktionsklassade tjänster.

### Vad blir nästa?

* Utforska **conditional formatting** på de genererade bladen för att markera nyckelvärden.  
* Använd **Smart Markers** för att automatiskt fylla i tabeller, diagram eller pivottabeller.  
* Integrera koden i ett ASP.NET Core‑API och returnera XLSX‑filen som en nedladdningsström.

Känn dig fri att experimentera med olika datakällor (JSON, XML eller en databas) och anpassa smart‑marker‑syntaxen för att passa dina rapporteringsbehov. Lycka till med kodandet!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i denna guide. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Skapa Excel-arbetsbok C# – Steg‑för‑steg‑guide för att skriva datum & spara som XLSX](/cells/english/net/excel-workbook/create-excel-workbook-c-step-by-step-guide-to-write-dates-sa/)
- [Skapa ny arbetsbok i C# – Lägg till formel och spara Excel‑fil](/cells/english/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/)
- [Skapa excel‑arbetsbok och spara den till fil i C#](/cells/english/net/excel-workbook/create-excel-workbook-and-save-it-to-file-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}