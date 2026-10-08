---
category: general
date: 2026-03-18
description: Lär dig hur du tillämpar alternerande radfärger i ett kalkylblad med
  C#. Inkluderar att sätta radens bakgrundsfärg, lägga till ljusgul bakgrund och färga
  raderna alternerande.
draft: false
keywords:
- apply alternating row colors
- set row background color
- add light yellow background
- set alternating row shading
- color rows alternately
language: sv
og_description: Använd alternerande radfärger i C# för att förbättra läsbarheten.
  Denna guide visar hur du sätter radens bakgrundsfärg, lägger till ljusgul bakgrund
  och färgar raderna alternerande.
og_title: Applicera alternerande radfärger i C# – Komplett handledning
tags:
- C#
- DataTable
- Spreadsheet styling
- UI design
title: Applicera alternerande radfärger i C# – Steg‑för‑steg‑guide
url: /sv/net/excel-colors-and-background-settings/apply-alternating-row-colors-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Applicera alternerande radfärger i C# – Komplett handledning

Har du någonsin behövt **apply alternating row colors** till ett data‑drivet kalkylblad men var osäker på var du ska börja? Du är inte ensam — de flesta utvecklare stöter på det problemet när de första gången försöker göra tabeller lite mer vänliga. Den goda nyheten? På bara några rader C# kan du **set row background color**, lägga till en **add light yellow background**, och få ett polerat rutnät som omedelbart förbättrar läsbarheten.

I den här handledningen går vi igenom hela processen, från att hämta en `DataTable` till minnet till att styla varje rad med ett subtilt gult‑vitt streck. I slutet kommer du att kunna **color rows alternately** med självförtroende, och du kommer också att se några praktiska varianter för när du behöver olika nyanser eller dynamisk tematisering.

## Vad du behöver

- Ett .NET‑projekt som riktar sig mot .NET 6 eller senare (koden fungerar även på .NET Framework 4.7+).  
- Ett kalkylbladsbibliotek som stöder stilobjekt – exemplet använder ett generiskt `Workbook`/`Worksheet`‑API som speglar bibliotek som **Aspose.Cells**, **GemBox.Spreadsheet**, eller **ClosedXML**.  
- En `DataTable`‑källa – kan komma från en databasfråga, CSV‑import eller någon in‑memory‑samling.  

Inga extra NuGet‑paket behövs utöver själva kalkylbladsbiblioteket. Om du använder Aspose.Cells är namnrymden `Aspose.Cells`; för ClosedXML är den `ClosedXML.Excel`. Byt ut anropen `CreateStyle` och `ImportDataTable` därefter.

## Steg 1: Hämta källdata som en DataTable

Först och främst—hämta de data du vill visa. I verkliga appar betyder det vanligtvis att slå mot en databas, men för tydlighetens skull kommer vi att stubba en hjälpfunktion som heter `GetData()` och som returnerar en fylld `DataTable`.

```csharp
// Step 1: Retrieve the source data as a DataTable
DataTable dataTable = GetData();   // Replace with your actual data retrieval logic
```

> **Varför detta är viktigt:** `DataTable` definierar raderna och kolumnerna som senare får den alternerande skuggningen. Om tabellen är tom finns det inget att styla, så verifiera alltid att `Rows.Count` > 0 innan du fortsätter.

### Proffstips
Om du hämtar data från Entity Framework kan du använda `DataTable.Load(reader)` efter att ha kört ett `SqlCommand`. Det håller koden prydlig och undviker manuella kolumndefinitioner.

## Steg 2: Allokera en array för att hålla en stil för varje rad

Nästa steg, vi behöver en behållare som matchar antalet rader. De flesta kalkylblads‑API:er låter dig skicka en stilarray till importmetoden, så vi skapar en `Style[]` med exakt storlek för radantalet.

```csharp
// Step 2: Allocate an array to hold a style for each row
Style[] rowStyles = new Style[dataTable.Rows.Count];
```

> **Förklaring:** Genom att förallokera arrayen undviker vi att allokera ett nytt stilobjekt på varje iteration, vilket kan ge en prestandafördel när man hanterar tusentals rader.

## Steg 3: Applicera alternerande radfärger (ljusgul / vit)

Nu kommer kärnan i saken: **apply alternating row colors**. Vi loopar igenom varje rad, skapar en ny stilinstans från arbetsboken och sätter dess bakgrund baserat på radindexet. Jämna rader får en ljusgul fyllning, udda rader förblir vita.

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

### Varför detta fungerar
- **`rowIndex % 2 == 0`** kontrollerar om raden är jämn.  
- **`Color.LightYellow`** ger en mjuk, icke‑intrusiv nyans som är perfekt för datatabeller.  
- **`BackgroundType.Solid`** säkerställer att fyllningen täcker hela cellen, vilket ger **set row background color**‑effekten.  

Du kan byta `Color.LightYellow` mot någon annan nyans (t.ex. `Color.LightCyan`) om du föredrar ett annat utseende. Samma logik låter dig också **color rows alternately** baserat på andra kriterier, såsom statusflaggor.

## Steg 4: Importera DataTable till arbetsbladet med de förberedda stilarna

Till sist lägger vi in allt i arbetsbladet. De flesta bibliotek exponerar en `ImportDataTable`‑överladdning som accepterar en stilarray. Flaggan `true` talar om för API:et att skriva kolumnrubriker, och koordinaterna `0, 0` startar i den övre‑vänstra cellen.

```csharp
// Step 4: Import the DataTable into the worksheet, applying the prepared row styles
ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);
```

> **Resultat:** Arbetsbladet visar nu dina data med ett rent **alternating row shading**‑mönster—ljusgul på jämna rader, vit på udda rader. Användare kan skanna rutnätet utan att ögonen hoppar fram och tillbaka.

### Förväntat resultat
Om du öppnade den resulterande kalkylbladet skulle du se något liknande detta:

| ID | Name      | Quantity |
|----|-----------|----------|
| **1** | Apple      | 50       |
| **2** | Banana     | 30       |
| **3** | Cherry     | 20       |
| **4** | Date       | 15       |

Rader 1, 3, 5… har en **light yellow background**, medan rader 2, 4, 6… förblir **white**. Rubrikraden (rad 0) ärver standardstilen om du inte anpassar den separat.

## Valfria varianter & kantfall

### 1. Använda en annan färgpalett
Om ljusgul krockar med ditt varumärke, ersätt helt enkelt `Color.LightYellow` med en annan `System.Drawing.Color`. För ett blå‑grått tema kan du använda:

```csharp
rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
    ? Color.FromArgb(220, 235, 247) // soft blue
    : Color.White;
```

### 2. Dynamisk skuggning baserad på data
Ibland vill du markera rader som uppfyller ett villkor (t.ex. låg lager). Kombinera modulo‑kontrollen med ett anpassat test:

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

### 3. Applicera stilar endast på specifika kolumner
Om du bara behöver **set row background color** på vissa kolumner, skapa en separat stil för varje kolumn och tilldela den efter importen med hjälp av arbetsbladets cellintervall‑API.

```csharp
// Example for column B only
var colBStyle = wb.CreateStyle();
colBStyle.ForegroundColor = Color.LightYellow;
colBStyle.Pattern = BackgroundType.Solid;

// Apply after import
ws.Cells[$"B2:B{dataTable.Rows.Count + 1}"].SetStyle(colBStyle);
```

### 4. Prestandatips för stora tabeller
När du hanterar > 10 000 rader, överväg att återanvända ett enda stilobjekt för varje färg istället för att skapa ett nytt per rad. Arrayen innehåller då referenser till de två delade stilarna, vilket kraftigt minskar minnesanvändningen.

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

## Fullt fungerande exempel

Nedan är ett självständigt program som du kan klistra in i en konsolapp. Det använder ett fiktivt `Workbook`/`Worksheet`‑API; ersätt typerna med de från ditt valda bibliotek.

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

**Output:** En fil med namnet `AlternatingRows.xlsx` där varje rad alternerar mellan en ljusgul fyllning och vit, vilket gör tabellen skonsammare för ögonen.

## Vanliga frågor

**Q: Fungerar detta tillvägagångssätt med Excel‑liknande villkorsformatering?**  
A: Ja. Om ditt bibliotek stöder villkorsregler kan du översätta samma logik till en regel som kontrollerar `MOD(ROW(),2)=0`. Den kodbaserade metoden som visas här är mer portabel över bibliotek som saknar inbyggd villkorsformatering.

**Q: Vad händer om jag behöver **color rows alternately** i en PDF‑tabell istället för ett Excel‑ark?**  
A: De flesta PDF‑tabellgeneratorer (t.ex. iTextSharp, PdfSharp) låter dig sätta en `BackgroundColor` per rad. Samma modulo‑beräkning gäller—

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}