---
category: general
date: 2026-06-17
description: Nastavte formát data v Excelu pomocí C# a také nastavte pozadí buňky,
  aplikujte barvu popředí a obarvěte sloupec v Excelu během importu. Naučte se krok
  po kroku.
draft: false
keywords:
- set date format
- set cell background
- apply foreground color
- color excel column
- excel import formatting
language: cs
og_description: Nastavte formát data v Excelu pomocí C# při nastavování pozadí buňky,
  aplikaci barvy popředí a barvení sloupce v Excelu během importu. Kompletní návod.
og_title: Nastavte formát data v Excelu pomocí C# – Kompletní průvodce
schemas:
- author: Aspose
  dateModified: '2026-06-17'
  description: Set date format in Excel using C# and also set cell background, apply
    foreground color, and color Excel column during import. Learn step‑by‑step.
  headline: Set date format in Excel with C# – Full Import Formatting Guide
  type: TechArticle
- description: Set date format in Excel using C# and also set cell background, apply
    foreground color, and color Excel column during import. Learn step‑by‑step.
  name: Set date format in Excel with C# – Full Import Formatting Guide
  steps:
  - name: 2.1 Set Date Format for the First Column
    text: The first column (`OrderDate`) should display as “MM/dd/yyyy”. Aspose uses
      the built‑in number format index 14 for the short date, but you can also supply
      a custom format string if you prefer.
  - name: 2.2 Set Cell Background for the Second Column
    text: Let’s give the `CustomerName` column a light blue background. This is where
      **set cell background** comes into play.
  - name: 2.3 Apply Foreground (Text) Color – Optional Extra
    text: 'If you also want the text itself to be a contrasting color, you can tweak
      the same style:'
  - name: 3.1 Save the Workbook
    text: '```csharp // Save to a file – change path as needed wb.Save("FormattedReport.xlsx",
      SaveFormat.Xlsx); Console.WriteLine("Excel file created with date format and
      colors."); ```'
  - name: What if I have more than two columns?
    text: Just expand the `columnStyles` array and assign a `Style` to each index
      you care about. Unassigned indexes will fall back to the default style, which
      is perfectly fine.
  - name: How do I format a column as currency?
    text: '```csharp columnStyles[3] = wb.CreateStyle(); columnStyles[3].Number =
      164; // Built‑in currency format (e.g., $#,##0.00) ```'
  - name: Can I change the header row style separately?
    text: 'Yes. After the import, you can grab the first row and apply a distinct
      style:'
  - name: What if the DataTable contains null dates?
    text: 'Aspose will leave those cells blank. If you prefer a placeholder like “N/A”,
      you can preprocess the table:'
  type: HowTo
tags:
- excel
- csharp
- aspnet
- data-import
title: Nastavte formát data v Excelu pomocí C# – Kompletní průvodce formátováním importu
url: /cs/net/excel-custom-number-date-formatting/set-date-format-in-excel-with-c-full-import-formatting-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Nastavení formátu data v Excelu pomocí C# – Kompletní průvodce importním formátováním

Už jste někdy potřebovali **nastavit formát data** v listu Excelu generovaném z C# kódu a zároveň chtěli, aby sloupec měl vlastní pozadí nebo barvu textu? Nejste v tom sami. V mnoha scénářích reportování načtete `DataTable` z databáze, vložíte ho do listu a pak se snažíte, aby data vypadala správně a sloupce vynikly požadovanými barvami.  

V tomto tutoriálu projdeme čistým, end‑to‑end řešením, které **nastavuje formát data**, **nastavuje pozadí buňky**, **aplikuje barvu popředí** a dokonce **obarvuje sloupec v Excelu** během importu dat. Na konci budete mít znovupoužitelný vzor, který zvládne **excel import formatting** bez typického pokusu‑a‑omylu.

> **Co budete potřebovat**  
> * .NET 6+ (nebo .NET Framework 4.7+)  
> * Aspose.Cells pro .NET (volná zkušební verze stačí pro testování)  
> * Zdroj `DataTable` – libovolný ADO.NET dotaz bude stačit  
> * Visual Studio nebo vaše oblíbené IDE  

Pojďme na to.

---

## Přehled řešení

Problém rozdělíme do tří logických částí:

1. **Načtení zdrojových dat** – `DataTable` s řádky, které chcete exportovat.  
2. **Vytvoření stylů specifických pro sloupce** – jeden styl pro sloupec s datem, druhý pro textový sloupec a případně další styly podle potřeby.  
3. **Import tabulky se styly** – použijeme `Worksheet.Cells.ImportDataTable`, takže každý sloupec zdědí připravený styl.

Proč takto? Protože Aspose.Cells umožňuje přímo při volání `ImportDataTable` přiřadit pole `Style`, což eliminuje potřebu druhého průchodu pro opětovné formátování. Je to rychlejší, méně náchylné k chybám a kód zůstane přehledný.

---

## Krok 1: Načtení dat k exportu

Nejprve potřebujete `DataTable`. V reálném projektu byste pravděpodobně volali uloženou proceduru nebo použili Entity Framework k naplnění, ale pro ukázku vytvoříme jednoduchou tabulku s datovým a textovým sloupcem.

```csharp
using System;
using System.Data;
using Aspose.Cells;

DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("OrderDate", typeof(DateTime));
    table.Columns.Add("CustomerName", typeof(string));

    // Sample rows – replace with your DB call
    table.Rows.Add(DateTime.Today.AddDays(-2), "Acme Corp");
    table.Rows.Add(DateTime.Today.AddDays(-1), "Globex Inc");
    table.Rows.Add(DateTime.Today, "Soylent Co");

    return table;
}
```

> **Tip:** Pokud váš zdroj používá nullable datumy, ujistěte se, že typ sloupce je `typeof(DateTime?)` – Aspose i tak respektuje formát, který později přiřadíte.

---

## Krok 2: Příprava pole stylů – jeden styl na sloupec

Nyní vytvoříme `Style[]`, jehož délka odpovídá počtu sloupců v `DataTable`. Každý prvek bude obsahovat formátování pro příslušný sloupec.

```csharp
// Create a new workbook and get the first worksheet
Workbook wb = new Workbook();
Worksheet ws = wb.Worksheets[0];

// Pull the data
DataTable dataTable = GetData();

// Allocate the style array
Style[] columnStyles = new Style[dataTable.Columns.Count];
```

### 2.1 Nastavení formátu data pro první sloupec

První sloupec (`OrderDate`) by měl být zobrazen jako “MM/dd/yyyy”. Aspose používá vestavěný číselný formát index 14 pro krátké datum, ale můžete také zadat vlastní formátovací řetězec, pokud chcete.

```csharp
// Style for the date column (index 0)
columnStyles[0] = wb.CreateStyle();
columnStyles[0].Number = 14;               // Built‑in short date format
// Or a custom pattern:
// columnStyles[0].Custom = "mm/dd/yyyy";
```

**Proč je to důležité:** Excel ukládá data jako sériová čísla. Přiřazením číselného formátu říkáte Excelu, aby tato čísla zobrazil jako lidsky čitelné datumy místo surových čísel.

### 2.2 Nastavení pozadí buňky pro druhý sloupec

Dejme sloupci `CustomerName` světle modré pozadí. Zde vstupuje do hry **set cell background**.

```csharp
// Style for the text column (index 1)
columnStyles[1] = wb.CreateStyle();
columnStyles[1].ForegroundColor = System.Drawing.Color.LightBlue;
columnStyles[1].Pattern = BackgroundType.Solid; // Needed to show the color
```

> **Poznámka:** Bez nastavení `Pattern` na `Solid` se barva popředí nezobrazí, protože výchozí vzor je “None”.

### 2.3 Aplikace barvy popředí (textu) – volitelný doplněk

Pokud chcete, aby samotný text měl kontrastní barvu, můžete upravit stejný styl:

```csharp
columnStyles[1].Font.Color = System.Drawing.Color.DarkBlue; // apply foreground color
```

Tím splníte požadavek **apply foreground color**, přičemž zachováte pozadí sloupce.

---

## Krok 3: Import `DataTable` s definovanými styly

S připravenými styly je posledním krokem jediný řádek, který importuje data a aplikuje styly sloupec po sloupci.

```csharp
// Import the DataTable starting at cell A1 (row 0, column 0)
// includeColumnNames = true to add a header row
ws.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

**Jak to funguje:** Aspose načte pole `columnStyles` a přiřadí každý `Style` ke konkrétnímu indexu sloupce. Hlavičkový řádek zdědí výchozí styl, pokud neposkytnete samostatný styl pro řádek 0.

### 3.1 Uložení sešitu

```csharp
// Save to a file – change path as needed
wb.Save("FormattedReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Excel file created with date format and colors.");
```

Spusťte program, otevřete *FormattedReport.xlsx* a měli byste vidět:

- **OrderDate** sloupec zobrazený jako datum (např. `06/15/2026`).  
- **CustomerName** sloupec se světle modrou výplní a tmavě modrým textem.  

To je celý **excel import formatting** workflow během méně než 30 řádků C#.

---

## Shrnutí krok za krokem (s vysvětlením)

| Krok | Co děláte | Proč je to důležité |
|------|-----------|---------------------|
| **Retrieve data** | Zavoláte `GetData()` k naplnění `DataTable`. | Poskytuje strukturovaný zdroj, který Aspose může přímo ingestovat. |
| **Create style array** | Alokujete `Style[]` odpovídající počtu sloupců. | Umožňuje stylování jednotlivých sloupců v jediném importním volání. |
| **Set date format** | `columnStyles[0].Number = 14;` | Zajišťuje, že data se v Excelu zobrazí správně. |
| **Set background color** | `ForegroundColor = LightBlue; Pattern = Solid;` | Zvýrazní sloupec, splňuje **set cell background**. |
| **Apply foreground color** | `Font.Color = DarkBlue;` | Zlepšuje čitelnost a splňuje **apply foreground color**. |
| **Import with styles** | `ImportDataTable(..., columnStyles);` | Jednopřechodový import, který respektuje veškeré formátování. |
| **Save workbook** | `wb.Save(...);` | Uloží výsledek pro další uživatele. |

---

## Řešení okrajových případů a časté otázky

### Co když mám více než dva sloupce?

Jednoduše rozšiřte pole `columnStyles` a přiřaďte `Style` ke každému indexu, který chcete formátovat. Nevyplněné indexy použijí výchozí styl, což je naprosto v pořádku.

```csharp
columnStyles[2] = wb.CreateStyle();
columnStyles[2].Number = 0; // General format for numeric columns
```

### Jak naformátovat sloupec jako měnu?

```csharp
columnStyles[3] = wb.CreateStyle();
columnStyles[3].Number = 164; // Built‑in currency format (e.g., $#,##0.00)
```

### Můžu stylovat řádek s hlavičkou samostatně?

Ano. Po importu můžete získat první řádek a aplikovat na něj odlišný styl:

```csharp
Style headerStyle = wb.CreateStyle();
headerStyle.Font.IsBold = true;
headerStyle.ForegroundColor = System.Drawing.Color.Gold;
headerStyle.Pattern = BackgroundType.Solid;

ws.Cells.Rows[0].ApplyStyle(headerStyle, new StyleFlag { All = true });
```

### Co když `DataTable` obsahuje null datumy?

Aspose nechá tyto buňky prázdné. Pokud chcete místo toho zobrazit zástupný text jako “N/A”, můžete tabulku předzpracovat:

```csharp
foreach (DataRow row in dataTable.Rows)
{
    if (row.IsNull("OrderDate"))
        row["OrderDate"] = DateTime.MinValue; // or any sentinel
}
```

Pak upravte styl tak, aby zobrazoval vlastní formát, který pro sentinel hodnotu zobrazí “N/A”.

---

## Kompletní funkční příklad

Níže je kompletní, připravený k zkopírování program. Spusťte jej jako konzolovou aplikaci a získáte pěkně naformátovaný Excel soubor.



## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobným vysvětlením, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Set Font Color in Excel Cells using Aspose.Cells for .NET](/cells/english/net/formatting/setting-font-color/)
- [Set Font Color in .NET Excel with Aspose.Cells](/cells/english/net/formatting/set-font-color-net-excel-aspose-cells/)
- [Set Excel Column Widths in Pixels Using Aspose.Cells for .NET | Step-by-Step Guide](/cells/english/net/formatting/set-excel-column-width-pixels-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}