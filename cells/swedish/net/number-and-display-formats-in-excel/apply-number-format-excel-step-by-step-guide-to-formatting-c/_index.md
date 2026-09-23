---
category: general
date: 2026-02-26
description: Applicera talformat i Excel snabbt och lär dig hur du formaterar en kolumn
  som valuta, sätter kolumnens talformat och ändrar kolumnens teckensnittsfärg med
  bara några rader C#.
draft: false
keywords:
- apply number format excel
- format column as currency
- set column number format
- format currency column
- set column font color
language: sv
og_description: tillämpa talformat i Excel med C# i enkla steg. Lär dig att formatera
  kolumn som valuta, ange kolumnens talformat och sätt kolumnens teckensnittsfärg
  för professionella kalkylblad.
og_title: Tillämpa talformat i Excel – Komplett guide till kolumnformatering
tags:
- C#
- Excel
- Aspose.Cells
- DataTable
- Styling
title: Applicera talformat i Excel – Steg‑för‑steg guide för att formatera kolumner
url: /sv/net/number-and-display-formats-in-excel/apply-number-format-excel-step-by-step-guide-to-formatting-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# apply number format excel – Hur man formaterar Excel-kolumner i C#

Har du någonsin undrat hur man **apply number format excel** medan du redan loopar igenom en `DataTable`? Du är inte ensam. De flesta utvecklare stöter på problem när de behöver ett blått teckensnitt i rubriken *och* en valuta‑formaterad kolumn i samma importoperation. Den goda nyheten? Med några rader C# och rätt stil‑objekt kan du göra det utan efterbearbetning av bladet.

I den här handledningen går vi igenom ett komplett, körbart exempel som visar hur du **format column as currency**, **set column number format** för någon annan kolumn, och till och med **set column font color** för rubriker. I slutet har du ett återanvändbart mönster som du kan släppa in i vilket Aspose.Cells‑projekt (eller liknande) som helst.

## Vad du kommer att lära dig

- Hur du hämtar en `DataTable` och mappar varje kolumn till en specifik `Style`.
- De exakta stegen för att **apply number format excel** med `Worksheet.Cells.ImportDataTable`.
- Varför det är mer effektivt att skapa stilar i förväg än att formatera celler en efter en.
- Hantering av edge‑case när källtabellen har fler kolumner än du har stylat.
- Ett komplett, kopiera‑och‑klistra‑klart kodexempel som du kan köra idag.

> **Förutsättning:** Denna guide förutsätter att du har Aspose.Cells för .NET (eller något bibliotek som exponerar `Workbook`, `Worksheet`, `Style`‑API:er) refererat i ditt projekt. Om du använder ett annat bibliotek översätts koncepten direkt—byt bara ut typnamnen.

## Steg 1: Hämta källdata som en DataTable

Innan någon formatering kan ske behöver du rådata. I de flesta verkliga scenarier lagras data i en databas, CSV eller ett API. För tydlighetens skull kommer vi att mocka en enkel `DataTable` med två kolumner: *Product* (string) och *Price* (decimal).

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

> **Varför detta är viktigt:** Att hämta data till en `DataTable` ger dig en tabellbaserad, minnesrepresentation som `ImportDataTable` kan konsumera direkt, vilket eliminerar behovet av manuell cell‑för‑cell‑insättning.

## Steg 2: Skapa en array av Styles – en per kolumn

`ImportDataTable`‑överladdningen vi kommer att använda accepterar en array av `Style`‑objekt. Varje post motsvarar ett kolumnindex. Om du lämnar en post som `null` ärver kolumnen standardstilen för arbetsboken.

```csharp
// Initialize the workbook (Aspose.Cells)
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Prepare the style array based on the number of columns
DataTable dataTable = GetData();
Style[] columnStyles = new Style[dataTable.Columns.Count];
```

> **Proffstips:** Att deklarera arrayen *efter* att du har `DataTable` säkerställer att storleken matchar exakt, vilket förhindrar `IndexOutOfRangeException` senare.

## Steg 3: Ställ in kolumnens teckensnittsfärg (blå) för den första kolumnen

En vanlig begäran är att markera rubrik‑ eller nyckelkolumner med en tydlig teckensnittsfärg. Här gör vi den första kolumnens text blå.

```csharp
// Style for the first column – blue font
columnStyles[0] = workbook.CreateStyle();
columnStyles[0].Font.Color = Color.Blue;
```

> **Varför använda ett style‑objekt?** Stilar är återanvändbara och appliceras i bulk, vilket är mycket snabbare än att iterera över varje cell efter import. Arbetsboken cachar stilen en gång och återanvänder den för varje cell i den kolumnen.

## Steg 4: Formatera den andra kolumnen som valuta

Excels inbyggda talformat identifieras med ett index. `14` motsvarar standardvalutaformatet (t.ex. `$1,234.00`). Om du behöver ett anpassat format kan du istället tilldela en formatsträng.

```csharp
// Style for the second column – built‑in currency format (ID 14)
columnStyles[1] = workbook.CreateStyle();
columnStyles[1].Number = 14; // 14 = built‑in currency format
```

> **Edge case:** Om din arbetsbok använder en lokal där valutasymbolen inte är `$`, anpassas samma index automatiskt (t.ex. `€` för tyska lokaler).

## Steg 5: Importera DataTable med de definierade stilarna

Nu sätter vi ihop allt. Metoden `ImportDataTable` kommer att klistra in data med start i cell `A1` (rad 0, kolumn 0) och applicera de stilar vi förberett.

```csharp
// Import the DataTable into the worksheet, applying the column styles
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

- Den andra parametern `true` talar om för Aspose.Cells att behandla den första raden i `DataTable` som kolumnrubriker.
- `0, 0`‑koordinaterna specificerar det övre vänstra hörnet där importen börjar.
- `columnStyles` mappar varje kolumn till dess respektive stil.

## Steg 6: Spara arbetsboken (valfritt, men praktiskt för verifiering)

Om du vill se resultatet i Excel, spara bara arbetsboken till disk. Detta steg krävs inte för formateringslogiken, men det är användbart för felsökning.

```csharp
// Save the workbook to a file
workbook.Save("StyledReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Workbook saved as StyledReport.xlsx");
```

### Förväntat resultat

| **Produkt** (blått teckensnitt) | **Pris** (valuta) |
|--------------------------|----------------------|
| Apple                    | $1.25                |
| Banana                   | $0.75                |
| Cherry                   | $2.10                |

- Kolumnen *Produkt* visas i blått, vilket får den att sticka ut.
- Kolumnen *Pris* visar värden med standardvalutasymbolen och två decimaler.

## Vanliga frågor & variationer

### Hur ställer jag in **set column number format** för fler än två kolumner?

Utöka bara `columnStyles`‑arrayen. Till exempel, för att visa en procentsats i den tredje kolumnen:

```csharp
columnStyles[2] = workbook.CreateStyle();
columnStyles[2].Number = 10; // 10 = built‑in percentage format
```

### Vad händer om jag behöver ett *anpassat* valutaformat, som “USD 1,234.00”?

Byt ut `Number`‑egenskapen mot en formatsträng:

```csharp
columnStyles[1].Custom = "\"USD\" #,##0.00";
```

### Kan jag applicera en **set column font color** på en numerisk kolumn utan att påverka dess talformat?

Absolut. Stilar är sammansättningsbara. Du kan sätta både `Font.Color` och `Number` på samma `Style`‑instans:

```csharp
columnStyles[3] = workbook.CreateStyle();
columnStyles[3].Font.Color = Color.Green;
columnStyles[3].Number = 2; // 2 = built‑in date format (just an example)
```

### Vad händer om `DataTable` har fler kolumner än stilar?

Alla kolumner utan en explicit stil (`null`‑post) ärver arbetsbokens standardstil. För att undvika oavsiktliga `null`‑värden kan du först initiera hela arrayen med en basstil:

```csharp
Style defaultStyle = workbook.CreateStyle();
defaultStyle.Font.Size = 11;
for (int i = 0; i < columnStyles.Length; i++)
    columnStyles[i] = defaultStyle;
```

Överskriv sedan bara de kolumner du bryr dig om.

### Fungerar detta tillvägagångssätt med stora datamängder (10 000+ rader)?

Ja. Eftersom formateringen appliceras *en gång per kolumn* före importen förblir operationen O(N) med avseende på rader, och minnesanvändningen hålls låg. Undvik att loopa över varje cell efter import – det är där prestandan försämras.

## Fullt fungerande exempel (Kopiera‑klistra‑klart)

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

Kör programmet, öppna `StyledReport.xlsx`, och du kommer omedelbart att se resultatet av **apply number format excel**.

## Slutsats

Vi har just demonstrerat ett rent, effektivt sätt att **apply number format excel** på en importerad `DataTable`. Genom att förbereda en `Style[]`‑array i förväg kan du **format column as currency**, **set column number format** och **set column font color** i ett enda anrop – ingen efterbearbetning behövs.

Känn dig fri att utöka mönstret: lägg till villkorad formatering, slå ihop celler för rubriker eller till och med injicera formler. Samma principer gäller, vilket håller din kod snygg och dina kalkylblad professionella.

### Vad blir nästa?

- Utforska **conditional formatting** för att markera värden som överstiger ett tröskelvärde.
- Kombinera denna teknik med **pivot table generation** för dynamisk rapportering.
- Prova **set column number format** för datum, procentsatser eller anpassad vetenskaplig notation.

Got a twist you tried? Share it in the comments—let’s keep the

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}