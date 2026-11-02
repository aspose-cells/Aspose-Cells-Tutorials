---
category: general
date: 2026-05-30
description: Lär dig hur du lägger till alternerande radfärger i C#‑arbetsblad, sätter
  cellbakgrund med ett solid fyllningsmönster och anpassar arbetsbladets cellstil
  utan ansträngning.
draft: false
keywords:
- alternating row colors
- set cell background
- solid fill pattern
- add background color
- worksheet cell style
language: sv
og_description: Växla radfärger i C#‑arbetsblad enkelt. Lär dig att sätta cellbakgrund,
  använda ett solid fyllningsmönster och bemästra arbetsbladets cellstil.
og_title: Växlande radfärger i C#‑arbetsblad – Komplett guide
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Learn how to add alternating row colors in C# worksheets, set cell
    background with a solid fill pattern, and customize worksheet cell style effortlessly.
  headline: Alternating Row Colors in C# Worksheets – Complete Guide
  type: TechArticle
- description: Learn how to add alternating row colors in C# worksheets, set cell
    background with a solid fill pattern, and customize worksheet cell style effortlessly.
  name: Alternating Row Colors in C# Worksheets – Complete Guide
  steps:
  - name: Why Use a **Solid Fill Pattern**?
    text: The `Pattern` property tells the engine how to render the color. A `Solid`
      fill guarantees that the entire cell background is painted, eliminating any
      faint gridlines that might otherwise show through. This is the most common way
      to **set cell background** when you want a clean look.
  - name: Change the Colors
    text: 'If your brand uses different hues, just replace `Color.LightYellow` and
      `Color.LightCyan` with any `System.Drawing.Color` you prefer. For example:'
  - name: Use a Different **Background Type**
    text: While `BackgroundType.Solid` is the most common, you can experiment with
      `BackgroundType.Gray125`, `BackgroundType.Horizontal`, or any pattern that the
      library supports. This changes the visual texture while still **adding background
      color**.
  - name: Apply a **Worksheet Cell Style** to Specific Columns
    text: 'Sometimes you only want the alternating effect on data columns, leaving
      the first column (e.g., IDs) untouched. Create a separate style for that column
      and assign it after the import:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- DataTable
- Styling
title: Växlande radfärger i C#-arbetsblad – Komplett guide
url: /sv/net/excel-colors-and-background-settings/alternating-row-colors-in-c-worksheets-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Växlande radfärger i C#-arbetsblad – Komplett guide

Har du någonsin undrat hur du kan få ditt Excel‑export att se snyggt ut genom att använda **växlande radfärger**? Du är inte ensam—utvecklare frågar ständigt hur man *lägger till bakgrundsfärg* på rader utan att skriva en miljon rader kod.  

I den här handledningen går vi igenom ett enkelt sätt att **sätta cellbakgrund** på varje rad, applicera ett **solid fyllningsmönster**, och kontrollera **arbetsbladets cellstil** så att resultatet blir både läsbart och visuellt tilltalande.

## Vad du kommer att lära dig

- Hämta data till en `DataTable` (eller någon tabellkälla).  
- Bygg en array av `Style`‑objekt som växlar mellan två färger.  
- Importera `DataTable` till ett arbetsblad samtidigt som du applicerar dessa stilar.  
- Verifiera resultatet och justera färgerna eller mönstren vid behov.  

Inga externa verktyg behövs utöver en .NET‑miljö och ett kalkylbladsbibliotek (vi använder **Aspose.Cells** i exemplen). När du är klar har du en återanvändbar metod som du kan lägga in i vilken rapporteringspipeline som helst.

---

## Steg 1: Hämta källdata som en `DataTable`

Först och främst—utan data finns det inget att formatera. Nedan finns en liten hjälpfunktion som bygger en `DataTable` med exempelrader. I ett riktigt projekt skulle du ersätta detta med ett databasanrop eller en CSV‑parser.

```csharp
using System;
using System.Data;

static DataTable GetData()
{
    // Create a simple table with three columns
    DataTable table = new DataTable("Report");
    table.Columns.Add("ID", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    // Populate with dummy rows
    for (int i = 1; i <= 10; i++)
    {
        table.Rows.Add(i, $"Item {i}", Math.Round(new Random().NextDouble() * 100, 2));
    }

    return table;
}
```

> **Varför detta är viktigt:** Att ha data i en `DataTable` låter arbetsblads‑motorn *importera* den i ett anrop, och bevarar kolumnnamn och datatyper automatiskt.

## Steg 2: Skapa **växlande radfärger**‑stilar

Nu genererar vi en array av `Style`‑objekt—ett per rad—så att jämna rader får en ljusgul nyans medan udda rader får en mjuk cyan. Detta är kärnan i tekniken för **växlande radfärger**.

```csharp
using Aspose.Cells;
using System.Drawing;

// Assume workbook and worksheet are already instantiated
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Retrieve data
DataTable dataTable = GetData();

// Prepare an array of styles – one for each row in the table
Style[] rowStyles = new Style[dataTable.Rows.Count];

for (int i = 0; i < rowStyles.Length; i++)
{
    // Create a fresh style for the current row
    rowStyles[i] = workbook.CreateStyle();

    // **Add background color**: LightYellow for even rows, LightCyan for odd rows
    rowStyles[i].ForegroundColor = (i % 2 == 0)
        ? Color.LightYellow
        : Color.LightCyan;

    // **Set cell background** using a **solid fill pattern**
    rowStyles[i].Pattern = BackgroundType.Solid;

    // Optional: you could also set font color, borders, etc., here
}
```

### Varför använda ett **solid fyllningsmönster**?

`Pattern`‑egenskapen talar om för motorn hur färgen ska renderas. En `Solid`‑fyllning garanterar att hela cellbakgrunden målas, vilket eliminerar svaga rutnätslinjer som annars kan synas. Detta är det vanligaste sättet att **sätta cellbakgrund** när du vill ha ett rent utseende.

## Steg 3: Importera `DataTable` med de förberedda stilarna

När stil‑arrayen är klar blir import‑anropet en enradare. Aspose.Cells kommer automatiskt att applicera motsvarande stil på varje rad.

```csharp
// Import the DataTable into the worksheet, applying the prepared styles
worksheet.Cells.ImportDataTable(
    dataTable,                     // source
    true,                          // include column names
    0,                             // start row (0‑based)
    0,                             // start column (0‑based)
    rowStyles);                    // array of styles
```

> **Vad händer under huven?**  
> Biblioteket itererar över varje rad, kopierar värdena till celler och applicerar sedan den matchande `Style` från `rowStyles`. Eftersom vi redan har definierat ett **solid fyllningsmönster**, ärver varje cell i en rad samma bakgrundsfärg, vilket ger dig perfekta **växlande radfärger**.

## Steg 4: Spara arbetsboken och verifiera resultatet

En snabb sparning låter dig öppna filen i Excel (eller någon kompatibel visare) och se effekten.

```csharp
// Save to disk – you can change the format to .xlsx, .xls, .csv, etc.
workbook.Save("AlternatingRowsReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Workbook saved. Open 'AlternatingRowsReport.xlsx' to see the result.");
```

När du öppnar filen kommer rader 1, 3, 5… att vara ljusgula, medan rader 2, 4, 6… blir ljus cyan. Kolumnrubrikerna förblir vita, vilket får data att sticka ut.

![Arbetsblad som visar växlande radfärger](/images/alternating-row-colors.png "Skärmbild av arbetsblad med växlande radfärger")

*Bildens alt‑text:* **växlande radfärger** skärmbild av ett arbetsblad där varje rads bakgrund växlar mellan ljusgul och ljus cyan.

## Steg 5: Anpassa ytterligare (valfritt)

### Ändra färgerna

Om ditt varumärke använder andra nyanser, ersätt bara `Color.LightYellow` och `Color.LightCyan` med någon `System.Drawing.Color` du föredrar. Till exempel:

```csharp
rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.FromArgb(255, 235, 205) // Peach
                                            : Color.FromArgb(205, 235, 255); // Soft blue
```

### Använd en annan **bakgrundstyp**

Även om `BackgroundType.Solid` är den vanligaste, kan du experimentera med `BackgroundType.Gray125`, `BackgroundType.Horizontal` eller något annat mönster som biblioteket stödjer. Detta ändrar den visuella strukturen samtidigt som du fortfarande **lägger till bakgrundsfärg**.

### Applicera en **Worksheet Cell Style** på specifika kolumner

Ibland vill du bara ha den växlande effekten på datakolumner och låta den första kolumnen (t.ex. ID:n) vara orörd. Skapa en separat stil för den kolumnen och tilldela den efter importen:

```csharp
Style idStyle = workbook.CreateStyle();
idStyle.ForegroundColor = Color.White;
idStyle.Pattern = BackgroundType.Solid;

// Apply to the first column (A)
for (int row = 0; row < dataTable.Rows.Count + 1; row++) // +1 for header
{
    worksheet.Cells[row, 0].SetStyle(idStyle);
}
```

---

## Slutsats

Du har nu en komplett, återanvändbar lösning för **växlande radfärger** i C#‑arbetsblad. Genom att bygga en array av `Style`‑objekt, **sätta cellbakgrund** med ett **solid fyllningsmönster**, och importera en `DataTable` i ett anrop, kan du skapa professionella rapporter med minimal kod.  

Från här kan du:

- **Lägg till bakgrundsfärg** på rubrikrader för extra betoning.  
- Kombinera tekniken med villkorsstyrd formatering för dynamiska visuella ledtrådar.  
- Utforska andra **worksheet cell style**‑egenskaper som teckensnitt, kanter eller talformat.

Prova det i ditt nästa exportflöde—dina användare kommer att tacka dig för de renare, mer läsbara kalkylbladen. Lycka till med kodningen!

## Vad bör du lära dig härnäst?

- [Ställ in radhöjd i arbetsblad med Aspose.Cells för .NET](/cells/english/net/size-and-spacing-customization/setting-height-of-all-rows-in-worksheet/)
- [Konvertera Excel‑cellnamn till rad‑ och kolumnindex med Aspose.Cells för .NET](/cells/english/net/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-dotnet/)
- [Ställ in flikfärger i arbetsblad i Excel med Aspose.Cells .NET – En omfattande guide](/cells/english/net/worksheet-management/set-worksheet-tab-colors-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}