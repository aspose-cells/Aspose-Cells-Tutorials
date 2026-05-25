---
category: general
date: 2026-03-30
description: Leer hoe je een getal met scheidingsteken kunt opmaken met Aspose.Cells
  in C#. Inclusief het instellen van een aangepast getalformaat, het toevoegen van
  een duizendtallen‑scheidingsteken, het opmaken van decimalen en hoe je een cel kunt
  opmaken.
draft: false
keywords:
- format number with separator
- set custom number format
- add thousands separator
- format decimal places
- how to format cell
language: nl
og_description: Getal formatteren met scheidingsteken in C#. Deze gids laat zien hoe
  je een aangepast getalformaat instelt, een duizendtallen scheidingsteken toevoegt,
  decimalen formatteert en hoe je een cel formatteert met Aspose.Cells.
og_title: Getal formatteren met scheidingsteken in C# – Aspose.Cells‑handleiding
tags:
- C#
- Aspose.Cells
- Number Formatting
title: Getal formatteren met scheidingsteken in C# – Complete Aspose.Cells‑gids
url: /nl/net/excel-custom-number-date-formatting/format-number-with-separator-in-c-complete-aspose-cells-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Getal formatteren met scheidingsteken in C# – Complete Aspose.Cells-gids

Heb je ooit moeten **getal formatteren met scheidingsteken** in een spreadsheet, maar wist je niet welke API‑aanroep je moest gebruiken? Je bent niet de enige—ontwikkelaars worstelen voortdurend met duizendtallen scheidingstekens, decimalen en aangepaste patronen bij het exporteren van gegevens.  

Goed nieuws: Aspose.Cells maakt het een fluitje van een cent. In deze tutorial lopen we een real‑world voorbeeld door dat **een aangepast getalformaat instelt**, **een duizendtallen scheidingsteken toevoegt**, **decimalen formatteert**, en laat zien **hoe een cel te formatteren** als string. Aan het einde heb je een kant‑klaar fragment dat je in elk .NET‑project kunt plaatsen.

## Wat deze gids behandelt

* Het exacte NuGet‑pakket dat je nodig hebt en hoe je het installeert.  
* Stapsgewijze code die een workbook maakt, een numerieke waarde schrijft en een aangepast formaat toepast.  
* Waarom `ExportTableOptions.ExportAsString` de voorkeur heeft om een geformatteerde waarde op te halen.  
* Veelvoorkomende valkuilen—zoals vergeten `ExportAsString` in te schakelen of een verkeerd formaatmasker te gebruiken.  
* Hoe je het formaatmasker kunt aanpassen als je een ander aantal decimalen of een andere scheidingstekenstijl nodig hebt.

Er zijn geen externe documentatielinks nodig; alles wat je nodig hebt staat hier. Laten we beginnen.

---

## Prerequisites

| Vereiste | Reden |
|----------|-------|
| .NET 6.0 of later | Aspose.Cells 23.10+ richt zich op .NET Standard 2.0+, dus .NET 6 is veilig en actueel. |
| Visual Studio 2022 (of elke C#‑IDE) | Maakt debuggen en pakketbeheer moeiteloos. |
| Aspose.Cells for .NET NuGet‑pakket | Biedt de `Workbook`, `Worksheet` en `ExportTableOptions`‑klassen die we gaan gebruiken. |

Je kunt het pakket installeren via de Package Manager Console:

```powershell
Install-Package Aspose.Cells
```

Dat is alles—geen extra DLL’s, geen COM‑interop, slechts één NuGet‑referentie.

---

## Stap 1: Een nieuw workbook initialiseren (Hoe een cel te formatteren)

Het eerste wat we doen is een verse `Workbook`‑instantie maken. Beschouw het als een leeg Excel‑bestand dat klaar is om data te ontvangen.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook – this is where we’ll format the cell.
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];
```

> **Waarom dit belangrijk is:** `Workbook` is het toegangspunt voor elke bewerking in Aspose.Cells. Door het eerste werkblad (`Worksheets[0]`) te pakken, krijgen we een schoon canvas zonder een bladnaam te hoeven specificeren.

---

## Stap 2: Een numerieke waarde in de doelcel schrijven

Vervolgens plaatsen we een ruwe getal in cel **A1**. De waarde zelf is nog niet geformatteerd—het is gewoon een double.

```csharp
        // Step 2: Insert a raw numeric value.
        worksheet.Cells["A1"].PutValue(12345.6789);
```

> **Pro tip:** Gebruik `PutValue` in plaats van `PutString` wanneer je later numerieke opmaak wilt toepassen. Dit behoudt het onderliggende datatype, waardoor Excel‑compatibele berekeningen mogelijk zijn.

---

## Stap 3: Aangepast getalformaat instellen (Duizendtallen scheidingsteken toevoegen & decimalen formatteren)

Nu volgt het hart van de tutorial: een formaatmasker definiëren dat Aspose.Cells vertelt hoe het getal moet worden weergegeven. Het masker `#,##0.00` doet drie dingen:

1. **`#,##0`** – voegt een duizendtallen scheidingsteken toe (komma standaard).  
2. **`.00`** – dwingt precies twee decimalen af.  

Als je een ander aantal decimalen nodig hebt, wijzig je simpelweg het aantal `0`‑tjes na de decimale punt.

```csharp
        // Step 3: Configure the custom number format.
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,          // Return the value as a formatted string.
            NumberFormat = "#,##0.00"       // Add thousands separator and fix to 2 decimals.
        };
```

> **Waarom we `ExportAsString` gebruiken:** Standaard geeft `ExportString` de ruwe waarde terug. Door `ExportAsString = true` in te stellen, dwingt de API het `NumberFormat`‑masker af voordat het naar tekst wordt geconverteerd. Dit is essentieel wanneer je de exacte stringrepresentatie nodig hebt voor rapporten, JSON‑payloads of UI‑weergave.

---

## Stap 4: De geformatteerde tekst exporteren (Hoe een cel te formatteren)

Met de opties klaar, roepen we `ExportString` aan op dezelfde cel. De methode respecteert het masker dat we zojuist hebben gedefinieerd en levert een mooi geformatteerde string terug.

```csharp
        // Step 4: Export the formatted value.
        string formattedCellText = worksheet.Cells["A1"].ExportString(exportOptions);

        // Step 5: Show the result.
        Console.WriteLine(formattedCellText); // Expected output: 12,345.68
    }
}
```

Het uitvoeren van het programma print **`12,345.68`** naar de console—exact het formaat dat we hebben gevraagd.

> **Edge case:** Als het brongetal meer dan twee decimalen heeft, rondt het masker af. Als je in plaats van afronden wilt afkappen, moet je de waarde vooraf verwerken met `Math.Truncate` voordat je `PutValue` aanroept.

---

## Stap 5: Het formaat aanpassen – Veelvoorkomende variaties

### 5.1 Decimalprecisie wijzigen

Wil je drie decimalen? Vervang simpelweg het masker:

```csharp
NumberFormat = "#,##0.000"   // → 12,345.679
```

### 5.2 Een ander duizendtallen scheidingsteken gebruiken

Sommige regio’s geven de voorkeur aan een spatie of een punt. Je kunt het teken direct in het masker opnemen:

```csharp
NumberFormat = "# ##0.00"    // Uses a non‑breaking space as separator.
```

Of vertrouwen op de cultuursinstellingen van het workbook:

```csharp
workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("de-DE");
NumberFormat = "#.##0,00";   // German style: 12.345,68
```

### 5.3 Voorvoegsel of achtervoegsel (Valuta, Procent)

Voeg een dollarteken of een procentteken direct in het masker toe:

```csharp
NumberFormat = "$#,##0.00";   // → $12,345.68
NumberFormat = "0.00%";       // → 1,234,568.00%
```

> **Opmerking:** Het masker is hoofdlettergevoelig. `$` en `%` zijn letterlijke symbolen; ze beïnvloeden de onderliggende numerieke waarde niet.

---

## Stap 6: Volledig werkend voorbeeld (Klaar om te kopiëren en plakken)

Hieronder staat het complete programma dat je kunt kopiëren naar een nieuwe console‑applicatie. Het bevat alle stappen, commentaren en de uiteindelijke output‑verificatie.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialise workbook and worksheet.
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Write raw numeric value to A1.
        worksheet.Cells["A1"].PutValue(12345.6789);

        // 3️⃣ Define custom format: thousands separator + two decimals.
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "#,##0.00"
        };

        // 4️⃣ Export the formatted string.
        string result = worksheet.Cells["A1"].ExportString(exportOptions);

        // 5️⃣ Display the outcome.
        Console.WriteLine(result); // Output: 12,345.68

        // Optional: keep console open.
        Console.WriteLine("Press any key to exit...");
        Console.ReadKey();
    }
}
```

Voer het programma uit (`dotnet run` vanuit de terminal of druk op F5 in Visual Studio) en je ziet het geformatteerde getal precies zoals weergegeven.

---

## Veelgestelde vragen (FAQ)

**Q: Werkt dit met oudere versies van Excel?**  
A: Ja. Het formaatmasker volgt de native getal‑formaatsyntaxis van Excel, dus elke versie die `#,##0.00` begrijpt, zal dezelfde string weergeven.

**Q: Wat als ik een bereik van cellen moet formatteren?**  
A: Loop over het gewenste bereik en pas dezelfde `ExportTableOptions` toe op elke cel, of stel de eigenschap `Style.Custom` in op het bereik en roep vervolgens `ExportString` aan op één cel.

**Q: Kan ik direct naar CSV exporteren met deze formaten toegepast?**  
A: Absoluut. Gebruik `Workbook.Save("output.csv", SaveFormat.CSV);` nadat je het formaat op elke cel hebt ingesteld. Aspose.Cells respecteert de `Style` van de cel bij het genereren van CSV.

---

## Conclusie

We hebben zojuist laten zien hoe je **getal formatteren met scheidingsteken** in C# kunt doen met Aspose.Cells, waarbij we alles behandelen van **een aangepast getalformaat instellen** tot **een duizendtallen scheidingsteken toevoegen**, **decimalen formatteren**, en de essentiële **hoe een cel te formatteren** voor string‑export. De code is volledig zelf‑voorzienend, werkt met .NET 6+ en kan worden aangepast voor elke locale of precisie‑vereiste.

Vervolgens kun je verkennen:

* Dezelfde techniek toepassen op datums en tijden (`NumberFormat = "dd‑MMM‑yyyy"`).  
* Bulk‑exports automatiseren waarbij elke kolom een ander masker nodig heeft.  
* De geformatteerde strings integreren in PDF‑rapporten met Aspose.Words.

Probeer het uit, en je wordt snel de go‑to persoon voor spreadsheet‑formattering in je team. Happy coding!   (Image: ![Screenshot showing formatted number with separator in Aspose.Cells](image-placeholder.png){alt="Geformatteerd getal met scheidingsteken weergegeven in Aspose.Cells-uitvoer"} )

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}