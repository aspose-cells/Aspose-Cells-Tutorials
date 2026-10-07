---
category: general
date: 2026-03-01
description: De Read write Excel C#‑tutorial toont hoe je een Excel‑celwaarde leest
  en een datum/tijd naar Excel schrijft met C# en Aspose.Cells in een paar eenvoudige
  stappen.
draft: false
keywords:
- read write excel c#
- read excel cell value
- write datetime to excel
- c# excel interop
- aspnet excel automation
language: nl
og_description: Read write Excel C# tutorial legt uit hoe je een Excel-celwaarde kunt
  lezen en een datum‑tijd naar Excel kunt schrijven, met duidelijke codevoorbeelden
  en best practices.
og_title: Excel lezen en schrijven C# – Stapsgewijze gids
tags:
- C#
- Excel
- Aspose.Cells
title: Excel lezen en schrijven C# – Complete gids voor het lezen en schrijven van
  Excel‑cellen
url: /nl/net/cell-operations/read-write-excel-c-complete-guide-to-reading-and-writing-exc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Read Write Excel C# – Complete Gids voor het Lezen en Schrijven van Excel‑cellen

Heb je ooit geprobeerd **read write Excel C#** en kreeg je een cryptische uitzondering of een verkeerde datum? Je bent niet de enige. Veel ontwikkelaars lopen tegen problemen aan wanneer ze een Japanse jaartal‑datum uit een werkblad moeten halen en vervolgens een correcte `DateTime` terug in dezelfde cel moeten opslaan.  

In deze gids lopen we stap voor stap door hoe je **read excel cell value** en **write datetime to excel** kunt gebruiken met C# en de krachtige Aspose.Cells‑bibliotheek. Aan het einde heb je een zelfstandige, uitvoerbare voorbeeldcode die je in elk .NET‑project kunt plaatsen.

## Wat je gaat leren

- Hoe je Aspose.Cells installeert en referentieert in een .NET 6+ project.  
- De exacte code die nodig is om een cel op te halen die een Japanse jaartal‑string bevat zoals `"R3/5/12"`.  
- Hoe je die string parseert naar een `DateTime` met de `"ja-JP"`‑cultuur.  
- De stappen om de resulterende `DateTime` terug te schrijven naar dezelfde werkbladcel.  
- Tips voor het afhandelen van randgevallen zoals lege cellen of onverwachte era‑formaten.  

Ervaring met Excel‑interop is niet vereist—alleen een basisbegrip van C# en .NET. Laten we beginnen.

![Screenshot van read write Excel C# bewerking die cel B2 vóór en na conversie toont](read-write-excel-csharp.png "read write excel c# voorbeeld")

## Stap 1: Het project opzetten – Read Write Excel C# Fundamentals

Voordat we in de code duiken, hebben we een solide basis nodig.

1. **Maak een nieuwe console‑app** (of een ander .NET‑project) aan gericht op .NET 6 of hoger:

   ```bash
   dotnet new console -n ExcelEraDemo
   cd ExcelEraDemo
   ```

2. **Voeg het Aspose.Cells NuGet‑pakket toe**. Het is een volledig beheerde bibliotheek die werkt zonder COM‑interop:

   ```bash
   dotnet add package Aspose.Cells
   ```

3. **Kopieer een Excel‑bestand** (`EraDates.xlsx`) naar de project‑root. Deze werkmap moet een blad bevatten met de naam `"Sheet1"` waarin cel **B2** een waarde heeft zoals `"R3/5/12"` (Reiwa 3, 12 mei).

Dat is alle scaffolding die je nodig hebt. De rest van de tutorial richt zich op de daadwerkelijke **read excel cell value** en **write datetime to excel**‑logica.

## Stap 2: Read Excel Cell Value met C#

Nu het project klaar is, halen we de string op uit het werkblad. Het volgende fragment toont de exacte aanroepketen:

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Load the workbook (adjust the path as needed)
        Workbook wb = new Workbook("EraDates.xlsx");
        Worksheet ws = wb.Worksheets["Sheet1"];   // assumes the sheet is named Sheet1

        // Step 2: Get the cell that holds the Japanese era date string
        // B2 contains something like "R3/5/12"
        Cell dateCell = ws.Cells["B2"];  

        // Step 3: Read the string representation from the cell
        string eraDateString = dateCell.StringValue;  

        Console.WriteLine($"Original cell value: {eraDateString}");
        // -------------------------------------------------
        // From here we’ll convert the era string to a DateTime.
        // -------------------------------------------------
    }
}
```

**Waarom dit werkt:** `Cell.StringValue` geeft altijd de weergegeven tekst terug, ongeacht het onderliggende getalformaat. Dat garandeert dat we werken met precies de `"R3/5/12"`‑string die de gebruiker ziet.

### Veelvoorkomende valkuilen

- **Lege cellen** – `StringValue` geeft een lege string terug. Bescherm je code hiertegen vóór het parsen.  
- **Onverwachte formaten** – Als de cel `"2023/05/12"` bevat, zal de era‑parser een fout gooien; je hebt een fallback nodig.

## Stap 3: Write DateTime to Excel met C#

Met de era‑string in de hand, parseren we deze nu met `DateTime.ParseExact`. Het formaat `"ggyy/MM/dd"` vertelt .NET dat er een Japanse era (`gg`), een twee‑cijferig jaar (`yy`) en maand/dag‑componenten verwacht worden.

```csharp
        // Step 4: Convert the era date string to a DateTime using the Japanese culture
        DateTime parsedDate;
        try
        {
            parsedDate = DateTime.ParseExact(
                eraDateString,
                "ggyy/MM/dd",
                new CultureInfo("ja-JP"));
        }
        catch (FormatException)
        {
            Console.WriteLine("The cell value does not match the expected Japanese era format.");
            return;
        }

        Console.WriteLine($"Parsed DateTime (UTC): {parsedDate:u}");

        // Step 5: Store the resulting DateTime back into the same cell
        dateCell.PutValue(parsedDate);

        // Optional: Apply a standard date format so Excel shows it nicely
        dateCell.SetStyle(new Style { Number = 14 }); // 14 = "m/d/yyyy"

        // Save the workbook to a new file so we don’t overwrite the original
        wb.Save("EraDates_Converted.xlsx");
        Console.WriteLine("Workbook saved as EraDates_Converted.xlsx");
```

**Waarom we `PutValue` gebruiken**: Aspose.Cells detecteert automatisch het .NET‑type en schrijft het juiste Excel‑celtype. Het doorgeven van een `DateTime` resulteert in een echte Excel‑datum, die later kan worden opgemaakt of in formules kan worden gebruikt.

### Randgevallen en tips

- **Tijdzones** – `DateTime`‑objecten worden opgeslagen zonder zone‑informatie. Als je UTC nodig hebt, roep dan `DateTime.SpecifyKind` aan.  
- **Cultuur‑fallback** – Als je andere culturen verwacht, wikkel het parse‑proces in een helper die meerdere `CultureInfo`‑objecten probeert.  
- **Prestaties** – Bij het verwerken van duizenden rijen, hergebruik een enkele `CultureInfo`‑instantie in plaats van elke keer een nieuwe te maken.

## Stap 4: Volledig werkend voorbeeld – Alles bij elkaar

Hieronder staat het complete, kant‑en‑klaar programma. Kopieer‑plak het in `Program.cs`, zorg dat `EraDates.xlsx` naast het gecompileerde binaire bestand staat, en voer `dotnet run` uit.

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Load workbook
        Workbook wb = new Workbook("EraDates.xlsx");
        Worksheet ws = wb.Worksheets["Sheet1"];   // Change if your sheet has a different name

        // -------------------------------------------------
        // 1️⃣ Read the Japanese era string from B2
        // -------------------------------------------------
        Cell dateCell = ws.Cells["B2"];
        string eraDateString = dateCell.StringValue?.Trim();

        if (string.IsNullOrEmpty(eraDateString))
        {
            Console.WriteLine("Cell B2 is empty. Nothing to convert.");
            return;
        }

        Console.WriteLine($"Original cell value: {eraDateString}");

        // -------------------------------------------------
        // 2️⃣ Parse the era string into a DateTime
        // -------------------------------------------------
        DateTime parsedDate;
        try
        {
            parsedDate = DateTime.ParseExact(
                eraDateString,
                "ggyy/MM/dd",
                new CultureInfo("ja-JP"));
        }
        catch (FormatException)
        {
            Console.WriteLine("The value does not match the expected Japanese era format (ggyy/MM/dd).");
            return;
        }

        Console.WriteLine($"Parsed DateTime: {parsedDate:u}");

        // -------------------------------------------------
        // 3️⃣ Write the DateTime back into the same cell
        // -------------------------------------------------
        dateCell.PutValue(parsedDate);

        // Apply a friendly date format (e.g., 2023/05/12)
        Style style = wb.CreateStyle();
        style.Number = 14; // Built‑in date format
        dateCell.SetStyle(style);

        // Save the updated workbook
        wb.Save("EraDates_Converted.xlsx");
        Console.WriteLine("Conversion complete – saved as EraDates_Converted.xlsx");
    }
}
```

**Verwachte output**

```
Original cell value: R3/5/12
Parsed DateTime: 2021-05-12 00:00:00Z
Conversion complete – saved as EraDates_Converted.xlsx
```

Wanneer je `EraDates_Converted.xlsx` opent, toont cel **B2** nu een reguliere datum (bijv. `5/12/2021`) en kan deze net als elke andere datumwaarde in Excel‑berekeningen worden gebruikt.

## Pro‑tips voor robuuste Read Write Excel C#‑code

- **Valideer vóór je schrijft** – Gebruik `Cell.IsFormula` of `Cell.Type` om te voorkomen dat je per ongeluk formules overschrijft.  
- **Batchverwerking** – Als je een hele kolom moet converteren, loop dan door `ws.Cells.Columns[1]` (kolom B) en pas dezelfde logica toe.  
- **Thread‑veiligheid** – Aspose.Cells‑objecten zijn niet thread‑safe; maak aparte `Workbook`‑instanties per thread bij parallelle verwerking.  
- **Logging** – Vervang in productiescripts `Console.WriteLine` door een echte logger (bijv. Serilog) om parse‑fouten vast te leggen.  
- **Testen** – Schrijf unit‑tests die bekende era‑strings aan een helper‑methode voeren en controleer de resulterende `DateTime`‑waarden.

## Conclusie

Je hebt zojuist **read write Excel C#** onder de knie gekregen door te leren hoe je **read excel cell value** kunt lezen, een Japanse era‑string kunt parsen, en **write datetime to excel** met vertrouwen. Het volledige voorbeeld toont een schone, end‑to‑end workflow die je kunt aanpassen voor bulk‑operaties, verschillende culturen, of zelfs Excel‑naar‑database‑pijplijnen.

Wat nu? Probeer het script uit te breiden zodat het een volledige kolom era‑datums verwerkt, of verken de rijke opmaakopties van Aspose.Cells om de uitvoercellen te stylen. Je kunt ook experimenteren met andere bibliotheken zoals EPPlus of ClosedXML—de meeste logica blijft gelijk, alleen de API‑aanroepen verschillen.

Heb je vragen of een lastig Excel‑scenario? Laat een reactie achter, en happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}