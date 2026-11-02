---
category: general
date: 2026-03-22
description: Aangepaste getalnotatie Excel‑tutorial die laat zien hoe je een datatabel
  naar Excel importeert, de achtergrondkleur van een kolom instelt, een kolom als
  valuta formatteert en de werkmap opslaat als xlsx.
draft: false
keywords:
- custom number format excel
- import datatable to excel
- set column background color
- format column as currency
- save workbook as xlsx
language: nl
og_description: Aangepaste getalnotatie Excel‑tutorial die je stap voor stap begeleidt
  bij het importeren van een DataTable, het instellen van de achtergrondkleur van
  een kolom, het opmaken van een kolom als valuta en het opslaan van de werkmap als
  xlsx.
og_title: Aangepast getalformaat Excel in C# – Stapsgewijze handleiding
tags:
- C#
- Excel automation
- Aspose.Cells
- Data export
title: Aangepast getalformaat Excel in C# – Complete gids
url: /nl/net/excel-custom-number-date-formatting/custom-number-format-excel-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aangepast Getalformaat Excel – Full‑Stack C# Tutorial

Heb je je ooit afgevraagd hoe je een **custom number format excel** stijl direct vanuit C# kunt toepassen? Misschien heb je geprobeerd een DataTable in een spreadsheet te dumpen, maar alleen platte getallen te zien, geen kleuren en geen valuta‑opmaak. Dat is een veelvoorkomend pijnpunt—vooral wanneer je een gepolijst rapport voor belanghebbenden nodig hebt.

In deze gids lossen we dat probleem samen op: je leert hoe je **import datatable to excel**, **set column background color**, **format column as currency**, en uiteindelijk **save workbook as xlsx** met een aangepast getalformaat dat je cijfers laat opvallen. Geen vage verwijzingen, alleen een complete, uitvoerbare oplossing die je kunt copy‑paste in je project.

---

## Wat je gaat bouwen

Aan het einde van deze tutorial heb je een zelfstandige C# console‑app die:

1. Haalt een `DataTable` op (je kunt de stub vervangen door je eigen query).  
2. Maakt een nieuw Excel‑werkboek aan met Aspose.Cells (of een andere compatibele bibliotheek).  
3. Past een blauw, vet lettertype toe op de eerste kolom, een licht‑gele achtergrond op de tweede, en een valuta‑formaat (`$#,##0.00`) op de derde.  
4. Slaat het bestand op als `DataTableWithStyleArray.xlsx` in een map naar keuze.

Je ziet precies hoe elke regel bijdraagt aan het uiteindelijke Excel‑bestand, en we bespreken waarom die keuzes belangrijk zijn voor onderhoudbaarheid en prestaties.

---

## Vereisten

- .NET 6.0 of later (de code werkt ook met .NET Framework 4.7+).  
- Aspose.Cells voor .NET (gratis proefversie of gelicentieerde versie). Installeer via NuGet:

```bash
dotnet add package Aspose.Cells
```

- Basiskennis van `DataTable` en C# console‑applicaties.

---

## Stap 1: Haal de brongegevens op als een DataTable

Eerst hebben we wat gegevens nodig om te exporteren. In een real‑world scenario zou je waarschijnlijk een repository aanroepen of een SQL‑query uitvoeren. Voor illustratie maken we een eenvoudige tabel in‑memory.

```csharp
using System;
using System.Data;
using Aspose.Cells;

static DataTable GetSampleData()
{
    var table = new DataTable("Sales");
    table.Columns.Add("Product", typeof(string));
    table.Columns.Add("Quantity", typeof(int));
    table.Columns.Add("Revenue", typeof(decimal));

    table.Rows.Add("Widget A", 120, 3450.75m);
    table.Rows.Add("Widget B", 85, 2190.00m);
    table.Rows.Add("Widget C", 60, 1580.40m);

    return table;
}
```

> **Waarom dit belangrijk is:** Het gebruik van een `DataTable` geeft je een tabel‑achtige, schema‑bewuste bron die netjes overeenkomt met Excel‑rijen en -kolommen. Het stelt je ook in staat om dezelfde exportlogica te hergebruiken voor elke dataset zonder de code opnieuw te schrijven.

---

## Stap 2: Maak een nieuw werkboek aan en pak het eerste werkblad

Nu maken we een Excel‑werkboek aan. De `Workbook`‑klasse vertegenwoordigt het volledige bestand; `Worksheets[0]` is het standaardblad waarop we onze gegevens zullen plaatsen.

```csharp
// Initialize a fresh workbook
Workbook workbook = new Workbook();

// Grab the first (and only) worksheet
Worksheet worksheet = workbook.Worksheets[0];
```

> **Pro tip:** Als je meerdere bladen nodig hebt, roep dan gewoon `workbook.Worksheets.Add("SheetName")` aan en herhaal de stijl‑stappen voor elk blad.

---

## Stap 3: Definieer kolomstijlen – Lettertype, achtergrond en getalformaat

Stijlen in Aspose.Cells worden gedaan via `Style`‑objecten. We bouwen een array waarbij elk element overeenkomt met een kolom in de DataTable.

```csharp
// Prepare an array to hold three distinct styles
Style[] columnStyles = new Style[3];

// 1️⃣ First column – blue, bold font
columnStyles[0] = workbook.CreateStyle();
columnStyles[0].Font.Color = System.Drawing.Color.Blue;
columnStyles[0].Font.IsBold = true;

// 2️⃣ Second column – light‑yellow background
columnStyles[1] = workbook.CreateStyle();
columnStyles[1].ForegroundColor = System.Drawing.Color.LightYellow;
columnStyles[1].Pattern = BackgroundType.Solid;

// 3️⃣ Third column – custom currency format (custom number format excel)
columnStyles[2] = workbook.CreateStyle();
columnStyles[2].Custom = "$#,##0.00";
```

> **Waarom een stijl‑array?** Het doorgeven van een array aan `ImportDataTable` stelt je in staat om een aparte stijl toe te passen op elke kolom in één oproep, wat zowel beknopt als performant is. Het garandeert ook dat de opmaak synchroon blijft met de volgorde van de gegevens.

---

## Stap 4: Importeer de DataTable terwijl je de stijlen toepast

Dit is de kern van de operatie: we voeren de `DataTable` in het werkblad in, vertellen Aspose de koprij op te nemen, en geven onze `columnStyles`‑array door.

```csharp
// Import data starting at cell A1 (row 0, column 0)
worksheet.Cells.ImportDataTable(
    GetSampleData(),   // source DataTable
    true,              // include column names as header
    0, 0,              // start row, start column
    columnStyles);     // apply the style array
```

> **Wat er onder de motorkap gebeurt:** Aspose doorloopt elke kolom, schrijft de kop, en daarna elke rijwaarde. Terwijl het dat doet, past het de overeenkomstige `Style` uit de array toe, zodat je een blauwe kop krijgt voor “Product”, een geel‑getinte “Quantity”, en een mooi opgemaakte “Revenue”‑kolom.

---

## Stap 5: Sla het werkboek op als een XLSX‑bestand

Tot slot slaan we het werkboek op naar schijf. De `Save`‑methode kiest automatisch het XLSX‑formaat op basis van de bestandsextensie.

```csharp
// Choose a folder that exists on your machine
string outputPath = @"C:\Temp\DataTableWithStyleArray.xlsx";

// Ensure the directory exists (optional safety check)
System.IO.Directory.CreateDirectory(System.IO.Path.GetDirectoryName(outputPath)!);

// Save the workbook
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

> **Tip:** Als je het bestand moet streamen (bijv. voor een web‑API), gebruik dan `workbook.Save(stream, SaveFormat.Xlsx)` in plaats van een bestandspad.

---

## Volledig werkend voorbeeld

Hieronder staat het volledige programma dat je kunt plakken in een nieuw console‑project. Het compileert en draait direct, en produceert een gestileerd Excel‑bestand.

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1 – Get data
            DataTable dataTable = GetSampleData();

            // Step 2 – Create workbook & worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // Step 3 – Prepare column styles
            Style[] columnStyles = new Style[3];

            // Font style for first column (blue, bold)
            columnStyles[0] = workbook.CreateStyle();
            columnStyles[0].Font.Color = System.Drawing.Color.Blue;
            columnStyles[0].Font.IsBold = true;

            // Background style for second column (light yellow)
            columnStyles[1] = workbook.CreateStyle();
            columnStyles[1].ForegroundColor = System.Drawing.Color.LightYellow;
            columnStyles[1].Pattern = BackgroundType.Solid;

            // Currency format for third column (custom number format excel)
            columnStyles[2] = workbook.CreateStyle();
            columnStyles[2].Custom = "$#,##0.00";

            // Step 4 – Import data with styles
            worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

            // Step 5 – Save as XLSX
            string outputPath = @"C:\Temp\DataTableWithStyleArray.xlsx";
            System.IO.Directory.CreateDirectory(System.IO.Path.GetDirectoryName(outputPath)!);
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }

        // Helper method to build a demo DataTable
        static DataTable GetSampleData()
        {
            var table = new DataTable("Sales");
            table.Columns.Add("Product", typeof(string));
            table.Columns.Add("Quantity", typeof(int));
            table.Columns.Add("Revenue", typeof(decimal));

            table.Rows.Add("Widget A", 120, 3450.75m);
            table.Rows.Add("Widget B", 85, 2190.00m);
            table.Rows.Add("Widget C", 60, 1580.40m);

            return table;
        }
    }
}
```

### Verwacht resultaat

Wanneer je `DataTableWithStyleArray.xlsx` opent, zie je:

| **Product** (blue, bold) | **Quantity** (light‑yellow) | **Revenue** (currency) |
|--------------------------|-----------------------------|------------------------|
| Widget A                 | 120                         | $3,450.75              |
| Widget B                 | 85                          | $2,190.00              |
| Widget C                 | 60                          | $1,580.40              |

Het **custom number format excel** dat je hebt opgegeven (`$#,##0.00`) zorgt ervoor dat elke omzetcel een dollarteken, duizendtallen‑scheidingsteken en twee decimalen toont—precies wat financiële teams verwachten.

---

## Veelgestelde vragen & randgevallen

### Kan ik dit gebruiken met een andere Excel‑bibliotheek?

Absoluut. Het concept—een stijl per kolom maken en die toepassen tijdens het importeren—kan worden overgezet naar EPPlus, ClosedXML of NPOI. De API‑aanroepen verschillen, maar het patroon blijft hetzelfde.

### Wat als mijn DataTable meer kolommen heeft dan stijlen?

Aspose zal de standaardstijl toepassen op elke kolom zonder een overeenkomend item in de `columnStyles`‑array. Om verrassingen te vermijden, zorg ervoor dat de array de grootte `dataTable.Columns.Count` heeft of genereer stijlen dynamisch in een lus.

### Hoe stel ik een aangepast getalformaat in voor datums?

Stel gewoon `style.Custom = "dd‑mm‑yyyy"` in (of een andere geldige Excel‑formaatstring). Dezelfde array‑gebaseerde aanpak werkt voor datums, percentages of wetenschappelijke notatie.

### Is er een manier om kolommen automatisch te dimensioneren na import?

Ja—roep `worksheet.AutoFitColumns();` aan na de import. Het voert een snelle breedte‑berekening uit op basis van de celinhoud.

### Wat met grote datasets (100k+ rijen)?

`ImportDataTable` is geoptimaliseerd voor bulk‑operaties, maar je kunt geheugenlimieten tegenkomen. In dat geval kun je overwegen om rijen handmatig te streamen met `Cells[i, j].PutValue(...)` en een enkele `Style`‑object te hergebruiken om overhead te verminderen.

---

## Pro‑tips & veelvoorkomende valkuilen

- **Vermijd hard‑coded paden** in productcode; gebruik `Environment.GetFolderPath` of configuratie‑instellingen.  
- **Dispose het werkboek** als je in een langdurige service werkt—omsluit het in een `using`‑blok om native resources vrij te geven.  
- **Let op cultuur‑specifieke scheidingstekens**. Het aangepaste formaat `$#,##0.00` dwingt een punt als decimale scheidingsteken af, ongeacht de OS‑locale, wat meestal gewenst is voor financiële rapporten.  
- **Vergeet niet System.Drawing te refereren** (of `System.Drawing.Common` op .NET Core) voor de kleur‑structs die bij het stijlen worden gebruikt.  
- **Test de output op verschillende Excel‑versies**; oudere versies kunnen sommige aangepaste formaten iets anders interpreteren.

---

## Conclusie

We hebben alles behandeld wat je nodig hebt om **custom number format excel** bestanden vanuit C# te maken: gegevens ophalen uit een `DataTable`, **import datatable to excel**, een **set column background color** toepassen, **format column as currency** gebruiken, en uiteindelijk **save workbook as x

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}