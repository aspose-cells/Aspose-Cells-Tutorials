---
category: general
date: 2026-04-07
description: Hoe een sjabloon te laden en een Excel‑rapport te genereren met SmartMarker.
  Leer hoe je een Excel‑sjabloon verwerkt, een blad automatisch hernoemt en een Excel‑sjabloon
  efficiënt laadt.
draft: false
keywords:
- how to load template
- create excel report
- process excel template
- how to rename sheet
- load excel template
language: nl
og_description: Hoe een sjabloon te laden in C# en een Excel‑rapport te maken. Deze
  gids behandelt het verwerken van een Excel‑sjabloon, automatische bladhernoeming
  en best practices.
og_title: Hoe een sjabloon te laden en een Excel-rapport te maken – volledige gids
tags:
- Aspose.Cells
- C#
- Excel automation
title: Hoe een sjabloon te laden en een Excel‑rapport te maken met SmartMarker
url: /nl/net/smart-markers-dynamic-data/how-to-load-template-and-create-excel-report-with-smartmarke/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een sjabloon te laden en een Excel‑rapport te maken met SmartMarker

Heb je je ooit afgevraagd **how to load template** en dit om te zetten in een gepolijst Excel‑rapport met slechts een paar regels C#? Je bent niet de enige—veel ontwikkelaars lopen tegen dit probleem aan wanneer ze voor het eerst proberen rapportage te automatiseren. Het goede nieuws is dat je met Aspose.Cells SmartMarker **process excel template**‑bestanden kunt verwerken, automatisch werkbladen kunt hernoemen wanneer nodig, en een voltooid werkboek kunt genereren zonder Excel te openen.

In deze tutorial lopen we elke stap door, van het laden van het sjabloonbestand tot het opslaan van het uiteindelijke rapport. Aan het einde weet je **how to rename sheet** on the fly, hoe je **create excel report** vanuit een gegevensbron maakt, en waarom **load excel template** op de juiste manier belangrijk is voor prestaties en onderhoudbaarheid.

---

## Wat je nodig hebt

- **Aspose.Cells for .NET** (versie 23.10 of nieuwer) – de bibliotheek die SmartMarker aandrijft.
- Een **template.xlsx**‑bestand dat al Smart Markers bevat zoals `&=CustomerName` of `&=OrderDetails`.
- Basiskennis van C# en .NET (elke recente versie werkt).
- Een IDE naar keuze – Visual Studio, Rider, of zelfs VS Code.

Er zijn geen extra NuGet‑pakketten nodig naast Aspose.Cells. Als je de bibliotheek nog niet hebt, voer dan uit:

```bash
dotnet add package Aspose.Cells
```

Dat is alles. Laten we beginnen.

---

## Hoe een sjabloon te laden en te verwerken met SmartMarker

Het eerste dat je moet doen is het sjabloon in het geheugen laden. Hier is **how to load template** echt van belang: je wilt één `Workbook`‑instantie die je kunt hergebruiken voor meerdere rapporten zonder het bestand elke keer opnieuw van de schijf te lezen.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

class ExcelReportGenerator
{
    static void Main()
    {
        // 1️⃣ Load the Excel template (the “how to load template” step)
        // -------------------------------------------------------------
        // The Workbook constructor reads the file into a stream.
        // If the file is large, consider using a FileStream with
        // FileAccess.Read to avoid locking the file.
        Workbook workbook = new Workbook(@"C:\Reports\template.xlsx");

        // 2️⃣ Set up SmartMarker options – we’ll enable automatic sheet renaming
        // ----------------------------------------------------------------------
        SmartMarkerProcessor processor = new SmartMarkerProcessor();
        processor.Options.DetailSheetNewName = true;   // how to rename sheet automatically

        // 3️⃣ Prepare a realistic data source – here we use an anonymous object.
        // ---------------------------------------------------------------
        var dataSource = new
        {
            ReportDate = DateTime.Today,
            CustomerName = "Acme Corp",
            Orders = new[]
            {
                new { Item = "Widget A", Qty = 10, Price = 9.99 },
                new { Item = "Widget B", Qty = 5,  Price = 19.99 },
                new { Item = "Widget C", Qty = 2,  Price = 49.99 }
            }
        };

        // 4️⃣ Run the processor – this is the core of “process excel template”
        // -------------------------------------------------------------------
        processor.Process(workbook, dataSource);

        // 5️⃣ Save the final report
        // -------------------------
        string outputPath = @"C:\Reports\Report.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);
        Console.WriteLine($"Report generated at: {outputPath}");
    }
}
```

### Waarom elke regel belangrijk is

1. **Loading the template** (`new Workbook(...)`) is de basis. Als je deze stap overslaat of een verkeerd pad gebruikt, zal de processor een *FileNotFoundException* werpen.  
2. **Enabling `DetailSheetNewName`** vertelt SmartMarker om automatisch een suffix zoals “(1)” toe te voegen wanneer er al een werkblad met de naam “Detail” bestaat. Dat is de essentie van **how to rename sheet** zonder extra code te schrijven.  
3. **Data source** kan een `DataTable`, een lijst van objecten, of zelfs een JSON‑string zijn. Aspose.Cells zal de markers koppelen aan de overeenkomende eigenschapsnamen.  
4. **`processor.Process`** doet het zware werk—markers vervangen, tabellen uitbreiden, en nieuwe werkbladen aanmaken als je sjabloon een `detail`‑marker bevat.  
5. **Saving** van het werkboek maakt het rapport af, klaar om te e-mailen, af te drukken, of te uploaden naar een SharePoint‑bibliotheek.

---

## Een Excel‑rapport maken vanuit het verwerkte werkboek

Nu het sjabloon is verwerkt, heb je een volledig ingevuld werkboek. De volgende stap is ervoor te zorgen dat het gegenereerde bestand voldoet aan de verwachtingen van de eindgebruiker.

### Controleer de output

Open het opgeslagen `Report.xlsx` en kijk naar:

- De **ReportDate**‑cel gevuld met de datum van vandaag.
- De **CustomerName**‑cel die “Acme Corp” toont.
- Een **Orders**‑tabel met drie rijen, elk overeenkomend met de gegevensbron.
- Als het sjabloon al een werkblad met de naam “Detail” bevatte, zie je een nieuw werkblad genaamd “Detail (1)” – bewijs dat **how to rename sheet** heeft gewerkt.

### Exporteren naar andere formaten (optioneel)

Aspose.Cells stelt je in staat om met één regel op te slaan naar PDF, CSV, of zelfs HTML:

```csharp
workbook.Save(@"C:\Reports\Report.pdf", SaveFormat.Pdf);
```

Handig wanneer belanghebbenden een niet‑bewerkbaar formaat verkiezen.

---

## Hoe een werkblad te hernoemen wanneer het al bestaat – Geavanceerde opties

Soms is de standaard “(1)” suffix niet voldoende. Misschien heb je een tijdstempel of een aangepast voorvoegsel nodig. Je kunt de `DetailSheetNewName`‑logica koppelen door een aangepaste delegate te leveren:

```csharp
processor.Options.DetailSheetNewName = true;
processor.Options.DetailSheetNameGenerator = (baseName, index) =>
{
    // Example: "Detail_20240407_01"
    string datePart = DateTime.Now.ToString("yyyyMMdd");
    return $"{baseName}_{datePart}_{index:D2}";
};
```

**Why bother?** In een batch‑verwerkingssituatie kun je tientallen rapporten in dezelfde map genereren. Unieke werkbladnamen voorkomen verwarring wanneer hetzelfde sjabloon meerdere keren binnen één werkboek wordt hergebruikt.

---

## Excel‑sjabloon laden – Best practices en prestatietips

Wanneer je **load excel template** in een high‑throughput service, overweeg dan deze trucs:

| Tip | Reason |
|-----|--------|
| **Reuse `Workbook` objects** wanneer het sjabloon nooit verandert. | Vermindert I/O en versnelt de verwerking. |
| **Use `FileStream` with `FileShare.Read`** als meerdere threads hetzelfde bestand kunnen lezen. | Voorkomt bestandsvergrendelings‑exceptions. |
| **Disable calculation engine** (`workbook.Settings.CalcEngine = false`) vóór verwerking als het sjabloon veel formules bevat die toch opnieuw worden berekend. | Vermindert CPU‑tijd. |
| **Compress the output** (`SaveFormat.Xlsx` comprimeert al als zip) maar je kunt ook opslaan als `Xlsb` voor binair formaat als de bestandsgrootte cruciaal is. | Kleinere bestanden, snellere downloads. |

---

## Veelvoorkomende valkuilen en pro‑tips

- **Missing markers** – Als een marker in het sjabloon niet overeenkomt met een eigenschap in de gegevensbron, laat SmartMarker deze simpelweg onaangeroerd. Controleer de spelling of gebruik `processor.Options.PreserveUnusedMarkers = false` om ze te verbergen.  
- **Large data sets** – Voor duizenden rijen, schakel `processor.Options.EnableStreaming = true` in. Dit streamt gegevens naar het bestand in plaats van alles in het geheugen te laden.  
- **Date formatting** – SmartMarker respecteert het bestaande getalformaat van de cel. Als je een aangepast formaat nodig hebt, stel dit in het sjabloon in (bijv. `mm/dd/yyyy`).  
- **Thread safety** – Elke `SmartMarkerProcessor`‑instantie is **niet** thread‑safe. Maak een nieuwe instantie per verzoek of wikkel het in een `using`‑block.

---

## Volledig werkend voorbeeld (Alle code op één plek)

Hieronder staat het volledige, kant‑klaar te kopiëren programma dat alles bevat wat we hebben behandeld:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

class ExcelReportGenerator
{
    static void Main()
    {
        // Load the template – primary step for "how to load template"
        Workbook workbook = new Workbook(@"C:\Reports\template.xlsx");

        // Configure SmartMarker processor
        SmartMarkerProcessor processor = new SmartMarkerProcessor
        {
            Options = {
                DetailSheetNewName = true,
                // Optional custom naming:
                // DetailSheetNameGenerator = (baseName, idx) =>
                //     $"{baseName}_{DateTime.Now:yyyyMMdd}_{idx:D2}"
            }
        };

        // Sample data source – replace with your real data source
        var dataSource = new
        {
            ReportDate = DateTime.Today,
            CustomerName = "Acme Corp",
            Orders = new[]
            {
                new { Item = "Widget A", Qty = 10, Price = 9.99 },
                new { Item = "Widget B", Qty = 5,  Price = 19.99 },
                new { Item = "Widget C", Qty = 2,  Price = 49.99 }
            }
        };

        // Process the template – core of "process excel template"
        processor.Process(workbook, dataSource);

        // Save the final report – this creates the Excel file you can share
        string outputPath = @"C:\Reports\Report.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Report generated successfully at {outputPath}");
    }
}
```

Voer het programma uit, open `Report.xlsx`, en je ziet een volledig ingevuld **excel report** klaar voor distributie.

---

## Conclusie

We hebben **how to load template**, hoe **process excel template** met SmartMarker, de nuances van **how to rename sheet** automatisch, en best practices voor **load excel template** efficiënt behandeld. Door de bovenstaande stappen te volgen kun je elk vooraf ontworpen werkboek omzetten in een dynamische rapportgenerator—geen handmatig kopiëren‑plakken nodig.

Klaar voor de volgende uitdaging? Probeer de processor te voeden met een `DataTable` die uit een SQL‑query komt, of exporteer het resultaat naar PDF voor een één‑klik‑rapportageoplossing. De mogelijkheden zijn eindeloos wanneer je Aspose.Cells combineert met een solide template‑gedreven aanpak.

Heb je vragen, of een lastig randgeval ontdekt? Laat een reactie achter—laten we het gesprek gaande houden. Veel plezier met coderen! 

![Hoe sjabloon te laden in Excel met SmartMarker](/images/how-to-load-template-excel.png "hoe sjabloon te laden")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}