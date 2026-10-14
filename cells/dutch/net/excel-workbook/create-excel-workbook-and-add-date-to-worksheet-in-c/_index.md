---
category: general
date: 2026-10-13
description: Maak een Excel-werkmap in C# en schrijf een datum naar Excel met Aspose.Cells.
  Leer hoe je een Excel‑bestand opslaat als xlsx en een datum toevoegt aan het werkblad
  met volledige code.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- save excel file
- write date to excel
- save workbook as xlsx
- add date to worksheet
language: nl
lastmod: 2026-10-13
og_description: Maak een Excel-werkmap in C# en schrijf een datum naar Excel. Volg
  deze volledige gids om het Excel‑bestand op te slaan als xlsx en een datum toe te
  voegen aan het werkblad met Aspose.Cells.
og_image_alt: Excel workbook screenshot showing a Japanese imperial date in cell A1
og_title: Maak een Excel-werkmap en voeg datum toe aan werkblad – C# stap‑voor‑stap
schemas:
- author: Aspose
  dateModified: '2026-10-13'
  description: Create excel workbook in C# and write date to excel using Aspose.Cells.
    Learn to save excel file as xlsx and add date to worksheet with full code.
  headline: Create excel workbook and add date to worksheet in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Maak een Excel-werkmap en voeg een datum toe aan het werkblad in C#
url: /nl/net/excel-workbook/create-excel-workbook-and-add-date-to-worksheet-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Maak excel-werkmap en voeg datum toe aan werkblad in C#

Als je programmatically **excel-werkmap moet maken**, laat deze gids zien hoe je **datum naar excel kunt schrijven** en **excel-bestand kunt opslaan** als een *.xlsx* werkmap. Je ziet een compleet, uitvoerbaar voorbeeld dat een Japanse keizerlijke jaartal‑string parseert en de resulterende `DateTime` opslaat in cel A1.

Werken met Excel vanuit C# vereist vaak drie stappen: de werkmap instantiëren, gegevens op een werkblad plaatsen en uiteindelijk het bestand opslaan. Deze tutorial behandelt elke stap, legt uit waarom de code op die manier is geschreven, en belicht veelvoorkomende valkuilen zoals cultuurspecifieke parsing en bestands‑systeemrechten. Aan het einde kun je **datum toevoegen aan werkblad**, **werkmap opslaan als xlsx**, en het patroon aanpassen voor elk gegevenstype.

> **Voorvereiste** – Het voorbeeld gebruikt de **Aspose.Cells for .NET** bibliotheek (versie 23.10 of later). Installeer deze via NuGet:

```bash
dotnet add package Aspose.Cells
```

Je hebt ook een .NET 6+ SDK en een beschrijfbare map nodig voor het uitvoerbestand.

---

## Maak excel-werkmap en configureer werkblad

De eerste stap is een lege werkmap te instantiëren en het standaard werkblad te pakken. Aspose.Cells maakt automatisch een werkmap met één blad genaamd “Sheet1”.

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

// Step 1: Create a new workbook
Workbook workbook = new Workbook();

// Step 2: Get the first worksheet (index 0)
Worksheet sheet = workbook.Worksheets[0];
```

**Waarom dit belangrijk is** – `Workbook` is het toegangspunt voor alle Excel‑bewerkingen. Door het zonder parameters te maken krijg je een schone werkmap die je later kunt **excel‑bestand opslaan** in elk formaat dat je kiest.

---

## Parse Japanse keizerlijke datum

Japanse keizerlijke data gebruiken een era‑symbool (bijv. “R” voor Reiwa) gevolgd door een twee‑cijferig jaar. De .NET `DateTime.ParseExact`‑methode kan dit formaat verwerken wanneer je een aangepast `DateTimeParseOptions`‑object opgeeft dat de parser instrueert de Japanse keizerkalender te gebruiken.

```csharp
// Step 3: Define a date string in the Japanese imperial era
string imperialDate = "R3/04/01"; // Reiwa 3, April 1st

// Step 4: Configure parsing options for the Japanese Emperor calendar
var parseOptions = new DateTimeParseOptions
{
    Calendar = DateTimeParseOptions.CalendarType.JapaneseEmperor
};

// Step 5: Parse the string into a .NET DateTime
DateTime parsedDate = DateTime.ParseExact(
    imperialDate,
    "ggyy/MM/dd",
    CultureInfo.InvariantCulture,
    DateTimeStyles.None,
    parseOptions);
```

**Uitleg** –  
* `gg` leest de era‑aanduiding (`R` voor Reiwa).  
* `yy` leest het twee‑cijferige jaar binnen die era.  
* `MM/dd` leest maand en dag.  

Als je `parseOptions` weglaat, gaat de parser uit van de Gregoriaanse kalender en gooit een `FormatException`. Dit is een veelvoorkomende randvoorwaarde bij het omgaan met niet‑Gregoriaanse kalenders.

---

## Schrijf datum naar werkblad

Nu je een `DateTime`‑waarde hebt, kun je deze in een cel plaatsen. Aspose.Cells formatteert de cel automatisch op basis van het type van de waarde.

```csharp
// Step 6: Write the parsed date into cell A1
sheet.Cells["A1"].PutValue(parsedDate);

// Optional: Apply a date format for better readability
Style style = workbook.CreateStyle();
style.Custom = "yyyy-mm-dd";
sheet.Cells["A1"].SetStyle(style);
```

**Waarom een stijl instellen?** – Zonder een stijl kan Excel de datum weergeven met het standaardformaat van het systeem, wat verwarrend kan zijn voor gebruikers in andere regio’s. Het expliciet definiëren van `"yyyy-mm-dd"` zorgt voor een consistente weergave.

---

## Sla excel‑bestand op als xlsx

Ten slotte sla je de werkmap op schijf op. De `Save`‑methode bepaalt het uitvoerformaat aan de hand van de bestandsextensie, dus het gebruik van “.xlsx” activeert automatisch het Office Open XML‑formaat.

```csharp
// Step 7: Define the output path (adjust to your environment)
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "JapaneseDate.xlsx");

// Step 8: Save the workbook
workbook.Save(outputPath, SaveFormat.Xlsx);
```

**Tip** – Als de doelmap niet bestaat of je geen schrijfrechten hebt, gooit `Save` een `IOException`. Controleer altijd het pad voordat je `Save` aanroept.

---

## Volledig uitvoerbaar voorbeeld

Hieronder staat het volledige programma dat je kunt kopiëren, plakken en uitvoeren. Het bevat alle `using`‑directieven, foutafhandeling en commentaren die elke bewerking verduidelijken.

```csharp
using Aspose.Cells;
using System;
using System.Globalization;
using System.IO;

class Program
{
    static void Main()
    {
        try
        {
            // 1️⃣ Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();
            Worksheet sheet = workbook.Worksheets[0];

            // 2️⃣ Define the Japanese imperial date string
            string imperialDate = "R3/04/01"; // Reiwa 3, April 1st

            // 3️⃣ Set up parsing options for the Japanese Emperor calendar
            var parseOptions = new DateTimeParseOptions
            {
                Calendar = DateTimeParseOptions.CalendarType.JapaneseEmperor
            };

            // 4️⃣ Parse the string into a .NET DateTime
            DateTime parsedDate = DateTime.ParseExact(
                imperialDate,
                "ggyy/MM/dd",
                CultureInfo.InvariantCulture,
                DateTimeStyles.None,
                parseOptions);

            // 5️⃣ Write the date to cell A1
            sheet.Cells["A1"].PutValue(parsedDate);

            // Apply a consistent date format
            Style dateStyle = workbook.CreateStyle();
            dateStyle.Custom = "yyyy-mm-dd";
            sheet.Cells["A1"].SetStyle(dateStyle);

            // 6️⃣ Determine the output file location
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "JapaneseDate.xlsx");

            // 7️⃣ Save the workbook as an .xlsx file
            workbook.Save(outputPath, SaveFormat.Xlsx);

            Console.WriteLine($"Workbook saved successfully to: {outputPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }
}
```

**Verwacht resultaat**

Wanneer je `JapaneseDate.xlsx` opent, bevat cel A1 de datum **2021‑04‑01** (het Gregoriaanse equivalent van Reiwa 3 / 04 / 01) weergegeven in het `yyyy‑mm‑dd` formaat.

![Excel workbook with date in cell A1](excel-date-screenshot.png){alt="Schermafbeelding van een Excel-werkmap die een Japanse keizerlijke datum in cel A1 toont"}

---

## Veelgestelde vragen en randgevallen

| Vraag | Antwoord |
|-------|----------|
| *Wat als de era verandert (bijv. Heisei naar Reiwa)?* | De `JapaneseEmperor`‑kalender map automatisch era‑symbolen (`H`, `R`, enz.) naar het juiste Gregoriaanse bereik, dus je hoeft alleen de invoer‑string bij te werken. |
| *Kan ik meerdere datums in een kolom schrijven?* | Ja. Loop door je gegevens en roep `sheet.Cells[row, column].PutValue(dateValue)` aan voor elke rij. |
| *Wat als ik een ander datumformaat nodig heb?* | Verander `dateStyle.Custom` naar een willekeurige Excel‑datumopmaak‑string, zoals `"dd-mmm-yyyy"` of `"mm/dd/yyyy"`. |
| *Is er een manier om het blad te beveiligen na het schrijven van de datum?* | Gebruik `sheet.Protect(ProtectOptions.All, "password")` vóór het opslaan. |
| *Hoe ga ik om met tijdzones?* | `DateTime` slaat UTC of lokale tijd op. Converteer met `DateTime.SpecifyKind` of `TimeZoneInfo.ConvertTime` vóór het aanroepen van `PutValue`. |

---

## Conclusie

Je weet nu hoe je **excel-werkmap kunt maken**, **datum naar excel kunt schrijven**, **datum aan werkblad kunt toevoegen**, en **werkmap kunt opslaan als xlsx** met Aspose.Cells in C#. Het volledige voorbeeld toont het parseren van een Japanse keizerlijke kalender‑string, het toepassen van een consistente stijl, en het omgaan met bestands‑systeemkwesties.  

Vanaf hier kun je

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stapsgewijze uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Excel-werkmap maken C# – Opmerking toevoegen & opslaan als XLSX](/cells/english/net/excel-comment-annotation/create-excel-workbook-c-add-comment-save-as-xlsx/)
- [Nieuwe werkmap maken in C# – Formule toevoegen en Excel‑bestand opslaan](/cells/english/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/)
- [Excel-werkmap maken – Kolommen omsluiten en opslaan als XLSX](/cells/english/net/formatting-rows-and-columns-in-excel/create-excel-workbook-wrap-columns-and-save-as-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}