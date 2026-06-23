---
category: general
date: 2026-06-05
description: Pas celstijlen toe tijdens het importeren met Aspose.Cells. Leer hoe
  je een DataTable met opmaak importeert, rijen stijlt en werkbladen netjes houdt.
draft: false
keywords:
- apply cell styles
- aspose cells import
- import with formatting
- how to import datatable
- import datatable worksheet
language: nl
og_description: Pas celstijlen toe bij het importeren van een DataTable in een Aspose.Cells-werkblad.
  Stapsgewijze handleiding met volledige code en tips.
og_title: Celstijlen toepassen met Aspose.Cells – DataTable importeren
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: Apply cell styles while using Aspose.Cells import. Learn how to import
    DataTable with formatting, style rows, and keep worksheets tidy.
  headline: Apply Cell Styles with Aspose.Cells – Import DataTable with Formatting
  type: TechArticle
- description: Apply cell styles while using Aspose.Cells import. Learn how to import
    DataTable with formatting, style rows, and keep worksheets tidy.
  name: Apply Cell Styles with Aspose.Cells – Import DataTable with Formatting
  steps:
  - name: How It Works
    text: 1. **Headers** – Because we passed `true`, Aspose writes “Name” and “Score”
      into the first row. 2. **Data Rows** – Each subsequent row receives the corresponding
      style from `importStyles`. 3. **Performance** – The method streams the data
      directly into the worksheet, which is faster than looping cell
  - name: What if My DataTable Has More Columns Than Styles?
    text: Aspose will apply the last style in the array to any extra columns. To avoid
      unexpected colors, always match the array length to the column count, or pass
      `null` for columns you don’t want styled.
  - name: Can I Apply Different Styles to Specific Rows?
    text: 'Absolutely. After the import, you can loop through rows and assign new
      `Style` objects based on conditions (e.g., highlight scores > 90 in green).
      Here’s a quick snippet:'
  - name: Does This Work with Large DataSets?
    text: Yes. `ImportDataTable` streams data efficiently, and applying a static style
      array adds negligible overhead. For millions of rows, consider using `ImportDataTable`
      in chunks or leveraging `Cells.ImportDataTable` with a `DataReader` for even
      better memory usage.
  - name: How Do I Preserve Existing Formatting in the Worksheet?
    text: If the target range already has formatting you want to keep, set the `ImportDataTable`
      overload’s `importOptions` parameter (`ImportTableOptions`) and tweak `ImportDataTableOptions.PreserveCellFormatting`.
      The default behavior overwrites styles with the ones you supply.
  type: HowTo
tags:
- Aspose.Cells
- C#
- DataTable
title: Celstijlen toepassen met Aspose.Cells – DataTable importeren met opmaak
url: /nl/net/excel-formatting-and-styling/apply-cell-styles-with-aspose-cells-import-datatable-with-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Celstijlen toepassen met Aspose.Cells – DataTable importeren met opmaak

Heb je je ooit afgevraagd hoe je **celstijlen** kunt **toepassen** wanneer je een `DataTable` in een Excel‑blad laadt? Je bent niet de enige. In veel rapportagescenario's moet de data er direct goed uitzien—geen handmatige opmaak later. Het goede nieuws is dat Aspose.Cells het moeiteloos maakt om **met opmaak te importeren**, zodat je rijen rood of blauw, vetgedrukt, of wat je maar wilt, kunnen zijn.

In deze tutorial lopen we een compleet, uitvoerbaar voorbeeld door dat laat zien **hoe je een datatable kunt importeren** in een werkblad **met toegepaste celstijlen**. Aan het einde heb je een kant‑klaar C# console‑applicatie die een werkmap maakt, de eerste twee kolommen opmaakt, en het bestand opslaat—alles met de `aspose cells import` API.

## Wat je zult leren

- Aspose.Cells instellen in een .NET‑project  
- Een voorbeeld‑`DataTable` bouwen die real‑world data nabootst  
- `Style`‑objecten definiëren voor rode en blauwe lettertypen  
- `Worksheet.Cells.ImportDataTable` gebruiken om **datatables te importeren naar een werkblad** terwijl de stijlen worden toegepast  
- Het resultaat verifiëren en de werkmap opslaan  

Geen externe tools, alleen pure C# en Aspose.Cells. Laten we beginnen.

---

## Vereisten

Voordat we in de code duiken, zorg dat je het volgende hebt:

| Vereiste | Waarom het belangrijk is |
|----------|--------------------------|
| .NET 6.0 of later | Aspose.Cells 23.x richt zich op .NET Standard 2.0+, dus .NET 6 biedt de nieuwste runtime‑functies. |
| Aspose.Cells for .NET (NuGet) | De bibliotheek levert de `Workbook`, `Worksheet`, `Style` en `ImportDataTable`‑methoden die we nodig hebben. |
| Basis C#‑kennis | Je begrijpt klassen, arrays en `using`‑statements. |
| Een IDE (Visual Studio, VS Code, Rider) | Elke editor werkt, maar je moet wel NuGet‑pakketten herstellen. |

Je kunt het pakket installeren via de opdrachtregel:

```bash
dotnet add package Aspose.Cells
```

---

## Stap 1: Maak een nieuwe Workbook en krijg toegang tot het eerste werkblad

Allereerst—laten we een `Workbook` aanmaken en het eerste blad pakken. Beschouw de werkmap als een leeg notitieboek; het eerste werkblad is de pagina waarop we gaan schrijven.

```csharp
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;

class Program
{
    static void Main()
    {
        // Create a new workbook (equivalent to a new Excel file)
        Workbook wb = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet worksheet = wb.Worksheets[0];
```

> **Pro tip:** Als je ooit meerdere bladen nodig hebt, voeg ze dan toe met `wb.Worksheets.Add()` en verwijs ernaar via de naam of index.

---

## Stap 2: Bereid een voorbeeld‑DataTable voor (Hoe een DataTable te importeren)

Nu hebben we iets nodig om te importeren. In echte projecten zou je een database aanroepen, maar voor de duidelijkheid bouwen we een `DataTable` in het geheugen.

```csharp
        // Build a sample DataTable with two columns: Name and Score
        DataTable dataTable = new DataTable("Results");
        dataTable.Columns.Add("Name", typeof(string));
        dataTable.Columns.Add("Score", typeof(int));

        // Populate rows – imagine these came from a query
        dataTable.Rows.Add("Alice", 85);
        dataTable.Rows.Add("Bob", 92);
        dataTable.Rows.Add("Charlie", 78);
        dataTable.Rows.Add("Diana", 91);
```

> **Waarom dit belangrijk is:** Een `DataTable` hebben stelt ons in staat de **aspose cells import**‑stroom te testen zonder externe afhankelijkheden.

---

## Stap 3: Definieer de stijlen die op de geïmporteerde cellen moeten worden toegepast

Hier gebeurt de magie. We maken twee `Style`‑objecten: één met een rood lettertype, een andere met een blauw lettertype. Deze worden kolom‑gewijs toegepast tijdens het importeren.

```csharp
        // Define an array of styles – one per column
        Style[] importStyles = new Style[2];

        // Style for the first column (Name) – red text
        Style redStyle = wb.CreateStyle();
        redStyle.Font.Color = Color.Red;
        importStyles[0] = redStyle;

        // Style for the second column (Score) – blue text
        Style blueStyle = wb.CreateStyle();
        blueStyle.Font.Color = Color.Blue;
        importStyles[1] = blueStyle;
```

> **Let op:** De lengte van `importStyles` moet overeenkomen met het aantal kolommen dat je importeert, anders zal Aspose een `ArgumentException` gooien.

---

## Stap 4: Importeer de DataTable in het werkblad **met opmaak**

Nu brengen we alles samen. De `ImportDataTable`‑overload die we gebruiken accepteert de `Style[]`‑array, waardoor we **celstijlen kunnen toepassen** terwijl de data in het blad terechtkomt.

```csharp
        // Import the DataTable starting at cell A1 (row 0, column 0)
        // The 'true' flag tells Aspose to generate column headers automatically
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);
```

### Hoe het werkt

1. **Headers** – Omdat we `true` hebben doorgegeven, schrijft Aspose “Name” en “Score” in de eerste rij.  
2. **Data‑rijen** – Elke volgende rij krijgt de overeenkomstige stijl uit `importStyles`.  
3. **Prestaties** – De methode streamt de data direct naar het werkblad, wat sneller is dan cel‑voor‑cel itereren.

---

## Stap 5: Controleer het resultaat en sla de werkmap op

Laten we een kijkje nemen in de eerste paar cellen om te controleren of de stijlen zijn toegepast, en daarna het bestand naar schijf schrijven.

```csharp
        // Optional: Quick sanity check – print the first row's values
        Console.WriteLine("Header Row:");
        Console.WriteLine($"{worksheet.Cells[0, 0].StringValue} | {worksheet.Cells[0, 1].StringValue}");

        // Save the workbook to an Excel file
        string outputPath = "StyledImport.xlsx";
        wb.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Wanneer je **StyledImport.xlsx** opent, zie je:

- De “Name”‑kolom in **rode** tekst.  
- De “Score”‑kolom in **blauwe** tekst.  
- Kolomkoppen in de standaardstijl (je kunt ze ook stijlen, maar dat is een andere tutorial).

![Voorbeeld van celstijlen toepassen](https://example.com/images/apply-cell-styles.png "Celstijlen toepassen in Aspose.Cells")

> **Opmerking:** De afbeelding hierboven toont het uiteindelijke uiterlijk. Het `alt`‑attribuut bevat het primaire zoekwoord, wat voldoet aan SEO‑vereisten.

---

## Veelgestelde vragen & randgevallen

### Wat als mijn DataTable meer kolommen heeft dan stijlen?

Aspose past de laatste stijl in de array toe op eventuele extra kolommen. Om onverwachte kleuren te voorkomen, zorg dat de array‑lengte overeenkomt met het aantal kolommen, of geef `null` door voor kolommen die je niet wilt stijlen.

### Kan ik verschillende stijlen toepassen op specifieke rijen?

Absoluut. Na het importeren kun je door rijen itereren en nieuwe `Style`‑objecten toewijzen op basis van voorwaarden (bijv. scores > 90 in groen markeren). Hier is een kort fragment:

```csharp
for (int i = 1; i <= dataTable.Rows.Count; i++) // start at 1 to skip header
{
    int score = worksheet.Cells[i, 1].IntValue;
    if (score > 90)
    {
        Style highScore = wb.CreateStyle();
        highScore.Font.Color = Color.Green;
        worksheet.Cells[i, 1].SetStyle(highScore);
    }
}
```

### Werkt dit met grote datasets?

Ja. `ImportDataTable` streamt data efficiënt, en het toepassen van een statische stijlarray voegt nauwelijks overhead toe. Voor miljoenen rijen kun je overwegen `ImportDataTable` in delen te gebruiken of `Cells.ImportDataTable` met een `DataReader` te benutten voor nog beter geheugenverbruik.

### Hoe behoud ik bestaande opmaak in het werkblad?

Als het doelbereik al opmaak heeft die je wilt behouden, stel dan de `ImportDataTable`‑overload’s `importOptions`‑parameter (`ImportTableOptions`) in en pas `ImportDataTableOptions.PreserveCellFormatting` aan. Het standaardgedrag overschrijft stijlen met de door jou opgegeven stijlen.

---

## Samenvatting: wat we hebben bereikt

- **Celstijlen toegepast** tijdens een **aspose cells import**‑operatie.  
- Gedemonstreerd **import met opmaak** door een `Style[]`‑array door te geven.  
- Getoond **hoe je een datatable kunt importeren** in een werkblad en het resultaat opslaat.  
- Randgevallen behandeld zoals niet‑overeenkomende stijl‑aantallen en conditionele rij‑opmaak.

Dit alles werd gedaan in één zelfstandige console‑applicatie—geen externe scripts, geen handmatig Excel‑geklied. Je hebt nu een solide basis voor elke rapportage‑ of data‑exportfunctie die een nette Excel‑output vereist.

## Volgende stappen

Klaar om een stap hoger te gaan? Hier zijn een paar ideeën die voortbouwen op wat je net geleerd hebt:

- **Stijl de header‑rij** (bijv. vet, achtergrondkleur).  
- **Conditionele opmaak toepassen** met `Worksheet.Cells[i, j].ConditionalFormattingCollection`.  
- **Exporteren naar andere formaten** zoals CSV of PDF met `wb.Save("file.pdf", SaveFormat.Pdf)`.  
- **Meerdere DataTables combineren** in één werkmap, elk op een eigen blad, met dezelfde opmaakbenadering.

Als je ergens tegenaan loopt, laat een reactie achter of raadpleeg de officiële documentatie van Aspose over `ImportDataTable`. Veel plezier met coderen, en geniet van die prachtig gestylede Excel‑bestanden!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids zijn gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe een DataTable te importeren in Excel met Aspose.Cells voor .NET (Stap‑voor‑stap gids)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [Hoe lettertype‑stijlen in te stellen in Excel met Aspose.Cells voor .NET (Stap‑voor‑stap gids)](/cells/english/net/formatting/aspose-cells-dotnet-set-font-styles-excel/)
- [Hoe tekstschaduw toe te passen in Excel met Aspose.Cells .NET: Een stap‑voor‑stap gids](/cells/english/net/formatting/apply-text-shadow-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}