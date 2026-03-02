---
category: general
date: 2026-03-01
description: Importera data med formatering till Excel med C#. Lär dig hur du importerar
  en DataTable till Excel och lägger till bakgrundsfärg i celler på bara några steg.
draft: false
keywords:
- import data with formatting
- how to import datatable into excel
- add background color to excel cells
language: sv
og_description: Importera data med formatering till Excel med C#. Steg‑för‑steg‑guide
  som visar hur du importerar en DataTable och lägger till bakgrundsfärg i celler.
og_title: Importera data med formatering till Excel – C#‑guide
tags:
- C#
- Excel
- DataTable
- Formatting
title: Importera data med formatering till Excel med C#
url: /sv/net/excel-data-import-export/import-data-with-formatting-into-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Importera data med formatering till Excel med C#

Har du någonsin behövt **importera data med formatering** till en Excel-arbetsbok men bara fått ett enkelt, tråkigt blad? Du är inte ensam. De flesta utvecklare stöter på det när de upptäcker att standardimporten tar bort alla färger och stilar som de noggrant har satt upp i sina källdata.

I den här handledningen går vi igenom en komplett, färdig‑att‑köra lösning som **importerar en DataTable till Excel** och **lägger till bakgrundsfärg i Excel‑celler** samtidigt. Ingen extra efterbehandling behövs—ditt kalkylblad kommer att se exakt ut som du vill direkt ur lådan.

## Vad du kommer att lära dig

- Hur du hämtar data till en `DataTable`.
- Hur du definierar en array av `Style`‑objekt som bär bakgrundsfärger.
- Hur du anropar `ImportDataTable` med dessa stilar så att importen bevarar formatering.
- Ett komplett, körbart exempel som du kan klistra in i en konsolapp och se resultatet omedelbart.
- Tips, fallgropar och varianter för verkliga projekt.

### Förutsättningar

- .NET 6.0 eller senare (koden fungerar även med .NET Framework 4.6+).
- Biblioteket **GemBox.Spreadsheet** (den fria versionen räcker för demonstrationen).
- Grundläggande kunskap om C# och Excel‑koncept.

Om du undrar *varför GemBox?* så är det för att det erbjuder en enradig `ImportDataTable`‑metod som accepterar stil‑arrayer—precis vad vi behöver för att **importera data med formatering** utan att skriva en loop.

---

## Steg 1: Ställ in projektet och lägg till GemBox.Spreadsheet

För att komma igång, skapa en ny konsolapp:

```bash
dotnet new console -n ExcelImportDemo
cd ExcelImportDemo
dotnet add package GemBox.Spreadsheet
```

> **Pro tip:** Den fria versionen begränsar arbetsblad till 150 k celler, vilket är gott för demo. Om du når gränsen, uppgradera eller byt till EPPlus, men API:et kommer att se något annorlunda ut.

## Steg 2: Hämta källdata som en `DataTable`

Det första vi behöver är en `DataTable` som efterliknar den data du normalt skulle hämta från en databas. Här är en liten hjälpfunktion som skapar en i minnet:

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // Register the free license (remove for paid version).
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Retrieve the source data as a DataTable.
        DataTable dataTable = GetSampleData();

        // Remaining steps will follow...
    }

    /// <summary>
    /// Generates a sample DataTable with three columns and five rows.
    /// In a real app you’d replace this with a DB call.
    /// </summary>
    static DataTable GetSampleData()
    {
        var table = new DataTable("Report");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        table.Rows.Add(1, "Alice", 93.5);
        table.Rows.Add(2, "Bob", 78.0);
        table.Rows.Add(3, "Charlie", 85.2);
        table.Rows.Add(4, "Diana", 91.3);
        table.Rows.Add(5, "Ethan", 67.8);

        return table;
    }
}
```

**Varför detta är viktigt:** Genom att separera datahämtning i en egen metod kan du byta ut vilken källa som helst—SQL, CSV, webbtjänst—utan att röra importlogiken. Detta håller koden ren och gör handledningen **hur man importerar datatable till excel** återanvändbar.

## Steg 3: Definiera de stilar du vill tillämpa

Nu kommer den roliga delen: vi skapar en array av `Style`‑objekt, var och en med en distinkt `ForegroundColor`. GemBox låter dig sätta `BackgroundPatternColor` (cellens fyllning) och `ForegroundColor` (textfärgen). För den här demonstrationen färgar vi de två första kolumnerna olika.

```csharp
        // 2️⃣ Define the styles to apply to the imported cells.
        Style[] importStyles = new Style[]
        {
            new Style() { BackgroundPatternColor = Color.LightBlue },   // Column 0 – Light blue fill
            new Style() { BackgroundPatternColor = Color.LightGreen }   // Column 1 – Light green fill
            // No style for column 2 – it will keep the default look.
        };
```

**Förklaring:**  
- `Style`‑objekt är lätta behållare; du behöver inte skapa ett nytt för varje cell.  
- Genom att matcha ordningen på arrayen med kolumnordningen applicerar GemBox automatiskt rätt stil under import.  
- Detta är nyckeln till **importera data med formatering**—formateringen följer med data, inte i efterhand.

## Steg 4: Importera `DataTable` till arbetsbladet med stilar

När data och stilar är klara kan vi nu skapa en arbetsbok, välja det första arbetsbladet och anropa `ImportDataTable`. Metodsignaturen ser ut så här:

```csharp
public void ImportDataTable(
    DataTable dataTable,
    bool includeColumnNames,
    int startRow,
    int startColumn,
    Style[] columnStyles = null);
```

Här är hur vi använder den:

```csharp
        // 3️⃣ Create a new workbook and import the DataTable.
        var workbook = new ExcelFile();
        var worksheet = workbook.Worksheets.Add("Report");

        // Import, include column headers, start at A1 (0,0), apply our styles.
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);

        // Save the file to disk.
        workbook.Save("Report.xlsx");

        Console.WriteLine("Excel file 'Report.xlsx' created with formatted data.");
```

**Vad som händer under huven?**  
- `true` säger åt GemBox att skriva kolumnnamnen som den första raden.  
- `0, 0` placerar importen i cell A1.  
- `importStyles` kopplar varje kolumn till färgerna vi definierade tidigare.

När du öppnar *Report.xlsx* kommer du att se att **ID**‑kolumnen är skuggad ljusblå, **Name**‑kolumnen ljusgrön, och **Score**‑kolumnen förblir oförändrad. Det är **importera data med formatering** i ett enda anrop.

## Steg 5: Verifiera resultatet (förväntad output)

Öppna den genererade `Report.xlsx`. Du bör se något liknande detta:

| ID (light blue) | Name (light green) | Score |
|-----------------|--------------------|-------|
| 1               | Alice              | 93.5 |
| 2               | Bob                | 78.0 |
| 3               | Charlie            | 85.2 |
| 4               | Diana              | 91.3 |
| 5               | Ethan              | 67.8 |

- Cellerna i **ID**‑kolumnen har en ljusblå bakgrund.
- Cellerna i **Name**‑kolumnen har en ljusgrön bakgrund.
- **Score**‑kolumnen behåller standardvit bakgrund.

Den visuella ledtråden gör rapporten omedelbart skannbar—en liten detalj som kan förbättra användarupplevelsen avsevärt.

![Excel‑blad som visar import av data med formatering – ID‑kolumn ljusblå, Name‑kolumn ljusgrön](excel-screenshot.png "exempel på import av data med formatering")

*Bildens alt‑text innehåller huvudnyckelordet för SEO.*

## Vanliga frågor & edge‑cases

### Kan jag använda mer än bara bakgrundsfärger?

Absolut. `Style` låter dig sätta teckensnitt, kanter, talformat och till och med villkorlig formatering. Till exempel, för att göra poäng över 90 fetstil och röda:

```csharp
Style highScoreStyle = new Style()
{
    FontColor = Color.Red,
    FontBold = true
};
worksheet.Cells["C2:C6"].ConditionalFormatting.Add(
    ConditionalFormattingCondition.GreaterThan, "90", highScoreStyle);
```

### Vad händer om min DataTable har fler kolumner än stilar?

GemBox kommer endast att applicera stilar på de kolumner som har en motsvarande post i arrayen. Extra kolumner återgår till standardstilen—inget fel kastas.

### Fungerar detta med stora dataset?

Ja, men håll koll på den fria versionens cellgräns (150 k celler). För enorma rapporter, överväg den betalda licensen eller strömma data rad‑för‑rad med `worksheet.Cells[row, col].Value = …`—även om du förlorar enradslösningens bekvämlighet.

### Hur importerar jag data med formatering från en befintlig Excel‑mall?

Du kan ladda en mallarbetsbok först:

```csharp
var template = ExcelFile.Load("Template.xlsx");
var targetSheet = template.Worksheets[0];
targetSheet.Cells.ImportDataTable(dataTable, true, 5, 2, importStyles);
template.Save("FilledReport.xlsx");
```

Det låter dig bevara rubriklogotyper, sidfötter och eventuella befintliga stilar samtidigt som du **importerar data med formatering** för den dynamiska delen.

---

## Fullt fungerande exempel (Kopiera‑klistra redo)

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // Register free license key.
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Get the source data.
        DataTable dataTable = GetSampleData();

        // 2️⃣ Define column styles (background colors).
        Style[] importStyles = new Style[]
        {
            new Style() { BackgroundPatternColor = Color.LightBlue },   // ID column
            new Style() { BackgroundPatternColor = Color.LightGreen }   // Name column
            // Score column gets default style.
        };

        // 3️⃣ Create workbook and import with styles.
        var workbook = new ExcelFile();
        var worksheet = workbook.Worksheets.Add("Report");

        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);

        // Save the result.
        workbook.Save("Report.xlsx");

        Console.WriteLine("Report.xlsx created – import data with formatting complete.");
    }

    static DataTable GetSampleData()
    {
        var table = new DataTable("Report");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        table.Rows.Add(1, "Alice", 93.5);
        table.Rows.Add(2, "Bob", 78.0);
        table.Rows.Add(3, "Charlie", 85.2);
        table.Rows.Add(4, "Diana", 91.3);
        table.Rows.Add(5, "Ethan", 67.8);

        return table;
    }
}
```

Kör programmet (`dotnet run`) och öppna den genererade *Report.xlsx* för att se färgerna tillämpas omedelbart.

## Slutsats

Du har nu en solid, end

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}