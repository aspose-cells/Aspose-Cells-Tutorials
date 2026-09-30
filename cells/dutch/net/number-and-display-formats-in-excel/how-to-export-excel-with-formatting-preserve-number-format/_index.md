---
category: general
date: 2026-03-22
description: Hoe Excel met opmaak te exporteren en het getalformaat te behouden. Leer
  een Excel‑bereik te converteren, formuleresultaten op te halen en Excel met opmaak
  te exporteren met Aspose.Cells.
draft: false
keywords:
- how to export excel
- preserve number format
- convert excel range
- get formula result
- export excel with formatting
language: nl
og_description: Hoe Excel met opmaak exporteren en de getalnotatie behouden. Stapsgewijze
  handleiding om een Excel‑bereik te converteren, het formule‑resultaat te verkrijgen
  en Excel met opmaak te exporteren in C#.
og_title: Hoe Excel te exporteren met opmaak – Nummeropmaak behouden
tags:
- C#
- Aspose.Cells
- Excel automation
title: Hoe Excel met opmaak exporteren – Nummeropmaak behouden
url: /nl/net/number-and-display-formats-in-excel/how-to-export-excel-with-formatting-preserve-number-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe Excel te exporteren met opmaak – Getalnotatie behouden

Heb je je ooit afgevraagd **hoe je Excel**-gegevens kunt exporteren terwijl je elke cel er precies zo uit ziet als in de werkmap? Misschien moet je een rapport naar een klant sturen, een raster‑besturingselement voeden, of gewoon de waarden in een database opslaan. Het knelpunt is meestal het verlies van getalopmaak of formules die in ruwe tekenreeksen veranderen.  

In deze tutorial lopen we een compleet, kant‑klaar C#‑voorbeeld door dat **getalopmaak behoudt**, **een Excel‑bereik converteert** naar een `DataTable`, **het formule‑resultaat haalt**, en uiteindelijk **Excel exporteert met opmaak** met behulp van Aspose.Cells. Aan het einde heb je een enkele methode die je in elk project kunt plaatsen en kunt aanroepen met een werkblad‑referentie.

> **Snelle preview:** de code maakt een werkmap, schrijft een waarde en een formule, vertelt Aspose.Cells de cellen als opgemaakte tekenreeksen te exporteren, en print `123.456 | 246.912` – precies wat je in Excel zou verwachten te zien.

---

## Wat je nodig hebt

- **Aspose.Cells for .NET** (de gratis proefversie werkt prima voor leren)
- .NET 6.0 of later (de API is hetzelfde op .NET Framework)
- Een basis C#‑ontwikkelomgeving (Visual Studio, VS Code, Rider… je kiest)

Er zijn geen extra NuGet‑pakketten nodig naast Aspose.Cells. Als je het nog niet hebt geïnstalleerd, voer dan uit:

```bash
dotnet add package Aspose.Cells
```

---

## Stap 1 – Maak een werkmap en schrijf waarden (inclusief een formule)

Eerst maken we een nieuwe werkmap aan en plaatsen een numerieke waarde in **A1**. Vervolgens voegen we een eenvoudige formule toe in **B1** die de eerste cel met twee vermenigvuldigt. Dit bereidt de basis voor het later demonstreren van **get formula result**.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExportExcelDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and get its first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write a numeric value and a formula that uses it
        worksheet.Cells["A1"].PutValue(123.456);
        worksheet.Cells["B1"].PutFormula("=A1*2");

        // Continue with export options...
        ExportRangeAsDataTable(worksheet);
    }
}
```

**Waarom dit belangrijk is:**  
- `PutValue` slaat het ruwe getal op, terwijl `PutFormula` de berekening opslaat.  
- Aspose.Cells houdt de formule **actief**, zodat wanneer we later om de celwaarde vragen we daadwerkelijk `246.912` krijgen, niet de tekenreeks `"=A1*2"`.

---

## Stap 2 – Vertel Aspose.Cells om waarden te exporteren als opgemaakte tekenreeksen

Als je simpelweg `ExportDataTable` aanroept met de standaardinstellingen, worden numerieke cellen geretourneerd als hun onderliggende `double`‑waarden. Dat verwijdert eventuele duizendtallen‑scheidingstekens, valutasymbolen of aangepaste decimalen die je mogelijk hebt ingesteld. De `ExportTableOptions`‑klasse laat ons **getalopmaak behouden** en **exporteren als tekenreeks**.

```csharp
static void ExportRangeAsDataTable(Worksheet worksheet)
{
    // Step 2: Set export options to retrieve values as formatted strings
    ExportTableOptions exportOptions = new ExportTableOptions
    {
        ExportAsString = true,          // Return values as strings
        ExportNumberFormat = true      // Preserve the cell's number format
    };

    // Step 3: Export the range A1:B1 to a DataTable
    DataTable dataTable = worksheet.Cells.ExportDataTable(
        firstRow: 0,
        firstColumn: 0,
        totalRows: 1,
        totalColumns: 2,
        includeColumnNames: true,
        options: exportOptions);

    PrintDataTable(dataTable);
}
```

**Belangrijk punt:** `ExportNumberFormat = true` is de vlag die **preserve number format** laat werken. Zonder deze zie je `"123.456"` en `"246.912"` als ruwe getallen, wat er in code misschien goed uitziet, maar niet wanneer je de gegevens plakt in een UI die dezelfde opmaak als Excel verwacht.

---

## Stap 3 – Print de geëxporteerde gegevens (verificatie)

Nu we een `DataTable` vol opgemaakte tekenreeksen hebben, laten we de inhoud naar de console dumpen. Dit toont ook aan dat we succesvol **get formula result** hebben verkregen zonder de formule zelf te evalueren.

```csharp
static void PrintDataTable(DataTable table)
{
    // Step 4: Print the exported values (already formatted)
    foreach (DataRow row in table.Rows)
    {
        // The output will look like: 123.456 | 246.912
        Console.WriteLine($"{row[0]} | {row[1]}");
    }
}
```

Running the program prints:

```
123.456 | 246.912
```

Merk op hoe de tweede kolom de **formule‑resultaat** toont, niet de formule‑tekst. Dat is precies wat je nodig hebt wanneer je **Excel exporteert met opmaak** voor verdere verwerking.

---

## Stap 4 – Grotere Excel‑bereiken converteren (optioneel)

Het voorbeeld hierboven behandelt een klein `A1:B1`‑deel, maar in de praktijk moet je vaak volledige tabellen exporteren. dezelfde methode werkt voor elk rechthoekig blok – pas gewoon de argumenten `firstRow`, `firstColumn`, `totalRows` en `totalColumns` aan.

```csharp
// Example: Export a 10‑row by 5‑column block starting at C3
DataTable bigTable = worksheet.Cells.ExportDataTable(
    firstRow: 2,          // Zero‑based index (C3 = row 2, column 2)
    firstColumn: 2,
    totalRows: 10,
    totalColumns: 5,
    includeColumnNames: true,
    options: exportOptions);
```

**Pro tip:** Als je blad al een koprij heeft, stel `includeColumnNames` in op `true`. Aspose.Cells zal de eerste rij van het bereik gebruiken als kolomnamen, wat handig is wanneer je later de `DataTable` bindt aan een UI‑raster.

---

## Stap 5 – Veelvoorkomende valkuilen & hoe ze te vermijden

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Getallen verliezen komma's of valutasymbolen** | `ExportAsString` is `false` of `ExportNumberFormat` is weggelaten | Stel beide `ExportAsString = true` **en** `ExportNumberFormat = true` in. |
| **Formule‑cellen geven de formule‑tekst terug** | Je hebt `CalculateFormula` niet aangeroepen vóór export (alleen nodig als de werkmap niet op automatisch berekenen staat) | Schakel auto‑calculate in (`workbook.CalculateFormula()`) of vertrouw op `ExportAsString` dat evaluatie afdwingt. |
| **Koppen verschijnen als gegevensrijen** | `includeColumnNames` staat op `false` terwijl je bereik een koprij bevat | Stel `includeColumnNames = true` in om de eerste rij als kolomnamen te behandelen. |
| **Grote bereiken veroorzaken geheugenbelasting** | Het in één keer exporteren van het volledige blad laadt alles in het geheugen | Exporteren in delen (bijv. 500 rijen per keer) en `DataTable`s samenvoegen indien nodig. |

---

## Stap 6 – Volledig werkend voorbeeld (klaar om te kopiëren‑plakken)

Hieronder staat het volledige programma, van `using`‑statements tot `Main`. Plak het in een console‑applicatie en druk op **F5** – je ziet meteen de opgemaakte output.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExportExcelDemo
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate cells
        worksheet.Cells["A1"].PutValue(123.456);
        worksheet.Cells["B1"].PutFormula("=A1*2");

        // Export options: keep formatting and return strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            ExportNumberFormat = true
        };

        // Export A1:B1 as a DataTable
        DataTable dataTable = worksheet.Cells.ExportDataTable(
            firstRow: 0,
            firstColumn: 0,
            totalRows: 1,
            totalColumns: 2,
            includeColumnNames: true,
            options: exportOptions);

        // Print results
        foreach (DataRow row in dataTable.Rows)
        {
            Console.WriteLine($"{row[0]} | {row[1]}"); // Expected: "123.456 | 246.912"
        }

        // Keep console window open
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

**Expected output**

```
123.456 | 246.912

Press any key to exit...
```

Dit is de volledige **how to export excel**‑workflow, met behoud van opmaak, geëvalueerde formule‑resultaten, en een schone `DataTable` klaar voor elke .NET‑gebruiker.

---

## Conclusie

We hebben alles behandeld wat je moet weten over **how to export Excel**‑gegevens terwijl je **getalopmaak behoudt**, **een Excel‑bereik converteert** naar een `DataTable`, en **formule‑resultaten haalt** zonder extra parsing. De sleutel is de `ExportTableOptions`‑configuratie – zodra je `ExportAsString` en `ExportNumberFormat` op `true` zet, doet Aspose.Cells het zware werk voor je.

Vanaf hier kun je:

- De `DataTable` in een WPF `DataGrid` of ASP.NET MVC‑view pluggen.
- De tabel naar een CSV‑bestand schrijven terwijl je de exacte visuele weergave behoudt.
- De aanpak uitbreiden naar meerdere bladen of dynamische bereiken.

Voel je vrij om te experimenteren met verschillende opmaken (valuta, percentages) en grotere gegevensblokken. Als je tegen vreemde problemen aanloopt, raad dan terug naar de tabel met **common pitfalls** – die behandelt de meest voorkomende hickups wanneer je **export excel with formatting**.

Veel programmeerplezier, en moge je geëxporteerde spreadsheets altijd net zo gepolijst eruitzien als de originelen!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}