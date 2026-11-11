---
category: general
date: 2026-10-26
description: Lär dig hur du importerar en DataTable till ett Excel‑ark med C# och
  Aspose.Cells, och bevarar stilar och rubriker med bara några rader kod.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to import datatable
- ImportTableOptions
- ImportDataTableStyle
- Aspose.Cells
- Excel worksheet import
- C# DataTable import
language: sv
lastmod: 2026-10-26
og_description: hur du importerar en datatabell till ett Excel‑kalkylblad med C# och
  Aspose.Cells. Följ den här kompletta guiden för att bevara stilar, rubriker och
  formatering.
og_image_alt: Screenshot of C# code that imports a DataTable into an Excel worksheet
  with Aspose.Cells
og_title: Hur du importerar DataTable till ett Excel‑blad – C# steg‑för‑steg‑guide
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to import DataTable into an Excel worksheet with C# and Aspose.Cells,
    preserving styles and headers in just a few lines of code.
  headline: How to import DataTable into an Excel worksheet using C#
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: Hur man importerar DataTable till ett Excel‑ark med C#
url: /sv/net/excel-data-import-export/how-to-import-datatable-into-an-excel-worksheet-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man importerar DataTable till ett Excel‑blad med C#

Om du behöver **hur man importerar datatable** till ett Excel‑blad, visar den här guiden de exakta stegen i C#. Oavsett om du bygger en rapporteringsmotor eller exporterar rutnätsdata, får du se hur du behåller kolumnrubriker och cellstilar intakta med Aspose.Cells. Lösningen fungerar med .NET 6+ och kräver bara några få rader kod.

Att importera en DataTable är en vanlig uppgift när man arbetar med kalkylblad, men utvecklare glömmer ofta att aktivera stilöverföring eller att skicka header‑flaggan korrekt. I den här handledningen lär du dig hur du konfigurerar **ImportTableOptions**, slår på **ImportDataTableStyle**, och anropar `ImportDataTable` på ett säkert sätt. I slutet har du en färdig metod som du kan klistra in i vilket C#‑projekt som helst.

## Förutsättningar

Innan du börjar, se till att du har:

* .NET 6 SDK eller senare installerat.
* En licensierad kopia av **Aspose.Cells for .NET** (gratis provversion fungerar för testning).
* Grundläggande kunskap om `DataTable` och Excel‑koncept.
* En IDE såsom Visual Studio 2022 (valfri editor som stödjer C# fungerar).

Inga extra NuGet‑paket krävs utöver `Aspose.Cells`.

## Steg 1: Hämta källdata till en DataTable

Det första du gör när du svarar på **hur man importerar datatable** är att ha datan klar. I de flesta verkliga scenarier kommer `DataTable` från en databasfråga, en CSV‑parser eller en samling i minnet. Här är ett minimalt exempel som skapar en tabell med några rader:

```csharp
using System;
using System.Data;

public static DataTable GetSampleData()
{
    var table = new DataTable("Employees");
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Department", typeof(string));

    table.Rows.Add(1, "Alice Johnson", "Finance");
    table.Rows.Add(2, "Bob Smith", "Engineering");
    table.Rows.Add(3, "Carol White", "Marketing");

    return table;
}
```

*Varför detta är viktigt*: Genom att konstruera `DataTable` först styr du kolumnordning, datatyper och rubriknamn – allt som bevaras när du senare importerar tabellen till ett Excel‑blad.

## Steg 2: Skapa `ImportTableOptions` och aktivera stilimport

När du svarar på **hur man importerar datatable**, är nästa beslut om du vill ha den visuella stilen (typsnitt, färger, kanter) som redan kan vara definierad på käll‑`DataTable`. Aspose.Cells tillhandahåller klassen `ImportTableOptions` för fin‑granulär kontroll. Att sätta `ImportDataTableStyle = true` kopierar stilinformationen till mål‑arbetsbladet.

```csharp
using Aspose.Cells;

public static ImportTableOptions CreateImportOptions()
{
    var options = new ImportTableOptions
    {
        // Preserve the style of the DataTable cells (font, background, borders)
        ImportDataTableStyle = true
    };
    return options;
}
```

*Varför detta är viktigt*: Utan att aktivera `ImportDataTableStyle` skulle de importerade cellerna använda standardstilen för arbetsbladet, och förlora all anpassad formatering du eventuellt har applicerat på `DataTable`. Denna flagga är avgörande för en polerad export.

## Steg 3: Importera DataTable till arbetsbladet, inklusive rubriker

Nu har du allt du behöver för att svara på **hur man importerar datatable** till en Excel‑fil. Du skapar en arbetsbok, väljer ett arbetsblad och anropar `ImportDataTable`. Metodens andra argument (`true`) talar om för Aspose.Cells att skriva kolumnrubriker som den första raden.

```csharp
using Aspose.Cells;
using System.IO;

public static void ExportDataTableToExcel(string filePath)
{
    // 1️⃣ Retrieve the source data
    DataTable dataTable = GetSampleData();

    // 2️⃣ Prepare import options (style preservation)
    ImportTableOptions importOptions = CreateImportOptions();

    // 3️⃣ Create a new workbook and select the first worksheet
    var workbook = new Workbook();
    Worksheet ws = workbook.Worksheets[0];
    ws.Name = "Employees";

    // 4️⃣ Import the DataTable, include headers, and apply options
    ws.Cells.ImportDataTable(dataTable, true, importOptions);

    // 5️⃣ Save the workbook to the specified path
    workbook.Save(filePath, SaveFormat.Xlsx);
}
```

När du kör `ExportDataTableToExcel("Employees.xlsx")` skapas en `Employees.xlsx`‑fil där den första raden innehåller **Id**, **Name** och **Department**, och varje cell behåller den stil som definierades i den ursprungliga `DataTable`.

### Fullt körbart exempel

Nedan följer ett komplett, självständigt konsolprogram som demonstrerar **hur man importerar datatable** och sparar resultatet i den aktuella katalogen. Kopiera‑klistra in det i ett nytt konsolprojekt och kör.

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace DataTableImportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            string outputPath = Path.Combine(Directory.GetCurrentDirectory(), "Employees.xlsx");
            ExportDataTableToExcel(outputPath);
            Console.WriteLine($"Excel file created at: {outputPath}");
        }

        // Retrieves sample data
        private static DataTable GetSampleData()
        {
            var table = new DataTable("Employees");
            table.Columns.Add("Id", typeof(int));
            table.Columns.Add("Name", typeof(string));
            table.Columns.Add("Department", typeof(string));

            table.Rows.Add(1, "Alice Johnson", "Finance");
            table.Rows.Add(2, "Bob Smith", "Engineering");
            table.Rows.Add(3, "Carol White", "Marketing");
            return table;
        }

        // Configures import options to keep styles
        private static ImportTableOptions CreateImportOptions()
        {
            return new ImportTableOptions
            {
                ImportDataTableStyle = true
            };
        }

        // Performs the import and saves the workbook
        private static void ExportDataTableToExcel(string filePath)
        {
            DataTable dataTable = GetSampleData();
            ImportTableOptions importOptions = CreateImportOptions();

            var workbook = new Workbook();
            Worksheet ws = workbook.Worksheets[0];
            ws.Name = "Employees";

            // Here we answer the core question: how to import datatable
            ws.Cells.ImportDataTable(dataTable, true, importOptions);
            workbook.Save(filePath, SaveFormat.Xlsx);
        }
    }
}
```

**Förväntad output**  
När du öppnar `Employees.xlsx` ser du:

| Id | Name          | Department |
|----|---------------|------------|
| 1  | Alice Johnson | Finance    |
| 2  | Bob Smith     | Engineering|
| 3  | Carol White   | Marketing  |

Alla celler behåller standard‑DataTable‑stilen (typsnitt, justering). Om du har applicerat anpassade stilar på `DataTable` innan import, visas dessa stilar identiskt i arbetsbladet eftersom `ImportDataTableStyle` är satt till `true`.

## Vanliga fallgropar och bästa praxis‑tips

| Problem | Varför det händer | Hur du undviker det |
|---------|-------------------|----------------------|
| **Rubriker saknas** | `false` skickas som andra argument till `ImportDataTable`, vilket hoppar över kolumnnamnen. | Använd alltid `true` när du behöver rubriker, eller skriv dem manuellt innan importen. |
| **Stil överförs inte** | Glömt att aktivera `ImportDataTableStyle`. | Sätt `ImportDataTableStyle = true` i `ImportTableOptions`. |
| **Stora tabeller ger prestandaproblem** | Import av miljontals rader utan sidindelning. | Importera i batcher eller använd `ImportDataTable` med `startRow`‑överladdning för att strömma data. |
| **Fel arbetsbladreferens** | Använder `workbook.Worksheets[1]` när bara ett blad finns. | Använd `workbook.Worksheets[0]` eller skapa ett nytt blad med `workbook.Worksheets.Add()`. |
| **Licensutgång** | Aspose.Cells‑provan ger ett vattenstämpel efter 30 dagar. | Applicera en giltig licens med `License license = new License(); license.SetLicense("Aspose.Cells.lic");`. |

**Pro‑tips**: Om du behöver applicera ett eget tema efter import, anropa `ws.Cells.ApplyStyle(style)` där `style` är ett `Style`‑objekt du konfigurerar en gång och återanvänder för rader.

## Utöka lösningen

Nu när du vet **hur man importerar datatable** kan du utforska relaterade scenarier:

* **Importera flera tabeller** – upprepa importen på olika arbetsblad.
* **Villkorsstyrd formatering** – efter import, lägg till regler med `ws.Cells.ApplyConditionalFormatting`.
* **Exportera till CSV** – använd `workbook.Save("file.csv", SaveFormat.Csv)` om ett ren‑text‑format krävs.
* **Läsa tillbaka till en DataTable** – använd `ws.Cells.ExportDataTable` för att verifiera rund‑resan‑integritet.

Alla dessa utökningar bygger på det grundläggande mönster som demonstrerats ovan: hämta data, konfigurera importalternativ och anropa en enda Aspose.Cells‑metod.

## Slutsats

Du har nu ett komplett, produktionsklart svar på **hur man importerar datatable** till ett Excel‑blad med C#. Handledningen täckte hämtning av källdata, konfiguration av `ImportTableOptions` med `ImportDataTableStyle` och själva importen med `ImportDataTable`. Genom att följa kodexemplet bevarar du automatiskt rubriker och stilar, och du kan anpassa mönstret för större dataset, flera blad eller ytterligare formateringsbehov.

Redo att automatisera ditt rapporteringsflöde? Prova att byta ut exempel‑`DataTable` mot en riktig databasfråga, experimentera med anpassade cellstilar och integrera metoden i ditt befintliga servicelag. Lycka till med kodandet!


## Vad bör du lära dig härnäst?


Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationssätt i dina egna projekt.

- [How to Import Arrays into Excel Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/import-export/import-arrays-excel-aspose-cells-net/)
- [How to Import XML Data into Excel with Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/import-export/import-xml-data-net-aspose-cells-guide/)
- [How to Import HTML-Formatted DataTables into Excel Using Aspose.Cells for .NET](/cells/english/net/import-export/aspose-cells-net-data-table-import-html-formatting/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}