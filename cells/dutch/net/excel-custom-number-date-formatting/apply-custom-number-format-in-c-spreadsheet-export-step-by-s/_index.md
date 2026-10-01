---
category: general
date: 2026-04-07
description: Pas een aangepast getalformaat toe op een spreadsheetcel en leer hoe
  je een getal in een spreadsheet formatteert tijdens het exporteren van de celwaarde
  met C#. Snelle, volledige gids.
draft: false
keywords:
- apply custom number format
- format number in spreadsheet
- how to format numeric cell
- how to export cell value
language: nl
og_description: Pas een aangepast getalformaat toe op een spreadsheetcel en exporteer
  het als een opgemaakte tekenreeks. Leer hoe je een getal in een spreadsheet formatteert
  en de celwaarde exporteert.
og_title: Pas een aangepast getalformaat toe – Complete C# Export Tutorial
tags:
- C#
- Spreadsheet
- Number Formatting
title: Pas aangepaste getalnotatie toe in C# spreadsheet‑export – Stapsgewijze gids
url: /nl/net/excel-custom-number-date-formatting/apply-custom-number-format-in-c-spreadsheet-export-step-by-s/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aangepaste getalnotatie toepassen in C# Spreadsheet-export – Volledige tutorial

Heb je ooit **aangepaste getalnotatie** moeten toepassen op een cel en vervolgens die opgemaakte string uit een spreadsheet moeten halen? Je bent niet de enige. Veel ontwikkelaars lopen tegen een muur aan wanneer ze ontdekken dat de ruwe waarde wordt geretourneerd in plaats van de mooie, locale‑bewuste string die ze verwachten. In deze gids laten we je precies zien hoe je getallen in spreadsheetcellen formatteert en hoe je de celwaarde exporteert als een opgemaakte string met behulp van een populaire C# spreadsheet‑bibliotheek.

Aan het einde van deze walkthrough kun je **aangepaste getalnotatie** toepassen op elke numerieke cel, het resultaat exporteren met `ExportTable`, en de exacte output zien die je zou verwachten te tonen in een UI of een rapport. Geen externe documentatie nodig—alles staat hier.

## Vereisten

- .NET 6.0 of later (de code werkt ook op .NET Framework 4.7+)
- Een referentie naar de spreadsheet‑bibliotheek die `Workbook`, `Worksheet` en `ExportTableOptions` levert (bijv. **Aspose.Cells** of **GemBox.Spreadsheet**; de getoonde API komt overeen met Aspose.Cells)
- Basiskennis van C#—als je een `Console.WriteLine` kunt schrijven, ben je klaar om te beginnen

> **Pro tip:** Als je een andere bibliotheek gebruikt, zijn de eigenschapsnamen meestal vergelijkbaar (`NumberFormat`, `ExportAsString`). Map ze gewoon overeenkomstig.

## Waar de tutorial over gaat

1. Een workbook maken en het eerste werkblad selecteren.  
2. Een numerieke waarde in een cel invoegen.  
3. `ExportTableOptions` configureren om **aangepaste getalnotatie** toe te passen en een string te retourneren.  
4. De cel exporteren en het opgemaakte resultaat afdrukken.  
5. Edge‑case handling – wat als de cel een formule of een null‑waarde bevat?

Laten we beginnen.

![apply custom number format example](https://example.com/image.png "apply custom number format")

## Stap 1 – Maak een workbook en haal het eerste werkblad op

Het eerste wat je nodig hebt is een workbook‑object. Beschouw het als het Excel‑bestand dat je in de Office‑app zou openen. Zodra je het hebt, pak je het eerste blad—de meeste tutorials beginnen daar omdat het voorbeeld beknopt blijft.

```csharp
// Step 1: Initialize the workbook and fetch the first worksheet
Workbook workbook = new Workbook();                 // creates an in‑memory workbook
Worksheet worksheet = workbook.Worksheets[0];      // first sheet (index 0)
```

**Waarom dit belangrijk is:** Een nieuw workbook geeft je een schone lei, zodat er geen verborgen opmaak interfereert met onze aangepaste getalnotatie later.

## Stap 2 – Plaats een numerieke waarde in cel B2 (de cel die we gaan exporteren)

Nu hebben we iets nodig om te formatteren. Cel **B2** is een handige plek—gemakkelijk te refereren en ver genoeg van de standaard A1‑hoek om per ongeluk overschrijven te voorkomen.

```csharp
// Step 2: Insert a raw numeric value
worksheet.Cells["B2"].Value = 1234.56;   // raw double, no formatting yet
```

**Wat als de waarde een formule is?**  
Als je later de ruwe waarde vervangt door een formule (bijv. `=SUM(A1:A10)`), zal de exportroutine nog steeds de getalnotatie die we in de volgende stap toepassen respecteren, omdat opmaak aan de cel is gekoppeld, niet aan het type waarde.

## Stap 3 – Configureer exportopties om de waarde als een opgemaakte string te ontvangen

Dit is het hart van de tutorial: we vertellen de bibliotheek om **aangepaste getalnotatie** toe te passen tijdens het exporteren. De `NumberFormat`‑string volgt hetzelfde patroon dat je in Excel’s “Aangepast”‑categorie zou gebruiken.

```csharp
// Step 3: Set up options for exporting as a formatted string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,                         // forces string output
    NumberFormat = "#,##0.00;(#,##0.00)"           // custom format: 1,234.56 or (1,234.56) for negatives
};
```

- `ExportAsString = true` zorgt ervoor dat de methode een `string` retourneert in plaats van een ruwe double.  
- `NumberFormat = "#,##0.00;(#,##0.00)"` weerspiegelt het Excel‑patroon: komma’s voor duizendtallen, twee decimalen, en haakjes voor negatieve getallen.

> **Waarom een aangepaste notatie gebruiken?** Het garandeert consistentie over culturen heen (bijv. VS vs. Europese scheidingstekens) en laat je bedrijfsspecifieke styling toevoegen, zoals haakjes voor boekhoudkundige notatie.

## Stap 4 – Exporteer de cel met de geconfigureerde opties

Nu halen we de waarde daadwerkelijk uit het werkblad, waarbij we de bibliotheek het zware werk laten doen van het toepassen van de door ons gedefinieerde notatie.

```csharp
// Step 4: Export the formatted value from B2
string formattedResult = worksheet.Cells.ExportTable(
    worksheet.Cells["B2"],   // the source cell
    exportOptions);         // our custom options
```

**Edge case – lege cel:** Als `B2` leeg zou zijn, zou `formattedResult` `null` zijn. Je kunt dat voorkomen met een eenvoudige null‑check vóór het afdrukken.

## Stap 5 – Toon de opgemaakte string

Tot slot schrijven we het resultaat naar de console. In een echte app zou je deze string kunnen plaatsen in een PDF, een e‑mail, of een UI‑label.

```csharp
// Step 5: Show the result
Console.WriteLine(formattedResult);   // Expected output: 1,234.56
```

**Verwachte output**

```
1,234.56
```

Als je de ruwe waarde verandert naar `-9876.54`, geeft dezelfde notatie je `(9,876.54)`—precies wat veel boekhoudkundige rapporten vereisen.

## Volledig, uitvoerbaar voorbeeld

Hieronder staat het volledige programma dat je kunt kopiëren‑en‑plakken in een nieuw console‑project. Het compileert en draait direct, ervan uitgaande dat je het juiste NuGet‑pakket voor de spreadsheet‑bibliotheek hebt toegevoegd.

```csharp
using System;
using Aspose.Cells;   // Replace with your library’s namespace if different

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Insert numeric value into B2
        worksheet.Cells["B2"].Value = 1234.56;

        // 3️⃣ Set export options – apply custom number format
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "#,##0.00;(#,##0.00)"   // custom format
        };

        // 4️⃣ Export the cell as a formatted string
        string formattedResult = worksheet.Cells.ExportTable(
            worksheet.Cells["B2"], exportOptions);

        // 5️⃣ Output the result
        Console.WriteLine(formattedResult);   // → 1,234.56
    }
}
```

### Snelle controle

- **Compileert het?** Ja—zorg er alleen voor dat de `Aspose.Cells` (of equivalent) DLL is gerefereerd.
- **Werkt het met andere culturen?** De notatiestring is cultuur‑agnostisch; de bibliotheek respecteert het patroon dat je opgeeft. Als je locale‑specifieke scheidingstekens nodig hebt, kun je vóór het exporteren `CultureInfo`‑afhandeling toevoegen.

## Veelgestelde vragen & variaties

### Hoe **getal in spreadsheet** te **formatten** met een ander patroon?

Vervang de `NumberFormat`‑string. Bijvoorbeeld, om een percentage met één decimaal weer te geven:

```csharp
NumberFormat = "0.0%";
```

### Wat als ik de **celwaarde moet exporteren** als HTML in plaats van platte tekst?

De meeste bibliotheken hebben een overload die een exporttype accepteert. Je zou `ExportAsString = true` instellen en `ExportHtml = true` (of iets dergelijks) toevoegen. Het principe blijft hetzelfde: definieer de notatie, kies vervolgens de output‑representatie.

### Kan ik de notatie toepassen op een heel bereik, niet alleen op één cel?

Zeker. Je kunt `NumberFormat` toewijzen aan een `Style`‑object en die stijl vervolgens toepassen op een `Range`. De exportaanroep blijft ongewijzigd; hij zal de stijl automatisch oppikken.

```csharp
Style style = workbook.CreateStyle();
style.Custom = "#,##0.00;(#,##0.00)";
Range range = worksheet.Cells.CreateRange("A1:C10");
range.ApplyStyle(style, new StyleFlag { NumberFormat = true });
```

### Wat gebeurt er wanneer de cel een formule bevat?

De exportroutine evalueert eerst de formule, en formatteert daarna de resulterende numerieke waarde. Er is geen extra code nodig—zorg er alleen voor dat `Calculate` is aangeroepen als je automatische berekening hebt uitgeschakeld.

```csharp
worksheet.Cells["B2"].Formula = "=SUM(A1:A5)";
worksheet.Calculate();   // forces evaluation
```

## Conclusie

Je weet nu hoe je **aangepaste getalnotatie** kunt toepassen op een spreadsheet‑cel, **getallen in een spreadsheet** kunt formatteren, en **celwaarde kunt exporteren** als een kant‑klaar‑te‑tonen string. Het beknopte code‑voorbeeld hierboven behandelt elke stap—van workbook‑creatie tot eindoutput—zodat je het direct in een productieproject kunt gebruiken.

Klaar voor de volgende uitdaging? Probeer deze techniek te combineren met **hoe numerieke cellen te formatteren** voor datums, valutatekens of voorwaardelijke opmaak. Of verken het exporteren van meerdere cellen als CSV terwijl je elke cel‑aangepaste notatie behoudt. De mogelijkheden zijn eindeloos, en met deze basisprincipes heb je een solide fundament.

Veel plezier met coderen, en vergeet niet te experimenteren—soms komen de beste oplossingen naar voren wanneer je de notatiestring net een beetje aanpast!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}