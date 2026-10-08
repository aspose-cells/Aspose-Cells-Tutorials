---
category: general
date: 2026-06-05
description: Applicera cellstilar när du använder Aspose.Cells‑import. Lär dig hur
  du importerar DataTable med formatering, formaterar rader och håller kalkylbladen
  organiserade.
draft: false
keywords:
- apply cell styles
- aspose cells import
- import with formatting
- how to import datatable
- import datatable worksheet
language: sv
og_description: Applicera cellstilar när du importerar en DataTable till ett Aspose.Cells‑arkblad.
  Steg‑för‑steg‑guide med fullständig kod och tips.
og_title: Tillämpa cellstilar med Aspose.Cells – Importera DataTable
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
title: Applicera cellstilar med Aspose.Cells – Importera DataTable med formatering
url: /sv/net/excel-formatting-and-styling/apply-cell-styles-with-aspose-cells-import-datatable-with-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Applicera cellstilar med Aspose.Cells – Importera DataTable med formatering

Har du någonsin undrat hur du **applikerar cellstilar** när du hämtar en `DataTable` till ett Excel‑blad? Du är inte ensam. I många rapporteringsscenarier vill du att data ska se bra ut direkt – utan manuell formatering i efterhand. Den goda nyheten är att Aspose.Cells gör det enkelt att **importera med formatering** så att dina rader kan vara röda eller blå, fetstilta eller vad du än önskar.

I den här handledningen går vi igenom ett komplett, körbart exempel som visar **hur du importerar en datatable** till ett arbetsblad **med cellstilar** applicerade. I slutet har du en färdig C#‑konsolapp som skapar en arbetsbok, formaterar de två första kolumnerna och sparar filen – allt med `aspose cells import`‑API:t.

## Vad du kommer att lära dig

- Konfigurera Aspose.Cells i ett .NET‑projekt  
- Bygga en exempel‑`DataTable` som efterliknar verklig data  
- Definiera `Style`‑objekt för röd och blå teckensnitt  
- Använda `Worksheet.Cells.ImportDataTable` för att **importera datatable till arbetsblad** samtidigt som stilarna appliceras  
- Verifiera resultatet och spara arbetsboken  

Ingen extern verktygslåda, bara ren C# och Aspose.Cells. Låt oss sätta igång.

---

## Förutsättningar

Innan vi dyker ner i koden, se till att du har följande:

| Krav | Varför det är viktigt |
|------|-----------------------|
| .NET 6.0 eller senare | Aspose.Cells 23.x riktar sig mot .NET Standard 2.0+, så .NET 6 ger dig de senaste runtime‑funktionerna. |
| Aspose.Cells för .NET (NuGet) | Biblioteket tillhandahåller `Workbook`, `Worksheet`, `Style` och `ImportDataTable`‑metoderna vi behöver. |
| Grundläggande kunskaper i C# | Du bör förstå klasser, arrayer och `using`‑satser. |
| En IDE (Visual Studio, VS Code, Rider) | Vilken editor som helst fungerar, men du måste återställa NuGet‑paket. |

Du kan installera paketet från kommandoraden:

```bash
dotnet add package Aspose.Cells
```

---

## Steg 1: Skapa en ny arbetsbok och hämta det första arbetsbladet

Först och främst – låt oss skapa ett `Workbook` och ta det första bladet. Tänk på arbetsboken som en tom anteckningsbok; det första arbetsbladet är sidan vi ska skriva på.

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

> **Proffstips:** Om du någonsin behöver flera blad, lägg bara till dem med `wb.Worksheets.Add()` och referera dem med namn eller index.

---

## Steg 2: Förbered en exempel‑DataTable (Hur man importerar DataTable)

Nu behöver vi något att importera. I riktiga projekt skulle du anropa en databas, men för tydlighetens skull bygger vi en `DataTable` i minnet.

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

> **Varför detta är viktigt:** En `DataTable` låter oss testa **aspose cells import**‑flödet utan externa beroenden.

---

## Steg 3: Definiera stilarna som ska appliceras på de importerade cellerna

Här sker magin. Vi skapar två `Style`‑objekt: ett med röd teckensnitt, ett med blått teckensnitt. Dessa kommer att appliceras kolumnvis under importen.

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

> **Observera:** Längden på `importStyles` måste matcha antalet kolumner du importerar, annars kastar Aspose ett `ArgumentException`.

---

## Steg 4: Importera DataTable till arbetsbladet **med formatering**

Nu sätter vi ihop allt. Överlagringen av `ImportDataTable` vi använder accepterar `Style[]`‑arrayen, så vi kan **applikerar cellstilar** när data skrivs in i bladet.

```csharp
        // Import the DataTable starting at cell A1 (row 0, column 0)
        // The 'true' flag tells Aspose to generate column headers automatically
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);
```

### Så här fungerar det

1. **Rubriker** – Eftersom vi skickade `true` skriver Aspose “Name” och “Score” i den första raden.  
2. **Datarrader** – Varje efterföljande rad får den motsvarande stilen från `importStyles`.  
3. **Prestanda** – Metoden strömmar data direkt till arbetsbladet, vilket är snabbare än att loopa cell för cell.

---

## Steg 5: Verifiera resultatet och spara arbetsboken

Låt oss titta på de första cellerna för att försäkra oss om att stilarna har satts, och sedan skriva filen till disk.

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

När du öppnar **StyledImport.xlsx** kommer du att se:

- “Name”-kolumnen i **röd** text.  
- “Score”-kolumnen i **blå** text.  
- Kolumnrubrikerna i standardstil (du kan också styla dem, men det är ett annat exempel).

![Applicera cellstilar exempel](https://example.com/images/apply-cell-styles.png "Applicera cellstilar i Aspose.Cells")

> **Obs:** Bilden ovan visar det slutgiltiga utseendet. `alt`‑attributet innehåller huvudnyckelordet, vilket uppfyller SEO‑kraven.

---

## Vanliga frågor & kantfall

### Vad händer om min DataTable har fler kolumner än stilar?

Aspose kommer att använda den sista stilen i arrayen för eventuella extra kolumner. För att undvika oväntade färger, se till att arrayens längd matchar antalet kolumner, eller skicka `null` för kolumner du inte vill formatera.

### Kan jag applicera olika stilar på specifika rader?

Absolut. Efter importen kan du loopa igenom rader och tilldela nya `Style`‑objekt baserat på villkor (t.ex. markera poäng > 90 i grönt). Här är ett kort kodexempel:

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

### Fungerar detta med stora dataset?

Ja. `ImportDataTable` strömmar data effektivt, och att använda en statisk stilarray ger obetydlig extra belastning. För miljontals rader kan du överväga att importera i omgångar eller använda `Cells.ImportDataTable` med en `DataReader` för ännu bättre minneshantering.

### Hur bevarar jag befintlig formatering i arbetsbladet?

Om målområdet redan har formatering du vill behålla, ange `importOptions`‑parametern (`ImportTableOptions`) i `ImportDataTable`‑överlagringen och justera `ImportDataTableOptions.PreserveCellFormatting`. Standardbeteendet skriver över stilar med de du anger.

---

## Sammanfattning: Vad vi har åstadkommit

- **Applikerat cellstilar** under en **aspose cells import**‑operation.  
- Visat **import med formatering** genom att skicka en `Style[]`‑array.  
- Demonstrerat **hur man importerar en datatable** till ett arbetsblad och sparar resultatet.  
- Täckt kantfall som missmatchade stilantal och villkorlig radformatering.

Allt detta gjordes i en enda, självständig konsolapp – utan externa skript, utan manuellt Excel‑arbete. Du har nu en solid grund för alla rapporterings‑ eller data‑exportfunktioner som kräver snygg Excel‑utmatning.

---

## Nästa steg

Redo att ta det ett steg längre? Här är några idéer som bygger på det du just lärt dig:

- **Formatera rubrikraden** (t.ex. fetstil, bakgrundsfärg).  
- **Applicera villkorlig formatering** med `Worksheet.Cells[i, j].ConditionalFormattingCollection`.  
- **Exportera till andra format** som CSV eller PDF med `wb.Save("file.pdf", SaveFormat.Pdf)`.  
- **Kombinera flera DataTables** i en enda arbetsbok, var och en på ett eget blad, med samma stilstrategi.

Om du stöter på problem, lämna en kommentar eller kolla Asposes officiella dokumentation för `ImportDataTable`. Lycka till med kodningen, och njut av de vackert stylade Excel‑filerna!

## Vad bör du lära dig härnäst?

De följande handledningarna täcker närliggande ämnen som bygger vidare på teknikerna i den här guiden. Varje resurs innehåller kompletta kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra fler API‑funktioner och utforska alternativa implementeringssätt i dina egna projekt.

- [How to Import DataTable into Excel Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [How to Set Font Styles in Excel Using Aspose.Cells for .NET (Step‑By‑Step Guide)](/cells/english/net/formatting/aspose-cells-dotnet-set-font-styles-excel/)
- [How to Apply Text Shadow in Excel Using Aspose.Cells .NET: A Step‑By‑Step Guide](/cells/english/net/formatting/apply-text-shadow-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}