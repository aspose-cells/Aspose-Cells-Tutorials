---
category: general
date: 2026-09-24
description: Maak een Excel-werkmap programmatisch en leer hoe je meerdere detailbladen
  maakt, en sla vervolgens de werkmap op als xlsx‑bestand met een duidelijk C#‑voorbeeld.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook programmatically
- how to create multiple detail sheets
- save workbook as xlsx file
language: nl
lastmod: 2026-09-24
og_description: Maak een Excel-werkmap programmatically, zie hoe je meerdere detailbladen
  maakt en de werkmap opslaat als xlsx‑bestand in één uitvoerbaar voorbeeld.
og_image_alt: Screenshot of an Excel workbook created programmatically in C#
og_title: Maak een Excel-werkmap via code – volledige C#-gids
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Create Excel workbook programmatically and learn how to create multiple
    detail sheets, then save workbook as xlsx file with a clear C# example.
  headline: Create Excel workbook programmatically using Smart Markers
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
title: Creëer Excel-werkmap programmatisch met Smart Markers
url: /nl/net/smart-markers-dynamic-data/create-excel-workbook-programmatically-using-smart-markers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel-werkmap programmatically maken met Smart Markers

Als je **een Excel-werkmap programmatically wilt maken**, laat deze gids je precies zien hoe je dat doet met Aspose.Cells .NET. Je ontdekt ook **hoe je meerdere detailbladen kunt maken** vanuit één gegevensbron en uiteindelijk **de werkmap kunt opslaan als xlsx‑bestand** zonder handmatige stappen.  

De oplossing is volledig zelf‑voorzien: we lopen elke regel code door, leggen uit waarom elke instelling belangrijk is, en behandelen veelvoorkomende valkuilen zoals dubbele bladnamen. Aan het einde heb je een kant‑klaar console‑programma dat een werkmap produceert met een masterblad en een reeks detailbladen.

## Wat je nodig hebt

| Vereiste | Reden |
|--------------|--------|
| .NET 6.0 SDK of later | Biedt de runtime voor de C# console‑app |
| Aspose.Cells for .NET (NuGet‑pakket `Aspose.Cells`) | Levert de klassen `Workbook`, `SmartMarkerProcessor` en `SmartMarkerOptions` |
| Een eenvoudige gegevensbron (bijv. `DataTable` of een lijst met objecten) | Levert de waarden die Smart Markers zullen uitbreiden |
| Visual Studio 2022 of een andere editor die .NET ondersteunt | Maakt het eenvoudig om de code te compileren en uit te voeren |

> **Pro tip:** Installeer het Aspose.Cells‑pakket via de CLI voordat je begint:  
> `dotnet add package Aspose.Cells`

## Stap 1: Het project instellen en namespaces importeren

Maak een nieuw console‑project aan en breng de benodigde namespaces in scope.

```csharp
using System;
using System.Data;               // For DataTable (sample data source)
using Aspose.Cells;              // Core Excel API
using Aspose.Cells.SmartMarkers; // Smart Marker processing
```

*Waarom dit belangrijk is*: `Aspose.Cells` beheert de levenscyclus van de werkmap, terwijl `Aspose.Cells.SmartMarkers` je de krachtige Smart Marker‑engine biedt die veel bladen kan genereren vanuit één sjabloon.

## Stap 2: De Excel-werkmap programmatically maken

De eerste concrete actie is het instantieren van een `Workbook`. Dit object vertegenwoordigt het volledige Excel‑bestand in het geheugen.

```csharp
// Step 2: Create a new workbook (or load an existing template)
Workbook workbook = new Workbook(); // an empty workbook with one default sheet
```

Als je liever begint vanuit een sjabloon dat al koprijen of opmaak bevat, vervang dan `new Workbook()` door `new Workbook("Template.xlsx")`. De rest van het proces werkt identiek.

## Stap 3: Een Smart Marker‑sjabloon voorbereiden

Smart Markers werken op celinhoud die placeholders bevat zoals `&=Employees.Name`. Voor deze tutorial voegen we een eenvoudig sjabloon direct via code toe, maar je kunt het blad ook handmatig in Excel bewerken.

```csharp
// Access the first worksheet (index 0)
Worksheet sheet = workbook.Worksheets[0];

// Write a header row
sheet.Cells["A1"].PutValue("Employee Report");

// Insert a Smart Marker that will generate a detail sheet for each employee
sheet.Cells["A3"].PutValue("&=Employees.Name");

// Optional: add column titles for the detail sheet
sheet.Cells["A4"].PutValue("Name");
sheet.Cells["B4"].PutValue("Department");
sheet.Cells["C4"].PutValue("Salary");
```

*Waarom dit belangrijk is*: De placeholder `&=Employees.Name` vertelt de Smart Marker‑processor om door de `Employees`‑collectie te itereren. Elke iteratie zal een nieuw werkblad aanmaken omdat we de processor configureren om een **detailblad** voor elke rij te maken.

## Stap 4: Een gegevensbron bouwen die meerdere rijen bevat

We gebruiken een `DataTable` als een snelle manier om een collectie van werknemersrecords te simuleren.

```csharp
// Step 4: Create a DataTable with sample employee data
DataTable employees = new DataTable("Employees");
employees.Columns.Add("Name", typeof(string));
employees.Columns.Add("Department", typeof(string));
employees.Columns.Add("Salary", typeof(decimal));

employees.Rows.Add("Alice Johnson", "Finance", 72000);
employees.Rows.Add("Bob Smith", "Engineering", 95000);
employees.Rows.Add("Carol Lee", "Marketing", 63000);
```

Je kunt dit vervangen door elke `IEnumerable` (bijv. `List<Employee>`) – Smart Markers accepteren elke gegevensbron die `IEnumerable` implementeert.

## Stap 5: Smart Marker‑opties configureren – hoe meerdere detailbladen te maken

Standaard schrijven Smart Markers gegevens terug naar hetzelfde blad. Om **meerdere detailbladen** te genereren, moet je de eigenschap `DetailSheetNewName` instellen. Dit toont ook **hoe meerdere detailbladen** te maken zonder naamconflicten.

```csharp
// Step 5: Configure Smart Marker options
SmartMarkerOptions smOptions = new SmartMarkerOptions
{
    // Each iteration will create a new sheet named "Detail"
    DetailSheetNewName = "Detail"
};
```

Als de gegevensbron dubbele namen bevat, voegt de processor automatisch een numeriek achtervoegsel toe (bijv. `Detail_1`, `Detail_2`). Dit voorkomt runtime‑fouten en zorgt ervoor dat alle detailbladen worden opgeslagen.

## Stap 6: De Smart Markers verwerken

Nu roepen we de processor aan, waarbij we de gegevensbron en de opties die we zojuist hebben gedefinieerd doorgeven.

```csharp
// Step 6: Process Smart Markers
workbook.Worksheets[0].SmartMarkerProcessor.Process(employees, smOptions);
```

*Waarom dit belangrijk is*: De processor leest de placeholder `&=Employees.Name`, iterereert over elke rij van `employees`, maakt een nieuw blad genaamd “Detail” aan en schrijft de rij‑gegevens naar dat blad. Het oorspronkelijke blad blijft bestaan als een samenvattend of master‑blad.

## Stap 7: Werkmap opslaan als xlsx‑bestand

Tot slot sla je de werkmap op schijf op met het **save workbook as xlsx file**‑patroon.

```csharp
// Step 7: Save the resulting workbook
string outputPath = @"./output/detail.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}");
```

De `SaveFormat.Xlsx`‑enum garandeert dat het bestand wordt opgeslagen in het moderne Office Open XML‑formaat, dat compatibel is met Excel 2007+ en de meeste clouddiensten.

## Volledig, uitvoerbaar voorbeeld

Kopieer de volgende code naar `Program.cs` van een .NET console‑project en voer het uit. Het programma genereert `detail.xlsx` in de map `output`, met één masterblad en drie detailbladen (één per werknemer).

```csharp
using System;
using System.Data;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace ExcelSmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create an empty workbook
            Workbook workbook = new Workbook();

            // 2️⃣ Build a simple template with a Smart Marker
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Cells["A1"].PutValue("Employee Report");
            sheet.Cells["A3"].PutValue("&=Employees.Name");
            sheet.Cells["A4"].PutValue("Name");
            sheet.Cells["B4"].PutValue("Department");
            sheet.Cells["C4"].PutValue("Salary");

            // 3️⃣ Prepare the data source
            DataTable employees = new DataTable("Employees");
            employees.Columns.Add("Name", typeof(string));
            employees.Columns.Add("Department", typeof(string));
            employees.Columns.Add("Salary", typeof(decimal));

            employees.Rows.Add("Alice Johnson", "Finance", 72000);
            employees.Rows.Add("Bob Smith", "Engineering", 95000);
            employees.Rows.Add("Carol Lee", "Marketing", 63000);

            // 4️⃣ Configure Smart Marker options (how to create multiple detail sheets)
            SmartMarkerOptions smOptions = new SmartMarkerOptions
            {
                DetailSheetNewName = "Detail"
            };

            // 5️⃣ Process the markers
            workbook.Worksheets[0].SmartMarkerProcessor.Process(employees, smOptions);

            // 6️⃣ Save workbook as xlsx file
            string outPath = "./output/detail.xlsx";
            workbook.Save(outPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved to {outPath}");
        }
    }
}
```

**Verwachte output**

- `output/detail.xlsx` bevat:
  - **Sheet1** – het oorspronkelijke sjabloon met de kop “Employee Report”.
  - **Detail** – eerste detailblad met het record van Alice.
  - **Detail_1** – tweede detailblad met het record van Bob.
  - **Detail_2** – derde detailblad met het record van Carol.

Open het bestand in Excel en je ziet elke werknemer op een eigen blad, wat bewijst dat we succesvol **meerdere detailbladen maken** en **de werkmap opslaan als xlsx‑bestand**.

## Veelgestelde vragen & afhandeling van randgevallen

| Vraag | Antwoord |
|----------|--------|
| *Wat als ik een aangepaste naam voor elk detailblad nodig heb?* | Stel `DetailSheetNewName = "Employee_"` in en voeg een kolom met de naam `SheetName` toe aan de gegevensbron. De processor voegt de waarde van `SheetName` toe aan de basisnaam. |
| *Kan ik het oorspronkelijke blad behouden als een samenvatting van alle details?* | Ja. Het masterblad blijft onaangeroerd; je kunt formules toevoegen die verwijzen naar de gegenereerde detailbladen. |
| *Wat gebeurt er als de gegevensbron leeg is?* | Er worden geen detailbladen aangemaakt, maar de werkmap wordt toch opgeslagen. Overweeg `employees.Rows.Count` te controleren vóór het verwerken als je speciale afhandeling nodig hebt. |
| *Is het mogelijk om een bestaand sjabloonbestand te gebruiken?* | Vervang `new Workbook()` door `new Workbook("Template.xlsx")`. Alle Smart Marker‑logica werkt op dezelfde manier. |

## Conclusie

Je weet nu **hoe je een Excel-werkmap programmatically kunt maken**, hoe je **meerdere detailbladen** kunt **maken** met Smart Markers, en hoe je **de werkmap kunt opslaan als xlsx‑bestand** met Aspose.Cells. Het volledige voorbeeld kan worden aangepast voor facturen, rapporten, of elke situatie waarin een master‑detail Excel‑output vereist is.

### Volgende stappen

- Verken andere Smart Marker‑functies zoals **group markers** en **conditional formatting**.
- Vervang de `DataTable` door een echte database‑query om grootschalige rapporten te genereren.
- Gebruik `Workbook.Save("output.pdf", SaveFormat.Pdf)` om dezelfde gegevens naar PDF te exporteren voor distributie.

Voel je vrij om te experimenteren met verschillende naamgevingsschema's, opmaak of extra werkbladen—je nieuwe programmatic Excel‑generatievaardigheden zijn klaar voor productiegebruik. Veel plezier met coderen!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stapsgewijze uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Create Excel Workbook C# – Add Comment & Save as XLSX](/cells/english/net/excel-comment-annotation/create-excel-workbook-c-add-comment-save-as-xlsx/)
- [Create New Workbook in C# – Add Formula and Save Excel File](/cells/english/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/)
- [Create Excel Workbook C# – Insert JSON and Save as XLSX](/cells/english/net/excel-data-import-export/create-excel-workbook-c-insert-json-and-save-as-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}