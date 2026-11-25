---
category: general
date: 2026-11-25
description: Maak een Excel-werkmap in C# en sla deze op als XLSB, terwijl je een
  aangepaste werkblad‑eigenschap instelt voor rapportmetadata.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook c#
- save workbook as xlsb
- set worksheet custom property
- Aspose.Cells Excel export
- C# Excel automation
language: nl
lastmod: 2026-11-25
og_description: Maak een Excel-werkmap in C# en sla deze op als XLSB. Deze gids laat
  zien hoe je een aangepaste eigenschap van een werkblad instelt zodat je rapporten
  de eigenaarsinformatie behouden.
og_image_alt: Screenshot of a C# program creating an Excel workbook and saving it
  as XLSB
og_title: Excel‑werkboek maken in C# – opslaan als XLSB met aangepaste eigenschappen
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Create Excel workbook C# and save as XLSB while setting worksheet custom
    property for report metadata.
  headline: Create Excel workbook C# and save as XLSB
  type: TechArticle
- description: Create Excel workbook C# and save as XLSB while setting worksheet custom
    property for report metadata.
  name: Create Excel workbook C# and save as XLSB
  steps:
  - name: '**Create a new workbook** – the in‑memory representation of an Excel file.'
    text: '**Create a new workbook** – the in‑memory representation of an Excel file.'
  - name: '**Set worksheet custom property** – attach key/value metadata to the first
      sheet.'
    text: '**Set worksheet custom property** – attach key/value metadata to the first
      sheet.'
  - name: '**Save workbook as XLSB** – write the file in the binary XLSB format, which
      keeps the custom property intact.'
    text: '**Save workbook as XLSB** – write the file in the binary XLSB format, which
      keeps the custom property intact.'
  type: HowTo
tags:
- excel
- csharp
- xlsb
- custom-properties
title: Excel-werkmap maken in C# en opslaan als XLSB
url: /nl/net/saving-and-exporting-excel-files-with-options/create-excel-workbook-c-and-save-as-xlsb/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Maak Excel‑werkmap C# en sla op als XLSB

Als je een **Excel‑werkmap C#** moet **maken** voor een rapportageroutine, wil je waarschijnlijk ook dat het bestand extra metadata bevat, zoals de eigenaar van het rapport. Deze tutorial laat zien hoe je een **werkblad‑aangepaste eigenschap** kunt **instellen** en vervolgens de **werkmap kunt opslaan als XLSB** in één reproduceerbare workflow.

Je eindigt met een binair gecodeerd XLSB‑bestand dat in Excel opent, de aangepaste eigenschap behoudt en klaar is voor distributie. Er zijn geen externe scripts nodig — alleen de Aspose.Cells for .NET‑bibliotheek en een paar regels C#.

## Voorvereisten

Voordat je begint, zorg dat je het volgende hebt:

* .NET 6.0 (of hoger) geïnstalleerd – Aspose.Cells ondersteunt .NET Standard 2.0+.
* Een geldige Aspose.Cells‑licentie (of een gratis evaluatiesleutel).  
* Visual Studio 2022 of een andere C#‑IDE naar keuze.

Voeg het NuGet‑pakket toe:

```bash
dotnet add package Aspose.Cells
```

> **Pro tip:** Gebruik de **Aspose.Cells**‑gratis proefversie om runtime‑licentie‑fouten tijdens het testen te vermijden.

## Excel‑werkmap maken C# – overzicht

Het proces bestaat uit drie afzonderlijke acties:

1. **Maak een nieuwe werkmap** – de in‑memory‑representatie van een Excel‑bestand.
2. **Stel werkblad‑aangepaste eigenschap in** – koppel sleutel/waarde‑metadata aan het eerste blad.
3. **Sla werkmap op als XLSB** – schrijf het bestand in het binaire XLSB‑formaat, waardoor de aangepaste eigenschap behouden blijft.

Elke stap wordt geïllustreerd met volledige, uitvoerbare code.

![Create Excel workbook C# screenshot](excel_workbook.png)

## Stap 1: Initialiseer een nieuwe werkmap

```csharp
using Aspose.Cells;

namespace ExcelAutomation
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook
            Workbook workbook = new Workbook();          // creates a default workbook with one worksheet
            Worksheet worksheet = workbook.Worksheets[0]; // reference to the first worksheet
```

**Waarom dit belangrijk is** – `Workbook` is het toegangspunt voor alle Excel‑bewerkingen. Wanneer je het zonder parameters instantiateert, maakt Aspose.Cells een lege werkmap met één werkblad, wat perfect is voor programmatische generatie.

## Stap 2: Stel werkblad‑aangepaste eigenschap in

```csharp
            // Step 2: Add a custom property to the worksheet (e.g., the report owner)
            worksheet.CustomProperties.Add("ReportOwner", "Alice");
```

*`set worksheet custom property`* is de exacte aanroep die de **ReportOwner**‑sleutel met de waarde **Alice** opslaat in de aangepaste‑eigenschapcollectie van het blad. Excel kan deze eigenschap later lezen via **Bestand → Info → Eigenschappen → Geavanceerde eigenschappen**.

> **Veelgestelde vraag:** *Wat als ik meerdere eigenschappen nodig heb?*  
> Roep gewoon `Add` herhaaldelijk aan met verschillende namen, bijv. `worksheet.CustomProperties.Add("Department", "Finance");`.

## Stap 3: Sla werkmap op als XLSB

```csharp
            // Step 3: Save the workbook in XLSB format – the custom property is preserved
            string outputPath = @"YOUR_DIRECTORY\custom_props.xlsb";
            workbook.Save(outputPath, SaveFormat.Xlsb);
        }
    }
}
```

De **save workbook as xlsb**‑regel schrijft het bestand met het binaire XLSB‑formaat. Vergeleken met het klassieke XLSX laadt XLSB sneller bij grote datasets en behoudt aangepaste eigenschappen zonder extra stappen.

### Verwacht resultaat

Na het uitvoeren van het programma:

* `custom_props.xlsb` verschijnt in `YOUR_DIRECTORY`.
* Het openen van het bestand in Excel toont één blad zonder zichtbare data (we hebben alleen metadata toegevoegd).
* Navigeer naar **Bestand → Info → Eigenschappen → Geavanceerde eigenschappen → Aangepast** – je ziet **ReportOwner = Alice**.

## De aangepaste eigenschap programmatisch verifiëren (optioneel)

Als je wilt bevestigen dat de eigenschap de round‑trip heeft overleefd, kun je het bestand opnieuw laden:

```csharp
            // Verify the property after loading
            Workbook loaded = new Workbook(outputPath);
            string owner = loaded.Worksheets[0].CustomProperties["ReportOwner"].Value.ToString();
            System.Console.WriteLine($"Report owner: {owner}"); // should print "Alice"
```

Het uitvoeren van dit fragment geeft weer:

```
Report owner: Alice
```

## Randgevallen en best practices

| Situatie                               | Aanbeveling                                                                      |
|----------------------------------------|---------------------------------------------------------------------------------|
| Grote werkmappen (>10 000 rijen)       | Gebruik **XLSB** omdat de binaire compressie het geheugenverbruik verlaagt.   |
| Cultuurspecifieke data behouden        | Stel `Workbook.Settings.CultureInfo` in voordat je waarden toevoegt.           |
| Meerdere werkbladen hebben dezelfde eigenschap | Loop door `workbook.Worksheets` en voeg de eigenschap aan elk blad toe.        |
| Uitvoering op Linux/macOS              | Zorg dat de Aspose.Cells .NET Standard‑build wordt gerefereerd; geen Windows‑only API’s. |

> **Let op:** Opslaan naar een map zonder schrijfrechten veroorzaakt een `UnauthorizedAccessException`. Valideer altijd het pad of gebruik `Path.GetTempPath()` voor tijdelijke bestanden.

## Volledig, uitvoerbaar voorbeeld

```csharp
using System;
using Aspose.Cells;

namespace ExcelAutomation
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create Excel workbook C#
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Set worksheet custom property
            worksheet.CustomProperties.Add("ReportOwner", "Alice");
            worksheet.CustomProperties.Add("ReportDate", DateTime.Today.ToShortDateString());

            // 3️⃣ Save workbook as XLSB
            string outputPath = @"C:\Temp\custom_props.xlsb";
            workbook.Save(outputPath, SaveFormat.Xlsb);

            // Optional verification
            Workbook loaded = new Workbook(outputPath);
            string owner = loaded.Worksheets[0].CustomProperties["ReportOwner"].Value.ToString();
            Console.WriteLine($"Report owner verified: {owner}");
        }
    }
}
```

Kopieer de code naar een nieuw console‑project, vervang `C:\Temp\` door een map waar je schrijfrechten hebt, en voer uit. De console zal `Report owner verified: Alice` weergeven, wat bewijst dat **create Excel workbook C#**, **set worksheet custom property** en **save workbook as xlsb** allemaal samenwerkten.

## Conclusie

Je weet nu hoe je een **Excel‑werkmap C#** kunt **maken**, een **werkblad‑aangepaste eigenschap** kunt **toevoegen**, en de **werkmap kunt opslaan als XLSB** in een nette, productie‑klare patroon. Deze aanpak is ideaal voor geautomatiseerde rapportage‑pijplijnen, data‑exportservices, of elke situatie waarin metadata met het Excel‑bestand moet meereizen.

Vervolgens kun je verkennen:

* Het toevoegen van datatabellen en ze stylen (`Cells`, `Style`‑objecten).
* Exporteren naar andere formaten zoals **XLSX** of **CSV** terwijl je eigenschappen behoudt.
* Met **Aspose.Cells** aangepaste eigenschappen lezen uit bestaande werkmappen.

Voel je vrij om te experimenteren met verschillende eigenschapsnamen, meerdere werkbladen, of grote datasets. Hetzelfde drie‑stappen‑patroon schaalt van een simpel één‑blad‑bestand tot enterprise‑niveau rapportage‑oplossingen. Veel programmeerplezier!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat complete werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Create Excel Workbook C# – Add Custom Property & Save XLSB](/cells/english/net/document-properties/create-excel-workbook-c-add-custom-property-save-xlsb/)
- [Create Excel Workbook – Add Custom Properties and Save as XLSB](/cells/english/net/document-properties/create-excel-workbook-add-custom-properties-and-save-as-xlsb/)
- [How to create Excel workbook C# with custom formatting and save as XLSX](/cells/english/net/excel-formatting-and-styling/how-to-create-excel-workbook-c-with-custom-formatting-and-sa/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}