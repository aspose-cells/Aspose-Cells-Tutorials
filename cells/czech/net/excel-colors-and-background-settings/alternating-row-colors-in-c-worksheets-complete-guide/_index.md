---
category: general
date: 2026-05-30
description: Naučte se, jak přidat střídavé barvy řádků v listech C#, nastavit pozadí
  buňky pomocí plné výplně a snadno přizpůsobit styl buňky listu.
draft: false
keywords:
- alternating row colors
- set cell background
- solid fill pattern
- add background color
- worksheet cell style
language: cs
og_description: Střídavé barvy řádků v C# listech jednoduše. Naučte se nastavit pozadí
  buňky, použít plnou výplň a zvládnout styl buňky listu.
og_title: Střídavé barvy řádků v C# listech – kompletní průvodce
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
title: Střídavé barvy řádků v C# listech – kompletní průvodce
url: /cs/net/excel-colors-and-background-settings/alternating-row-colors-in-c-worksheets-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Střídavé barvy řádků v C# listových tabulkách – Kompletní průvodce

Už jste se někdy zamýšleli, jak učinit export do Excelu elegantním pomocí **střídavých barev řádků**? Nejste sami – vývojáři se neustále ptají, jak *přidat barvu pozadí* řádkům, aniž by museli psát milion řádků kódu.  

V tomto tutoriálu projdeme jednoduchý způsob, jak **nastavit barvu pozadí buňky** v každém řádku, použít **solid fill pattern** a ovládat **worksheet cell style**, aby výsledek byl čitelný i vizuálně atraktivní.

## Co se naučíte

- Načíst data do `DataTable` (nebo jakéhokoli tabulkového zdroje).  
- Vytvořit pole objektů `Style`, které střídavě používají dvě barvy.  
- Importovat `DataTable` do listu a aplikovat tyto styly.  
- Ověřit výstup a případně upravit barvy nebo vzory.

Žádné externí nástroje kromě .NET prostředí a knihovny pro tabulky (v příkladech použijeme **Aspose.Cells**) nejsou potřeba. Na konci budete mít znovupoužitelnou metodu, kterou můžete vložit do libovolného reportovacího pipeline.

---

## Krok 1: Načíst zdrojová data jako `DataTable`

Nejprve – bez dat není co stylovat. Níže je malý pomocník, který vytvoří `DataTable` s ukázkovými řádky. V reálném projektu byste to nahradili voláním databáze nebo CSV parserem.

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

> **Proč je to důležité:** Mít data v `DataTable` umožňuje enginu listu *importovat* je jedním voláním, automaticky zachovává názvy sloupců a datové typy.

## Krok 2: Vytvořit styly **střídavých barev řádků**

Nyní vygenerujeme pole objektů `Style` – jeden pro každý řádek – tak, aby sudé řádky měly světle žlutý odstín, zatímco liché řádky získají jemnou azurovou barvu. Toto je jádro techniky **střídavých barev řádků**.

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

### Proč použít **solid fill pattern**?

Vlastnost `Pattern` říká enginu, jak barvu vykreslit. Výplň `Solid` zaručuje, že celé pozadí buňky je natřeno, čímž se eliminuje jakýkoli slabý mřížkový vzor, který by jinak mohl být vidět. To je nejčastější způsob, jak **nastavit barvu pozadí buňky**, když chcete čistý vzhled.

## Krok 3: Importovat `DataTable` s připravenými styly

S připraveným polem stylů se importní volání zkrátí na jeden řádek. Aspose.Cells automaticky aplikuje odpovídající styl na každý řádek.

```csharp
// Import the DataTable into the worksheet, applying the prepared styles
worksheet.Cells.ImportDataTable(
    dataTable,                     // source
    true,                          // include column names
    0,                             // start row (0‑based)
    0,                             // start column (0‑based)
    rowStyles);                    // array of styles
```

> **Co se děje pod kapotou?**  
> Knihovna iteruje přes každý řádek, kopíruje hodnoty do buněk a poté použije odpovídající `Style` z `rowStyles`. Protože jsme již definovali **solid fill pattern**, každá buňka v řádku zdědí stejnou barvu pozadí, což vám poskytne dokonalé **střídavé barvy řádků**.

## Krok 4: Uložit sešit a ověřit výsledek

Rychlé uložení vám umožní otevřít soubor v Excelu (nebo jakémkoli kompatibilním prohlížeči) a vidět efekt.

```csharp
// Save to disk – you can change the format to .xlsx, .xls, .csv, etc.
workbook.Save("AlternatingRowsReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Workbook saved. Open 'AlternatingRowsReport.xlsx' to see the result.");
```

Když soubor otevřete, řádky 1, 3, 5… budou světle žluté, zatímco řádky 2, 4, 6… budou světle azurové. Záhlaví sloupců zůstane bílé, takže data vyniknou.

![List ukazující střídavé barvy řádků](/images/alternating-row-colors.png "Snímek obrazovky listu s střídavými barvami řádků")

*Text alternativy obrázku:* **střídavé barvy řádků** snímek listu, kde se pozadí každého řádku střídá mezi světle žlutou a světle azurovou barvou.

## Krok 5: Další úpravy (volitelné)

### Změna barev

Pokud vaše značka používá jiné odstíny, stačí nahradit `Color.LightYellow` a `Color.LightCyan` libovolnou `System.Drawing.Color`, kterou preferujete. Například:

```csharp
rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.FromArgb(255, 235, 205) // Peach
                                            : Color.FromArgb(205, 235, 255); // Soft blue
```

### Použít jiný **typ pozadí**

Zatímco `BackgroundType.Solid` je nejčastější, můžete experimentovat s `BackgroundType.Gray125`, `BackgroundType.Horizontal` nebo jakýmkoli vzorem, který knihovna podporuje. To změní vizuální texturu a přesto **přidá barvu pozadí**.

### Aplikovat **worksheet cell style** na konkrétní sloupce

Někdy chcete střídavý efekt jen na datové sloupce a první sloupec (např. ID) nechat nedotčený. Vytvořte samostatný styl pro tento sloupec a přiřaďte ho po importu:

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

## Závěr

Nyní máte kompletní, znovupoužitelný řešení pro **střídavé barvy řádků** v C# listových tabulkách. Vytvořením pole objektů `Style`, **nastavením barvy pozadí buňky** pomocí **solid fill pattern** a importem `DataTable` jedním voláním můžete generovat profesionální reporty s minimálním množstvím kódu.  

Odtud můžete:

- **Přidat barvu pozadí** do záhlaví řádků pro větší důraz.  
- Kombinovat techniku s podmíněným formátováním pro dynamické vizuální nápovědy.  
- Prozkoumat další vlastnosti **worksheet cell style**, jako jsou písma, okraje nebo formáty čísel.

Vyzkoušejte to ve svém dalším exportním procesu – uživatelé vám poděkují za přehlednější a čitelnější tabulky. Šťastné kódování!

## Co byste se měli naučit dál?

- [Nastavit výšku řádku v listu pomocí Aspose.Cells pro .NET](/cells/english/net/size-and-spacing-customization/setting-height-of-all-rows-in-worksheet/)
- [Převést názvy buněk Excelu na indexy řádků a sloupců pomocí Aspose.Cells pro .NET](/cells/english/net/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-dotnet/)
- [Nastavit barvy záložek listu v Excelu pomocí Aspose.Cells .NET – Kompletní průvodce](/cells/english/net/worksheet-management/set-worksheet-tab-colors-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}