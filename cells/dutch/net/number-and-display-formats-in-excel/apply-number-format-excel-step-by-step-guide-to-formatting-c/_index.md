---
category: general
date: 2026-02-26
description: Pas snel een getalnotatie toe in Excel en leer hoe je een kolom als valuta
  formatteert, de getalnotatie van een kolom instelt en de letterkleur van een kolom
  wijzigt in slechts een paar regels C#.
draft: false
keywords:
- apply number format excel
- format column as currency
- set column number format
- format currency column
- set column font color
language: nl
og_description: Pas getalnotatie toe in Excel met C# in eenvoudige stappen. Leer een
  kolom als valuta te formatteren, de getalnotatie van een kolom in te stellen en
  de letterkleur van een kolom te wijzigen voor professionele spreadsheets.
og_title: nummeropmaak toepassen in Excel – Complete gids voor kolomstyling
tags:
- C#
- Excel
- Aspose.Cells
- DataTable
- Styling
title: Nummeropmaak toepassen in Excel – Stapsgewijze gids voor het opmaken van kolommen
url: /nl/net/number-and-display-formats-in-excel/apply-number-format-excel-step-by-step-guide-to-formatting-c/
---

are preserved. No extra spaces? It's fine.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# getalnotatie toepassen excel – Hoe Excel‑kolommen opmaken in C#

Heb je je ooit afgevraagd hoe je **apply number format excel** kunt **toepassen** terwijl je al door een `DataTable` loopt? Je bent niet de enige. De meeste ontwikkelaars lopen tegen een muur aan wanneer ze een blauwe‑lettertype‑koptekst *en* een valuta‑opgemaakte kolom in dezelfde importoperatie nodig hebben. Het goede nieuws? Met een paar regels C# en de juiste style‑objecten kun je dit doen zonder de sheet na‑te bewerken.

In deze tutorial lopen we een volledig, uitvoerbaar voorbeeld door dat laat zien hoe je **format column as currency**, **set column number format** voor elke andere kolom, en zelfs **set column font color** voor kopteksten kunt instellen. Aan het einde heb je een herbruikbaar patroon dat je in elk Aspose.Cells (of vergelijkbaar) project kunt gebruiken.

## Wat je zult leren

- Hoe je een `DataTable` ophaalt en elke kolom toewijst aan een specifieke `Style`.
- De exacte stappen om **apply number format excel** te **toepassen** met `Worksheet.Cells.ImportDataTable`.
- Waarom het vooraf creëren van stijlen efficiënter is dan cellen één‑voor‑één opmaken.
- Afhandeling van randgevallen wanneer de bron‑tabel meer kolommen heeft dan je hebt gestyled.
- Een volledige, copy‑and‑paste‑klare code‑voorbeeld die je vandaag nog kunt uitvoeren.

> **Voorwaarde:** Deze gids gaat ervan uit dat je Aspose.Cells voor .NET (of een andere bibliotheek die `Workbook`, `Worksheet`, `Style`‑API’s exposeert) in je project hebt opgenomen. Als je een andere bibliotheek gebruikt, vertalen de concepten zich direct—vervang gewoon de type‑namen.

---

## Stap 1: Haal de brongegevens op als een DataTable

Voordat er gestyled kan worden, heb je de ruwe data nodig. In de meeste real‑world scenario’s staan de gegevens in een database, CSV of een API. Voor de duidelijkheid mocken we een eenvoudige `DataTable` met twee kolommen: *Product* (string) en *Price* (decimal).

```csharp
using System;
using System.Data;
using Aspose.Cells;
using System.Drawing;

public static DataTable GetData()
{
    var dt = new DataTable();
    dt.Columns.Add("Product", typeof(string));
    dt.Columns.Add("Price", typeof(decimal));

    dt.Rows.Add("Apple", 1.25m);
    dt.Rows.Add("Banana", 0.75m);
    dt.Rows.Add("Cherry", 2.10m);

    return dt;
}
```

> **Waarom dit belangrijk is:** Het ophalen van de data in een `DataTable` geeft je een tabel‑achtige, in‑memory representatie die `ImportDataTable` direct kan verwerken, waardoor handmatige cel‑voor‑cel invoeging overbodig wordt.

## Stap 2: Maak een array van stijlen – één per kolom

De `ImportDataTable`‑overload die we gebruiken accepteert een array van `Style`‑objecten. Elk element correspondeert met een kolomindex. Als je een element `null` laat, erft de kolom de standaard werkboekstijl.

```csharp
// Initialize the workbook (Aspose.Cells)
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Prepare the style array based on the number of columns
DataTable dataTable = GetData();
Style[] columnStyles = new Style[dataTable.Columns.Count];
```

> **Pro tip:** Het declareren van de array *na* het hebben van de `DataTable` zorgt ervoor dat de grootte exact overeenkomt, waardoor later een `IndexOutOfRangeException` wordt voorkomen.

## Stap 3: Stel kolomletterkleur (blauw) in voor de eerste kolom

Een veelgevraagd verzoek is om header‑ of sleutelkolommen te markeren met een opvallende letterkleur. Hier maken we de tekst van de eerste kolom blauw.

```csharp
// Style for the first column – blue font
columnStyles[0] = workbook.CreateStyle();
columnStyles[0].Font.Color = Color.Blue;
```

> **Waarom een style‑object gebruiken?** Stijlen zijn herbruikbaar en kunnen in bulk worden toegepast, wat veel sneller is dan na de import over elke cel itereren. Het werkboek cachet de stijl één keer en hergebruikt deze vervolgens voor elke cel in die kolom.

## Stap 4: Formatteer de tweede kolom als valuta

De ingebouwde getalnotaties van Excel worden geïdentificeerd door een index. `14` komt overeen met de standaard valuta‑notatie (bijv. `$1,234.00`). Als je een aangepaste notatie nodig hebt, kun je in plaats daarvan een format‑string toewijzen.

```csharp
// Style for the second column – built‑in currency format (ID 14)
columnStyles[1] = workbook.CreateStyle();
columnStyles[1].Number = 14; // 14 = built‑in currency format
```

> **Randgeval:** Als je werkboek een locale gebruikt waarin het valutasymbool niet `$` is, past dezelfde index zich automatisch aan (bijv. `€` voor Duitse locales).

## Stap 5: Importeer de DataTable met de gedefinieerde stijlen

Nu brengen we alles samen. De `ImportDataTable`‑methode plakt de data beginnend bij cel `A1` (rij 0, kolom 0) en past de stijlen toe die we hebben voorbereid.

```csharp
// Import the DataTable into the worksheet, applying the column styles
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

- De tweede parameter `true` vertelt Aspose.Cells om de eerste rij van de `DataTable` als kolom‑headers te behandelen.
- De coördinaten `0, 0` geven de linkerbovenhoek aan waar de import start.
- `columnStyles` koppelt elke kolom aan de respectieve stijl.

## Stap 6: Sla het werkboek op (optioneel, maar handig voor verificatie)

Wil je het resultaat in Excel zien, sla dan gewoon het werkboek op schijf op. Deze stap is niet vereist voor de styling‑logica, maar is nuttig voor debugging.

```csharp
// Save the workbook to a file
workbook.Save("StyledReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Workbook saved as StyledReport.xlsx");
```

### Verwachte output

| **Product** (blauw lettertype) | **Price** (valuta) |
|-------------------------------|--------------------|
| Apple                         | $1.25              |
| Banana                        | $0.75              |
| Cherry                        | $2.10              |

- De *Product*‑kolom verschijnt in blauw, waardoor deze opvalt.
- De *Price*‑kolom toont waarden met het standaard valutasymbool en twee decimalen.

---

## Veelgestelde vragen & variaties

### Hoe stel ik **set column number format** in voor meer dan twee kolommen?

Breid gewoon de `columnStyles`‑array uit. Bijvoorbeeld, om een percentage in de derde kolom weer te geven:

```csharp
columnStyles[2] = workbook.CreateStyle();
columnStyles[2].Number = 10; // 10 = built‑in percentage format
```

### Wat als ik een *aangepaste* valuta‑notatie nodig heb, zoals “USD 1,234.00”?

Vervang de `Number`‑eigenschap door een format‑string:

```csharp
columnStyles[1].Custom = "\"USD\" #,##0.00";
```

### Kan ik een **set column font color** toepassen op een numerieke kolom zonder de getalnotatie te beïnvloeden?

Absoluut. Stijlen zijn composable. Je kunt zowel `Font.Color` als `Number` op dezelfde `Style`‑instantie instellen:

```csharp
columnStyles[3] = workbook.CreateStyle();
columnStyles[3].Font.Color = Color.Green;
columnStyles[3].Number = 2; // 2 = built‑in date format (just an example)
```

### Wat gebeurt er als de `DataTable` meer kolommen heeft dan stijlen?

Elke kolom zonder een expliciete stijl (`null`‑item) erft de standaard stijl van het werkboek. Om onbedoelde `null`s te voorkomen, kun je de hele array eerst initialiseren met een basisstijl:

```csharp
Style defaultStyle = workbook.CreateStyle();
defaultStyle.Font.Size = 11;
for (int i = 0; i < columnStyles.Length; i++)
    columnStyles[i] = defaultStyle;
```

Vervang vervolgens alleen de kolommen die je nodig hebt.

### Werkt deze aanpak met grote datasets (10k+ rijen)?

Ja. Omdat de styling *eenmaal per kolom* wordt toegepast vóór de import, blijft de operatie O(N) ten opzichte van rijen, en blijft het geheugenverbruik laag. Vermijd het itereren over elke cel na import—dat is waar de prestaties afnemen.

---

## Volledig werkend voorbeeld (Klaar om te kopiëren)

```csharp
using System;
using System.Data;
using System.Drawing;
using Aspose.Cells;

class ExcelStyler
{
    static void Main()
    {
        // 1️⃣ Retrieve data
        DataTable dataTable = GetData();

        // 2️⃣ Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 3️⃣ Prepare style array (one per column)
        Style[] columnStyles = new Style[dataTable.Columns.Count];

        // 4️⃣ Style first column – blue font
        columnStyles[0] = workbook.CreateStyle();
        columnStyles[0].Font.Color = Color.Blue;

        // 5️⃣ Style second column – built‑in currency format (ID 14)
        columnStyles[1] = workbook.CreateStyle();
        columnStyles[1].Number = 14;

        // 6️⃣ (Optional) Add more styles here – e.g., percentage, custom formats

        // 7️⃣ Import the DataTable with styles
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // 8️⃣ Save to file for verification
        workbook.Save("StyledReport.xlsx", SaveFormat.Xlsx);
        Console.WriteLine("Excel file created: StyledReport.xlsx");
    }

    // Helper method to mock data
    public static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("Product", typeof(string));
        dt.Columns.Add("Price", typeof(decimal));

        dt.Rows.Add("Apple", 1.25m);
        dt.Rows.Add("Banana", 0.75m);
        dt.Rows.Add("Cherry", 2.10m);
        return dt;
    }
}
```

Voer het programma uit, open `StyledReport.xlsx`, en je ziet direct het **apply number format excel**‑resultaat.

---

## Conclusie

We hebben zojuist een nette, efficiënte manier gedemonstreerd om **apply number format excel** toe te passen op een geïmporteerde `DataTable`. Door vooraf een `Style[]`‑array te maken, kun je **format column as currency**, **set column number format**, en **set column font color** in één enkele aanroep—zonder post‑processing.  

Voel je vrij om het patroon uit te breiden: voeg conditionele styling toe, merge cellen voor kopteksten, of injecteer formules. Dezelfde principes gelden, waardoor je code overzichtelijk blijft en je spreadsheets er professioneel uitzien.

---

### Wat is het volgende?

- Verken **conditional formatting** om waarden die een drempel overschrijden te markeren.
- Combineer deze techniek met **pivot table generation** voor dynamische rapportage.
- Probeer **set column number format** voor datums, percentages, of aangepaste wetenschappelijke notatie.

Heb je een eigen twist geprobeerd? Deel het in de reacties—laten we de

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}