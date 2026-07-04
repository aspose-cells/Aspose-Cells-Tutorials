---
category: general
date: 2026-07-03
description: Hoe SEQUENCE in C# te gebruiken om oplopende nummers in Excel te genereren.
  Leer hoe je een Excel-werkmap maakt met C# en ASP.NET en een Excel-bestand maakt
  met slechts een paar regels code.
draft: false
keywords:
- how to use sequence
- create excel workbook c#
- asp.net create excel file
- generate incremental numbers excel
language: nl
og_description: Hoe SEQUENCE in C# te gebruiken om incrementele nummers in Excel te
  genereren. Stapsgewijze handleiding voor het maken van een Excel-werkmap met C#
  en ASP.NET om een Excel‑bestand te creëren.
og_title: Hoe SEQUENCE te gebruiken in C# – Excel‑werkboek maken
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: How to use SEQUENCE in C# to generate incremental numbers in Excel.
    Learn to create Excel workbook C# and ASP.NET create Excel file with a few lines
    of code.
  headline: How to Use SEQUENCE in C# – Create Excel Workbook
  type: TechArticle
- description: How to use SEQUENCE in C# to generate incremental numbers in Excel.
    Learn to create Excel workbook C# and ASP.NET create Excel file with a few lines
    of code.
  name: How to Use SEQUENCE in C# – Create Excel Workbook
  steps:
  - name: Why Use SEQUENCE Instead of a Loop?
    text: '- **Performance** – Excel does the math on its own engine, which is highly
      optimized. - **Maintainability** – The formula is self‑documenting; anyone opening
      the sheet instantly knows the intent. - **Dynamic resizing** – Change the `rows`
      argument and the spill range expands automatically.'
  - name: Pro Tip
    text: 'If you need the workbook in memory (e.g., to send it over a web API), use
      a `MemoryStream`:'
  - name: What If the Client Uses an Older Excel Version?
    text: 'Dynamic arrays (including `SEQUENCE`) were introduced in Excel 365/2019.
      If you need backward compatibility, fall back to a manual fill:'
  type: HowTo
- questions:
  - answer: No. `SEQUENCE` is a non‑iterative function; a simple `CalculateFormula()`
      call is enough.
    question: Do I need to enable iterative calculation?
  - answer: 'Change the second argument: `=SEQUENCE(1,5,10,2)` spills across B1:F1.'
    question: What if I want a horizontal spill?
  - answer: Absolutely. For example, `=INDEX(A:A, SEQUENCE(5,1,10,2))` can pull rows
      from another column.
    question: Can I combine SEQUENCE with other functions?
  - answer: The file size impact of a formula is negligible. Only when you start populating
      millions of cells manually does size become an issue.
    question: Is the workbook size a concern?
  type: FAQPage
tags:
- C#
- Excel
- Aspose.Cells
- ASP.NET
title: Hoe SEQUENCE in C# te gebruiken – Maak een Excel‑werkmap
url: /nl/net/formulas-functions/how-to-use-sequence-in-c-create-excel-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe SEQUENCE te gebruiken in C# – Excel-werkmap maken

Heb je je ooit afgevraagd **hoe je SEQUENCE** kunt gebruiken om een lijst met getallen in een Excel‑blad vanuit C# te genereren? Je bent niet de enige. Of je nu een rapportagedashboard bouwt, een data‑grid voedt, of gewoon snel ID’s wilt aanmaken, deze truc beheersen bespaart je het gedoe met loops.

In deze tutorial **maken we een Excel‑werkmap in C#**, plaatsen we een `SEQUENCE`‑dynamic‑array‑formule in cel A1, en krijgen we een mooie kolom met oplopende getallen. We laten ook zien hoe je dat bestand vanuit een ASP.NET‑controller kunt serveren — ja, **ASP.NET create Excel file** wordt ook behandeld. Aan het einde kun je **incremental numbers Excel**‑stijl genereren met één regel code.

## Wat je nodig hebt

- .NET 6+ (de code werkt ook op .NET Framework 4.6+)  
- Het **Aspose.Cells for .NET** NuGet‑pakket (of een andere bibliotheek die `Workbook`/`Worksheet`‑objecten exposeert)  
- Een basis ASP.NET Core‑ of MVC‑project als je het web‑download‑gedeelte wilt uitproberen  

Dat is alles. Geen extra COM‑interop, geen Office‑installatie vereist.

---

## Hoe SEQUENCE te gebruiken om oplopende getallen te genereren

De Excel‑functie `SEQUENCE(rows, [columns], [start], [step])` retourneert een **spill**‑bereik. In ons geval willen we 5 rijen, 1 kolom, starten bij 10, stap 2. De formule ziet er zo uit:

```excel
=SEQUENCE(5,1,10,2)
```

Wanneer Excel de formule evalueert, bevatten de cellen A1:A5 **10, 12, 14, 16, 18**. Het mooie is dat we geen C#‑loops hoeven te schrijven — de formule doet het zware werk.

Hieronder staat de volledige C#‑snippet die een werkmap maakt, de formule invoegt, de berekening afdwingt en het bestand opslaat.

```csharp
using Aspose.Cells;
using System.IO;

// 1️⃣ Create a new workbook
Workbook workbook = new Workbook();

// 2️⃣ Grab the first worksheet (Aspose creates one by default)
Worksheet sheet = workbook.Worksheets[0];

// 3️⃣ Insert the SEQUENCE formula – this will spill a 5‑row column starting at 10, step 2
sheet.Cells["A1"].Formula = "=SEQUENCE(5,1,10,2)";

// 4️⃣ Force calculation so the spilled range is materialized
workbook.CalculateFormula();

// 5️⃣ Save to disk (you can change the path as needed)
workbook.Save("DynamicArray.xlsx");
```

**Verwacht resultaat** – open *DynamicArray.xlsx* en je ziet:

| A |
|---|
| 10 |
| 12 |
| 14 |
| 16 |
| 18 |

Dat is het volledige **how to use sequence**‑verhaal in C#. Simpel, toch? Laten we echter iets dieper ingaan.

### Waarom SEQUENCE gebruiken in plaats van een loop?

- **Performance** – Excel doet de berekening met zijn eigen, sterk geoptimaliseerde engine.  
- **Maintainability** – De formule is zelf‑documenterend; iedereen die het blad opent, ziet meteen de bedoeling.  
- **Dynamisch schalen** – Verander je het `rows`‑argument en het spill‑bereik wordt automatisch uitgebreid.

---

## Excel-werkmap maken in C# – Stap voor stap

Als je nieuw bent met **create excel workbook c#**, helpt de volgende checklist je om veelvoorkomende valkuilen te vermijden.

1. **Voeg het Aspose.Cells‑pakket toe**  
   ```bash
   dotnet add package Aspose.Cells
   ```
   (Je kunt ook ClosedXML of EPPlus gebruiken, maar de hier getoonde API komt overeen met de bovenstaande code.)

2. **Stel een licentie in** (optioneel voor een trial).  
   ```csharp
   var license = new Aspose.Cells.License();
   license.SetLicense("Aspose.Total.NET.lic");
   ```

3. **Instantieer `Workbook`** – dit geeft je een frisse, lege werkmap.

4. **Verwijs naar het werkblad** – `workbook.Worksheets[0]` is het standaardblad met de naam *Sheet1*.

5. **Pas de SEQUENCE‑formule toe** – zoals eerder getoond.

6. **Bereken** – `workbook.CalculateFormula()` dwingt het spill af; anders zou het bestand alleen de formule bevatten.

7. **Sla op** – je kunt naar schijf schrijven, naar een `MemoryStream`, of direct naar een HTTP‑response.

### Pro Tip

Als je de werkmap in het geheugen nodig hebt (bijvoorbeeld om via een web‑API te versturen), gebruik dan een `MemoryStream`:

```csharp
using var ms = new MemoryStream();
workbook.Save(ms, SaveFormat.Xlsx);
byte[] excelBytes = ms.ToArray(); // ready to return or attach
```

---

## ASP.NET Create Excel File – Streamen naar de browser

Nu we **create excel workbook c#** kennen, integreren we het in een ASP.NET Core‑controller zodat gebruikers het bestand on‑the‑fly kunnen downloaden.

```csharp
using Aspose.Cells;
using Microsoft.AspNetCore.Mvc;
using System.IO;

[Route("api/[controller]")]
public class ExcelController : ControllerBase
{
    [HttpGet("download")]
    public IActionResult Download()
    {
        // 1️⃣ Build the workbook (same steps as before)
        var workbook = new Workbook();
        var sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].Formula = "=SEQUENCE(5,1,10,2)";
        workbook.CalculateFormula();

        // 2️⃣ Save to a memory stream
        using var ms = new MemoryStream();
        workbook.Save(ms, SaveFormat.Xlsx);
        ms.Position = 0; // reset stream position

        // 3️⃣ Return the file as a download
        const string fileName = "DynamicArray.xlsx";
        return File(ms, 
                    "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", 
                    fileName);
    }
}
```

Wanneer een gebruiker `/api/excel/download` aanroept, vraagt de browser om een download van *DynamicArray.xlsx*. Het bestand bevat al de **generated incremental numbers excel**‑kolom dankzij de `SEQUENCE`‑formule.

### Wat als de client een oudere Excel‑versie gebruikt?

Dynamic arrays (inclusief `SEQUENCE`) werden geïntroduceerd in Excel 365/2019. Als je achterwaartse compatibiliteit nodig hebt, val dan terug op een handmatige vulling:

```csharp
// Alternative for older Excel: write numbers directly
for (int i = 0; i < 5; i++)
{
    sheet.Cells[i, 0].PutValue(10 + i * 2); // column 0 = A
}
```

Dat fragment laat de klassieke **generate incremental numbers excel**‑aanpak zien zonder gebruik te maken van de nieuwe functie.

---

## Veelgestelde vragen & randgevallen

- **Moet ik iteratieve berekening inschakelen?**  
  Nee. `SEQUENCE` is een niet‑iteratieve functie; een eenvoudige `CalculateFormula()`‑aanroep volstaat.

- **Wat als ik een horizontaal spill wil?**  
  Verander het tweede argument: `=SEQUENCE(1,5,10,2)` spillt over B1:F1.

- **Kan ik SEQUENCE combineren met andere functies?**  
  Zeker. Bijvoorbeeld, `=INDEX(A:A, SEQUENCE(5,1,10,2))` kan rijen uit een andere kolom halen.

- **Is de grootte van de werkmap een zorg?**  
  De impact van een formule op de bestandsgrootte is verwaarloosbaar. Alleen wanneer je miljoenen cellen handmatig vult, wordt de grootte een probleem.

---

## Conclusie

We hebben stap voor stap laten zien **how to use sequence** in C# om **create excel workbook c#** te maken, die werkmap via **ASP.NET create excel file** te serveren, en een nette manier om **generate incremental numbers excel** te realiseren zonder loops te schrijven. De belangrijkste les: laat Excel’s eigen dynamic‑array‑engine het tellen doen, en laat jouw .NET‑code zich richten op de orkestratie.

Voel je vrij om te experimenteren — verander de `rows`, `start` of `step`‑argumenten, spill horizontaal, of combineer de formule met `IF` of `FILTER` voor meer geavanceerde rapporten. Wanneer je er klaar voor bent, probeer dan meerdere bladen te koppelen of de werkmap als CSV te exporteren voor downstream‑systemen.

Heb je een eigen twist die je wilt delen? Laat een reactie achter, of ping me op GitHub. Veel plezier met coderen!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids zijn gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑features onder de knie te krijgen en alternatieve implementaties in je eigen projecten te verkennen.

- [Hoe Excel‑werkboeken te maken en configureren met Aspose.Cells .NET: Een stapsgewijze handleiding](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Hoe Excel‑bestanden te maken en op te slaan met Aspose.Cells voor .NET: Een volledige gids](/cells/english/net/workbook-operations/create-save-excel-file-aspose-cells-dotnet/)
- [Hoe Excel‑werkboeken te maken en te stylen met Aspose.Cells voor .NET (2023‑gids)](/cells/english/net/formatting/create-style-excel-workbooks-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}