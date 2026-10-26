---
category: general
date: 2026-10-26
description: Leer hoe je WRAPCOLS in C# gebruikt om een bereik in kolommen te splitsen,
  WRAPROWS voor rijen toepast, en het werkboek programmatisch als XLSX opslaat.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- split range into rows
- excel wrapcols example
- save workbook as xlsx
- create excel workbook programmatically
language: nl
lastmod: 2026-10-26
og_description: Hoe je WRAPCOLS in C# gebruikt om gegevens in kolommen te splitsen,
  WRAPROWS voor rijen gebruikt, en het werkboek opslaat als XLSX. Volg de volledige
  stapsgewijze handleiding.
og_image_alt: Screenshot illustrating how to use WRAPCOLS to split a range into columns
  in Excel
og_title: Hoe WRAPCOLS te gebruiken in C# – bereik splitsen en opslaan als XLSX
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to use WRAPCOLS in C# to split a range into columns, apply
    WRAPROWS for rows, and save workbook as XLSX programmatically.
  headline: How to use WRAPCOLS in C# and save workbook as XLSX
  type: TechArticle
- description: Learn how to use WRAPCOLS in C# to split a range into columns, apply
    WRAPROWS for rows, and save workbook as XLSX programmatically.
  name: How to use WRAPCOLS in C# and save workbook as XLSX
  steps:
  - name: What the saved file looks like
    text: 'When you open `wrapcols_wraprows_output.xlsx` in Excel you’ll see:'
  - name: Changing the number of columns or rows
    text: '* **More columns:** Increase the second argument of `WRAPCOLS`. Example:
      `=WRAPCOLS(A1:A10,5)` creates five columns, leaving empty cells where data runs
      out. * **Dynamic column count:** Use a cell reference instead of a hard‑coded
      number. `=WRAPCOLS(A1:A10, G1)` where `G1` holds the desired column c'
  - name: Handling empty or non‑numeric cells
    text: WRAPCOLS and WRAPROWS ignore empty cells by default, but they preserve the
      order of non‑empty values. If you need to preserve blanks, wrap the source range
      with `IFERROR` or `TEXT` functions before applying WRAPCOLS.
  - name: Saving to other formats
    text: 'While this tutorial focuses on **save workbook as xlsx**, Aspose.Cells
      supports many formats (`.xls`, `.csv`, `.pdf`, etc.):'
  - name: What’s next?
    text: '* Explore **conditional formatting** to highlight the spilled data. * Combine
      **WRAPCOLS** with **SORT** or **FILTER** for dynamic dashboards. * Use Aspose.Cells’
      **charting API** to visualize the rearranged data directly from code.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Hoe WRAPCOLS in C# te gebruiken en een werkmap op te slaan als XLSX
url: /nl/net/row-and-column-management/how-to-use-wrapcols-in-c-and-save-workbook-as-xlsx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe WRAPCOLS te gebruiken in C# en werkmap opslaan als XLSX

Als je **hoe WRAPCOLS te gebruiken** nodig hebt om gegevens in een Excel‑bestand te reorganiseren, laat deze gids je een volledige, uitvoerbare oplossing zien. Je ziet een **excel wrapcols‑voorbeeld**, leert hoe je **een bereik in rijen splitst** met WRAPROWS, en eindigt met **werkmap opslaan als XLSX** — alles **programmatically** gedaan.

Werken met Excel vanuit C# betekent vaak een werkmap maken, formules toepassen en het bestand opslaan. De onderstaande code maakt gebruik van de Aspose.Cells‑bibliotheek, waarmee je Excel‑bestanden kunt manipuleren zonder Microsoft Office geïnstalleerd te hebben. Aan het einde van deze tutorial kun je **een Excel‑werkmap programmatically maken**, gegevens zowel horizontaal als verticaal splitsen, en een nette `.xlsx`‑file produceren die klaar is voor verdere verwerking.

## Vereisten

Voordat je begint, zorg dat je het volgende hebt:

* .NET 6.0 of later (de code werkt ook met .NET Framework 4.7+)
* Een referentie naar het **Aspose.Cells** NuGet‑pakket  
  ```bash
  dotnet add package Aspose.Cells
  ```
* Basiskennis van C# en Excel‑formules

## Stap 1: Hoe WRAPCOLS te gebruiken om een bereik in kolommen te splitsen

De **WRAPCOLS**‑functie neemt een één‑dimensionaal bereik en spreidt de waarden over het opgegeven aantal kolommen. In dit voorbeeld beginnen we met waarden in `A1:A10` en vragen we WRAPCOLS drie kolommen te maken.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook – this is the “create excel workbook programmatically” step
        Workbook workbook = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet ws = workbook.Worksheets[0];

        // Populate source data for demonstration
        for (int i = 0; i < 10; i++)
        {
            ws.Cells[i, 0].PutValue($"Item {i + 1}");
        }

        // Apply WRAPCOLS: split A1:A10 into 3 columns starting at C1
        // The formula is entered in cell C1 (row 0, column 2)
        ws.Cells[0, 2].Formula = "=WRAPCOLS(A1:A10,3)";

        // -------------------------------------------------
        // Why this works:
        // -------------------------------------------------
        // * WRAPCOLS reads the source range (A1:A10) vertically.
        // * The second argument (3) tells Excel to create three columns.
        // * The function returns a 2‑dimensional array that Excel spills into the
        //   surrounding cells automatically.
        // -------------------------------------------------
```

> **Resultaat:** Cellen `C1:E4` bevatten nu de oorspronkelijke tien items verdeeld over drie kolommen (de laatste kolom bevat de resterende items).

![Schermafbeelding die laat zien hoe WRAPCOLS te gebruiken om een bereik in kolommen te splitsen in Excel](image-url.png)

## Stap 2: Bereik splitsen in rijen met WRAPROWS

Terwijl **WRAPCOLS** horizontaal werkt, voert **WRAPROWS** het tegenovergestelde uit: het spreidt een bereik over een opgegeven aantal rijen. Hier nemen we waarden uit `B1:B10` en rangschikken ze in twee rijen, beginnend bij `F1`.

```csharp
        // Populate a second source column for WRAPROWS
        for (int i = 0; i < 10; i++)
        {
            ws.Cells[i, 1].PutValue($"Value {i + 1}");
        }

        // Apply WRAPROWS: split B1:B10 into 2 rows starting at F1
        ws.Cells[0, 5].Formula = "=WRAPROWS(B1:B10,2)";

        // -------------------------------------------------
        // Why WRAPROWS is useful:
        // -------------------------------------------------
        // * It converts a vertical list into a matrix with the specified row count.
        // * Handy when you need to prepare data for pivot tables, charts, or
        //   reporting layouts that expect a horizontal orientation.
        // -------------------------------------------------
```

> **Resultaat:** De formule vult cellen `F1:K2` met de tien waarden, verdeeld over twee rijen.

## Stap 3: Werkmap opslaan als XLSX

Na het toepassen van de formules is de laatste stap het bestand permanent opslaan. De **save workbook as xlsx**‑operatie schrijft de in‑memory werkmap naar schijf in het moderne OpenXML‑formaat.

```csharp
        // Save the workbook – this completes the “save workbook as xlsx” step
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "wrapcols_wraprows_output.xlsx");

        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to: {outputPath}");
    }
}
```

### Hoe het opgeslagen bestand eruitziet

Wanneer je `wrapcols_wraprows_output.xlsx` opent in Excel zie je:

| C | D | E |
|---|---|---|
| Item 1 | Item 4 | Item 7 |
| Item 2 | Item 5 | Item 8 |
| Item 3 | Item 6 | Item 9 |
|        |        | Item 10 |

en

| F | G | H | I | J | K |
|---|---|---|---|---|---|
| Waarde 1 | Waarde 3 | Waarde 5 | Waarde 7 | Waarde 9 | |
| Waarde 2 | Waarde 4 | Waarde 6 | Waarde 8 | Waarde 10 | |

De formules blijven in de cellen staan, zodat latere wijzigingen in de bronbereiken automatisch worden doorgevoerd.

## Stap 4: Veelvoorkomende variaties en randgevallen

### Het aantal kolommen of rijen wijzigen

* **Meer kolommen:** Verhoog het tweede argument van `WRAPCOLS`.  
  Voorbeeld: `=WRAPCOLS(A1:A10,5)` maakt vijf kolommen, waarbij lege cellen worden gelaten waar de data opraken.
* **Dynamisch kolomaantal:** Gebruik een celreferentie in plaats van een hard‑gecodeerd getal.  
  `=WRAPCOLS(A1:A10, G1)` waarbij `G1` het gewenste aantal kolommen bevat.

### Lege of niet‑numerieke cellen verwerken

WRAPCOLS en WRAPROWS negeren lege cellen standaard, maar behouden de volgorde van niet‑lege waarden. Als je lege cellen wilt behouden, wikkel dan het bronbereik met `IFERROR` of `TEXT` voordat je WRAPCOLS toepast.

### Opslaan in andere formaten

Hoewel deze tutorial zich richt op **save workbook as xlsx**, ondersteunt Aspose.Cells vele formaten (`.xls`, `.csv`, `.pdf`, enz.):

```csharp
workbook.Save("output.pdf", SaveFormat.Pdf);   // Export to PDF
workbook.Save("output.csv", SaveFormat.Csv);   // Export to CSV
```

## Pro‑tips en valkuilen

* **Pro tip:** Stel `Workbook.Settings.CalcEngineEnabled = true` in als je formules direct na het opslaan wilt evalueren.
* **Let op:** Grote bronbereiken kunnen zeer grote spill‑gebieden opleveren, wat de prestaties kan beïnvloeden. Beperk de bereikgrootte of verdeel de bewerking over meerdere werkbladen.
* **Thread‑veiligheid:** Aspose.Cells‑objecten zijn **niet** thread‑safe. Maak een aparte `Workbook`‑instantie per thread als je bestanden parallel verwerkt.

## Conclusie

Je weet nu **hoe WRAPCOLS te gebruiken** om een verticaal bereik in meerdere kolommen te splitsen, **hoe een bereik in rijen te splitsen** met WRAPROWS, en **hoe een werkmap op te slaan als XLSX** na het uitvoeren van deze transformaties. Door de bovenstaande stappen te volgen kun je **een Excel‑werkmap programmatically maken**, krachtige spill‑formules toepassen en kant‑klaar‑te‑delen Excel‑bestanden genereren zonder handmatige tussenkomst.

### Wat is het volgende?

* Verken **conditionele opmaak** om de gespilde data te markeren.
* Combineer **WRAPCOLS** met **SORT** of **FILTER** voor dynamische dashboards.
* Gebruik de **charting‑API** van Aspose.Cells om de herschikte data direct vanuit code te visualiseren.

Veel programmeerplezier, en geniet van het automatiseren van je Excel‑werkstromen!


## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [hoe wrapcols te gebruiken in C# – Volledige gids met Excel WRAPROWS & Formules opnieuw berekenen](/cells/english/net/row-and-column-management/how-to-use-wrapcols-in-c-full-guide-with-excel-wraprows-reca/)
- [Hoe WRAPCOLS te gebruiken in C# – Een array omvormen tot een matrix in Excel](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-reshape-an-array-to-a-matrix-in-exc/)
- [Hoe WRAPCOLS te gebruiken – Complete gids voor C# Excel‑automatisering](/cells/english/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-complete-guide-for-c-excel-automation/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}