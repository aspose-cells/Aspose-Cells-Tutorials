---
category: general
date: 2026-03-18
description: Leer hoe je afwisselende rijkleuren toepast in een werkblad met C#. Inclusief
  het instellen van de achtergrondkleur van een rij, het toevoegen van een lichtgele
  achtergrond en het afwisselend kleuren van rijen.
draft: false
keywords:
- apply alternating row colors
- set row background color
- add light yellow background
- set alternating row shading
- color rows alternately
language: nl
og_description: Pas afwisselende rijkleuren toe in C# om de leesbaarheid te verbeteren.
  Deze gids laat zien hoe je de achtergrondkleur van een rij instelt, een lichtgele
  achtergrond toevoegt en rijen afwisselend kleurt.
og_title: Pas afwisselende rijkleuren toe in C# – Volledige tutorial
tags:
- C#
- DataTable
- Spreadsheet styling
- UI design
title: Afwisselende rijkleuren toepassen in C# – Stapsgewijze handleiding
url: /nl/net/excel-colors-and-background-settings/apply-alternating-row-colors-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Toepassen van afwisselende rijkleuren in C# – Complete tutorial

Heb je ooit **afwisselende rijkleuren** moeten toepassen op een data‑gedreven werkblad, maar wist je niet waar te beginnen? Je bent niet de enige — de meeste ontwikkelaars lopen tegen dit probleem aan wanneer ze voor het eerst proberen tabellen er wat vriendelijker uit te laten zien. Het goede nieuws? Met slechts een paar regels C# kun je **rijachtergrondkleur instellen**, een **lichte gele achtergrond toevoegen**, en eindigen met een gepolijste raster die de leesbaarheid onmiddellijk verbetert.

In deze tutorial lopen we het volledige proces door, van het ophalen van een `DataTable` naar het geheugen tot het stylen van elke rij met een subtiele geel‑witte streep. Aan het einde kun je **rijen afwisselend kleuren** met vertrouwen, en zie je ook een paar handige variaties voor wanneer je verschillende tinten of dynamische thematisering nodig hebt.

## Wat je nodig hebt

- Een .NET‑project dat richt op .NET 6 of later (de code werkt ook op .NET Framework 4.7+).  
- Een spreadsheet‑bibliotheek die stijlobjecten ondersteunt – het voorbeeld gebruikt een generieke `Workbook`/`Worksheet` API die bibliotheken zoals **Aspose.Cells**, **GemBox.Spreadsheet**, of **ClosedXML** weerspiegelt.  
- Een `DataTable`‑bron – kan afkomstig zijn van een database‑query, CSV‑import, of een willekeurige in‑memory collectie.  

Geen extra NuGet‑pakketten naast de spreadsheet‑bibliotheek zelf. Als je Aspose.Cells gebruikt, is de namespace `Aspose.Cells`; voor ClosedXML is het `ClosedXML.Excel`. Vervang de `CreateStyle`‑ en `ImportDataTable`‑aanroepen dienovereenkomstig.

## Stap 1: Haal de brongegevens op als een DataTable

Eerst en vooral—pak de gegevens die je wilt weergeven. In real‑world apps betekent dit meestal een database aanspreken, maar voor de duidelijkheid maken we een helper‑methode genaamd `GetData()` die een gevulde `DataTable` retourneert.

```csharp
// Step 1: Retrieve the source data as a DataTable
DataTable dataTable = GetData();   // Replace with your actual data retrieval logic
```

> **Waarom dit belangrijk is:** De `DataTable` definieert de rijen en kolommen die later de afwisselende schaduw ontvangen. Als de tabel leeg is, is er niets om te stylen, dus controleer altijd dat `Rows.Count` > 0 voordat je verdergaat.

### Pro tip
Als je gegevens ophaalt uit Entity Framework, kun je `DataTable.Load(reader)` gebruiken na het uitvoeren van een `SqlCommand`. Dat houdt de code netjes en voorkomt handmatige kolomdefinities.

## Stap 2: Reserveer een array om een stijl voor elke rij op te slaan

Vervolgens hebben we een container nodig die overeenkomt met het aantal rijen. De meeste spreadsheet‑API’s laten je een stijl‑array doorgeven aan de import‑methode, dus we maken een `Style[]` die precies de rij‑telling heeft.

```csharp
// Step 2: Allocate an array to hold a style for each row
Style[] rowStyles = new Style[dataTable.Rows.Count];
```

> **Uitleg:** Door de array vooraf te reserveren, vermijden we het opnieuw aanmaken van een nieuw stijlobject bij elke iteratie, wat een prestatievoordeel kan opleveren bij duizenden rijen.

## Stap 3: Pas afwisselende rijkleuren toe (lichtgeel / wit)

Nu komt het hart van de zaak: **afwisselende rijkleuren toepassen**. We lopen door elke rij, maken een verse stijl‑instantie van de workbook, en stellen de achtergrond in op basis van de rij‑index. Even rijen krijgen een lichtgele vulling, oneven rijen blijven wit.

```csharp
// Step 3: Create alternating background colors (light yellow / white) for the rows
for (int rowIndex = 0; rowIndex < dataTable.Rows.Count; rowIndex++)
{
    // Create a new style instance from the workbook
    rowStyles[rowIndex] = wb.CreateStyle();

    // Apply a light yellow background to even rows, white to odd rows
    rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
        ? Color.LightYellow   // add light yellow background
        : Color.White;        // set row background color to white

    rowStyles[rowIndex].Pattern = BackgroundType.Solid; // set alternating row shading
}
```

### Waarom dit werkt
- **`rowIndex % 2 == 0`** controleert of de rij even is.  
- **`Color.LightYellow`** geeft een zachte, niet‑opdringerige tint die perfect is voor datatabellen.  
- **`BackgroundType.Solid`** zorgt ervoor dat de vulling de hele cel bedekt, waardoor het **rijachtergrondkleur instellen**‑effect ontstaat.  

Je kunt `Color.LightYellow` vervangen door elke andere tint (bijv. `Color.LightCyan`) als je een andere uitstraling wilt. Dezelfde logica laat je ook **rijen afwisselend kleuren** op basis van andere criteria, zoals status‑vlaggen.

## Stap 4: Importeer de DataTable in het werkblad met de voorbereide stijlen

Tot slot duwen we alles naar het werkblad. De meeste bibliotheken bieden een `ImportDataTable`‑overload die een stijl‑array accepteert. De `true`‑vlag vertelt de API om kolomkoppen te schrijven, en de coördinaten `0, 0` starten bij de boven‑linker cel.

```csharp
// Step 4: Import the DataTable into the worksheet, applying the prepared row styles
ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);
```

> **Resultaat:** Het werkblad toont nu je gegevens met een nette **afwisselende rij‑schaduw**‑patroon—lichtgeel op even rijen, wit op oneven rijen. Gebruikers kunnen het raster scannen zonder dat hun ogen heen en weer springen.

### Verwachte output
Als je het resulterende spreadsheet opent, zie je iets als dit:

| ID | Naam      | Hoeveelheid |
|----|-----------|-------------|
| **1** | Apple      | 50          |
| **2** | Banana     | 30          |
| **3** | Cherry     | 20          |
| **4** | Date       | 15          |

Rijen 1, 3, 5… hebben een **lichtgele achtergrond**, terwijl rijen 2, 4, 6… **wit** blijven. De header‑rij (rij 0) erft de standaardstijl tenzij je deze apart aanpast.

## Optionele variaties & randgevallen

### 1. Een ander kleurenpalet gebruiken
Als lichtgeel botst met je branding, vervang dan simpelweg `Color.LightYellow` door een andere `System.Drawing.Color`. Voor een blauw‑grijs thema kun je bijvoorbeeld gebruiken:

```csharp
rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
    ? Color.FromArgb(220, 235, 247) // soft blue
    : Color.White;
```

### 2. Dynamische schaduw op basis van data
Soms wil je rijen markeren die aan een voorwaarde voldoen (bijv. lage voorraad). Combineer de modulo‑controle met een aangepaste test:

```csharp
int quantity = Convert.ToInt32(dataTable.Rows[rowIndex]["Quantity"]);
if (quantity < 20)
{
    rowStyles[rowIndex].ForegroundColor = Color.Salmon; // urgent low‑stock color
}
else
{
    rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
        ? Color.LightYellow
        : Color.White;
}
```

### 3. Stijlen alleen op specifieke kolommen toepassen
Als je alleen de **rijachtergrondkleur instellen** op bepaalde kolommen nodig hebt, maak dan een aparte stijl voor elke kolom en wijs deze toe na de import via de cel‑bereik‑API van het werkblad.

```csharp
// Example for column B only
var colBStyle = wb.CreateStyle();
colBStyle.ForegroundColor = Color.LightYellow;
colBStyle.Pattern = BackgroundType.Solid;

// Apply after import
ws.Cells[$"B2:B{dataTable.Rows.Count + 1}"].SetStyle(colBStyle);
```

### 4. Prestatietip voor grote tabellen
Bij > 10.000 rijen, overweeg dan om één stijlobject per kleur te hergebruiken in plaats van elke rij een nieuw object te laten maken. De array bevat dan verwijzingen naar de twee gedeelde stijlen, wat het geheugenverbruik drastisch verlaagt.

```csharp
Style yellowStyle = wb.CreateStyle();
yellowStyle.ForegroundColor = Color.LightYellow;
yellowStyle.Pattern = BackgroundType.Solid;

Style whiteStyle = wb.CreateStyle();
whiteStyle.ForegroundColor = Color.White;
whiteStyle.Pattern = BackgroundType.Solid;

for (int i = 0; i < dataTable.Rows.Count; i++)
    rowStyles[i] = (i % 2 == 0) ? yellowStyle : whiteStyle;
```

## Volledig werkend voorbeeld

Hieronder staat een zelfstandige programma‑code die je in een console‑app kunt plakken. Het gebruikt een fictieve `Workbook`/`Worksheet` API; vervang de types door die van je gekozen bibliotheek.

```csharp
using System;
using System.Data;
using System.Drawing;          // For Color
using YourSpreadsheetLib;     // Replace with actual namespace

class Program
{
    static void Main()
    {
        // Initialize workbook & worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Step 1: Retrieve data
        DataTable dataTable = GetData();

        // Step 2: Allocate style array
        Style[] rowStyles = new Style[dataTable.Rows.Count];

        // Step 3: Apply alternating row colors
        for (int i = 0; i < dataTable.Rows.Count; i++)
        {
            rowStyles[i] = wb.CreateStyle();
            rowStyles[i].ForegroundColor = (i % 2 == 0)
                ? Color.LightYellow   // add light yellow background
                : Color.White;        // set row background color
            rowStyles[i].Pattern = BackgroundType.Solid; // set alternating row shading
        }

        // Step 4: Import with styles
        ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);

        // Save to file
        wb.Save("AlternatingRows.xlsx");
        Console.WriteLine("Workbook saved with alternating row colors.");
    }

    // Sample data generator
    static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("ID", typeof(int));
        dt.Columns.Add("Product", typeof(string));
        dt.Columns.Add("Quantity", typeof(int));

        dt.Rows.Add(1, "Apple", 50);
        dt.Rows.Add(2, "Banana", 30);
        dt.Rows.Add(3, "Cherry", 20);
        dt.Rows.Add(4, "Date", 15);
        dt.Rows.Add(5, "Elderberry", 5);
        return dt;
    }
}
```

**Output:** Een bestand genaamd `AlternatingRows.xlsx` waarin elke rij afwisselt tussen een lichtgele vulling en wit, waardoor de tabel makkelijker voor de ogen is.

## Veelgestelde vragen

**Q: Werkt deze aanpak met Excel‑style voorwaardelijke opmaak?**  
A: Ja. Als je bibliotheek voorwaardelijke regels ondersteunt, kun je dezelfde logica vertalen naar een regel die controleert `MOD(ROW(),2)=0`. De code‑gebaseerde methode die hier wordt getoond is draagbaarder over bibliotheken die geen ingebouwde voorwaardelijke opmaak hebben.

**Q: Wat als ik **rijen afwisselend kleuren** in een PDF‑tabel nodig heb in plaats van een Excel‑blad?**  
A: De meeste PDF‑tabelgeneratoren (bijv. iTextSharp, PdfSharp) laten je een `BackgroundColor` per rij instellen. Dezelfde modulo‑berekening is van toepassing—

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}