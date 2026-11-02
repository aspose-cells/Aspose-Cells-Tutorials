---
category: general
date: 2026-05-30
description: Hoe AutoFilter te gebruiken in C# Excel‑automatisering. Leer hoe je een
  Excel‑werkmap maakt, rijen filtert op waarde en je spreadsheet‑taken stroomlijnt.
draft: false
keywords:
- how to use autofilter
- create excel workbook
- filter rows by value
- filter column b
- excel automation c#
language: nl
og_description: Hoe AutoFilter te gebruiken in C# Excel‑automatisering. Beheers het
  maken van een Excel‑werkmap, het filteren van rijen op waarde en het automatiseren
  van spreadsheets met gemak.
og_title: Hoe AutoFilter te gebruiken in C# Excel‑automatisering – Volledige gids
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: How to use AutoFilter in C# Excel automation. Learn how to create Excel
    workbook, filter rows by value, and streamline your spreadsheet tasks.
  headline: How to Use AutoFilter in C# Excel Automation – Full Step‑by‑Step Guide
  type: TechArticle
- description: How to use AutoFilter in C# Excel automation. Learn how to create Excel
    workbook, filter rows by value, and streamline your spreadsheet tasks.
  name: How to Use AutoFilter in C# Excel Automation – Full Step‑by‑Step Guide
  steps:
  - name: '**Creating the workbook** – `new Workbook()` gives you a clean file; `Worksheets[0]`
      grabs the default sheet.'
    text: '**Creating the workbook** – `new Workbook()` gives you a clean file; `Worksheets[0]`
      grabs the default sheet.'
  - name: '**Filling sample data** – We write a tiny dataset so you can see the filter
      in action.'
    text: '**Filling sample data** – We write a tiny dataset so you can see the filter
      in action.'
  - name: '**Adding a table** – `ListObjects.Add` converts the range into an Excel
      table, which automatically supports filtering and styling.'
    text: '**Adding a table** – `ListObjects.Add` converts the range into an Excel
      table, which automatically supports filtering and styling.'
  - name: '**Applying AutoFilter** – `table.AutoFilter.Filter(1, "Apple")` tells the
      engine: “Show only rows where the second column (B) equals *Apple*.”'
    text: '**Applying AutoFilter** – `table.AutoFilter.Filter(1, "Apple")` tells the
      engine: “Show only rows where the second column (B) equals *Apple*.”'
  - name: '**Saving files** – Two files are written: one filtered, one with the filter
      removed, proving that `RemoveAutoFilter()` works as expected.'
    text: '**Saving files** – Two files are written: one filtered, one with the filter
      removed, proving that `RemoveAutoFilter()` works as expected.'
  type: HowTo
- questions:
  - answer: Yes. Aspose.Cells can save to both `.xlsx` and `.xls` by changing the
      file extension or using `SaveOptions`.
    question: Does this work with older .xls files?
  - answer: Load the file with `new Workbook("path.xlsx")`, apply the filter, then
      `Save` again.
    question: What if I need to filter *after* the workbook is already saved?
  - answer: 'Absolutely. Use `worksheet.AutoFilter.Range = "A1:C5";` and then `worksheet.AutoFilter.ApplyFilter();`.
      However, tables give you built‑in styling and easier column referencing. ---
      ## Image – Visual Confirmation ![Screenshot showing AutoFilter applied to column
      B in an Excel workbook created with C#'
    question: Can I apply a filter to a *range* that isn’t a table?
  type: FAQPage
tags:
- C#
- Excel
- Automation
title: Hoe AutoFilter te gebruiken in C# Excel‑automatisering – Volledige stapsgewijze
  handleiding
url: /nl/net/excel-autofilter-validation/how-to-use-autofilter-in-c-excel-automation-full-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe AutoFilter te gebruiken in C# Excel-automatisering – Complete gids

Heb je je ooit afgevraagd **hoe je AutoFilter** kunt gebruiken wanneer je Excel‑bestanden genereert vanuit C#‑code? Je bent niet de enige—veel ontwikkelaars lopen tegen dit probleem aan wanneer ze rijen moeten verbergen die niet aan een bepaalde criterium voldoen.  

In deze tutorial lopen we een concreet, uitvoerbaar voorbeeld door dat **een Excel‑werkmap maakt**, een tabel toevoegt, en vervolgens **rijen filtert op waarde** in kolom B. Aan het einde heb je een nette, herbruikbare code‑fragment die je in elk C#‑project kunt plaatsen dat Excel‑automatisering nodig heeft.

## Wat je zult leren

- Een C#‑project opzetten met de Aspose.Cells (of Microsoft.Office.Interop) bibliotheek.  
- **Excel‑werkmap maken** programmatically en een gestylede tabel toevoegen.  
- Pas **AutoFilter** toe om alleen rijen te tonen waar **kolom B** gelijk is aan een specifieke tekenreeks.  
- Verwijder het filter volledig, waardoor de volledige dataset wordt hersteld.  
- Tips voor het omgaan met randgevallen zoals ontbrekende kolommen of meerdere filtercriteria.

Geen eerdere Excel‑VBA‑ervaring vereist; alleen een basisbegrip van C# en NuGet‑pakketten.

---

## Vereisten

| Vereiste | Waarom het belangrijk is |
|----------|--------------------------|
| .NET 6.0 or later (or .NET Framework 4.7+) | Moderne runtimes bieden betere prestaties en gemakkelijker pakketbeheer. |
| Aspose.Cells for .NET (or Microsoft.Office.Interop.Excel) installed via NuGet | Deze bibliotheek levert de `Workbook`, `Worksheet` en `Table` objecten die in de code worden gebruikt. |
| A code editor (Visual Studio, VS Code, Rider, etc.) | Je moet het voorbeeld compileren en uitvoeren. |
| Basic C# knowledge | De tutorial legt *waarom* elke regel bestaat uit, niet alleen *wat* het doet. |

Je kunt Aspose.Cells installeren met:

```bash
dotnet add package Aspose.Cells
```

---

## Hoe AutoFilter te gebruiken met Aspose.Cells in C#

Hieronder staat het volledige, zelfstandige programma. Sla het op als `Program.cs` in een console‑project en voer het uit – je krijgt `FilteredWorkbook.xlsx` in de output‑map.

```csharp
using System;
using Aspose.Cells;

namespace ExcelAutoFilterDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Create an Excel workbook and grab the first worksheet
            // -------------------------------------------------
            Workbook workbook = new Workbook();               // creates a new, empty workbook
            Worksheet sheet = workbook.Worksheets[0];         // the default sheet is named "Sheet1"

            // Populate the sheet with sample data (A‑C columns, 5 rows)
            sheet.Cells["A1"].PutValue("ID");
            sheet.Cells["B1"].PutValue("Fruit");
            sheet.Cells["C1"].PutValue("Quantity");

            sheet.Cells["A2"].PutValue(1);
            sheet.Cells["B2"].PutValue("Apple");
            sheet.Cells["C2"].PutValue(10);

            sheet.Cells["A3"].PutValue(2);
            sheet.Cells["B3"].PutValue("Banana");
            sheet.Cells["C3"].PutValue(15);

            sheet.Cells["A4"].PutValue(3);
            sheet.Cells["B4"].PutValue("Apple");
            sheet.Cells["C4"].PutValue(7);

            sheet.Cells["A5"].PutValue(4);
            sheet.Cells["B5"].PutValue("Cherry");
            sheet.Cells["C5"].PutValue(20);

            // -------------------------------------------------
            // Step 2: Convert the range into a ListObject (Excel table)
            // -------------------------------------------------
            // Parameters: firstRow, firstColumn, totalRows, totalColumns, hasHeaders
            int tableIdx = sheet.ListObjects.Add(0, 0, 5, 3, true);
            ListObject table = sheet.ListObjects[tableIdx];
            table.TableStyleType = TableStyleType.TableStyleMedium2; // nice built‑in styling

            // -------------------------------------------------
            // Step 3: Apply an AutoFilter to show only rows where column B = "Apple"
            // -------------------------------------------------
            // The AutoFilter is attached to the table’s range automatically.
            // We target column B (index 1) and set the criteria.
            table.AutoFilter.Filter(1, "Apple"); // 1 = zero‑based column index for B

            // -------------------------------------------------
            // Step 4: Save the filtered workbook to disk
            // -------------------------------------------------
            workbook.Save("FilteredWorkbook.xlsx");

            // -------------------------------------------------
            // Step 5: (Optional) Remove the AutoFilter completely
            // -------------------------------------------------
            // This demonstrates that you can revert to the full dataset without re‑loading.
            table.RemoveAutoFilter();   // clears the filter
            workbook.Save("UnfilteredWorkbook.xlsx");

            Console.WriteLine("Workbook created and filtered successfully.");
        }
    }
}
```

### Hoe de code werkt

1. **Creating the workbook** – `new Workbook()` geeft je een leeg bestand; `Worksheets[0]` pakt het standaardblad.  
2. **Filling sample data** – We schrijven een kleine dataset zodat je het filter in actie kunt zien.  
3. **Adding a table** – `ListObjects.Add` zet het bereik om in een Excel‑tabel, die automatisch filteren en opmaken ondersteunt.  
4. **Applying AutoFilter** – `table.AutoFilter.Filter(1, "Apple")` vertelt de engine: “Toon alleen rijen waar de tweede kolom (B) gelijk is aan *Apple*.”  
5. **Saving files** – Er worden twee bestanden geschreven: één gefilterd, één met het filter verwijderd, wat aantoont dat `RemoveAutoFilter()` werkt zoals verwacht.

> **Pro tip:** Als je moet filteren op meerdere criteria (bijv. “Apple” *of* “Banana”), gebruik dan de overload `Filter(int columnIndex, string criteria1, string criteria2)` of geef een array van strings door.

---

## Rijen filteren op waarde – Veelvoorkomende variaties

Hoewel het voorbeeld hierboven zich richt op **filter kolom B**, wil je misschien andere kolommen filteren of numerieke criteria gebruiken. Hier is een snel overzicht:

| Gewenst filter | Codefragment |
|----------------|--------------|
| Tekst overeenstemming in kolom C | `table.AutoFilter.Filter(2, "Cherry");` |
| Getallen groter dan 10 in kolom C | `table.AutoFilter.CustomFilter(2, "10", OperatorType.GreaterThan);` |
| Meerdere waarden in kolom B | `table.AutoFilter.Filter(1, new[] { "Apple", "Banana" });` |

**Randgeval:** Als de kolomkop verkeerd gespeld is of de kolomindex buiten bereik ligt, gooit Aspose.Cells een `ArgumentException`. Bescherm hiertegen door `table.ListColumns.Count` te controleren voordat je het filter toepast.

---

## Het AutoFilter verwijderen – Wanneer te resetten

Soms moet je de volledige dataset opnieuw tonen (bijv. nadat een gebruiker een zoekvak heeft geleegd). Het aanroepen van `table.RemoveAutoFilter()` doet het in één regel. Als je Microsoft.Office.Interop gebruikt, roep je `worksheet.AutoFilterMode = false;` aan.

---

## Volledig werkend voorbeeld samenvatting

Hieronder staat het *volledige* programma opnieuw, zonder commentaren voor wie een beknopte weergave prefereert:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        ws.Cells["A1"].PutValue("ID");
        ws.Cells["B1"].PutValue("Fruit");
        ws.Cells["C1"].PutValue("Quantity");

        ws.Cells["A2"].PutValue(1); ws.Cells["B2"].PutValue("Apple");  ws.Cells["C2"].PutValue(10);
        ws.Cells["A3"].PutValue(2); ws.Cells["B3"].PutValue("Banana"); ws.Cells["C3"].PutValue(15);
        ws.Cells["A4"].PutValue(3); ws.Cells["B4"].PutValue("Apple");  ws.Cells["C4"].PutValue(7);
        ws.Cells["A5"].PutValue(4); ws.Cells["B5"].PutValue("Cherry"); ws.Cells["C5"].PutValue(20);

        int idx = ws.ListObjects.Add(0, 0, 5, 3, true);
        ListObject tbl = ws.ListObjects[idx];
        tbl.TableStyleType = TableStyleType.TableStyleMedium2;

        tbl.AutoFilter.Filter(1, "Apple");
        wb.Save("FilteredWorkbook.xlsx");

        tbl.RemoveAutoFilter();
        wb.Save("UnfilteredWorkbook.xlsx");
    }
}
```

Het uitvoeren hiervan levert twee bestanden op:

- **FilteredWorkbook.xlsx** – alleen rijen met *Apple* zichtbaar.  
- **UnfilteredWorkbook.xlsx** – de oorspronkelijke data hersteld.

---

## Veelgestelde vragen

**Q: Werkt dit met oudere .xls‑bestanden?**  
A: Ja. Aspose.Cells kan zowel naar `.xlsx` als `.xls` opslaan door de bestandsextensie te wijzigen of `SaveOptions` te gebruiken.

**Q: Wat als ik moet filteren *nadat* de werkmap al is opgeslagen?**  
A: Laad het bestand met `new Workbook("path.xlsx")`, pas het filter toe, en sla vervolgens opnieuw op met `Save`.

**Q: Kan ik een filter toepassen op een *bereik* dat geen tabel is?**  
A: Zeker. Gebruik `worksheet.AutoFilter.Range = "A1:C5";` en vervolgens `worksheet.AutoFilter.ApplyFilter();`. Tabellen bieden echter ingebouwde opmaak en eenvoudigere kolomreferentie.

## Afbeelding – Visuele bevestiging

![Schermafbeelding die AutoFilter toegepast op kolom B in een Excel‑werkmap gemaakt met C#](/images/autofilter-column-b.png "AutoFilter op kolom B")

*(De afbeelding illustreert de gefilterde weergave waarbij alleen rijen met “Apple” overblijven.)*

## Conclusie

We hebben zojuist **hoe je AutoFilter** gebruikt in een C#‑gedreven Excel‑automatiseringsscenario, van **het maken van een Excel‑werkmap** tot **rijen filteren op waarde** in **kolom B**, en uiteindelijk **het filter verwijderen** wanneer het niet meer nodig is. De kernstappen — initialiseren, een tabel toevoegen, het filter toepassen en opruimen — zijn herbruikbaar in elk project dat **excel automation c#** nodig heeft.

Klaar voor de volgende uitdaging? Probeer:

- Voorwaardelijke opmaak toevoegen om gefilterde rijen te markeren.  
- De gefilterde data exporteren naar een CSV voor verdere verwerking.  
- Meerdere filters combineren (bijv. “Apple” *en* hoeveelheid > 8).

## Wat moet je hierna leren?

- [Hoe AutoFilter te implementeren in Excel met Aspose.Cells voor .NET (Data‑analysegids)](/cells/english/net/data-analysis/implement-autofilter-excel-aspose-cells-dotnet/)
- [Hoe Autofilter Niet Bevat te gebruiken in Aspose.Cells .NET voor Excel Data‑analyse](/cells/english/net/data-analysis/master-autofilter-not-contains-aspose-cells-net/)
- [Hoe Excel Autofilter 'EndsWith' te implementeren met Aspose.Cells voor .NET](/cells/english/net/data-analysis/implement-autofilter-endswith-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}