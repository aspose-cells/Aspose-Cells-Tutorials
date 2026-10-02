---
category: general
date: 2026-06-05
description: Aplikujte styly buněk při používání importu Aspose.Cells. Naučte se,
  jak importovat DataTable s formátováním, stylovat řádky a udržovat listy přehledné.
draft: false
keywords:
- apply cell styles
- aspose cells import
- import with formatting
- how to import datatable
- import datatable worksheet
language: cs
og_description: Použijte styly buněk při importu DataTable do listu Aspose.Cells.
  Podrobný návod krok za krokem s kompletním kódem a tipy.
og_title: Použijte styly buněk s Aspose.Cells – Import DataTable
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
title: Použijte styly buněk s Aspose.Cells – Importujte DataTable s formátováním
url: /cs/net/excel-formatting-and-styling/apply-cell-styles-with-aspose-cells-import-datatable-with-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Použití stylů buněk s Aspose.Cells – Import DataTable s formátováním

Už jste se někdy zamýšleli, jak **aplikovat styly buněk**, když načítáte `DataTable` do listu Excel? Nejste jediní. V mnoha scénářích reportování potřebujete, aby data vypadala dobře hned po vytvoření – bez ručního formátování později. Dobrou zprávou je, že Aspose.Cells to umožňuje snadno **importovat s formátováním**, takže vaše řádky mohou být červené nebo modré, tučné nebo jakékoliv jiné.

V tomto tutoriálu projdeme kompletním, spustitelným příkladem, který ukazuje **jak importovat datatable** do listu **s aplikovanými styly buněk**. Na konci budete mít připravenou C# konzolovou aplikaci, která vytvoří sešit, naformátuje první dva sloupce a uloží soubor – vše pomocí API `aspose cells import`.

## Co se naučíte

- Nastavení Aspose.Cells v .NET projektu  
- Vytvoření ukázkového `DataTable`, který napodobuje reálná data  
- Definování objektů `Style` pro červené a modré písmo  
- Použití `Worksheet.Cells.ImportDataTable` k **importu datatable do listu** s aplikovanými styly  
- Ověření výsledku a uložení sešitu  

Žádné externí nástroje, jen čistý C# a Aspose.Cells. Pojďme na to.

---

## Požadavky

Než se pustíme do kódu, ujistěte se, že máte následující:

| Požadavek | Proč je důležitý |
|-----------|-------------------|
| .NET 6.0 nebo novější | Aspose.Cells 23.x cílí na .NET Standard 2.0+, takže .NET 6 poskytuje nejnovější funkce runtime. |
| Aspose.Cells pro .NET (NuGet) | Knihovna poskytuje třídy `Workbook`, `Worksheet`, `Style` a metodu `ImportDataTable`, které potřebujeme. |
| Základní znalost C# | Budete rozumět třídám, políčkům a příkazům `using`. |
| IDE (Visual Studio, VS Code, Rider) | Jakýkoli editor stačí, ale budete muset obnovit NuGet balíčky. |

Balíček můžete nainstalovat z příkazové řádky:

```bash
dotnet add package Aspose.Cells
```

---

## Krok 1: Vytvořte nový Workbook a získejte první list

Nejprve – spusťte `Workbook` a načtěte první list. Představte si workbook jako prázdný zápisník; první list je stránka, na kterou budeme psát.

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

> **Tip:** Pokud budete potřebovat více listů, stačí je přidat pomocí `wb.Worksheets.Add()` a odkazovat se na ně podle názvu nebo indexu.

---

## Krok 2: Připravte ukázkový DataTable (Jak importovat DataTable)

Nyní potřebujeme něco, co naimportujeme. Ve skutečných projektech byste volali databázi, ale pro přehlednost vytvoříme `DataTable` v paměti.

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

> **Proč je to důležité:** `DataTable` vám umožní otestovat **aspose cells import** tok bez jakýchkoli externích závislostí.

---

## Krok 3: Definujte styly, které se mají použít na importované buňky

Tady se děje kouzlo. Vytvoříme dva objekty `Style`: jeden s červeným písmem, druhý s modrým. Tyto styly budou aplikovány sloupcově během importu.

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

> **Pozor:** Délka pole `importStyles` musí odpovídat počtu sloupců, které importujete, jinak Aspose vyhodí `ArgumentException`.

---

## Krok 4: Importujte DataTable do listu **s formátováním**

Nyní spojíme vše dohromady. Přetížení `ImportDataTable`, které používáme, přijímá pole `Style[]`, což nám umožňuje **aplikovat styly buněk** během zápisu dat do listu.

```csharp
        // Import the DataTable starting at cell A1 (row 0, column 0)
        // The 'true' flag tells Aspose to generate column headers automatically
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);
```

### Jak to funguje

1. **Hlavičky** – Protože jsme předali `true`, Aspose zapíše „Name“ a „Score“ do prvního řádku.  
2. **Datové řádky** – Každý následující řádek získá odpovídající styl z `importStyles`.  
3. **Výkon** – Metoda streamuje data přímo do listu, což je rychlejší než iterovat buňku po buňce.

---

## Krok 5: Ověřte výsledek a uložte workbook

Podívejme se na několik prvních buněk, abychom se ujistili, že styly zůstaly, a poté soubor zapíšeme na disk.

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

Když otevřete **StyledImport.xlsx**, uvidíte:

- Sloupec „Name“ v **červeném** textu.  
- Sloupec „Score“ v **modrém** textu.  
- Hlavičky sloupců ve výchozím stylu (můžete je také stylovat, ale to je už další tutoriál).

![Příklad aplikace stylů buněk](https://example.com/images/apply-cell-styles.png "Aplikace stylů buněk v Aspose.Cells")

> **Poznámka:** Obrázek výše ukazuje finální vzhled. Atribut `alt` obsahuje hlavní klíčové slovo, což splňuje SEO požadavky.

---

## Často kladené otázky a okrajové případy

### Co když má můj DataTable více sloupců než stylů?

Aspose použije poslední styl v poli na všechny další sloupce. Aby nedošlo k neočekávaným barvám, vždy zajistěte, že délka pole odpovídá počtu sloupců, nebo předávejte `null` pro sloupce, které nechcete stylovat.

### Můžu aplikovat různé styly na konkrétní řádky?

Ano. Po importu můžete projít řádky a přiřadit nové objekty `Style` na základě podmínek (např. zvýraznit skóre > 90 zeleně). Zde je rychlý úryvek:

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

### Funguje to i s velkými datovými sadami?

Ano. `ImportDataTable` efektivně streamuje data a aplikace statického pole stylů přidává zanedbatelnou režii. Pro miliony řádků zvažte import po částech nebo využití `Cells.ImportDataTable` s `DataReader` pro ještě lepší využití paměti.

### Jak zachovat existující formátování v listu?

Pokud cílový rozsah již obsahuje formátování, které chcete zachovat, nastavte parametr `importOptions` přetížení `ImportDataTable` (`ImportTableOptions`) a upravte `ImportDataTableOptions.PreserveCellFormatting`. Výchozí chování přepíše styly těmi, které poskytnete.

---

## Shrnutí: Co jsme dosáhli

- **Aplikovali styly buněk** během operace **aspose cells import**.  
- Ukázali **import s formátováním** předáním pole `Style[]`.  
- Demonstrovali **import datatable do listu** a uložení výsledku.  
- Pokryli okrajové případy jako nesoulad počtu stylů a podmíněné formátování řádků.

Vše bylo provedeno v jedné, samostatné konzolové aplikaci – žádné externí skripty, žádné ruční úpravy Excelu. Nyní máte pevný základ pro jakýkoli reporting nebo export dat, který vyžaduje vkusně naformátovaný výstup do Excelu.

---

## Další kroky

Chcete se posunout dál? Zde je několik nápadů, které staví na tom, co jste se právě naučili:

- **Stylizovat řádek s hlavičkou** (např. tučně, barva pozadí).  
- **Použít podmíněné formátování** pomocí `Worksheet.Cells[i, j].ConditionalFormattingCollection`.  
- **Exportovat do jiných formátů** jako CSV nebo PDF pomocí `wb.Save("file.pdf", SaveFormat.Pdf)`.  
- **Kombinovat více DataTable** v jednom sešitu, každou na samostatném listu, s použitím stejného přístupu ke stylování.

Pokud narazíte na problémy, zanechte komentář nebo si prostudujte oficiální dokumentaci Aspose k `ImportDataTable`. Šťastné programování a užívejte si krásně stylované Excel soubory!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobným krok‑za‑krokem vysvětlením, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Jak importovat DataTable do Excelu pomocí Aspose.Cells pro .NET (průvodce krok za krokem)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [Jak nastavit styly písma v Excelu pomocí Aspose.Cells pro .NET (průvodce krok za krokem)](/cells/english/net/formatting/aspose-cells-dotnet-set-font-styles-excel/)
- [Jak aplikovat stín textu v Excelu pomocí Aspose.Cells .NET: průvodce krok za krokem](/cells/english/net/formatting/apply-text-shadow-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}