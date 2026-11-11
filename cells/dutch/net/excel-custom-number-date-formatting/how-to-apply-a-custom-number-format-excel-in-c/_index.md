---
category: general
date: 2026-10-26
description: Leer hoe je een aangepast getalformaat voor een Excel‑bestand in C# instelt
  door significante cijfers te configureren, een Excel‑werkmap te maken en deze op
  te slaan als een XLSX‑document.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- custom number format excel
- set significant digits
- how to set number format
- create excel workbook c#
- save workbook xlsx
language: nl
lastmod: 2026-10-26
og_description: Aangepaste getalnotatie in Excel met C# stelt je in staat om significante
  cijfers te beheersen, een Excel-werkmap te maken en deze op te slaan als XLSX. Volg
  deze volledige tutorial.
og_image_alt: Excel cell A1 displaying a number formatted with 4 significant digits
  using C#
og_title: Aangepast getalformaat in Excel met C# – stapsgewijze handleiding
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to set a custom number format excel file in C# by configuring
    significant digits, creating an Excel workbook, and saving it as an XLSX document.
  headline: How to apply a custom number format excel in C#
  type: TechArticle
- description: Learn how to set a custom number format excel file in C# by configuring
    significant digits, creating an Excel workbook, and saving it as an XLSX document.
  name: How to apply a custom number format excel in C#
  steps:
  - name: Using a custom format string instead of global options
    text: 'If you need a format that applies only to a single range, you can assign
      a format string directly:'
  - name: Applying the setting to an entire column
    text: '```csharp // Apply the same significant‑digit rule to column B ws.Cells.Columns[1].ApplyNumberFormatOptions(
      new NumberFormatOptions { SignificantDigits = 4 }); ```'
  - name: Dealing with negative numbers
    text: 'The global `SignificantDigits` option works uniformly for positive and
      negative numbers. If you want a different display for negatives, combine it
      with a custom format:'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Hoe pas je een aangepast getalformaat toe in Excel met C#
url: /nl/net/excel-custom-number-date-formatting/how-to-apply-a-custom-number-format-excel-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een aangepast getalformaat in Excel toe te passen in C#

Als je een **custom number format excel** nodig hebt die een specifiek aantal significante cijfers toont, laat deze gids je precies zien hoe je dit in C# doet. Je zult zien hoe je significante cijfers instelt, een Excel‑werkmap maakt en de werkmap opslaat als een XLSX‑bestand — allemaal met een paar regels code.

Werken met Excel‑bestanden programmatically betekent vaak dat je moet bepalen hoe cijfers worden weergegeven. Met Aspose.Cells voor .NET kun je een globale number‑format‑optie definiëren die elke numerieke cel dwingt een opgegeven aantal significante cijfers te respecteren. Deze tutorial behandelt de volledige workflow, van projectconfiguratie tot het verifiëren van de output in Excel.

## Vereisten

* .NET 6.0 of later geïnstalleerd (de code werkt ook met .NET Framework 4.7.2+)
* Visual Studio 2022 of een andere C#‑IDE naar keuze
* Het **Aspose.Cells** NuGet‑pakket (`Install-Package Aspose.Cells`) – een volledig beheerde bibliotheek voor Excel‑manipulatie
* Basiskennis van C#‑syntaxis

## Stap 1: Een Excel‑werkmap maken in C#

De eerste handeling is het instantieren van een nieuw `Workbook`‑object. Dit object vertegenwoordigt het volledige Excel‑bestand in het geheugen.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook instance
        Workbook wb = new Workbook();

        // The workbook now contains a default worksheet named "Sheet1"
        // You can access it via the Worksheets collection.
        Worksheet ws = wb.Worksheets[0];
```

**Waarom dit belangrijk is:** `Workbook` is het toegangspunt voor elke Excel‑bewerking. Door het eerst te maken, zorg je voor een schoon bestand dat je later als XLSX kunt opslaan.

## Stap 2: Het getalformaat configureren om significante cijfers in te stellen

Aspose.Cells biedt een globale instelling genaamd `NumberFormatOptions`. Door `SignificantDigits = 4` toe te wijzen, zal elke numerieke cel tot vier significante cijfers weergeven, tenzij een specifiekere opmaak dit overschrijft.

```csharp
        // Step 2: Set the global number‑format option to 4 significant digits
        WorkbookSettings.SetNumberFormatOptions(
            new NumberFormatOptions { SignificantDigits = 4 });
```

**Waarom dit belangrijk is:** Met `SetNumberFormatOptions` kun je een **custom number format excel** definiëren zonder voor elke cel een opmaak‑string te schrijven. Het weerspiegelt de optie “Significant Digits” die je vindt in het Excel‑dialoogvenster *Format Cells → Number → Custom*.

## Stap 3: Waarden schrijven en het aangepaste getalformaat verifiëren

Plaats nu een numerieke waarde in een cel. De globale instelling past automatisch de 4‑cijfer‑regel toe.

```csharp
        // Step 3: Write a numeric value into cell A1 (row 0, column 0)
        ws.Cells[0, 0].PutValue(123.456789);

        // Optional: Add a label so you can see the effect in Excel
        ws.Cells[0, 1].PutValue("Original value:");
        ws.Cells[0, 2].PutValue(123.456789);
```

Wanneer je het opgeslagen bestand opent, zal cel **A1** `123.5` weergeven (afgerond op vier significante cijfers). De oorspronkelijke waarde blijft ongewijzigd in de onderliggende data, wat je kunt bevestigen door naar de formulebalk te kijken.

**Tip voor randgeval:** Als je een zeer groot getal opslaat, zoals `12345678.9`, zal dezelfde instelling `1.235E+07` weergeven (wetenschappelijke notatie) omdat Excel de meest compacte weergave kiest terwijl vier significante cijfers behouden blijven.

## Stap 4: De werkmap opslaan als XLSX

Sla tenslotte de werkmap op schijf op. De `Save`‑methode kiest automatisch het bestandsformaat op basis van de extensie.

```csharp
        // Step 4: Save the workbook to an XLSX file
        string outputPath = @"C:\Temp\SigDigits.xlsx";
        wb.Save(outputPath);

        // Inform the user
        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**Waarom dit belangrijk is:** Opslaan als **XLSX** (`save workbook xlsx`) garandeert maximale compatibiliteit met moderne versies van Excel, Office 365 en andere spreadsheet‑tools.

## Verwacht resultaat

Open *C:\Temp\SigDigits.xlsx* in Microsoft Excel. Je zou moeten zien:

| A          | B               | C               |
|------------|-----------------|-----------------|
| **123.5**  | Originele waarde: | **123.456789**  |

*Cel A1* toont het getal afgerond op vier significante cijfers, terwijl *C1* de volledige precisie behoudt voor vergelijking.

## Veelvoorkomende variaties en hoe je het getalformaat voor specifieke cellen instelt

### Een aangepaste opmaak‑string gebruiken in plaats van globale opties

Als je een opmaak nodig hebt die alleen op één bereik van toepassing is, kun je direct een opmaak‑string toewijzen:

```csharp
ws.Cells["D1"].PutValue(0.0012345);
Style style = wb.CreateStyle();
style.Custom = "0.####"; // shows up to 4 decimal places, not significant digits
ws.Cells["D1"].SetStyle(style);
```

### De instelling toepassen op een volledige kolom

```csharp
// Apply the same significant‑digit rule to column B
ws.Cells.Columns[1].ApplyNumberFormatOptions(
    new NumberFormatOptions { SignificantDigits = 4 });
```

### Omgaan met negatieve getallen

De globale `SignificantDigits`‑optie werkt uniform voor positieve en negatieve getallen. Als je een andere weergave voor negatieve getallen wilt, combineer deze dan met een aangepaste opmaak:

```csharp
Style negStyle = wb.CreateStyle();
negStyle.Custom = "#,##0.###;[Red]-#,##0.###";
ws.Cells["E1"].PutValue(-9876.54321);
ws.Cells["E1"].SetStyle(negStyle);
```

## Pro‑tips en valkuilen

* **Pro tip:** Stel de number‑format‑opties **vóór** het schrijven van gegevens in. Het wijzigen van de optie na het vullen van cellen formatteert bestaande waarden niet retroactief.
* **Let op:** Het gebruik van `PutValue` met een **string** die op een getal lijkt (bijv. `"123.45"`). Excel behandelt dit als tekst, en de aangepaste opmaak wordt niet toegepast.
* **Prestatie‑opmerking:** Globale instellingen zijn goedkoop, maar het toepassen van een stijl op miljoenen cellen kan het geheugenverbruik verhogen. Gebruik kolom‑niveau opmaak waar mogelijk.

## Volgende stappen

Nu je **custom number format excel** bestanden kunt maken met significante cijfers, kun je het volgende verkennen:

* **Hoe je het getalformaat** instelt voor datums en valuta met `Style.Custom`.
* **Grafieken maken** die je aangepaste opmaak respecteren.
* **Exporteren naar CSV** terwijl je numerieke precisie behoudt (`save workbook xlsx` → `wb.Save("file.csv", SaveFormat.Csv)`).

Deze onderwerpen bouwen voort op dezelfde `Workbook`‑ en `Worksheet`‑concepten die hier worden gedemonstreerd.

---

**Samenvatting**

Je hebt geleerd hoe je **custom number format excel** kunt toepassen door `NumberFormatOptions` te configureren om **significante cijfers in te stellen**, een Excel‑werkmap in C# te maken, waarden te schrijven en **de werkmap op te slaan als een XLSX**‑bestand. De volledige, uitvoerbare code hierboven toont elke stap, legt uit waarom elk onderdeel nodig is, en geeft tips voor veelvoorkomende variaties. Voel je vrij de fragmenten aan te passen aan je eigen projecten en te experimenteren met andere opmaak‑scenario's.

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Aangepast getalformaat Excel in C# – Complete Guide](/cells/english/net/excel-custom-number-date-formatting/custom-number-format-excel-in-c-complete-guide/)
- [Excel-werkmap maken C# – Limiet significante cijfers Excel](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-c-limit-significant-digits-excel/)
- [Hoe getalformaat Excel toe te passen met Aspose.Cells](/cells/english/net/excel-custom-number-date-formatting/how-to-apply-number-format-excel-with-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}