---
category: general
date: 2026-03-30
description: Maak een Excel-werkmap in C# met valutavormatting. Leer hoe je een DataTable
  importeert, een getalnotatie toevoegt in Excel en een valutavormatting toepast op
  een kolom in enkele minuten.
draft: false
keywords:
- create excel workbook c#
- format cells currency
- import datatable to excel
- add number format excel
- apply currency format column
language: nl
og_description: Maak een Excel-werkmap in C# en formatteer cellen direct als valuta.
  Deze stapsgewijze tutorial laat zien hoe je een DataTable naar Excel importeert
  en een getalnotatie toevoegt aan een kolom.
og_title: Excel-werkmap maken C# – Gids voor valutavormatting
tags:
- Aspose.Cells
- C#
- Excel automation
title: Excel-werkmap maken met C# – Valuta‑opmaak toepassen en DataTable importeren
url: /nl/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel-werkmap maken in C# – Valuta‑opmaak toepassen en DataTable importeren

Heb je ooit **een Excel-werkmap in C#** moeten maken die er al uitziet als een afgewerkt rapport? Misschien haal je verkoopcijfers uit een database en wil je dat de prijskolom als dollars wordt weergegeven zonder handmatig in Excel te rommelen. Klinkt bekend? Je bent niet de enige—de meeste ontwikkelaars lopen tegen dit probleem aan bij hun eerste Excel‑exportautomatisering.

In deze gids lopen we stap voor stap door een complete, kant‑klaar oplossing die **een Excel-werkmap in C# maakt**, een `DataTable` importeert, en **de Prijs‑kolom als valuta opmaakt**. Aan het einde heb je een bestand genaamd `StyledTable.xlsx` dat je kunt openen en waarin de getallen netjes zijn opgemaakt. Geen extra nabewerking nodig.

> **Wat je zult leren**
> - Hoe je Aspose.Cells instelt in een .NET‑project  
> - Hoe je **een datatable naar Excel importeert** met een stijl‑array  
> - Hoe je **een getalopmaak in Excel toevoegt** voor een specifieke kolom  
> - Tips voor het omgaan met meer kolommen of verschillende locales  

> **Prerequisites**  
> - .NET 6+ (of .NET Framework 4.6+) geïnstalleerd  
> - Aspose.Cells for .NET NuGet‑package (`Install-Package Aspose.Cells`)  
> - Basiskennis van C# en DataTables  

---

## Stap 1: De DataTable voorbereiden (import datatable to excel)

Eerst hebben we wat voorbeeldgegevens nodig. In een echte applicatie zou je deze tabel waarschijnlijk vullen vanuit een DB‑query, maar een hard‑coded voorbeeld houdt het simpel.

```csharp
using System.Data;

// Create a DataTable with two columns: Product (string) and Price (double)
DataTable dataTable = new DataTable();
dataTable.Columns.Add("Product", typeof(string));
dataTable.Columns.Add("Price", typeof(double));

// Add a few rows – you can add as many as you like
dataTable.Rows.Add("Apple", 1.23);
dataTable.Rows.Add("Banana", 0.78);
dataTable.Rows.Add("Cherry", 2.50);
```

*Waarom dit belangrijk is*: De `DataTable` is de brug tussen je bedrijfsgegevens en het Excel‑bestand. Aspose.Cells kan deze direct importeren, waarbij kolomnamen en gegevenstypen behouden blijven.

---

## Stap 2: Een nieuwe Workbook aanmaken (create excel workbook c#)

Nu maken we het daadwerkelijke Excel‑bestandobject. Beschouw het als het lege canvas waarop je gaat schilderen.

```csharp
using Aspose.Cells;

// Instantiate a fresh workbook – this is the core of create excel workbook c#
Workbook workbook = new Workbook();

// Grab the first worksheet (index 0). You could also add more sheets later.
Worksheet worksheet = workbook.Worksheets[0];
```

> **Pro tip:** Als je meerdere bladen nodig hebt, roep dan `workbook.Worksheets.Add()` aan en geef elk een betekenisvolle naam.

---

## Stap 3: Een valuta‑stijl definiëren (format cells currency)

Aspose.Cells laat je een `Style`‑object maken dat beschrijft hoe cellen eruit moeten zien. Voor valuta gebruiken we het ingebouwde getalopmaak‑ID 164 (`"$#,##0.00"`).

```csharp
// Create a new style object for the price column
Style priceStyle = workbook.CreateStyle();
priceStyle.Number = 164; // Built‑in currency format "$#,##0.00"
```

*Waarom niet gewoon de opmaak‑string instellen?* Het gebruik van het ingebouwde ID zorgt voor compatibiliteit over verschillende Excel‑versies heen en voorkomt locale‑specifieke eigenaardigheden.

---

## Stap 4: De stijl‑array bouwen (apply currency format column)

Bij het importeren van een `DataTable` kun je een array van `Style`‑objecten doorgeven—één per kolom. `null` betekent “gebruik de standaardstijl”. Hier passen we `priceStyle` alleen toe op de tweede kolom.

```csharp
// Column 0 (Product) gets the default style, Column 1 (Price) gets the currency style
Style[] columnStyles = { null, priceStyle };
```

Als je later meer kolommen toevoegt, breid je de array eenvoudig uit. De lengte van `columnStyles` moet overeenkomen met het aantal kolommen dat je importeert, anders gooit Aspose een uitzondering.

---

## Stap 5: De DataTable importeren met stijlen (import datatable to excel)

Nu gebeurt de magie—onze `DataTable` wordt in het werkblad geplaatst, en de prijskolom wordt direct als valuta weergegeven.

```csharp
// Parameters:
//  - dataTable: source data
//  - true: include column headers
//  - startRow: 0 (top of sheet)
//  - startColumn: 0 (first column)
//  - columnStyles: style array defined above
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

*Wat als je meer dan twee kolommen hebt?* Breid `columnStyles` gewoon uit zodat elke kolom de juiste stijl krijgt (of `null` voor de standaard). Dit is de netste manier om **een getalopmaak in Excel toe te voegen** selectief.

---

## Stap 6: De Workbook opslaan (create excel workbook c#)

Tot slot schrijven we het bestand naar schijf. Kies een map waar je schrijfrechten voor hebt.

```csharp
// Save the workbook as an XLSX file
workbook.Save("YOUR_DIRECTORY/StyledTable.xlsx");
```

Open `StyledTable.xlsx` in Excel en je zou moeten zien:

| Product | Prijs |
|---------|-------|
| Apple   | $1.23 |
| Banana  | $0.78 |
| Cherry  | $2.50 |

De **Prijs**‑kolom is al opgemaakt als valuta—geen extra stappen nodig.

---

## Edge Cases & Variations

### Meer kolommen, verschillende opmaken

Als je **cellen valuta wilt opmaken** voor meerdere kolommen (bijv. Kosten, Belasting, Totaal), maak dan een aparte `Style` voor elke kolom en vul `columnStyles` dienovereenkomstig:

```csharp
Style costStyle = workbook.CreateStyle();
costStyle.Number = 164; // currency

Style taxStyle = workbook.CreateStyle();
taxStyle.Number = 164;

// Assuming columns: Product, Cost, Tax, Total
Style[] styles = { null, costStyle, taxStyle, priceStyle };
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, styles);
```

### Locale‑specifieke valuta

Voor Euro of Britse Pond, gebruik andere ingebouwde IDs (bijv. 165 voor `€#,##0.00`). Je kunt ook een aangepaste opmaak‑string instellen:

```csharp
priceStyle.Custom = "€#,##0.00";
```

### Grote datasets

Aspose.Cells kan miljoenen rijen aan, maar het geheugenverbruik groeit met stijl‑objecten. Hergebruik één `Style`‑instantie voor alle valutakolommen om de footprint laag te houden.

### Ontbrekende stijlen

Als `columnStyles` korter is dan het aantal kolommen, past Aspose de standaardstijl toe op de resterende kolommen. Handig wanneer je slechts een paar kolommen wilt aanpassen.

---

## Volledig werkend voorbeeld (Alle stappen gecombineerd)

Hieronder staat het complete programma dat je kunt kopiëren‑plakken in een console‑applicatie. Het bevat alle besproken onderdelen, plus een paar nuttige commentaren.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Build sample DataTable (import datatable to excel)
        // -------------------------------------------------
        DataTable dataTable = new DataTable();
        dataTable.Columns.Add("Product", typeof(string));
        dataTable.Columns.Add("Price", typeof(double));
        dataTable.Rows.Add("Apple", 1.23);
        dataTable.Rows.Add("Banana", 0.78);
        dataTable.Rows.Add("Cherry", 2.50);
        // You can add as many rows as you like here.

        // -------------------------------------------------
        // Step 2: Create a new workbook (create excel workbook c#)
        // -------------------------------------------------
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // -------------------------------------------------
        // Step 3: Define a currency style (format cells currency)
        // -------------------------------------------------
        Style priceStyle = workbook.CreateStyle();
        priceStyle.Number = 164; // "$#,##0.00" – built‑in currency format

        // -------------------------------------------------
        // Step 4: Build the style array (apply currency format column)
        // -------------------------------------------------
        // First column gets default style (null), second column uses priceStyle.
        Style[] columnStyles = { null, priceStyle };

        // -------------------------------------------------
        // Step 5: Import the DataTable with the style array
        // -------------------------------------------------
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // -------------------------------------------------
        // Step 6: Save the workbook to disk
        // -------------------------------------------------
        string outputPath = @"YOUR_DIRECTORY\StyledTable.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**Verwacht resultaat:** Het openen van `StyledTable.xlsx` toont de `Prijs`‑kolom met een dollarteken en twee decimalen, precies zoals de **format cells currency**‑instructie eist.

---

## Frequently Asked Questions

**Q: Werkt dit met .NET Core?**  
A: Absoluut. Aspose.Cells is .NET‑standard compliant, dus je kunt targeten op .NET 5, .NET 6 of later zonder wijzigingen.

**Q: Wat als mijn DataTable 10 kolommen heeft maar ik alleen kolom 5 wil opmaken?**  
A: Maak een `Style[]` van lengte 10, vul posities 0‑4 en 6‑9 met `null`, en zet je aangepaste stijl op index 4 (nul‑gebaseerd). Aspose respecteert elke invoer.

**Q: Kan ik de koprij verbergen?**  
A: Na import kun je `worksheet.Cells.Rows[0].Hidden = true;` instellen of simpelweg `false` doorgeven voor de `includeColumnNames`‑parameter in `ImportDataTable`.

---

## Conclusie

We hebben zojuist **een Excel-werkmap in C# gemaakt**, een `DataTable` geïmporteerd, en **een valuta‑opmaak op een kolom toegepast** met Aspose.Cells. De belangrijkste stappen—data voorbereiden, een stijl definiëren, een stijl‑array bouwen, importeren met `ImportDataTable`, en opslaan—dekken de kern van de meeste Excel‑automatiseringstaken.

Van hieruit kun je verder gaan met:

- **een getalopmaak in Excel toevoegen** voor datums of percentages  
- Meerdere werkbladen exporteren in één bestand  
- **cellen valuta opmaken** met locale‑specifieke symbolen  
- Het automatiseren van grafiek‑creatie op basis van dezelfde data  

Probeer die uit, en je wordt snel de go‑to persoon voor Excel‑rapportage in je team. Heb je een eigen twist die je wilt delen? Laat een reactie achter—happy coding!  

![create excel workbook c# screenshot](image.png "create excel workbook c#")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}