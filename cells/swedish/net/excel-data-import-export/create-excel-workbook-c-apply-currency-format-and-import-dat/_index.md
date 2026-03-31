---
category: general
date: 2026-03-30
description: Skapa Excel‑arbetsbok i C# med valutformat. Lär dig hur du importerar
  en DataTable, lägger till talformat i Excel och tillämpar valutformat på en kolumn
  på några minuter.
draft: false
keywords:
- create excel workbook c#
- format cells currency
- import datatable to excel
- add number format excel
- apply currency format column
language: sv
og_description: Skapa Excel‑arbetsbok i C# och formatera celler som valuta direkt.
  Denna steg‑för‑steg‑handledning visar hur du importerar en DataTable till Excel
  och lägger till talformat i Excel för en kolumn.
og_title: Skapa Excel‑arbetsbok i C# – Guide för valutformatering
tags:
- Aspose.Cells
- C#
- Excel automation
title: Skapa Excel-arbetsbok i C# – Använd valutaformat och importera DataTable
url: /sv/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa Excel‑arbetsbok C# – Tillämpa valutformat och importera DataTable

Har du någonsin behövt **create Excel workbook C#** som redan ser ut som en färdig rapport? Kanske hämtar du försäljningssiffror från en databas och vill att pris‑kolumnen ska visas i dollar utan att manuellt justera Excel. Känns igen? Du är inte ensam – de flesta utvecklare stöter på detta när de först automatiserar Excel‑export.

I den här guiden går vi igenom en komplett, färdig‑att‑köra lösning som **creates an Excel workbook C#**, importerar en `DataTable` och **formats the Price column as currency**. I slutet har du en fil som heter `StyledTable.xlsx` som du kan öppna och se snyggt formaterade tal. Ingen extra efterbehandling behövs.

> **Vad du kommer att lära dig**
> - Hur du sätter upp Aspose.Cells i ett .NET‑projekt  
> - Hur du **import datatable to excel** med en stil‑array  
> - Hur du **add number format excel** för en specifik kolumn  
> - Tips för att hantera fler kolumner eller olika lokaler  

> **Förutsättningar**  
> - .NET 6+ (eller .NET Framework 4.6+) installerat  
> - Aspose.Cells for .NET NuGet‑paket (`Install-Package Aspose.Cells`)  
> - Grundläggande kunskap om C# och DataTables  

---

## Steg 1: Förbered DataTable (import datatable to excel)

Först behöver vi lite exempeldata. I en riktig applikation skulle du troligen fylla tabellen från en DB‑fråga, men ett hårdkodat exempel håller det enkelt.

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

*Varför detta är viktigt*: `DataTable` är bron mellan dina affärsdata och Excel‑filen. Aspose.Cells kan importera den direkt och bevara kolumnnamn och datatyper.

---

## Steg 2: Skapa en ny arbetsbok (create excel workbook c#)

Nu skapar vi själva Excel‑filobjektet. Tänk på det som en tom duk du ska måla på.

```csharp
using Aspose.Cells;

// Instantiate a fresh workbook – this is the core of create excel workbook c#
Workbook workbook = new Workbook();

// Grab the first worksheet (index 0). You could also add more sheets later.
Worksheet worksheet = workbook.Worksheets[0];
```

> **Pro tip:** Om du behöver flera blad, anropa `workbook.Worksheets.Add()` och ge varje ett meningsfullt namn.

---

## Steg 3: Definiera ett valutastil (format cells currency)

Aspose.Cells låter dig skapa ett `Style`‑objekt som beskriver hur celler ska se ut. För valuta använder vi det inbyggda talformat‑ID‑et 164 (`"$#,##0.00"`).

```csharp
// Create a new style object for the price column
Style priceStyle = workbook.CreateStyle();
priceStyle.Number = 164; // Built‑in currency format "$#,##0.00"
```

*Varför inte bara sätta formatsträngen?* Att använda det inbyggda ID‑et säkerställer kompatibilitet över Excel‑versioner och undviker lokalspecifika egenheter.

---

## Steg 4: Bygg stil‑arrayen (apply currency format column)

När du importerar en `DataTable` kan du skicka en array av `Style`‑objekt – ett per kolumn. `null` betyder “använd standardstilen”. Här applicerar vi `priceStyle` endast på den andra kolumnen.

```csharp
// Column 0 (Product) gets the default style, Column 1 (Price) gets the currency style
Style[] columnStyles = { null, priceStyle };
```

Om du senare lägger till fler kolumner, utöka bara arrayen därefter. Längden på `columnStyles` måste matcha antalet kolumner du importerar, annars kastar Aspose ett undantag.

---

## Steg 5: Importera DataTable med stilar (import datatable to excel)

Nu händer magin – vår `DataTable` landar i kalkylbladet, och pris‑kolumnen visas omedelbart som valuta.

```csharp
// Parameters:
//  - dataTable: source data
//  - true: include column headers
//  - startRow: 0 (top of sheet)
//  - startColumn: 0 (first column)
//  - columnStyles: style array defined above
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

*Vad händer om du har fler än två kolumner?* Utöka bara `columnStyles` så att varje kolumn får rätt stil (eller `null` för standard). Detta är det renaste sättet att **add number format excel** selektivt.

---

## Steg 6: Spara arbetsboken (create excel workbook c#)

Till sist skriver vi filen till disk. Välj någon mapp du har skrivbehörighet till.

```csharp
// Save the workbook as an XLSX file
workbook.Save("YOUR_DIRECTORY/StyledTable.xlsx");
```

Öppna `StyledTable.xlsx` i Excel så bör du se:

| Produkt | Pris |
|---------|------|
| Apple   | $1.23 |
| Banana  | $0.78 |
| Cherry  | $2.50 |

**Price**‑kolumnen är redan formaterad som valuta – inga extra steg behövs.

---

## Edge Cases & Variations

### Fler kolumner, olika format

Om du behöver **format cells currency** för flera kolumner (t.ex. Cost, Tax, Total), skapa ett separat `Style` för varje och fyll `columnStyles` därefter:

```csharp
Style costStyle = workbook.CreateStyle();
costStyle.Number = 164; // currency

Style taxStyle = workbook.CreateStyle();
taxStyle.Number = 164;

// Assuming columns: Product, Cost, Tax, Total
Style[] styles = { null, costStyle, taxStyle, priceStyle };
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, styles);
```

### Lokalspecifik valuta

För Euro eller brittiskt pund, använd andra inbyggda ID:n (t.ex. 165 för `€#,##0.00`). Alternativt kan du sätta en anpassad formatsträng:

```csharp
priceStyle.Custom = "€#,##0.00";
```

### Stora datamängder

Aspose.Cells kan hantera miljoner rader, men minnesanvändningen växer med stil‑objekt. Återanvänd ett enda `Style`‑instans för alla valutakolumner för att hålla fotavtrycket lågt.

### Saknade stilar

Om `columnStyles` är kortare än antalet kolumner, kommer Aspose att applicera standardstilen på de återstående kolumnerna. Detta är praktiskt när du bara bryr dig om några få kolumner.

---

## Fullt fungerande exempel (Alla steg kombinerade)

Nedan är det kompletta programmet som du kan kopiera‑klistra in i en konsolapp. Det innehåller alla delar vi diskuterat, plus några hjälpsamma kommentarer.

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

**Förväntat resultat:** När du öppnar `StyledTable.xlsx` visas `Price`‑kolumnen med dollartecken och två decimaler, exakt som instruktionen **format cells currency** krävde.

---

## Vanliga frågor

**Q: Fungerar detta med .NET Core?**  
A: Absolut. Aspose.Cells är .NET‑standard kompatibel, så du kan rikta mot .NET 5, .NET 6 eller senare utan ändringar.

**Q: Vad händer om min DataTable har 10 kolumner men jag bara vill formatera kolumn 5?**  
A: Skapa en `Style[]` med längd 10, fyll positionerna 0‑4 och 6‑9 med `null`, och placera din anpassade stil på index 4 (nollbaserat). Aspose respekterar varje post.

**Q: Kan jag dölja rubrikraden?**  
A: Efter import, sätt `worksheet.Cells.Rows[0].Hidden = true;` eller skicka `false` för parametern `includeColumnNames` i `ImportDataTable`.

---

## Slutsats

Vi har just **created an Excel workbook C#**, importerat en `DataTable` och **applied a currency format column** med Aspose.Cells. De primära stegen – förbereda data, definiera en stil, bygga en stil‑array, importera med `ImportDataTable` och spara – täcker kärnan i de flesta Excel‑automatiseringsuppgifter.

Från här kan du utforska:

- **add number format excel** för datum eller procenttal  
- Exportera flera kalkylblad i en enda fil  
- Använda **format cells currency** med lokalspecifika symboler  
- Automatisera diagramskapande baserat på samma data  

Prova dessa och du blir snabbt go‑to‑personen för Excel‑rapportering i ditt team. Har du ett eget knep du vill dela? Lägg en kommentar nedan – happy coding!  

![skapa excel arbetsbok c# skärmbild](image.png "skapa excel arbetsbok c#")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}