---
category: general
date: 2026-04-07
description: Lägg till bakgrundsfärg på Excel‑rader med C#. Lär dig hur du applicerar
  alternerande radfärger, ställer in solida bakgrundsstilar och importerar en datatabell
  till Excel i ett enda arbetsflöde.
draft: false
keywords:
- add background color excel
- apply alternating row colors
- style excel rows
- set solid background
- import datatable to excel
language: sv
og_description: Lägg till bakgrundsfärg på Excel‑rader med C#. Denna guide visar hur
  du applicerar alternerande radfärger, sätter en solid bakgrund och importerar en
  datatabell till Excel på ett effektivt sätt.
og_title: Lägg till bakgrundsfärg i Excel – Växlande radstilar i C#
tags:
- C#
- Excel
- DataTable
- Styling
title: Lägg till bakgrundsfärg i Excel – alternerande radstilar i C#
url: /sv/net/excel-colors-and-background-settings/add-background-color-excel-alternating-row-styles-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lägg till bakgrundsfärg i Excel – Växlande radstilar i C#

Har du någonsin behövt **add background color excel** rader men var osäker på hur du gör det utan tusen rader krånglig kod? Du är inte ensam—de flesta utvecklare stöter på den muren när de första gången försöker få sina kalkylblad att se mer ut än bara en rå dataavläsning.  

Den goda nyheten? På bara några minuter kan du **apply alternating row colors**, sätta en **solid background**, och till och med **import datatable to excel** med ett rent, återanvändbart mönster i C#.  

I den här handledningen går vi igenom hela processen, från att hämta data till en `DataTable` till att styla varje rad med ett ljus‑gul‑vit randmönster. Inga externa bibliotek behövs förutom ett robust Excel‑hanteringspaket (som **ClosedXML** eller **GemBox.Spreadsheet**) och du kommer att se varför detta tillvägagångssätt är både prestandaeffektivt och lätt att underhålla.

## Vad du kommer att lära dig

- Hur du hämtar data och matar in den i ett Excel‑arbetsblad.
- Hur du **style excel rows** med växlande bakgrundsfärger.
- Mekanismerna bakom **set solid background** med `Style`‑objektet.
- Hur du **import datatable to excel** samtidigt som du bevarar radstilar.
- Tips för att hantera kantfall såsom tomma tabeller eller anpassade färgscheman.

> **Pro tip:** Om du redan använder ett arbetsbok‑objekt (`wb`) från ett bibliotek som stöder stilskapande, kan du återanvända samma `Style`‑instanser över flera arbetsblad—spara minne och håll din kod prydlig.

---

## Steg 1: Hämta data – Förbereda DataTable

Innan någon styling kan ske behöver vi en källa av rader. I de flesta verkliga scenarier kommer detta från en databas, ett API eller en CSV‑fil. För illustration skapar vi bara en enkel `DataTable` i minnet.

```csharp
using System;
using System.Data;
using System.Drawing;          // For Color
using GemBox.Spreadsheet;      // Or ClosedXML, whichever you prefer

// Simulated data fetch – replace with your own data access logic
DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    // Populate with sample rows
    for (int i = 1; i <= 10; i++)
        table.Rows.Add(i, $"Student {i}", Math.Round(new Random().NextDouble() * 100, 2));

    return table;
}
```

**Varför detta är viktigt:** Att använda en `DataTable` ger dig en tabellbaserad, schema‑medveten behållare som Excel‑biblioteket kan importera direkt, vilket eliminerar behovet av att skriva cell‑för‑cell‑loopar.

---

## Steg 2: Skapa radstilar – **Apply alternating row colors**

Nu bygger vi en array av `Style`‑objekt—ett per rad—så att varje rad kan få sin egen bakgrund. Mönstret vi använder är en klassisk ljus‑gul för jämna rader och vit för udda rader.

```csharp
// Assume 'wb' is an existing Workbook instance
Workbook wb = new Workbook();

// Retrieve data
DataTable dataTable = GetData();

// Allocate a style for each row
Style[] rowStyles = new Style[dataTable.Rows.Count];

for (int i = 0; i < rowStyles.Length; i++)
{
    // Create a fresh style instance
    rowStyles[i] = wb.CreateStyle();

    // Choose background colour based on row index
    rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.LightYellow : Color.White;

    // Ensure the colour is actually applied
    rowStyles[i].Pattern = BackgroundType.Solid;   // <-- **set solid background**
}
```

**Explanation:**  
- `wb.CreateStyle()` ger dig ett rent stilobjekt som du kan justera utan att påverka andra.  
- Ternära operatorn `(i % 2 == 0)` bestämmer om raden är jämn (ljusgul) eller udda (vit).  
- Att sätta `Pattern = BackgroundType.Solid` är det avgörande steget som **set solid background**; utan detta skulle färgen ignoreras.

---

## Steg 3: Hämta mål‑arbetsbladet

De flesta bibliotek exponerar en samling av arbetsblad. Vi arbetar med det första, men du kan rikta in dig på vilket index eller namn du föredrar.

```csharp
Worksheet worksheet = wb.Worksheets[0];   // First worksheet in the workbook
```

Om arbetsboken är helt ny skapar biblioteket vanligtvis ett standardblad åt dig. Annars kan du lägga till ett explicit:

```csharp
// Alternative: create a new sheet named "Report"
Worksheet worksheet = wb.Worksheets.Add("Report");
```

---

## Steg 4: Importera DataTable med radstilar – **Import datatable to excel**

Med stilarna klara är sista steget att föra in `DataTable` i bladet samtidigt som du applicerar motsvarande stil på varje rad.

```csharp
// Parameters: (DataTable, includeHeaders, startRow, startColumn, stylesArray)
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);
```

**Vad händer under huven?**  
- `true` talar om för metoden att skriva kolumnrubriker som den första raden.  
- `0, 0` markerar det övre vänstra hörnet (A1) som infogningspunkt.  
- `rowStyles` matchar varje `Style` med motsvarande datarad, vilket ger oss de växlande färgerna vi förberedde tidigare.

---

## Steg 5: Spara arbetsboken

Den sista pusselbiten är att spara arbetsboken till en fil så att du kan öppna den i Excel och se resultatet.

```csharp
// Choose a format – XLSX is the modern default
wb.Save("StudentScores.xlsx");

// Optional: open automatically (Windows only)
System.Diagnostics.Process.Start("StudentScores.xlsx");
```

Öppna filen så bör du se ett snyggt formaterat blad:

- Rubrikrad i fetstil (standardbibliotekets stil).  
- Rad 1, 3, 5… med en ren vit bakgrund.  
- Rad 2, 4, 6… med en subtil ljus‑gul fyllning, vilket gör det lätt att skanna.

### Förväntad utsnitt av resultatet

| Id | Name      | Score |
|----|-----------|-------|
| 1  | Student 1 | 78.45 |
| 2  | Student 2 | 62.13 |
| 3  | Student 3 | 91.27 |
| …  | …         | …     |

Rader 2, 4, 6, … visas med en ljus‑gul bakgrund—exakt den **apply alternating row colors**‑effekt vi siktade på.

![Exempel på att lägga till bakgrundsfärg i Excel](https://example.com/excel-background.png "Exempel på att lägga till bakgrundsfärg i Excel")

*(Alt‑texten innehåller huvudnyckelordet för SEO.)*

---

## Hantera kantfall & variationer

### Tom DataTable

Om `dataTable.Rows.Count` är noll, kommer `rowStyles`‑arrayen att vara tom och `ImportDataTable` kommer fortfarande att skriva rubrikraden (om `includeHeaders` är `true`). Inget undantag kastas, men du kanske vill skydda mot att generera en nästan tom fil:

```csharp
if (dataTable.Rows.Count == 0)
{
    Console.WriteLine("No data to export – workbook will contain only headers.");
}
```

### Anpassade färgscheman

Vill du ha ett blått/grått streck istället för gult/vitt? Byt bara ut `Color`‑värdena:

```csharp
rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.LightBlue : Color.LightGray;
```

Känn dig fri att hämta färger från en konfigurationsfil så att icke‑utvecklare kan justera paletten utan att röra koden.

### Återanvända stilar över flera arbetsblad

Om du exporterar flera tabeller till samma arbetsbok kan du generera stil‑arrayen en gång och återanvända den:

```csharp
Style[] sharedStyles = CreateAlternatingStyles(dataTable.Rows.Count);
worksheet1.Cells.ImportDataTable(dt1, true, 0, 0, sharedStyles);
worksheet2.Cells.ImportDataTable(dt2, true, 0, 0, sharedStyles);
```

Var bara försiktig så att båda tabellerna har samma radantal, eller generera en ny array per blad.

---

## Fullt fungerande exempel

När vi sätter ihop allt, här är ett självständigt program du kan kopiera‑klistra in i en konsolapp.

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;   // Install-Package GemBox.Spreadsheet

class Program
{
    static void Main()
    {
        // License free for small projects – remove for commercial use
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Retrieve data
        DataTable dataTable = GetData();

        // 2️⃣ Initialise workbook
        Workbook wb = new Workbook();

        // 3️⃣ Create alternating row styles
        Style[] rowStyles = CreateAlternatingStyles(dataTable.Rows.Count);

        // 4️⃣ Get (or create) the target worksheet
        Worksheet ws = wb.Worksheets.Add("Report");

        // 5️⃣ Import data with styles
        ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);

        // 6️⃣ Save the file
        wb.Save("Report.xlsx");
        Console.WriteLine("Excel file created – check Report.xlsx");
    }

    // Helper: generate a DataTable with sample data
    static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("Id", typeof(int));
        dt.Columns.Add("Name", typeof(string));
        dt.Columns.Add("Score", typeof(double));

        var rnd = new Random();
        for (int i = 1; i <= 12; i++)
            dt.Rows.Add(i, $"Student {i}", Math.Round(rnd.NextDouble() * 100, 2));

        return dt;
    }

    // Helper: create style array for alternating colors
    static Style[] CreateAlternatingStyles(int rowCount)
    {
        var wb = new Workbook();               // Temporary workbook for style creation
        var styles = new Style[rowCount];
        for (int i = 0; i < rowCount; i++)
        {
            styles[i] = wb.CreateStyle();
            styles[i].ForegroundColor = (i % 2 == 0) ? Color.LightYellow : Color.White;
            styles[i].Pattern = BackgroundType.Solid;   // **set solid background**
        }
        return styles;
    }
}
```

Kör programmet, öppna `Report.xlsx`, och du kommer att se den växlande bakgrunden exakt som beskrivet.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}