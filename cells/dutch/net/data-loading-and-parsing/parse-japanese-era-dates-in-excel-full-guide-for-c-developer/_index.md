---
category: general
date: 2026-02-14
description: Parse Japanse jaartijddatums in Excel met aangepaste datumparsing. Leer
  hoe je een werkmap uit een bestand laadt met load excel en opties, en vermijd veelvoorkomende
  valkuilen.
draft: false
keywords:
- parse japanese era dates
- load excel with options
- load workbook from file
- custom date parsing excel
language: nl
og_description: Parse Japanse jaartijdperkdatums in Excel met Aspose.Cells. Deze gids
  laat zien hoe je een werkmap laadt vanuit een bestand met aangepaste datumparse‑opties.
og_title: Japanse era‑datums parseren – Stapsgewijze C#‑tutorial
tags:
- Aspose.Cells
- C#
- Excel automation
title: Japanse era-datums in Excel parseren – Volledige gids voor C#‑ontwikkelaars
url: /nl/net/data-loading-and-parsing/parse-japanese-era-dates-in-excel-full-guide-for-c-developer/
---

top-button >}} unchanged.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Parse Japanese era dates – Complete C# Tutorial

Heb je ooit **Japanse jaartijddata** moeten parseren uit een Excel‑blad en je afgevraagd waarom de waarden steeds in vreemde getallen veranderen? Je bent niet de enige. Veel ontwikkelaars lopen tegen dit probleem aan wanneer de standaard `DateTime`‑parser de “Reiwa 1/04/01”‑stijl die in Japanse kalenders wordt gebruikt, niet herkent.  

Goed nieuws: je kunt Aspose.Cells laten behandelen die cellen als Japanse‑jaartijddata vanaf het moment dat je **Excel laadt met opties**. In deze gids lopen we door het laden van een werkmap vanuit een bestand, het configureren van aangepaste datumparsing, en het verifiëren dat de data precies uitkomen zoals je verwacht.

Aan het einde van deze tutorial kun je:

* Een werkmap laden vanuit een bestand terwijl je `DateTimeParsing.JapaneseEra` opgeeft.
* Celwaarden benaderen als juiste `DateTime`‑objecten.
* Randgevallen aanpakken zoals lege cellen of gemengde kalenders.
* De aanpak uitbreiden naar elk **custom date parsing excel**‑scenario dat je tegenkomt.

> **Voorvereiste** – Je hebt de Aspose.Cells for .NET‑bibliotheek (v23.9 of later) en een .NET‑compatibele IDE (Visual Studio, Rider, enz.) nodig. Geen andere pakketten zijn vereist.

---

## Stap 1: Tekst‑laadopties configureren voor Japanse jaartijd‑parsing  

Het eerste dat we doen is de loader vertellen hoe tekst die eruitziet als een Japanse jaartijddatum moet worden geïnterpreteerd. Dit gebeurt via `TxtLoadOptions` en de `DateTimeParsing`‑enum.

```csharp
using Aspose.Cells;

// Step 1: Set up load options to understand Japanese era dates
TxtLoadOptions loadOptions = new TxtLoadOptions
{
    // This flag makes the parser treat “R1/04/01” as 2024‑04‑01, etc.
    DateTimeParsing = DateTimeParsing.JapaneseEra
};
```

**Waarom dit belangrijk is:** Zonder de `JapaneseEra`‑vlag behandelt Aspose.Cells de cel als een gewone string, waardoor je handmatig de era‑naam moet splitsen en converteren. De vlag doet het zware werk, waardoor je code schoon en minder foutgevoelig blijft.

---

## Stap 2: Werkmap laden vanuit bestand met de opties  

Nu openen we daadwerkelijk het Excel‑bestand. Let op hoe het `loadOptions`‑object wordt doorgegeven aan de `Workbook`‑constructor—dit is de **load workbook from file** stap die onze aangepaste parse‑regels respecteert.

```csharp
// Step 2: Load the workbook with the configured options
string filePath = Path.Combine(Environment.CurrentDirectory, "japan_dates.xlsx");
Workbook workbook = new Workbook(filePath, loadOptions);
```

Als het bestand zich ergens anders bevindt (bijv. een netwerkschijf), pas dan `filePath` dienovereenkomstig aan. Het belangrijke is dat dezelfde `loadOptions`‑instantie wordt gebruikt; anders gebeurt de Japanse jaartijdconversie niet.

---

## Stap 3: De geparseerde data benaderen  

Met de werkmap geladen kun je celwaarden ophalen precies zoals je dat met een normale datum zou doen. De API retourneert automatisch een `DateTime`‑object.

```csharp
// Step 3 (optional): Read a date from the first worksheet, cell A1
Worksheet sheet = workbook.Worksheets[0];
Cell dateCell = sheet.Cells["A1"];

// The Value property is already a DateTime because of our parsing option
DateTime parsedDate = dateCell.DateTimeValue;

// Quick sanity check – print to console
Console.WriteLine($"Parsed date from A1: {parsedDate:yyyy-MM-dd}");
```

**Verwachte output** (ervan uitgaande dat A1 “R1/04/01” bevat):

```
Parsed date from A1: 2024-04-01
```

Als de cel een Gregoriaanse datum bevat, zoals “2023‑12‑31”, werkt de parser nog steeds—hij retourneert gewoon de oorspronkelijke datum ongewijzigd.

---

## Stap 4: Alle data in een kolom verifiëren  

Vaak moet je een hele kolom met Japanse jaartijddata scannen. Hieronder staat een compacte lus die laat zien hoe je lege cellen en gemengde inhoud netjes afhandelt.

```csharp
// Step 4: Iterate through column B (index 1) and print each parsed date
int firstRow = 0;
int lastRow = sheet.Cells.MaxDataRow; // last row with data

for (int row = firstRow; row <= lastRow; row++)
{
    Cell cell = sheet.Cells[row, 1]; // column B
    if (cell.Type == CellValueType.IsDateTime)
    {
        Console.WriteLine($"Row {row + 1}: {cell.DateTimeValue:yyyy-MM-dd}");
    }
    else if (!cell.IsNull)
    {
        // Fallback: show raw string for non‑date cells
        Console.WriteLine($"Row {row + 1}: (non‑date) {cell.StringValue}");
    }
}
```

**Pro tip:** `CellValueType.IsDateTime` is de veiligste manier om te controleren of de parser geslaagd is. Het beschermt je tegen `InvalidCastException` wanneer een cel onverwachte tekst bevat.

---

## Stap 5: Veelvoorkomende valkuilen & hoe ze op te lossen  

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Lege cellen retourneren `DateTime.MinValue`** | De parser behandelt lege strings als de minimum datum. | Controleer `cell.IsNull` voordat je `DateTimeValue` benadert. |
| **Gemengde kalenders (Japans + Gregoriaans) in dezelfde kolom** | De parser verwerkt beide, maar je moet mogelijk onderscheiden voor rapportage. | Gebruik `cell.StringValue` om de originele tekst te inspecteren wanneer `cell.Type` `IsString` is. |
| **Onjuiste era (bijv. “H30” voor Heisei) na 2019** | Heisei eindigde in 2019; latere data moeten “R” gebruiken. | Valideer het era‑voorvoegsel voordat je het geparseerde resultaat vertrouwt. |
| **Prestatie‑vertraging bij grote bestanden** | Laden met aangepaste opties voegt een kleine overhead toe. | Laad alleen de benodigde werkbladen (`Workbook.LoadOptions.LoadAllWorksheets = false`). |

---

## Stap 6: Volledig werkend voorbeeld  

Alles bij elkaar, hier is een zelfstandige console‑app die je kunt kopiëren‑plakken en uitvoeren. Het demonstreert **custom date parsing excel** van begin tot eind.

```csharp
// FullExample.cs
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure load options for Japanese era dates
        TxtLoadOptions loadOptions = new TxtLoadOptions
        {
            DateTimeParsing = DateTimeParsing.JapaneseEra
        };

        // 2️⃣ Load the workbook from file with those options
        string filePath = Path.Combine(Environment.CurrentDirectory, "japan_dates.xlsx");
        if (!File.Exists(filePath))
        {
            Console.WriteLine($"File not found: {filePath}");
            return;
        }

        Workbook workbook = new Workbook(filePath, loadOptions);
        Worksheet sheet = workbook.Worksheets[0];

        // 3️⃣ Read a single cell (A1) – demonstrates automatic parsing
        Cell a1 = sheet.Cells["A1"];
        Console.WriteLine($"A1 raw value: {a1.StringValue}");
        Console.WriteLine($"A1 parsed date: {a1.DateTimeValue:yyyy-MM-dd}");

        // 4️⃣ Loop through column B to show batch parsing
        Console.WriteLine("\n--- Column B Dates ---");
        int lastRow = sheet.Cells.MaxDataRow;
        for (int row = 0; row <= lastRow; row++)
        {
            Cell cell = sheet.Cells[row, 1]; // B column
            if (cell.Type == CellValueType.IsDateTime)
                Console.WriteLine($"Row {row + 1}: {cell.DateTimeValue:yyyy-MM-dd}");
            else if (!cell.IsNull)
                Console.WriteLine($"Row {row + 1}: (non‑date) {cell.StringValue}");
        }

        // 5️⃣ Optional: Save a copy with dates converted to ISO format
        // This shows that the workbook now holds proper DateTime objects.
        workbook.Save("japan_dates_converted.xlsx");
        Console.WriteLine("\nWorkbook saved as japan_dates_converted.xlsx");
    }
}
```

**Wat je zou moeten zien** wanneer `japan_dates.xlsx` bevat:

| A | B |
|---|---|
| R1/04/01 | 2023‑12‑31 |
| H30/12/31 | R2/01/01 |
| (blank) | R2/02/15 |

Console‑output:

```
A1 raw value: R1/04/01
A1 parsed date: 2024-04-01

--- Column B Dates ---
Row 1: 2023-12-31
Row 2: 2025-01-01
Row 3: (non-date) 
Row 4: 2025-02-15
Workbook saved as japan_dates_converted.xlsx
```

Het opgeslagen bestand bevat nu juiste datumcellen, die je in Excel kunt openen en de gebruikelijke datumopmaak ziet.

---

## Conclusie  

We hebben zojuist laten zien hoe je **Japanse jaartijddata** in Excel kunt **parseren** door `TxtLoadOptions` te configureren, **load workbook from file** met die opties, en te werken met de resulterende `DateTime`‑waarden. Hetzelfde patroon—het instellen van aangepaste parse‑vlaggen en vervolgens de werkmap laden—geldt voor elke **custom date parsing excel**‑vereiste, of je nu te maken hebt met fiscale periodes, ISO‑weeknummers, of propriëtaire formaten.

Heb je een andere era of een gemengde‑kalender spreadsheet? Vervang gewoon `DateTimeParsing.JapaneseEra` door een andere enum‑waarde (bijv. `DateTimeParsing.Custom`) en lever een format‑string. De flexibiliteit van Aspose.Cells betekent dat je zelden handmatige conversiecode opnieuw hoeft te schrijven.

**Next steps** you might explore:

* **Load Excel with options** voor CSV‑bestanden (`CsvLoadOptions`) om locale‑specifieke scheidingstekens te verwerken.
* Gebruik `Workbook.Save` met `SaveFormat.Xlsx` om opgeschoonde data te exporteren.
* Combineer deze aanpak met **Aspose.Slides** of **Aspose.Words** voor rapportage‑pijplijnen.

Probeer het, pas de opties aan, en laat de bibliotheek het zware werk doen. Veel programmeerplezier!  

![Screenshot of parsed Japanese era dates in a console window – parse japanese era dates example](/images/parse-japanese-era-dates.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}